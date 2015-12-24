# k8s-postgresql

Run a postgresql server on a single node and mounts a volume from the host in order to persist data.

This role requires another one named [k8s-common](https://github.com/ansibl8s/k8s-common)

## Main variables

**postgres_password** : 'postgres' user password

## WAL archive
You should consider using a shared storage when you're using a master/slave cluster.
