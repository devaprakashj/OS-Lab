# Exercise 13 (a): Perform Root Password Recovery Using Rescue/Emergency Mode

## 🎯 Aim
To recover or reset the root password in Linux using Rescue/Emergency mode.

## 📚 Theory
In Linux systems, the root user has administrative privileges. If the root password is forgotten, it can be reset by booting into rescue mode or emergency mode.

**Rescue mode allows administrators to:**
- Access the system with minimal services
- Repair the system
- Reset the root password
- Fix boot errors

The password reset is done by editing the GRUB boot parameters and booting into a root shell.

---

## 📝 Procedure

### Step 1: Restart the System
Reboot the Linux system.

### Step 2: Open GRUB Menu
During boot, quickly press:
- `Shift` (for Ubuntu/Debian based systems)
- `Esc` (for Red Hat/CentOS based systems)

This opens the GRUB boot menu.

### Step 3: Edit GRUB Entry
1. Select the primary Linux kernel entry using the arrow keys.
2. Press `e` to edit its boot parameters.

### Step 4: Modify Boot Parameters
Find the line starting with:
```text
linux /boot/vmlinuz...
```
Add the following at the very end of that line:
```text
rd.break
```
*(Alternatively, you can use `init=/bin/bash` depending on the Linux distribution)*

### Step 5: Boot into Emergency Mode
Press `Ctrl + X` or `F10`.
The system will now boot directly into a single-user root shell.

### Step 6: Remount File System
By default, the root filesystem is mounted as read-only. Change it to read-write by executing:
```bash
mount -o remount,rw /
```

### Step 7: Reset Root Password
Run the password command to change the root password:
```bash
passwd root
```
Enter and confirm the new password.

### Step 8: Reboot the System
Save and reboot the system normally:
```bash
exec /sbin/init
# or
reboot
```

---

## 💻 Implementation Code (Commands Summary in Root Shell)
```bash
mount -o remount,rw /
passwd root
reboot
```

---

## 📥 Sample Input & Output

**Sample Input during password prompt:**
```text
New password: admin123
Retype new password: admin123
```

**Sample Output:**
```text
passwd: password updated successfully
```

---

## ✅ Result
The root password was successfully recovered and updated using the Linux rescue/emergency mode.
