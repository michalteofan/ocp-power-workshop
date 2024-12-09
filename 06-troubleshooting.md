
# Useful troubleshooting commands

## Checking cluster state

Login to lab workstation as labuserX, where X is your lab user number:

```
$ ssh labuserX@ZZZ.ZZZ.ZZZ.ZZZ
```

Login to OCP cluster as an admin:

```
oc login https://api.zzz.zzz.zzz:6443
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
oc describe node zzz.zzz.zzz.zzz

oc adm top node -l node-role.kubernetes.io/worker

oc adm node-logs --tail 50 -u crio zzz.zzz.zzz.zzz
oc adm node-logs --tail 50 -u kubelet zzz.zzz.zzz.zzz
oc adm node-logs --tail 50 zzz.zzz.zzz.zzz
```

## Execute commands on a node using debug pod

```
oc debug node/zzz.zzz.zzz.zzz
chroot /host
hostname
ip addr
systemctl status kubelet
systemctl status cri-o
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

```
oc get pods -A
oc get events -A
oc get pod -n openshift-image-registry
oc get pod -n openshift-image-registry -o wide
oc describe pod cluster-image-registry-operator-xxxx-xxx -n openshift-image-registry
oc logs --tail 10 -n openshift-image-registry cluster-image-registry-operator-xxxx-xxx -c cluster-image-registry-operator

oc rsh -n openshift-image-registry cluster-image-registry-operator-xxxx-xxx
hostname
ip addr
exit

```

