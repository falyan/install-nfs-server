# install-nfs-server ubuntu 20.04 LTS

| HOSTNAME              | IP              | KETERANGAN            |
| :---------------------| :---------------| :---------------------|
| `nfs-singleswitching` | `10.14.157.243` | Server for NFS Server |
| `ss-worker-01`        | `10.14.157.225` | Server For NFS Client |

Installation NFS Server
## Installing the NFS server
```bash
apt update
apt install nfs-kernel-server
```

![Alt text](image.png)

### Creating the file systems

```bash
mkdir -p /data/nfs-storage/data
mkdir -p /data/nfs-storage/logs
```

### make the bind mounts permanent across reboots, open the /etc/fstab file

```bash
/data/nfs-storage/  none   bind   0   0
```
![Alt text](image-1.png)

### Exporting the file systems
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

## Set Up the NFS Clients
login into server nfs client & setup host local for communicate with nfs server bellow
```bash
nano /etc/hosts
```
```bash
10.14.157.243 nfs-singleswitching
```
```bash
apt update
apt install nfs-common
```



