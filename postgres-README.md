# k8s-postgresql

Run a postgresql server on a single node and mounts a volume from the host in order to persist data.

## Main variables

**appname** : this variable allows to run multiple instances of the app in a single namespace. (default: 0)

**db_node** : Node where the database will run, it is used in order to control where the data will be stored.

**db_passwd** : 'postgres' user password


## TODO
replication
dumps
