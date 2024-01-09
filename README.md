# install-nfs-server
Installation NFS Server
## Installing the NFS server
```bash
apt update
apt install nfs-kernel-server
```

![Alt text](image.png)

## Creating the file systems

```bash
mkdir -p /data/nfs-storage/data
mkdir -p /data/nfs-storage/logs
```

## make the bind mounts permanent across reboots, open the /etc/fstab file

```bash
/data/nfs-storage/  none   bind   0   0
```
![Alt text](image-1.png)

## Exporting the file systems
```bash
nano /etc/exports
```
add following config

```bash
/data/nfs-storage   10.14.157.0/24(rw,sync,no_subtree_check)
```

```bash
exportfs -ar
exportfs -v
```

![Alt text](image-2.png)

