## Week 5 Homework Submission File: Archiving and Logging Data

Please edit this file by adding the solution commands on the line below the prompt.

Save and submit the completed file for your homework submission.

---

### Step 1: Create, Extract, Compress, and Manage tar Backup Archives

1. Command to **extract** the `TarDocs.tar` archive to the current directory:
tar -xfv <Archive Name> - this extracted the files but also listed them

2. Command to **create** the `Javaless_Doc.tar` archive from the `TarDocs/` directory, while excluding the `TarDocs/Documents/Java` directory:
tar czf Javaless_Docs.tar.gz --exclude "Java" ~/Projects/TarDocs/Documents

3. Command to ensure `Java/` is not in the new `Javaless_Docs.tar` archive:
tar xvf Javaless_Docs.tar.gz | grep "java"
**Bonus** 
- Command to create an incremental archive called `logs_backup_tar.gz` with only changed files to `snapshot.file` for the `/var/log` directory:

#### Critical Analysis Question

- Why wouldn't you use the options `-x` and `-c` at the same time with `tar`?
-x is to extract the data that is already within the archive
-c is creating a tar itself
this command will try and create and then extract files from the tar you've made?
---

### Step 2: Create, Manage, and Automate Cron Jobs

1. Cron job for backing up the `/var/log/auth.log` file:
0 6 * * * tar cvzf /auth_backup.tgz /var/log/auth.log

---

### Step 3: Write Basic Bash Scripts

1. Brace expansion command to create the four subdirectories:
mkdir -vp ~/backups/{freemem,diskuse,openlist,freedisk}
(I know you don't need the v but I like to double check it worked fully)
2. Paste your `system.sh` script edits below:

    ```bash
    #!/bin/bash
    free -h > ~/backups/freemem/free_mem.txt

du -hc > ~/backups/diskuse/disk_usage.txt

lsof > ~/backups/openlist/open_list.txt

df -h --total > ~/backups/freedisk/free_disk.txt


    ```

3. Command to make the `system.sh` script executable:
chmod +x system.sh

**Optional**
- Commands to test the script and confirm its execution:
./system.sh
**Bonus**
- Command to copy `system` to system-wide cron directory:
Depends on which one?
I'm going to say cp
cp system.sh /etc/cron.weekly
---

### Step 4. Manage Log File Sizes
 
1. Run `sudo nano /etc/logrotate.conf` to edit the `logrotate` configuration file. 

    Configure a log rotation scheme that backs up authentication messages to the `/var/log/auth.log`.

    - Add your config file edits below:
    # rotate log files weekly
weekly

# use the syslog group by default, since this is the owning group
# of /var/log/syslog.
su root syslog

# keep 7 weeks worth of backlogs
rotate 7

# do not rotate empty logs
notifempty

# delays compression
delaycompress

# skips error messages for missing logs and continues to next log
missingok


    ```bash
    [Your logrotate scheme edits here]
   /var/log/auth.log {
      weekly
      rotate 7
      notifempty
      delaycompress
      missingok
}
---

### Bonus: Check for Policy and File Violations

1. Command to verify `auditd` is active:
systemctl is-enabled auditd

2. Command to set number of retained logs and maximum log file size:

    - Add the edits made to the configuration file below:
max_log_file = 35
num_logs = 7

    ```bash
    [Your solution edits here]
    ```

3. Command using `auditd` to set rules for `/etc/shadow`, `/etc/passwd` and `/var/log/auth.log`:


    - Add the edits made to the `rules` file below:
# etc/shadow rules
-w /etc/shadow -p wra -k hashpass_audit

# etc/passwd rules
-w /etc/passwd -p wra -k userpass_audit 

# var/log/auth.log rules
-w /var/log/auth.log -p wra -k authlog_audit 


    ```bash
    [Your solution edits here]
    ```

4. Command to restart `auditd`:
Sudo systemctl restart auditd

5. Command to list all `auditd` rules:
auditd -l

6. Command to produce an audit report:
aureport
