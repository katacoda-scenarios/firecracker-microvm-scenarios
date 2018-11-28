With the instance running, access via the **first terminal window**, it's now possible to login as `root`{{execute T1}} with the password `root`{{execute T1}}.

## Instance Types

It's possible explore the instance to identify how it's configured.

CPU Information: `cat /proc/cpuinfo`{{execute T1}}

Disk Space: `df -h`{{execute T1}}

Memory: `free -mh`{{execute T1}}

Linux Version: `uname -a`{{execute T1}}

The default microVM will have 1 vCPU and 128 MiB RAM. This can be customised within the next step.

## Shutdown Instance

In future, to shutdown the instance will be done using a HTTP request with the action _InstanceHalt_.

`curl --unix-socket /tmp/firecracker.sock -i \
    -X PUT 'http://localhost/actions'       \
    -H  'Accept: application/json'          \
    -H  'Content-Type: application/json'    \
    -d '{
        "action_type": "InstanceHalt"
     }'`{{execute T2}}

At the moment, it needs to be done by killing the Firecracker process.

`ps aux | grep -ie firecracker | awk '{print $2}' | xargs kill -9`{{execute T2}}
