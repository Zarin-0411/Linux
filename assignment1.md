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

## Assingment 7

### Linux Virtualization Exercise

### Part 1: Introduction to virtualization concepts

#### Key Concepts Overview

**Virtualization**

Virtualization is a technology that uses software to create multiple virtual machines (VMs) on a single physical computer. Each VM operates like an independent computer, with its own operating system and applications, even though they share the same physical hardware.

**Hypervisor**

A hypervisor (or Virtual Machine Monitor) is software that creates and manages virtual machines. There are two types:

Type 1 (Bare Metal):Runs directly on the host’s hardware and acts like a lightweight operating system.
Type 2 (Hosted): Runs on top of an operating system , like any other software application.

**Virtual Machines (VMs)**

A virtual machine (VM) is a software-based emulation of a physical computer. It runs an operating system and applications just like a physical computer, but it operates within a host environment, which can be a physical server or a cloud infrastructure

**Containers**

Containers are a lightweight form of virtualization that package an application and its dependencies into a single unit, ensuring it runs consistently across different computing environments

#### The main differences between VMs and tanks

**Architecture**

- **VMs**:VMs run a complete operating system, including its own kernel, on top of the host’s hardware.
- **Containers**: Containers share the host operating system’s kernel and run as isolated processes within the host OS.

**Resource Utilization**

- **VMs**: VMs are more resource-intensive because they require a full OS for each VM, leading to higher CPU, memory, and storage usage
- **Containers**:Containers are more resource-efficient as they share the host OS and only include the necessary libraries and dependencies for the application

**Isolation Level**

- **VMs**: VMs provide strong isolation as each VM runs its own OS, making them suitable for running different operating systems on the same hardware
- **Containers**: Containers provide lightweight isolation by sharing the host OS kernel, making them more efficient but less isolated compared to VMs

### Part 2: Multipass Implementation

### Installation

