# Exercise 2: Linux File System Hierarchy and Creating a Development Directory Structure

## 🎯 Aim
To study the File system Hierarchy Standard in the Linux operating system by explaining any seven important directories and to create a development directory structure using Linux commands.

## 📝 Procedure

### Part A: Study of Linux File System Hierarchy
1. Open the Linux terminal.
2. Display the root directory structure using:
   ```bash
   ls /
   ```
3. Identify and study the important directories in the Linux file system.
4. Note the purpose and usage of at least seven directories.

### Part B: Creating a Development Directory Structure
1. Create a main directory named `development`:
   ```bash
   mkdir development
   ```
2. Move into the directory:
   ```bash
   cd development
   ```
3. Create subdirectories for different development components such as:
   - source code
   - documentation
   - scripts
   - build files
4. Use the `mkdir` command to create these directories.
5. Verify the created structure using the `ls` command.

---

## 📂 Important Linux Directories

| Directory | Description |
|-----------|-------------|
| `/`       | Root directory; the top-level directory that contains all other directories in Linux. |
| `/bin`    | Contains essential user command binaries such as `ls`, `cp`, `mv`, and `cat`. |
| `/etc`    | Stores system configuration files and settings. |
| `/home`   | Contains personal directories for all users. |
| `/dev`    | Contains device files representing hardware devices such as disks and printers. |
| `/usr`    | Contains user programs, libraries, and documentation. |
| `/var`    | Stores variable data such as logs, mail files, and temporary files. |

---

## 💻 Implementation Code (Linux Commands)

**1. Display root directories:**
```bash
ls /
```

**2. Create development directory and move into it:**
```bash
mkdir development
cd development
```

**3. Create subdirectories (You can do this in one line):**
```bash
mkdir src docs scripts build tests
```

**4. Display directory structure:**
```bash
ls
```

*(Optional) To view it exactly like the tree structure, you can use:*
```bash
tree
```

---

## 📥 Sample Input & Output

**Sample Input Commands:**
```bash
mkdir development
cd development
mkdir src docs scripts build tests
ls
```

**Sample Output:**
```text
build  docs  scripts  src  tests
```

**Example Directory Structure Representation:**
```text
development
│
├── src
├── docs
├── scripts
├── build
└── tests
```

---

## ✅ Result
Thus, the experiment was successfully performed to study seven important directories in the Linux File System Hierarchy and to create a development directory structure using Linux commands such as `mkdir`, `cd`, and `ls`. The exercise helps in understanding how Linux organizes system files and development environments.
