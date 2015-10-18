# k8s-postgresql

Run a postgresql server on a single node and mounts a volume from the host in order to persist data.

This role requires another one named [k8s-common](https://github.com/ansibl8s/k8s-common)

## Main variables

**db_node** : Node where the database will run, it is used in order to control where the data will be stored.

**db_passwd** : 'postgres' user password

## TODO
replication
dumps
