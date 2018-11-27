## Guest Kernel

```
curl -sSL -o hello-vmlinux.bin http://assets.joinscrapbook.com/firecracker/hello-vmlinux.bin
curl -sSL -o hello-rootfs.ext4 http://assets.joinscrapbook.com/firecracker/hello-rootfs.ext4
```{{execute}}

## Start 

```
rm /tmp/firecracker.sock
./firecracker --api-sock /tmp/firecracker.sock
```{{execute T2}}