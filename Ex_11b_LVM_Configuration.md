# Exercise 11 (b): Implementation of Logical Volume Management (LVM)

## 🎯 Aim
To configure Logical Volume Management (LVM) in Linux by creating a Physical Volume, Volume Group, Logical Volume, formatting it, and mounting it to the file system.

## 📚 Theory
Logical Volume Management (LVM) is a highly flexible storage management system in Linux. It allows administrators to resize, extend, or reduce partitions dynamically without system downtime.

**Core Components of LVM:**
1. **Physical Volume (PV):** The actual underlying hard disk or partition (e.g., `/dev/sdb1`).
2. **Volume Group (VG):** A storage pool created by combining one or more Physical Volumes.
3. **Logical Volume (LV):** A virtual partition created from the Volume Group that can be formatted and mounted like a normal drive.

---

## 📝 Procedure

### Step 1: Create a Physical Volume (PV)
Initialize the partition for LVM so it can be recognized as a physical volume:
```bash
sudo pvcreate /dev/sdb1
```

### Step 2: Create a Volume Group (VG)
Create a new volume group (e.g., `my_vg`) using the created physical volume:
```bash
sudo vgcreate my_vg /dev/sdb1
```

### Step 3: Create a Logical Volume (LV)
Create a logical volume (e.g., `my_lv`) of a specific size (e.g., 2GB) from the volume group:
```bash
sudo lvcreate -L 2G -n my_lv my_vg
```

### Step 4: Format the Logical Volume
Format the newly created logical volume with a file system like `ext4`:
```bash
sudo mkfs.ext4 /dev/my_vg/my_lv
```

### Step 5: Create a Mount Point and Mount the LV
Create a directory to act as a mount point and mount the logical volume to it:
```bash
sudo mkdir -p /mnt/lvm
sudo mount /dev/my_vg/my_lv /mnt/lvm
```

### Step 6: Verify the Mount
Check the disk space and ensure the volume is successfully mounted:
```bash
df -h
```

---

## 💻 Implementation Code (Commands Summary)
```bash
sudo pvcreate /dev/sdb1
sudo vgcreate my_vg /dev/sdb1
sudo lvcreate -L 2G -n my_lv my_vg
sudo mkfs.ext4 /dev/my_vg/my_lv
sudo mkdir -p /mnt/lvm
sudo mount /dev/my_vg/my_lv /mnt/lvm
df -h
```

---

## 📥 Sample Output

**Creating Physical Volume:**
```text
$ sudo pvcreate /dev/sdb1
Physical volume '/dev/sdb1' successfully created
```

**Mounting and Verifying:**
```text
$ sudo mount /dev/my_vg/my_lv /mnt/lvm
$ df -h
Filesystem                   Size  Used Avail Use% Mounted on
/dev/mapper/my_vg-my_lv      2.0G   24M  1.9G   2% /mnt/lvm
```

---

## ✅ Result
The Logical Volume Management (LVM) was successfully configured. A physical volume was initialized, combined into a volume group, and a 2GB logical volume was created, formatted, and mounted to `/mnt/lvm` successfully.
