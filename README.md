# Lab kubernetes

## Use to: Vagrant + linux + ansible + kubernetes + helm + cicd

## Requirements
- Vagrant
- ansible
- virtualbox

# Running k8s cluster

Just use:

```
vagrant up cpk8s01
vagrant ssh cpk8s01
sudo -i
kubernetes get nodes -o wide --kubeconfig /etc/kubernetes/admin.conf
```

You can copy ```/etc/kubernetes/admin.conf``` for you host. You can create a simple directory to storage the kubernetes config file. By default the name of this directory is ***.kube*** (is a hide dir) and the name of the file is ***config***. The result will should be  ```$HOME/.kube/config```

Now your cluster is ready.

# You can explorer anothers things in this Lab

## Monitoring services

