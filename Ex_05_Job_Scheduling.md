# Exercise 5: Job Scheduling in Linux (Using `at` and `cron`)

## 🎯 Aim
To study and implement job scheduling in Linux using the `at` command for one-time task scheduling and the `cron` scheduler for recurring job execution.

## 📝 Procedure

### Part A: Schedule Jobs Using `at` (One-time Job)
1. Open the Linux terminal.
2. Ensure the `at` service is installed and running.
3. Schedule a job using the command:
   ```bash
   at time
   ```
4. After entering the `at` prompt, type the command that should execute at the scheduled time.
5. Press `Ctrl + D` to save and exit.
6. View scheduled jobs using:
   ```bash
   atq
   ```
7. Remove a scheduled job (if required):
   ```bash
   atrm job_number
   ```

### Part B: Schedule Recurring Jobs Using `cron`
1. Open the crontab editor using:
   ```bash
   crontab -e
   ```
2. Add a cron entry in the format:
   ```bash
   * * * * * command
   ```
3. Save and exit the editor.
4. View scheduled cron jobs using:
   ```bash
   crontab -l
   ```

---

## ⏱️ Understanding Cron Time Fields

The five time fields (`* * * * *`) represent:

| Field | Meaning | Range |
|:---:|---|---|
| 1st | Minute | 0 – 59 |
| 2nd | Hour | 0 – 23 |
| 3rd | Day of Month | 1 – 31 |
| 4th | Month | 1 – 12 |
| 5th | Day of Week | 0 – 7 (Sunday = 0 or 7) |

**Example:** Run a script every day at 5:30 PM:
```bash
30 17 * * * /path/to/script.sh
```

---

## 💻 Implementation Code (Linux Commands)

**1. Schedule a one-time job using `at`:**
```bash
at 16:30
warning: commands will be executed using /bin/sh
at> echo "Hello Linux Scheduling" > test.txt
at> <EOT>  # Press Ctrl + D here to save and exit
```

**2. View and Remove `at` scheduled jobs:**
```bash
atq
atrm 1
```

**3. Schedule recurring job using `cron`:**
```bash
crontab -e
```

**4. Cron entry example (runs every minute):**
*(Paste this inside the crontab editor)*
```text
* * * * * echo "Cron Job Running" >> cron_output.txt
```

**5. View cron jobs:**
```bash
crontab -l
```

---

## 📥 Sample Input & Output

**Sample Input Commands:**
```bash
at 16:30
at> echo "Job executed using at command" > job.txt
at> <EOT>  # Press Ctrl + D
```

**Cron job entry:**
```text
* * * * * echo "Cron job executed" >> cron.txt
```

**Sample Output:**
```bash
$ atq
1	Tue Mar 10 16:30:00 2026 a student

$ cat job.txt
Job executed using at command

$ cat cron.txt
Cron job executed
Cron job executed
Cron job executed
```

---

## ✅ Result
Thus, the experiment was successfully performed to schedule jobs in Linux using:
- `at` command for one-time job scheduling.
- `cron` scheduler for recurring job execution.

This demonstrates how the Linux operating system manages background tasks and automates repetitive workflows efficiently.
