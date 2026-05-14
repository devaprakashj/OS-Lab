# Exercise 13 (b): Deploy an Application by Cloning a GitHub Repository

## 🎯 Aim
To deploy an application in Linux by cloning a GitHub repository using Git.

## 📚 Theory
**Git** is a distributed version control system used to manage source code.
**GitHub** is a hosting platform for Git repositories that allows developers to collaborate and deploy applications.

**Deployment process includes:**
1. Install Git
2. Clone repository
3. Build/run the application

**Benefits:**
- Easy application deployment
- Version tracking
- Collaboration support

---

## 📝 Procedure

### Step 1: Install Git
Update package lists:
```bash
sudo apt update
```
Install Git:
```bash
sudo apt install git
```

### Step 2: Verify Git Installation
Check the installed version of Git:
```bash
git --version
```

### Step 3: Clone GitHub Repository
Clone the application from GitHub using its repository URL.
*Example repository:*
```bash
git clone https://github.com/git/git.git
```
*This downloads the project to the local system.*

### Step 4: Navigate to Repository Folder
Change directory into the cloned project folder:
```bash
cd git
```

### Step 5: Run or Build Application
Compile or build the application. *Example command:*
```bash
make
```
*(Or run initialization scripts depending on the specific project, like `npm install`, `python app.py`, etc.)*

### Step 6: Verify Application Deployment
Check the files to ensure deployment was successful:
```bash
ls
```

---

## 💻 Implementation Code (Commands Summary)
```bash
sudo apt update
sudo apt install git
git --version
git clone https://github.com/git/git.git
cd git
ls
```

---

## 📥 Sample Input & Output

**Sample Input:**
```text
Repository URL: https://github.com/git/git.git
```

**Sample Output of `git --version`:**
```text
git version 2.34.1
```

**Sample Output of cloning:**
```text
Cloning into 'git'...
remote: Enumerating objects: 300000, done.
Receiving objects: 100% (300000/300000)
Resolving deltas: 100% done.
```

---

## ✅ Result
The application was successfully deployed by cloning the GitHub repository using Git.
