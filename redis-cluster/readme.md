# Setup Redis Cluster Vagrant

This config will setup 3 redis master with one replication each.

### <b>cluster-config:</b>

- cluster-enabled <b>yes</b>
- cluster-config-file <b>nodes-6379.conf</b>
- cluster-node-timeout <b>5000</b>

## <b>Instruction:</b>

Start our vagrant machines and SSH into master-01 machine

    vagrant up
    vagrant ssh master-01

### <b>Enable redis cluster:</b>

once we get into our machine we need to create our cluster with <b>redis-cli</b>

    redis-cli --cluster create 10.0.0.1:6379 10.0.0.2:6379 10.0.0.11:6379  \
    10.0.0.3:6379 10.0.0.13:6379 10.0.0.12:6379 \
    --cluster-replicas 1

### <b> Testing our cluster: </b>

In our master-01 machine connect to redis server by <b>redis-cli with cluster mode.</b>

    redis-cli -c

Set our first value

    set hi hello

    #output: 
    -> Redirected to slot [16140] located at 10.0.0.11:6379
    OK

Checking if it work properly:

    get hi
    
    #output:
    "hello"