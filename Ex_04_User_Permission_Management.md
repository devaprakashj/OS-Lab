# Exercise 4: User and Permission Management in Linux

## 🎯 Aim
To study and practice user and permission management in Linux by creating and managing users and groups, and by configuring file permissions, ownership, and group ownership.

## 📝 Procedure

### Part A: Create and Manage Users and Groups
1. Open the terminal in Linux.
2. Create a new user using the command:
   ```bash
   sudo useradd username
   ```
3. Set a password for the created user:
   ```bash
   sudo passwd username
   ```
4. Create a new group:
   ```bash
   sudo groupadd groupname
   ```
5. Add the user to a group:
   ```bash
   sudo usermod -aG groupname username
   ```
6. Verify the user and group information using:
   ```bash
   id username
   ```

### Part B: Configure File Permissions, Ownership and Group Ownership
1. Create a sample file:
   ```bash
   touch file1.txt
   ```
2. View the file permissions:
   ```bash
   ls -l file1.txt
   ```
3. Change file permissions using:
   ```bash
   chmod 755 file1.txt
   ```
4. Change file owner:
   ```bash
   sudo chown username file1.txt
   ```
5. Change group ownership:
   ```bash
   sudo chown username:groupname file1.txt
   ```
6. Verify the updated permissions and ownership:
   ```bash
   ls -l file1.txt
   ```

---

## 💻 Implementation Code (Linux Commands)

**1. Create a new user:**
```bash
sudo useradd student1
```

**2. Set password for the user:**
```bash
sudo passwd student1
```

**3. Create a group:**
```bash
sudo groupadd developers
```

**4. Add user to group:**
```bash
sudo usermod -aG developers student1
```

**5. Check user details:**
```bash
id student1
```

**6. Create a file & view permissions:**
```bash
touch file1.txt
ls -l file1.txt
```

**7. Change file permissions, owner, and group:**
```bash
chmod 755 file1.txt
sudo chown student1 file1.txt
sudo chown student1:developers file1.txt
```

**8. Verify changes:**
```bash
ls -l file1.txt
```

---

## 📥 Sample Input & Output

**Sample Input Commands:**
```bash
sudo useradd student1
sudo passwd student1
sudo groupadd developers
sudo usermod -aG developers student1
touch file1.txt
chmod 755 file1.txt
sudo chown student1:developers file1.txt
```

**Sample Output:**
```text
uid=1001(student1) gid=1001(student1) groups=1001(student1),1002(developers)
-rwxr-xr-x 1 student1 developers 0 Mar 10 12:30 file1.txt
```

### 🔑 Explanation of Permissions:

| Permission | Meaning |
|:---:|---|
| `r` | Read |
| `w` | Write |
| `x` | Execute |

**Example Analysis of `rwxr-xr-x` (755):**
- **Owner (7):** Read, Write, Execute (`rwx`)
- **Group (5):** Read, Execute (`r-x`)
- **Others (5):** Read, Execute (`r-x`)

---

## ✅ Result
Thus, the experiment was successfully performed to create and manage users and groups and configure file permissions, ownership, and group ownership in Linux. The commands such as `useradd`, `groupadd`, `chmod`, and `chown` were practiced effectively.
