# Introduction to OpenShift Container Platform Workshop

## OpenShift Lab Cluster
Cluster version: 4.12.X
Nodes: 3 master nodes + 3 worker nodes on IBM Power platform (ppc64le)
Storage: Ceph provided with OpenShift Data Foundation

## Using the labs

## Labs Requirements
1. VPN connection to the Lab (OpenVPN) - ip address, username and password provided by e-mail.
2. Admin account for OCP cluster - provided by e-mail.
3. Lab user account (labuserX) for lab workstation and OCP cluster - provided by e-mail.
4. Web browser (Firefox or Chrome).
6. SSH client.
7. Hosts file with entries based on an example below - IP addresses and FQDNs will be provided by e-mail.
```
10.XX.XX.XX	console-openshift-console.apps.yyy.yyy.yy
10.XX.XX.XX	oauth-openshift.apps.yyy.yyy.yy
10.XX.XX.XX	default-route-openshift-image-registry.apps.yyy.yyy.yy
10.XX.XX.XX	labuserXapp1-labuserX.apps.yyy.yyy.yy
10.XX.XX.XX	labuserXapp2-labuserX.apps.yyy.yyy.yy
```
where X is your lab user number, e.g. labuser1

## Lab Env

OCP cluster API: https://api.yyy.yyy.yy:6443

OCP console: https://console-openshift-console.apps.yyy.yyy.yy

Lab workstation: 10.ZZ.ZZ.ZZ

# Labs

* [01 Working with OpenShift cluster ](01-openshift-cluster.md)

* [02 Build and deploy simple application using GUI](02-app-build.md)

* [03 Deploy application from custom image](03-custom-image.md)

* [04 Deploy an apllication with persistent volume](04-pvolume.md)

