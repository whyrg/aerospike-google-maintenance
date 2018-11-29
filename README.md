# Aerospike quiesce script for GCP maintanence events

Based off of Google's own metadata [example](https://github.com/GoogleCloudPlatform/python-docs-samples/blob/master/compute/metadata/main.py),
this script will drain Aerospike nodes when the node gets a maintenence event.

A maintenence event typically means the VM will be live migrated. This plays havoc with Aerospike.
To mitigate the impact, the node will be drained via the `asinfo -v quiesce` command once a maintenence event is scheduled.

# Requirements

python requests 2.20.1
asinfo (or aerospike-tools)


# Running

run with nohup:

```
nohup ./maintenence.py & 
```

# Parameters:

```
usage: maintenence.py [-h] [-o OPTIONS [OPTIONS ...]]

optional arguments:
  -h, --help            show this help message and exit
  -o OPTIONS [OPTIONS ...], --options OPTIONS [OPTIONS ...]
                        Additional options to pass into asinfo. Can be
                        anything except commands, ie: "-v $COMMAND". Asinfo
                        flags must be escaped, eg: "\-u"
```

Example with user/password:

```
nohup ./maintenence.py -o "\-u" admin "\-p" admin &
```
