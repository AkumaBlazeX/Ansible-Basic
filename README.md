Here’s the revised markdown with "target's private IP" instead of specific IP addresses:

```markdown
# Ansible Practical Guide

## Overview
This guide explains how to set up Ansible on an Ubuntu server, configure passwordless authentication between two servers, and use Ansible for basic automation tasks. It also covers running a simple playbook to install and start the Nginx service.

---

## Repository Files

1. **`inventory`**  
   Contains the list of target servers with their private IP addresses.  
   Example:
   ```ini
   [all]
   <target's private IP>
   <target's private IP>
   ```

2. **first_playbook.yml**  
   An Ansible playbook to install and start the Nginx service on the target servers.

---

## Steps to Set Up Ansible

### 1. Connect to the Main EC2 Instance
Use the following command to connect to your EC2 instance:
```bash
ssh -i "Key-pair" ubuntu@<main instance public IP>
```

### 2. Update the System and Install Ansible
Run these commands to update the system and install Ansible:
```bash
sudo apt update
sudo apt install ansible
```

---

## Setting Up Passwordless Authentication

### 1. Generate SSH Key on the Main Server
Run the following command to create a passwordless authentication key:
```bash
ssh-keygen
```
**Note**: This generates a private-public key pair.

### 2. Copy the Public Key to the Target Server
On the **main server**, display the contents of your `.pub` file using:
```bash
cat ~/.ssh/id_rsa.pub
```
Log in to the **target server** and append the copied public key to the `authorized_keys` file:
```bash
ssh-keygen
nano ~/.ssh/authorized_keys
```

---

## Testing Ansible Adhoc Commands

### 1. Create an Inventory File
Ensure the `inventory` file contains the private IP addresses of your target servers.

Example:
```ini
[all]
<target's private IP>
<target's private IP>
```

### 2. Run an Ansible Adhoc Command
Use the following command to create a test file on all target servers:
```bash
ansible -i inventory all -m "shell" -a "touch /home/ubuntu/test"
```

---

## Running Your Playbook

### 1. Ensure the `first_playbook.yml` File is Ready
The repository includes a playbook named **`first_playbook.yml`** to install and start Nginx. Ensure it is available in the current directory.

### 2. Run the Playbook
Run the playbook using:
```bash
ansible-playbook -i inventory first_playbook.yml
```

