# install-nfs-server ubuntu 20.04 LTS

| HOSTNAME              | IP              | KETERANGAN            |
| :---------------------| :---------------| :---------------------|
| `nfs-singleswitching` | `10.14.157.243` | Server for NFS Server |
| `ss-worker-01`        | `10.14.157.225` | Server for NFS Client |

Installation NFS Server
## Installing the NFS server
- update & install
```bash
apt update
apt install nfs-kernel-server
```

![Alt text](image.png)

### Creating the file systems
- create directory for storage
```bash
mkdir -p /data/nfs-storage/data
mkdir -p /data/nfs-storage/logs
```

### make the bind mounts permanent across reboots, open the /etc/fstab file
- make a config bellow in path **/etc/fstab**
```bash
/data/nfs-storage/  none   bind   0   0
```
![Alt text](image-1.png)

### Exporting the file systems
```bash
nano /etc/exports
```
- add following config

```bash
/data/nfs-storage   10.14.157.0/24(rw,sync,no_subtree_check)
```
- apply config exports
```bash
exportfs -ar
exportfs -v
```

![Alt text](image-2.png)

- change owner directory file sharing
```bash
chown -R nobody:nogroup data
chown -R nobody:nogroup logs
```
![Alt text](image-5.png)

## Set Up the NFS Clients
### setup domain local first
- login into server nfs client & setup host local for communicate with nfs server bellow
```bash
nano /etc/hosts
```
```bash
10.14.157.243 nfs-singleswitching
```
![Alt text](image-3.png)
- update & install 
```bash
apt update
apt install nfs-common
```

### add mounting filesystem
- create directory for sharing file
```bash
mkdir -p /mnt/nfs-storage
```
- add & sync nfs client to path nfs server 
```bash
nano /etc/fstab
```
```bash
nfs-singleswitching:/data/nfs-storage /mnt/nfs-storage nfs nolock 0 0
```
- apply config (connect to nfs server)
```bash
mount -a
```
- cek your mounting filesystem
```bash
df -h | grep nfs-storage
```
![Alt text](image-4.png)

your nfs client & nfs server has been installed

# Testing 

- create a file in nfs server on path **/data/nfs-storage/data**
```bash
cd /data/nfs-storage/data
touch testing.py
touch tetsing.tf
```

- cek file in nfs client

```bash
cd /mnt/nfs-storage/data
ls
```

![Alt text](image-6.png)


# conclusion
in nfs server path for storage in **/data/nfs-storage/data** and path sharing for client in **/mnt/nfs-storage/data**

## 🔗 About me
[![linkedin](https://img.shields.io/badge/linkedin-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/falyan-zuril-587585247/)


