Firecracker is linked statically against musl, having no library dependencies. The binaries are available on the [Github release page](https://github.com/firecracker-microvm/firecracker/releases).

Firecracker uses the `jailer` binary to create the secure, execution jail for the instance.

## Task - Download

Run the following commands to download Firecracker v0.11.0.

```
curl -L -o firecracker http://assets.joinscrapbook.com/firecracker/firecracker-v0.11.0
curl -L -o jailer http://assets.joinscrapbook.com/firecracker/jailer-v0.11.0
chmod +x firecracker
chmod +x jailer
```{{execute}}

## Task - Start

Once downloaded, check to ensure that Firecracker can run by outputting the version number.

`./firecracker -V`{{execute}}