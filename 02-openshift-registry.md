# Working with OpenShift cluster registry

**Please replace labuserX with your lab user number, as well as FQDN and IP adresses, with values provided by instructor.**

## Logging to Openshift and registry using CLI

Login to lab workstation as labuserX, where X is your lab user number:
```
$ ssh labuserX@10.ZZ.ZZ.ZZ
```

Login to OCP cluster as an labuserX, where X is your lab user number and to cluster registry:
```
oc login -u labuserX https://api.yyy.yyy.yy:6443
podman login -u labuserX -p $(oc whoami -t) default-route-openshift-image-registry.apps.yyy.yyy.yy
```

## Create project for labuserX
```
oc new-project labuserX
```

## Pull container image from docker.io and push the image to cluster registry

Pull Fedora linux image:
```
podman pull ubuntu
podman image ls
```

Tag the image for cluster internal repository:
```
podman tag docker.io/library/ubuntu default-route-openshift-image-registry.apps.yyy.yyy.yy/labuserX/ubuntu
```

Push the image to cluster internal repository:
```
podman push default-route-openshift-image-registry.apps.yyy.yyy.yy/labuserX/ubuntu
```
