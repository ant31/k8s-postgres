# k8s-postgresql

This role will run a postgresql server on a given node and mounts a volume from the host for **data persistency** purposes.
A defined number of slaves servers can be installed (**streaming replication**). These slave servers will automatically synchronise with the master on startup.

This role requires another one named [k8s-common](https://github.com/ansibl8s/k8s-common)

## Main variables

There are two mandatory variables :
**postgres_password** : 'postgres' user password
**postgres_nodeName**: "node2"

If a slave server is configured you'll need the following vars too:
```
replication:
  user: <replication_username>
  password: <replication_password>
  master_host: postgres # kubernetes service name of the master server
```
Then where the slave servers will run
```
postgres_slave_shards:
  - name: 1
    nodeName: node3
  - name: 2
    nodeName: node4
```

## Postgres configuration
The postgres configuration is controlled by a dictionnary which looks as follows:
```
postgres_config:
  default_statistics_target : "100"
  maintenance_work_mem : "64MB"
  checkpoint_completion_target : "0.5"
  effective_cache_size : "1GB" # Must be lower than container limits
  work_mem : "4MB"
  wal_buffers : "-1"
  checkpoint_segments : "3"
  shared_buffers : "128MB"
  wal_level: "hot_standby"
  max_wal_senders: "5"
  wal_keep_segments: "32"
  archive_mode: "on"
```

## Replication
The replication is done by using a specific docker image : **quay.io/smana/k8s-postgres**
The entrypoint takes either the argument "postgres" (master server) or "replication" (slaves).

## WAL archive
You should consider using a shared storage when you're using a master/slave cluster.
This option is possible by using a kubernetes persistent storage.
The claim has to be created before running this playbook
