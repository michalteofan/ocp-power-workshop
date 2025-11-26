# Deploying an application with persistent volume

## Deploying an application with persistent volume using Openshift template...

Login to OCP as labuserX, where X is your lab user number, e.g. labuser1:
```
oc login -u labuserX
oc project labuserX
```

Check Storage Classes, persistent Volume Claims and persistent Volumes:
```
oc get sc
oc get pvc
```

List all local application templates and search for mariadb with persistent volume:
```
oc new-app -L
oc new-app -S --template=maria
```

Deply MariaDB from template:
```
oc new-app mariadb-persistent --name labuserXdb
```

Check pod status and pvc:
```
oc get all | grep mariadb
oc get pvc
```

Wait for Mariadb pod to start and login to the pod with rsh (take the name of the pod from command output):
```
oc get pod | grep mariadb
```
```
oc rsh pod/mariadb-1-XXXXXX
```

Check if the volume is mounted to the pod
```
mount | grep mysql

exit
```

## ...or more in K8s way

Create sql dump file michal.sql:

```
-- MySQL dump 10.17  Distrib 10.3.22-MariaDB, for Linux (ppc64le)
--
-- Host: nm.iic         Database: michal
-- ------------------------------------------------------
-- Server version	10.4.12-MariaDB-1:10.4.12+maria~bionic

/*!40101 SET @OLD_CHARACTER_SET_CLIENT=@@CHARACTER_SET_CLIENT */;
/*!40101 SET @OLD_CHARACTER_SET_RESULTS=@@CHARACTER_SET_RESULTS */;
/*!40101 SET @OLD_COLLATION_CONNECTION=@@COLLATION_CONNECTION */;
/*!40101 SET NAMES utf8mb4 */;
/*!40103 SET @OLD_TIME_ZONE=@@TIME_ZONE */;
/*!40103 SET TIME_ZONE='+00:00' */;
/*!40014 SET @OLD_UNIQUE_CHECKS=@@UNIQUE_CHECKS, UNIQUE_CHECKS=0 */;
/*!40014 SET @OLD_FOREIGN_KEY_CHECKS=@@FOREIGN_KEY_CHECKS, FOREIGN_KEY_CHECKS=0 */;
/*!40101 SET @OLD_SQL_MODE=@@SQL_MODE, SQL_MODE='NO_AUTO_VALUE_ON_ZERO' */;
/*!40111 SET @OLD_SQL_NOTES=@@SQL_NOTES, SQL_NOTES=0 */;

--
-- Table structure for table `michal_tbl`
--

DROP TABLE IF EXISTS `michal_tbl`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!40101 SET character_set_client = utf8 */;
CREATE TABLE `michal_tbl` (
  `michal_id` int(11) NOT NULL AUTO_INCREMENT,
  `product_name` varchar(100) NOT NULL,
  PRIMARY KEY (`michal_id`)
) ENGINE=InnoDB AUTO_INCREMENT=2 DEFAULT CHARSET=latin1;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `michal_tbl`
--

LOCK TABLES `michal_tbl` WRITE;
/*!40000 ALTER TABLE `michal_tbl` DISABLE KEYS */;
INSERT INTO `michal_tbl` VALUES (1,'dane');
/*!40000 ALTER TABLE `michal_tbl` ENABLE KEYS */;
UNLOCK TABLES;
/*!40103 SET TIME_ZONE=@OLD_TIME_ZONE */;

/*!40101 SET SQL_MODE=@OLD_SQL_MODE */;
/*!40014 SET FOREIGN_KEY_CHECKS=@OLD_FOREIGN_KEY_CHECKS */;
/*!40014 SET UNIQUE_CHECKS=@OLD_UNIQUE_CHECKS */;
/*!40101 SET CHARACTER_SET_CLIENT=@OLD_CHARACTER_SET_CLIENT */;
/*!40101 SET CHARACTER_SET_RESULTS=@OLD_CHARACTER_SET_RESULTS */;
/*!40101 SET COLLATION_CONNECTION=@OLD_COLLATION_CONNECTION */;
/*!40111 SET SQL_NOTES=@OLD_SQL_NOTES */;

-- Dump completed on 2020-04-03 15:44:27

```

Create secret yaml file mydb-sec.yaml:
```
apiVersion: v1
kind: Secret
metadata:
  name: mydb
  labels:
    app: mydb
type: Opaque
data:
  MYSQL_ROOT_PASSWORD: cGFzc3cwcmQ=
  MYSQL_USER: bWljaGFs
  MYSQL_PASSWORD: cGFzc3cwcmQ=
  MYSQL_DATABASE: bWljaGFs
```

Create service (nodeport) yaml file mydb-svc.yaml (change XX in 310XX to yours labuser two-digit number, with leading 0 for 1 to 9: - e.q. 01):
```
apiVersion: v1
kind: Service
metadata:
  name: mydb
  labels:
    app: mydb
spec:
  ports:
  - port: 3306
    nodePort: 310XX
    name: mydb
  selector:
    app: mydb
  sessionAffinity: None
  type: NodePort
```

Create statefulset yaml file mydb-sstate.yaml (please notice ConfigMap, Secret, PVC and probes):
```
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: mydb
spec:
  serviceName: mydb
  replicas: 1
  selector:
    matchLabels:
      app: mydb
  template:
    metadata:
      labels:
        app: mydb
    spec:
      containers:
      - name: mydb
        image: docker.io/ppc64le/mariadb:10.6.15-focal
        envFrom:
          - secretRef:
              name: mydb
        ports:
        - containerPort: 3306
          name: mydb
        volumeMounts:
        - name: mydb
          mountPath: /var/lib/mysql
          subPath: mydb
        - name: mydb-michal
          mountPath: /docker-entrypoint-initdb.d/michal.sql
          subPath: michal.sql
        resources:
          requests:
            cpu: 500m
            memory: 2048Mi
        livenessProbe:
          tcpSocket:
            port: 3306
          failureThreshold: 10
          initialDelaySeconds: 120
          periodSeconds: 10
          successThreshold: 1
          timeoutSeconds: 5
        readinessProbe:
          tcpSocket:
            port: 3306
          failureThreshold: 10
          initialDelaySeconds: 120
          periodSeconds: 10
          successThreshold: 1
          timeoutSeconds: 5
      volumes:
        - name: mydb
          persistentVolumeClaim:
            claimName: mydb
        - name: mydb-michal
          configMap:
            name: mydb-michal
  volumeClaimTemplates:
  - metadata:
      name: mydb
    spec:
      accessModes: [ "ReadWriteOnce" ]
      storageClassName: ibm-spectrum-scale-backup
      resources:
        requests:
          storage: 10Gi
```

Create configmap from michal.sql file:
```
oc create configmap mydb-michal --from-file=michal.sql
```

Create secret, statefulset and service:
```
oc apply -f mydb-sec.yaml
oc apply -f mydb-svc.yaml
oc apply -f mydb-sstate.yaml
```

Check the pod and persistent volume:
```
oc get statefulset
oc describe pod mydb-0
oc logs mydb-0
oc get pvc
oc exec -ti mydb-0 -- mount | grep mysql
```

Note node and node port:
```
oc get pod mydb-0 -o wide
oc get svc
```

Connect do database using node name and node port (the port should be added to load-balancer), wthere yyyy.yyy.yy is the node name and 31XXX is your node port:
```
mysql -h yyyy.yyy.yy --port=31XXX -u michal michal -p
```
the password is passw0rd

and check if the table exist:
```
show tables;
```

