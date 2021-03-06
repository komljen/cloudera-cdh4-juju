juju-cdh4
=========

Juju charm for Cloudera hadoop distribution CDH4 based on https://jujucharms.com/charms/precise/hadoop.

### Combined HDFS and MapReduce:

```shell
juju deploy local:cdh4 hadoop-master
juju deploy local:cdh4 hadoop-slavecluster
juju add-relation hadoop-master:namenode hadoop-slavecluster:datanode
juju add-relation hadoop-master:jobtracker hadoop-slavecluster:tasktracker
juju expose hadoop-master
```

### Separate HDFS and MapReduce deployment:

```shell
juju deploy local:cdh4 hdfs-namenode 
juju deploy local:cdh4 mapred-jobtracker 
juju deploy local:cdh4 hadoop-slavecluster 
juju add-relation hdfs-namenode:namenode hadoop-slavecluster:datanode 
juju add-relation mapred-jobtracker:mapred-namenode hdfs-namenode:namenode 
juju add-relation mapred-jobtracker:jobtracker hadoop-slavecluster:tasktracker 
juju expose hdfs-namenode 
juju expose mapred-jobtracker
```

Tested on AWS and OpenStack.
