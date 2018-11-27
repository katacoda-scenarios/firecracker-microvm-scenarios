```
curl -LO https://github.com/firecracker-microvm/firecracker/releases/download/v0.11.0/firecracker-v0.11.0
curl -LO https://github.com/firecracker-microvm/firecracker/releases/download/v0.11.0/jailer-v0.11.0
mv firecracker-v0.11.0 /usr/local/bin/firecracker
mv jailer-v0.11.0 /usr/local/bin/jailer
chmod +x /usr/local/bin/firecracker 
chmod +x /usr/local/bin/jailer
```{{execute}}


## Guest Kernel

```
curl -fsSL -o hello-vmlinux.bin https://s3.amazonaws.com/spec.ccfc.min/img/hello/kernel/hello-vmlinux.bin
curl -fsSL -o hello-rootfs.ext4 https://s3.amazonaws.com/spec.ccfc.min/img/hello/fsfiles/hello-rootfs.ext4
```{{execute}}
