# Exercise 8: Installation of VMware on Linux Host and Adding Guest Operating System

## 🎯 Aim
To install VMware Workstation/VMware Player on a Linux host system and create a Guest Operating System Virtual Machine.

## 🛠️ Requirements

**Software Requirements:**
1. Linux Operating System (Ubuntu / Fedora / Debian / Red Hat)
2. VMware Workstation Player / VMware Workstation Pro
3. Guest OS ISO file (Example: Windows / Ubuntu)
4. Internet connection

**Hardware Requirements:**
1. Processor: Intel/AMD processor with Virtualization Support
2. RAM: Minimum 8 GB recommended
3. Storage: Minimum 20 GB free disk space

## 📚 Theory
**Virtualization** is a technology that allows multiple operating systems to run on a single physical computer using a hypervisor.
**VMware** is a virtualization software that enables users to create virtual machines (VMs) that behave like real computers.
- **The Host OS** is the operating system installed on the physical machine.
- **The Guest OS** runs inside the virtual machine created by VMware.

**Advantages:**
- Testing different operating systems.
- Software development.
- Running legacy applications.
- Safe experimentation environment.

---

## 📝 Procedure

### Part A: Download and Install VMware

**Step 1: Download VMware**
1. Open a web browser and visit the [VMware official website](https://www.vmware.com).
2. Navigate to: `Products → Workstation Player`.
3. Download the Linux bundle file (Example: `VMware-Player-Full-17.x.x.bundle`).

**Step 2: Open Terminal in Linux**
Press `Ctrl + Alt + T` (or right-click on Desktop -> Open Terminal).

**Step 3: Navigate to Download Folder**
```bash
cd Downloads
ls
```

**Step 4: Make the Installer Executable**
```bash
chmod +x VMware-Player-Full-*.bundle
```

**Step 5: Install VMware**
Run the installer using root privileges:
```bash
sudo ./VMware-Player-Full-*.bundle
```
*Enter your root password when prompted. The VMware installation wizard will open. Follow the on-screen instructions (Accept License Agreement, etc.) to complete the installation.*

*(Expected Screenshots for Record: Welcome Screen, Accept License Agreement, Installation Progress).*

---

### Part B: Creating Guest Operating System

**Step 6: Launch VMware**
Open VMware from the applications menu: `VMware Workstation Player`.

**Step 7: Create a New Virtual Machine**
1. Click on **Create a New Virtual Machine**.
2. Select **Installer disc image file (ISO)**.
3. Browse and select your Guest OS ISO file (Example: `ubuntu-22.04.iso`).

**Step 8: Select Guest Operating System**
1. Choose Operating System: **Linux**
2. Choose Version: **Ubuntu 64-bit** (or whichever OS you are installing).

**Step 9: Name the Virtual Machine**
1. Enter a name (Example: `Ubuntu VM`).
2. Choose the storage location for your virtual machine files.

**Step 10: Allocate Disk Size**
1. Set the Maximum disk size (Example: `20 GB`).
2. Choose **Store virtual disk as single file**.

**Step 11: Finalize and Power On**
1. Review the Virtual Machine Hardware Configuration.
2. Click **Finish**.
3. Click **Play Virtual Machine** to power it on and begin the Guest OS installation process.

---

## ✅ Result
Thus, the experiment was successfully performed. VMware Workstation Player was downloaded, installed on the Linux host system, and a Guest Operating System Virtual Machine was successfully created and configured.
