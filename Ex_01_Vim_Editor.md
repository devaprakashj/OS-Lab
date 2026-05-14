# Exercise 1: Writing and Editing Text Files Using VIM Editor

## 🎯 Aim
To learn how to create, write, and edit text files using the Vim editor in the Linux environment and to understand the different modes of operation in VIM.

## 📝 Procedure
1. Open the Red Hat Linux terminal. (Right-click on desktop -> Open Terminal)
2. Create or open a file using the command:
   ```bash
   vim sample.txt
   ```
3. The editor opens in **Normal Mode** by default.
4. Press `i` to enter **Insert Mode** and start typing the content.
5. After editing the file, press `Esc` to return to **Normal Mode**.
6. Save the file and exit using different VIM commands.

---

## ⚙️ Modes of Operation in VIM

### 1. Normal Mode
- Default mode when VIM starts.
- Used for navigation and command execution.
- **Examples:**
  - `dd` → delete a line
  - `yy` → copy a line
  - `p` → paste copied text
  - `u` → undo last action

### 2. Insert Mode
- Used for typing or editing text.
- **Enter using:**
  - `i` → insert before cursor
  - `a` → insert after cursor
  - `o` → open a new line
- Press `Esc` to return to Normal Mode.

### 3. Command Mode (Last Line Mode)
- Used to save, quit, and execute commands.
- **Examples:**
  - `:w`  → Save file
  - `:q`  → Quit VIM
  - `:wq` → Save and quit
  - `:q!` → Quit without saving

---

## 💻 Implementation Code (Commands to Type)

**1. Open or create a file:**
```bash
vim sample.txt
```

**2. Enter insert mode:**
Press the `i` key on your keyboard.

**3. Type the content:**
```text
Operating Systems Lab
Learning VIM editor commands.
```

**4. Return to normal mode:**
Press the `Esc` key.

**5. Save and exit:**
Type the following and press Enter:
```vim
:wq
```

---

## 📥 Sample Input & Output

**Command to run:**
```bash
vim sample.txt
```

**Typed content inside the file:**
```text
Operating Systems Lab
Learning VIM editor commands.
```

**To Display the saved file output, run:**
```bash
cat sample.txt
```

**Output:**
```text
Operating Systems Lab
Learning VIM editor commands.
```

---

## ✅ Result
Thus, the experiment was successfully performed to create, write, and edit text files using the VIM editor in Linux. The different modes of VIM such as Normal Mode, Insert Mode, and Command Mode were studied and used for file editing and management.