- Install Multipass
``` bash
sudo snap install multipass
```
![image](https://github.com/user-attachments/assets/6c20aaf7-b0e5-4104-b088-808d85f9c7d0)

### Basic Commands Implementation

- Launch default Ubuntu instance

```bash
multipass launch --name primary-vm
```
![image](https://github.com/user-attachments/assets/3275d6ce-a413-4b10-97c1-5e51b87d01bf)

- List running instances

```bash
multipass list
```
![image](https://github.com/user-attachments/assets/edf47b93-2dd3-458a-b97d-7397f4b21419)

- View details about a specific instance

```bash
multipass info primary-vm
```
![image](https://github.com/user-attachments/assets/71bb8116-3260-4bed-8122-3aeb9d54edeb)

- Access to the shell of a running instance

```bash
multipass shell primary-vm
```
![image](https://github.com/user-attachments/assets/66d8d952-84cd-4db3-bedb-2da8b1a77e0b)

- Run the command on the instance

```bash
multipass exec primary-vm -- ls -la
```
![image](https://github.com/user-attachments/assets/68041273-05ed-4ea6-b146-d2e463b1881d)

- Stop the running instance

```bash
multipass stop primary-vm
```
![image](https://github.com/user-attachments/assets/b3ea813c-5548-4d88-bdee-916896c1f9b9)

- Delete the instance

```bash
multipass delete primary-vm
```
![image](https://github.com/user-attachments/assets/a2698178-c54d-4f50-8753-ff07fb693553)


#### Cloud-init Configuration

**Start a New Instance with Multipass**

![image](https://github.com/user-attachments/assets/2f18720d-c818-4296-8a25-1e5a3995932e)


To start a new instance using this cloud-init configuration, you can use the following multipass command:

```bash
multipass launch --name my-instance --cloud-init cloud-init.yaml
```
![image](https://github.com/user-attachments/assets/228fe400-4d38-447c-8d9f-999e5ada5306)
![image](https://github.com/user-attachments/assets/ec89cc62-9a0a-4931-900a-f7ba4fda9a41)

#### File sharing
To share files and folders between your host computer and Multipass instances
```bash
mkdir ~/shared-folder
```
#### Policy
Create a shared folder and access it from both your host and your Multipass instance
```bash
multipass mount ~/shared-folder my-instance:/shared
```
![image](https://github.com/user-attachments/assets/2db73608-8569-4e4d-8ca2-8316dc7786ed)


### Part 3: LXD Implementation

### Create container

```bash
lxc launch ubuntu:20.04 my-container
```
![image](https://github.com/user-attachments/assets/5c134c71-9207-4aaf-a202-d6a1453315d3)

### List containers
```bash
lxc list
```
![image](https://github.com/user-attachments/assets/11abc4ad-b1c4-43f6-835f-bf4959daf27e)

### Execute commands
```bash
lxc exec my-container -- apt update
```

### Stop container
```bash
lxc stop my-container
```

### Delete container

```bash
lxc delete my-container
```

# Part 4: Docker Implementation

#### Installation

```bash
sudo apt update
sudo apt install docker.io
```
### Start and enable Docker

```bash
sudo systemctl start docker
sudo systemctl enable docker
```

- Basic Docker Commands

```bash
docker pull ubuntu:latest
docker run -it ubuntu:latest
docker ps 
docker stop container_id
```
![image](https://github.com/user-attachments/assets/22f3d977-d06e-4447-9ef1-82f2742fe7c3)

![image](https://github.com/user-attachments/assets/29167e32-284a-4222-84c5-850acd831d59)


### Part 5: Snaps for Self-Contained Applications 

#### Creating a Basic Snap
- To install snapcraft:
```bash
sudo apt update
sudo snap install snapcraft --classic
```
- To create a project directory:
```bash
mkdir my-snapcraft
cd my-snapcraft
```
- To make an application script:
```bash
mkdir bin
nano bin/hello-snap
```
- Paste the content
```bash
#!/bin/bash
echo "Hello, Snap!"
```
- To execute script:
```bash
chmod +x bin/hello-snap
```
#### To create the snapcraft yaml file:
```bash
nano snapcraft.yaml
```
Paste the content:
```bash
name: my-snapcraft
base: core22
version: "1.0"
summary: "A simple Snapcraft app"
description: "This is a simple Snap application that prints Hello, Snap!"

grade: stable
confinement: strict

apps:
  hello:
    command: bin/hello-snap

parts:
  hello:
    plugin: dump
    source: .
```
![image](https://github.com/user-attachments/assets/3ad8ec07-ce87-4ec7-91f3-6ee407142e02)

### Build snap
```bash
snapcraft
```
#### Install locally
```bash
sudo snap install my-app_1.0_amd64.snap --dangerous
```
#### Run snap
```bash
my-snapcraft.hello
```
## Assingment 8

### Linux Server Firewall Configuration

### Creating a firewall 

#### 1. Enable UFW on system start

```bash
sudo systemctl enable ufw
sudo ufw enable
```

#### 2. Default Policies

```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
```
![image](https://github.com/user-attachments/assets/449bddd2-e49c-4aa5-9f6b-677c05215ee9)


### Service Rules

#### SSH Server

```bash
sudo ufw allow 22/tcp
sudo ufw limit ssh comment 'Rate limit SSH connections'
```
![image](https://github.com/user-attachments/assets/4a5cd753-b111-4c2a-bc3f-afe3c8fc0f69)


#### Web Server (HTTP/HTTPS) rules

```bash
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
```
![image](https://github.com/user-attachments/assets/f0c52537-82db-45f4-88ea-8625db667d90)


### Logging Configuration

```bash
sudo ufw logging on
sudo ufw logging high
```
![image](https://github.com/user-attachments/assets/6abd91db-c0c1-4c8f-8e3c-c0f4270544cb)


### Protection Against Common Attacks

#### 1. SYN Flood Protection

```bash
# Add to /etc/sysctl.conf
# Enable SYN cookies to prevent SYN flood attacks
net.ipv4.tcp_syncookies = 1

# Increase backlog queue to handle more concurrent SYN packets
net.ipv4.tcp_max_syn_backlog = 2048

# Reduce number of SYN-ACK retries to limit resource consumption
net.ipv4.tcp_synack_retries = 2

# Also add these parameters for additional SYN flood protection
net.ipv4.tcp_syn_retries = 5
net.ipv4.tcp_max_syn_backlog = 2048
net.ipv4.tcp_syncookies = 1
net.ipv4.tcp_ecn = 0
net.ipv4.tcp_wmem = 4096 87380 8388608
net.ipv4.tcp_rmem = 4096 87380 8388608

# Apply settings
sudo sysctl -p
```
![image](https://github.com/user-attachments/assets/0ca24b27-3c80-4587-b944-a16b4e61a1eb)


#### 2. Additional Protection Measures

#### Block invalid packets

**What are invalid packets?**

Invalid packets are those that do not start with the SYN flag alone in a TCP Three-Way Handshake. Any TCP connection that begins with a different flag or an unusual combination of flags, such as those from port-scanning tools like Nmap, should be blocked.

**How UFW blocks invalid packets**

Default rules added by UFW on /etc/ufw/before.rules file:

```bash
# drop INVALID packets (logs these in loglevel medium and higher)
-A ufw-before-input -m conntrack --ctstate INVALID -j ufw-logging-deny
-A ufw-before-input -m conntrack --ctstate INVALID -j DROP
```

Add these two rules below the ones added by default by UFW:

```bash
-A ufw-before-input -p tcp -m tcp ! --tcp-flags FIN,SYN,RST,ACK SYN -m conntrack --ctstate NEW -j ufw-logging-deny
-A ufw-before-input -p tcp -m tcp ! --tcp-flags FIN,SYN,RST,ACK SYN -m conntrack --ctstate NEW -j DROP
```
![image](https://github.com/user-attachments/assets/1ce6e9e7-e3db-4dcf-a66b-8819f048c3f9)


#### Block ping (ICMP) requests

**ICMP flood attack?**

An ICMP flood attack, also known as a ping flood, is a type of Denial of Service (DoS) attack. It overwhelms a system by sending a huge number of ICMP packets, specifically echo requests (pings).

**to prevent ICMP requests**

By commenting the lines below to block ping requests (icmp protocol) by ufw on file /etc/ufw/before.rules:

```bash
# ok icmp codes for INPUT
-A ufw-before-input -p icmp --icmp-type destination-unreachable -j ACCEPT
-A ufw-before-input -p icmp --icmp-type time-exceeded -j ACCEPT
-A ufw-before-input -p icmp --icmp-type parameter-problem -j ACCEPT
-A ufw-before-input -p icmp --icmp-type echo-request -j ACCEPT

# ok icmp code for FORWARD
-A ufw-before-forward -p icmp --icmp-type destination-unreachable -j ACCEPT
-A ufw-before-forward -p icmp --icmp-type time-exceeded -j ACCEPT
-A ufw-before-forward -p icmp --icmp-type parameter-problem -j ACCEPT
-A ufw-before-forward -p icmp --icmp-type echo-request -j ACCEPT
```
![image](https://github.com/user-attachments/assets/5d4dadfe-dc6d-4946-a4ca-3f41027dd979)

Now, reload UFW:

```bash
sudo ufw reload
```
![image](https://github.com/user-attachments/assets/557e835e-06e4-4ad8-a458-91529664846a)

### Verification and Monitoring

```bash
sudo ufw status verbose
sudo tail -f /var/log/ufw.log
```
###Test service accessibility
```bash
nc -zv [server-ip] 22
nc -zv [server-ip] 80
nc -zv [server-ip] 443
```
![image](https://github.com/user-attachments/assets/0db32cfe-ec58-40fa-8b9b-6ddf023bde2e)




