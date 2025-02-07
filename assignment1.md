## Assingment 1

# Account Setup
- In  the first step, I'd created a Microsoft Azure account using email address that university had provoded me.

- Then I got  to know about the cloud and its' importance. 

- Additionally, I explored student benefits  and open an student account and Azure give me **$100** worth of credits that I can use to purchase any package within the environment.


# Create Virtual Machine
- I created virtual machine where I have to work later on this course.

- Then I select Marketplace from **Ubuntu Server 24.04 LTS gen 2 Server** published by Canonical. 

- I named my machine **"zap-robotics"**.

- I choose B series version 2 which is **Standard_B2ls_v2**.

- Later, I create a new resource group for the machine and subnet to place the machine in.

# Link my HAMK email to my GitHub account

- I create a new repository named **"linux"** for the assignment.

- Then I add my HAMK email as a secondary mail for version control.

![screenshot 1](img/image.png)

## Assingment 3

This task is the process of creating users and managing permissions in a Linux environment. The tasks include creating different users, managing sudo privileges, and setting up a shared directory with specific permissions.

### Task 1: Creating User Tupu

The adduser script was used to create the Tupu user. This script provides an interactive way to create a new user with all necessary directories and settings.

![ss 1](https://github.com/user-attachments/assets/83cc20a3-79f0-4f3e-8342-765c2a0ac0df)


The adduser script automatically:
- Creates the home directory
- Sets up default shell
- Prompts for password
- Creates user-specific group
- Sets up basic profile

### Task 2: Creating User Lupu

Initially, I tried using the following given command:

``` bash
sudo useradd -m -d /home/lupu -s /bin/bash -G lupu lupu
```

But, this resulted in an error.The issue was that we tried to add the user to a group that doesn't exist yet. To fix this, I modified the command to include the -U flag, which automatically creates a user group with the same name as the user.
After creation,I set the password.

![ss 2](https://github.com/user-attachments/assets/c94493b6-3394-49cc-a092-7d2b578dcaf9)

### Task 3: Creating System User Hupu

Created a system user Hupu with restricted login capabilities.

![ss 3](https://github.com/user-attachments/assets/2d85b12b-97e3-4419-a63a-1f79c8654aec)


It creates a system account that:

- Has no login shell (/bin/false)
- Is typically used for running services
- Has no home directory by default

### Task 4: Adding Sudo Privileges

Added sudo privileges for both Tupu and Lupu users using the usermod command.

Then I add:

``` bash
tupu ALL=(ALL:ALL) ALL
lupu ALL=(ALL:ALL) ALL
```
![ss 4](https://github.com/user-attachments/assets/2a37164a-1cc3-4114-a999-16662a4743d4)
![ss 5](https://github.com/user-attachments/assets/ab05e686-987a-4f48-bd8b-fa3e37f3a2eb)


### Task 5: Setting Up Shared Directory

This task required creating a shared directory with specific permissions for Tupu and Lupu. Here's the steps:

![Ss 6](https://github.com/user-attachments/assets/b09f8778-5754-4b46-8bf4-71ac65024f28)


The permission setup (2770) breaks down as:

- 2: SetGID bit (ensures new files inherit group ownership)
- 7: Owner has full permissions (read/write/execute)
- 7: Group has full permissions (read/write/execute)
- 0: Others have no permissions

This configuration ensures:

- Only Tupu and Lupu can access the directory
- New files automatically inherit the projekti group
- Other users cannot access the directory
- Both users have full control over the directory and its contents

- ## Assingment 5

In this assignment, we created a shell script called print.sh to add a line to the file discspace.txt, reporting the home directory size and the current date and time. We used crontab to schedule this script to run every 12 hours,it runs at least six times to populate discspace.txt with multiple entries. Finally, we used command using awk-tool to find the line with the maximum value in the first column and printed it. 

## Create a script and add it to cron

we use `print.sh` command to add a line to the file discspace.txt, reporting the home directory size and the current date.

![image](https://github.com/user-attachments/assets/e42375a2-69fc-4efe-98b4-b323440333ae)

we use `crontab -e` command to open your crontab file:

Then I use `0 */12 * * * /home/zap/print.sh` to run the print.sh script every 12 hours:

![image](https://github.com/user-attachments/assets/55ee8eb7-c0bf-4d40-b7ac-d5e0816f16f8)

## Run the script a minimum of 6 times

After adding the script to cron, it will automatically run every 12 hours, adding a line to discspace.txt each time. Ensure that it runs at least 6 times so that the file contains at least 6 lines.

![image](https://github.com/user-attachments/assets/adc48173-f47c-45fe-80b4-761f24c1ae2c)


## Find and print the line containing the maximum size

I use the following awk command to find the line with the maximum size and print it in the specified format:

``` bash
awk 'NR == 1 || $1 > max { max = $1; max_line = $0 } END { print "Max=" max ", at " substr(max_line, index(max_line, $2)) }' /home/zap/discspace.txt
```

![image](https://github.com/user-attachments/assets/43777bdd-08fd-4e3e-b97e-7f20fe1825da)

# Assingment 6


# Part 1: Understanding APT & System Updates

### 1.APT Version Check

Command executed:
``` bash
apt --version
```

Output:

![image](https://github.com/user-attachments/assets/ac35da41-708b-4d7b-ae9a-5370f95c7b6b)


### 2. Package List Update

Command executed:
``` bash
sudo apt update
```
Output:

![image](https://github.com/user-attachments/assets/325da726-ee81-48f6-8e18-1fbabd9a9fc5)

 **This step is important because:**

- Ensures the system has the latest information about available packages
- Helps identify which packages need updates
- It synchronizes the local package index with the remote repositories
- Required before performing any package installations or upgrades


### 3. Upgrade installed packages

Command executed:
``` bash
sudo apt upgrade -y
```
Output:

![image](https://github.com/user-attachments/assets/f709ff35-8749-4892-9d6d-3bd0e724bd0a)

![image](https://github.com/user-attachments/assets/7daed2e2-25ca-410e-8f24-88d1c3925692)


**Difference between update and upgrade:**

- apt update only refreshes the package index and metadata
- apt upgrade actually downloads and installs newer versions of installed packages

### 4. Pending Updates Check

Command executed:
``` bash
apt list --upgradable
```

Output:

![image](https://github.com/user-attachments/assets/da5b43af-3125-4196-806b-317f5799fec4)


# Part 2: Installing & Managing Packages

### 5. Search for a package using APT

Command executed:
``` bash
apt search image editor
```

*Selected package: kolourpaint ( simple image editor and drawing application)*

### 6. View Package Details

Command executed:
``` bash
apt show kolourpaint
```

Output:

![image](https://github.com/user-attachments/assets/18508f48-578d-4bf4-894d-563c3cb789d8)


**Dependencies:**

- kio, libc6 (>= 2.38), libkf5configcore5 (>= 4.97.0), libkf5configgui5 (>= 4.97.0), libkf5configwidgets5 (>= 5.23.0), libkf5coreaddons5 (>= 5.16.0), libkf5guiaddons-bin, libkf5guiaddons5 (>= 5.90.0~), libkf5i18n5 (>= 5.90.0~), libkf5jobwidgets5 (>= 5.90.0~), libkf5kiocore5 (>= 5.90.0~), libkf5kiofilewidgets5 (>= 5.90.0~), libkf5kiogui5 (>= 5.90.0~), libkf5sane5 (>= 23.08.5~), libkf5textwidgets5 (>= 5.90.0~), libkf5widgetsaddons5 (>= 5.100.0), libkf5xmlgui5 (>= 5.90.0~), libqt5core5t64 (>= 5.15.2~), libqt5gui5t64 (>= 5.15.2~) | libqt5gui5-gles (>= 5.15.2~), libqt5printsupport5t64 (>= 5.15.2~), libqt5widgets5t64 (>= 5.15.2~), libstdc++6 (>= 4.1.1)

### 7. Package Installation

Command executed:
``` bash
sudo apt install kolourpaint -y
```

*Installation was successful, verified by launching the application.*

### 8. Version Check

Command executed:
``` bash
apt list --installed | grep kolourpaint
```

Output:

![image](https://github.com/user-attachments/assets/3597fe88-8042-4457-ae74-7666fc1c47fc)


# Part 3: Removing & Cleaning Packages

### 9. Uninstall the package

Command executed:
``` bash
sudo apt remove kolourpaint -y
```

*Note: This removes the package but keeps configuration files.*

### 10. Remove Configuration files

Command executed:
``` bash
sudo apt purge kolourpaint -y
```

**Difference between remove and purge:**

- remove only uninstalls the package binaries
- purge removes both the binaries and configuration files

### 11. Clear Unnecessary Dependencies

Command executed:
``` bash
sudo apt autoremove -y
```

**This step is important because:**

- Removes packages that were installed as dependencies but are no longer needed
- Keeps the system clean from unused software
- Free disk space


### 12. Clean Up Downloaded Package Files

Command executed:
``` bash
sudo apt clean
```

**This command:**

- Removes all downloaded package files (.deb) from the local cache
- Frees up disk space in /var/cache/apt/archives/
- Doesn't affect installed packages

# Part 4: Managing Repositories & Troubleshooting

### 13. Repository List

Command executed:
``` bash
cat /etc/apt/sources.list
```

Output:

![image](https://github.com/user-attachments/assets/ac63d78d-b4e7-4682-be54-ef3761398e34)

**Observations:**

- Contains main Ubuntu repositories
- Includes different components (main, restricted, universe, multiverse)
- Lists both source and binary package repositories
- Contains security updates repositories

### 14. To Add Universe Repository

Command executed:
``` bash
sudo add-apt-repository universe
sudo apt update
```

Output:

![image](https://github.com/user-attachments/assets/0862c2c9-f1da-488d-8c54-748c5db851fd)

**Universe repository contains:**

- Community-maintained software
- Wide range of applications
- Less official support
  

### 15. Installation Failure Simulation

Command executed:
``` bash
sudo apt install fakepackage
```

Error message:

![image](https://github.com/user-attachments/assets/f3c0ca33-f800-4a6b-ada0-fad0e6d0e070)

**Troubleshooting steps:**

1. Check package name 
2. Check repositories
3. Update package lists
4. Search for package
5. Fix broken package

### _Bonus Challenge: Package Hold Management_

Commands executed:
``` bash
sudo apt-mark hold firefox
sudo apt-mark unhold firefox
```
![image](https://github.com/user-attachments/assets/4c35a087-2474-4a35-bae0-2c648caa620b)

**Reasons to hold a package:**

- To prevent unwanted updates
- To maintain a stable version of a package that is known to work well with your system.
- To custom configurations
- To test new versions of other packages without affecting the held package.




