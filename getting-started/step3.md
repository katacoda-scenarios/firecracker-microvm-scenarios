The configuration of the instance to launch is defined via a series of HTTP requests.

## Set the guest kernel

The first configuration is to define the boot source and the kernel to use. It will look in the same directory as the Firecracker binary. A series of boot arguments can be passed to the Kernel to configure how it launches.

`curl --unix-socket /tmp/firecracker.sock -i \
    -X PUT 'http://localhost/boot-source'   \
    -H 'Accept: application/json'           \
    -H 'Content-Type: application/json'     \
    -d '{
        "kernel_image_path": "./hello-vmlinux.bin",
        "boot_args": "console=ttyS0 reboot=k panic=1 pci=off"
    }'`{{execute T2}}

The response of 204 No Content indicates that the request was successful.

## Set the guest rootfs

Next, define the rootfs and the guest operating system that will be booted.

`curl --unix-socket /tmp/firecracker.sock -i \
    -X PUT 'http://localhost/drives/rootfs' \
    -H 'Accept: application/json'           \
    -H 'Content-Type: application/json'     \
    -d '{
        "drive_id": "rootfs",
        "path_on_host": "./hello-rootfs.ext4",
        "is_root_device": true,
        "is_read_only": false
    }'`{{execute T2}}

## Start the guest machine

The instance is now configured and can be started. This is done by issuing a _InstanceStart_ action.

`curl --unix-socket /tmp/firecracker.sock -i \
    -X PUT 'http://localhost/actions'       \
    -H  'Accept: application/json'          \
    -H  'Content-Type: application/json'    \
    -d '{
        "action_type": "InstanceStart"
     }'`{{execute T2}}

Within the first terminal, you should see the VM start booting and after a few seconds, a login prompt will appear. If you see the error `KVM_EXIT_FAIL_ENTRY` then a problem has occurred. 

The Firecracker is the parent process ID that will manage the instance. This can be viewed within the process tree.

`ps aux | grep firecracker`{{execute T2}}

The VM is running as a KVM instance that is also listed as a process.

`ps aux | grep kvm`{{execute T2}}