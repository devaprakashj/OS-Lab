# Exercise 12 (b): Configure and Verify NFS Server and Client

## 🎯 Aim
To configure an NFS (Network File System) server and client in Linux for file sharing between systems.

## 📚 Theory
NFS allows a system to share directories across a network so that other systems can access them as if they were local storage.

**Architecture:**
```text
NFS Server    <---- Network ---->    NFS Client
(Shared Folder)                  (Mounted Folder)
```

**Advantages:**
- Centralized file storage
- Easy file sharing
- Reduced disk duplication

---

## 📝 Procedure

### Step 1: Install NFS Server
On the **Server machine**, open the terminal and run:
```bash
sudo apt install nfs-kernel-server
```

### Step 2: Create Shared Directory
Create the folder to be shared and set the appropriate permissions:
```bash
sudo mkdir /nfs_share
sudo chmod 777 /nfs_share
```

### Step 3: Configure NFS Export
Edit the `exports` configuration file:
```bash
sudo nano /etc/exports
```
Add the following line at the end of the file:
```text
/nfs_share 192.168.1.0/24(rw,sync,no_root_squash)
```
*Explanation of Options:*
| Option | Meaning |
|:---:|---|
| `rw` | Read & write permission |
| `sync` | Write changes to disk immediately |
| `no_root_squash` | Root access allowed from the client |

### Step 4: Restart NFS Service
Export the shared directory and restart the NFS service:
```bash
sudo exportfs -a
sudo systemctl restart nfs-kernel-server
```

### Step 5: Install NFS Client
On the **Client machine**, install the NFS common package:
```bash
sudo apt install nfs-common
```

### Step 6: Create Mount Directory
Create a local directory to act as a mount point:
```bash
sudo mkdir /mnt/nfs_client
```

### Step 7: Mount NFS Shared Directory
Mount the shared directory from the server to the client:
```bash
sudo mount 192.168.1.10:/nfs_share /mnt/nfs_client
```
*(Where `192.168.1.10` is the NFS server's IP address).*

### Step 8: Verify Mount
Check if the shared directory is successfully mounted:
```bash
df -h
# or
mount | grep nfs
```

---

## 💻 Implementation Code (Commands Summary)

**Server Commands:**
```bash
sudo apt install nfs-kernel-server
sudo mkdir /nfs_share
sudo chmod 777 /nfs_share
sudo nano /etc/exports
sudo exportfs -a
sudo systemctl restart nfs-kernel-server
```

**Client Commands:**
```bash
sudo apt install nfs-common
sudo mkdir /mnt/nfs_client
sudo mount 192.168.1.10:/nfs_share /mnt/nfs_client
df -h
```

---

## 📥 Sample Input & Output

**Sample Configuration Values:**
- **Server IP:** `192.168.1.10`
- **Shared Directory:** `/nfs_share`
- **Client Mount Directory:** `/mnt/nfs_client`

**Sample Output (`mount | grep nfs`):**
```text
192.168.1.10:/nfs_share on /mnt/nfs_client type nfs
```

**Sample Output (`df -h`):**
```text
Filesystem               Size  Used Avail Use% Mounted on
192.168.1.10:/nfs_share   20G    2G   18G  10% /mnt/nfs_client
```

---

## ✅ Result
The NFS server was successfully configured, and the client system was able to mount and access the shared directory over the network.
