# Working with OpenShift Cluster

**Please replace labuserX with your lab user number, as well as FQDN and IP adresses, with values provided by instructor.**

## Logging to Openshift using CLI

Login to lab workstation as labuserX, where X is your lab user number:
```
$ ssh labuserX@10.ZZ.ZZ.ZZ
```

Login to OCP cluster as an cluster admin - michal:
```
oc login -u michal -p https://api.yyy.yyy.yy:6443
```

Check cluster status with following commands and review the outputs:
```
oc get clusterversion
oc describe clusterversion
oc get clusteroperators
```

Check node status:
```
oc get nodes
oc get nodes -o wide
oc describe node <node_name>
oc adm node-logs --tail 50 -u crio <node_name>
oc adm node-logs --tail 50 -u kubelet <node_name>
oc adm node-logs --tail 50 <node_name>
```

Check worker nodes utilization using selector and label node-role.kubernetes.io/worker
```
oc adm top node -l node-role.kubernetes.io/worker

```

## Execute commands on a node using debug pod

```
oc debug node/<node_name>
chroot /host
hostname
ip addr
systemctl status kubelet
crictl ps
crictl ps --name router
exit
exit
```

## Oauth, RBAC and SCC

```
oc get users
oc get identity

oc get clusterrolebinding
oc get clusterrolebinding -o wide
oc get rolebinding
oc get rolebinding -A

oc get scc
oc describe scc anyuid
```

## Working with pods and troubleshooting pod issue

Display all pods and events in the cluster:
```
oc get pods -A
oc get events -A
```

Get pod details (pod name may changed after redepoyment - image-registry-XXXXXX):
```
oc get pod -n openshift-image-registry
oc get pod -n openshift-image-registry -o wide
oc describe pod image-registry-5986b9ff86-8c45v -n openshift-image-registry
oc logs --tail 10 -n openshift-image-registry image-registry-5986b9ff86-8c45v
```

Open remote shell to the pod container:
```
oc rsh -n openshift-image-registry image-registry-5986b9ff86-8c45v
hostname
ip addr
exit

```
