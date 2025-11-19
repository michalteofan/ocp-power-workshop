# Deploying application from custom image

## Building and deploying custom image

Login to lab workstation as labuserX, where X is your lab user number:
```
$ ssh labuserX@10.ZZ.ZZ.ZZ
```
Set project to labuserX

```
oc project labuserX
```

Clone git repo:
```
git clone https://github.com/michalteofan/labuser0.git
```

Change directory to labuser0
```
cd labuser0/
```

Inspect the dockerfile:
```
cat Dockerfile

FROM docker.io/ppc64le/ubuntu:focal

ENV TZ=Europe/Warsaw
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
RUN apt-get update && apt-get install -y apache2
ADD index.html /var/www/html/index.html
ADD webstart.sh /usr/sbin/webstart.sh
RUN chmod +x /usr/sbin/webstart.sh
RUN sed -i 's/Listen 80/Listen 8080/g' /etc/apache2/ports.conf
RUN sed -i 's/apache2$SUFFIX/apache2/g' /etc/apache2/envvars
RUN mkdir /var/run/apache2
RUN mkdir /var/lock/apache2
RUN chgrp -R 0 /var/www/html && \
    chmod -R g=u /var/www/html
RUN chgrp -R 0 /var/lock/apache2 && \
    chmod -R g=u /var/lock/apache2
RUN chgrp -R 0 /var/run/apache2 && \
    chmod -R g=u /var/run/apache2
RUN chgrp -R 0 /var/log/apache2 && \
    chmod -R g=u /var/log/apache2

EXPOSE 8080

CMD []

ENTRYPOINT ["webstart.sh"]
```

Customize index.html file:
```
cat index.html 

<html>
<head>
	<meta http-equiv="content-type" content="text/html; charset=utf-8"/>
	<title></title>
</head>
<body>
<font size="12">App deployed for OCP on POWER labuserX v1</font>
</body>
```

Check ENTRYPOINT script file content:
```
cat webstart.sh

#!/bin/bash
apache2ctl -DFOREGROUND
```

Build docker image:
```
podman build -t labuserXapp2:v1 .
podman image ls
```

Tag the image for the cluster registry:
```
podman tag labuserXapp2:v1 default-route-openshift-image-registry.apps.yyy.yyy.yy/labuserX/labuserXapp2:v1
```

Login to cluster registry and push the image:
```
oc login -u labuserX https://api.yyy.yyy.yy:6443
podman login -u $(oc whoami) -p $(oc whoami -t) default-route-openshift-image-registry.apps.yyy.yyy.yy
podman push default-route-openshift-image-registry.apps.yyy.yyy.yy/labuserX/labuserXapp2:v1
```

Deploy new applcation from custom image:
```
oc new-app image-registry.openshift-image-registry.svc:5000/labuserX/labuserXapp2:v1 --name labuserXapp2

warning: Cannot check if git requires authentication.
--> Found container image 283ae4d (47 minutes old) from image-registry.openshift-image-registry.svc:5000 for "image-registry.openshift-image-registry.svc:5000/labuser0/labuser0app2:v1"

    * An image stream tag will be created as "labuser0app2:v1" that will track this image

--> Creating resources ...
Warning: would violate PodSecurity "restricted:v1.24": allowPrivilegeEscalation != false (container "labuser0app2" must set securityContext.allowPrivilegeEscalation=false), unrestricted capabilities (container "labuser0app2" must set securityContext.capabilities.drop=["ALL"]), runAsNonRoot != true (pod or container "labuser0app2" must set securityContext.runAsNonRoot=true), seccompProfile (pod or container "labuser0app2" must set securityContext.seccompProfile.type to "RuntimeDefault" or "Localhost")
    deployment.apps "labuser0app2" created
    service "labuser0app2" created
--> Success
    Application is not exposed. You can expose services to the outside world by executing one or more of the commands below:
     'oc expose service/labuser0app2' 
    Run 'oc status' to view your app.

oc status
oc get deployments
oc get pods
oc get svc
```

Expose the application with route:
```
oc expose svc/labuserXapp2 --hostname=labuserXapp2-labuserX.apps.yyy.yyy.yy
oc get route
```

Check if the application works using web browser or curl:
```
curl http://labuserXapp2-labuserX.apps.yyy.yyy.yy
```

## Application scaling
```
oc get deployment
oc get pods -o wide
oc scale deployment/labuserXapp2 --replicas=3
oc get pods -o wide
oc get deployment
```

## Updating the application

Update index.html file:
```
cat index.html 

<html>
<head>
	<meta http-equiv="content-type" content="text/html; charset=utf-8"/>
	<title></title>
</head>
<body>
<font size="12">App deployed for OCP on POWER labuserX v2</font>
</body>
```

Push it with the same tag as previous version and update will be triggered automatically
```
podman build -t default-route-openshift-image-registry.apps.yyy.yyy.yy/labuserX/labuserXapp2:v1 .
podman push default-route-openshift-image-registry.apps.yyy.yyy.yy/labuserX/labuserXapp2:v1
```

Check update progress:
```
oc get pods
oc rollout status deployments/labuserXapp2
oc rollout history deployments/labuserXapp2
oc rollout history deployments/labuserXapp2 --revision 1
oc rollout history deployments/labuserXapp2 --revision 2
oc rollout history deployments/labuserXapp2 --revision 3
```

Check if the new version is available, you can use web browser or curl:
```
curl http://labuserXapp2-labuserX.apps.yyy.yyy.yy
```
