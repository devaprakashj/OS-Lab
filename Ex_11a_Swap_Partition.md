# Exercise 11 (a): Create and Activate a Swap Partition

## 🎯 Aim
To create and activate a swap partition in Linux to extend the system’s virtual memory.

## 📚 Theory
Swap space is used when the physical RAM is full. Linux temporarily moves inactive memory pages from RAM to swap space on disk. This helps prevent system crashes and allows more processes to run.

**Types of swap:**
- Swap Partition
- Swap File

In this experiment, we create a swap partition.

---

## 📝 Procedure

### Step 1: Check Existing Swap
Open terminal and run:
```bash
swapon --show
# or
free -h
```

### Step 2: List Available Disks
Check disk partitions:
```bash
sudo fdisk -l
```

### Step 3: Create a New Partition
Run disk partition tool:
```bash
sudo fdisk /dev/sda
```
**Follow these steps inside `fdisk`:**
| Command | Description | Example Input |
|:---:|---|---|
| `n` | Create new partition | `n` |
| `p` | Primary partition | `p` |
| Partition no. | Choose partition number | `3` |
| First sector | Default | *(Press Enter)* |
| Last sector | Set size | `+2G` |

### Step 4: Change Partition Type to Swap
Inside `fdisk`, type `t` to change the partition type, and enter `82` (Type 82 represents Linux swap). Save changes by typing `w` and pressing Enter.

### Step 5: Format the Partition as Swap
```bash
sudo mkswap /dev/sda3
```

### Step 6: Activate Swap Partition
```bash
sudo swapon /dev/sda3
```

### Step 7: Verify Swap
```bash
swapon --show
# or
free -h
```

---

## 💻 Implementation Code (Commands Summary)
```bash
sudo fdisk -l
sudo fdisk /dev/sda
sudo mkswap /dev/sda3
sudo swapon /dev/sda3
swapon --show
free -h
```

---

## 📥 Sample Input & Output

**Sample Inputs during creation:**
- Partition size: `+2G`
- Partition type: `82`
- Device name: `/dev/sda3`

**Sample Output (`swapon --show`):**
```text
NAME       TYPE      SIZE USED PRIO
/dev/sda3  partition   2G   0B   -2
```

**Sample Output (`free -h`):**
```text
              total        used        free      shared  buff/cache
Mem:           7.7G        1.8G        3.9G        120M        2.0G
Swap:          2.0G          0B        2.0G
```

---

## ✅ Result
The swap partition was successfully created and activated in the Linux system, extending the virtual memory capabilities.
