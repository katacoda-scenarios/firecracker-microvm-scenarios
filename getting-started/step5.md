The instance type can be customised, to include additional CPU, memory and networking settings.

## Restart Firecracker

In the previous step we shutdown Firecracker. Restart the process to launch the new instance.

```
rm /tmp/firecracker.sock
./firecracker --api-sock /tmp/firecracker.sock
```{{execute T1}}

## Set the guest kernel

As before, set the Kernel and Rootfs.

`curl --unix-socket /tmp/firecracker.sock -i \
    -X PUT 'http://localhost/boot-source'   \
    -H 'Accept: application/json'           \
    -H 'Content-Type: application/json'     \
    -d '{
        "kernel_image_path": "./hello-vmlinux.bin",
        "boot_args": "console=ttyS0 reboot=k panic=1 pci=off"
    }'
curl --unix-socket /tmp/firecracker.sock -i \
    -X PUT 'http://localhost/drives/rootfs' \
    -H 'Accept: application/json'           \
    -H 'Content-Type: application/json'     \
    -d '{
        "drive_id": "rootfs",
        "path_on_host": "./hello-rootfs.ext4",
        "is_root_device": true,
        "is_read_only": false
    }'
curl -fsS --unix-socket /tmp/firecracker.sock -i \
    -X PUT "http://localhost/logger" \
    -H  "accept: application/json" \
    -H  "Content-Type: application/json" \
    -d '{
           "log_fifo": "/dev/null",
           "metrics_fifo": "/dev/null",
           "level": "Error",
           "show_level": true,
           "show_log_origin": false
    }'`{{execute T2}}

## Customise Instance

Using a HTTP call, it's possible to configure the CPU and Memory allocated. In this case, it doubles the capacity.

`curl --unix-socket /tmp/firecracker.sock -i  \
    -X PUT 'http://localhost/machine-config' \
    -H 'Accept: application/json'            \
    -H 'Content-Type: application/json'      \
    -d '{
        "vcpu_count": 2,
        "mem_size_mib": 256
    }'`{{execute T2}}

## Start

It can now be started as before.

`curl --unix-socket /tmp/firecracker.sock -i \
    -X PUT 'http://localhost/actions'       \
    -H  'Accept: application/json'          \
    -H  'Content-Type: application/json'    \
    -d '{
        "action_type": "InstanceStart"
     }'`{{execute T2}}

## View Changes

As before, login and you can explore the instance with the increased capacity.

Login as `root`{{execute T1}} with the password `root`{{execute T1}}.

CPU Information: `cat /proc/cpuinfo`{{execute T1}}

Memory Information: `free -mh`{{execute T1}}

