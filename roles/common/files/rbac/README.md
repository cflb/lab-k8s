Pre Requesites:

- Have the ca.key and ca.crt files locally.
- Permission to administrate the cluster.

In Production/Staging environments we have four Roles:

1. *backend-dev* it has permissions to scale pods, execute things inside the pods, read logs, namespaces and configmaps
2. *frontend-dev* it has permissions only to read namespace, pods and their logs.
3. *cluster-deployer* only has permissions involved on deployments.
4. *cluster-admin* has ALL permissions, including DELETE things, take care!

The files `clusterrole.yaml` and `clusterrolebindings.yaml` should be created on cluster to get it working.
