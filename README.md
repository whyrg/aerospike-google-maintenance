# Aerospike quiesce script for GCP maintenance events

Based off of Google's own metadata [example](https://github.com/GoogleCloudPlatform/python-docs-samples/blob/master/compute/metadata/main.py),
this script will drain Aerospike nodes when the node gets a maintenance event.

A maintenance event typically means the VM will be live migrated. This plays havoc with Aerospike.
To mitigate the impact, the node will be drained via the `asinfo -v quiesce` command once a maintenance event is scheduled.

# Requirements

python requests 2.20.1  
asinfo (from aerospike-tools)


# Running

This script should run on every Aerospike node, as maintenance events are local to each VM.

run with nohup:

```
nohup ./maintenance.py & 
```

# Parameters:

```
usage: maintenance.py [-h] [-o OPTIONS [OPTIONS ...]]

optional arguments:
  -h, --help            show this help message and exit
  -o OPTIONS [OPTIONS ...], --options OPTIONS [OPTIONS ...]
                        Additional options to pass into asinfo. Can be
                        anything except commands, ie: "-v $COMMAND". Entire
                        string must be quoted, eg: -o="-u admin -p admin"
```


Example with user/password:

```
nohup ./maintenance.py -o="-u admin -p admin" & 
```
