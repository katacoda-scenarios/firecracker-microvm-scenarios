Firecracker boots instances with a particular Kernel version and Rootfs.

## Download Guest Kernel and RoofFS

```
curl -sSL -o hello-vmlinux.bin http://assets.joinscrapbook.com/firecracker/hello-vmlinux.bin
curl -sSL -o hello-rootfs.ext4 http://assets.joinscrapbook.com/firecracker/hello-rootfs.ext4
```{{execute}}

The file `hello-vmlinux.bin` is the guest Kernel. The rootfs (Operating System) is packaged as `hello-rootfs.ext4`.

If you want to customise the Kernel version or rootfs then we recommend you investigate [Linuxkit](https://github.com/linuxkit/linuxkit).

## Start 

With the binaries and Guest Kernel and RootFS in place, it's time to start Firecracker binary.

When starting, a sock file path is defined. The sock file is used to communicate with the Firecracker API.

```
rm /tmp/firecracker.sock
./firecracker --api-sock /tmp/firecracker.sock
```{{execute}}
