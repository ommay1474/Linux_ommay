# Virtualization Assignment

## Student Information
Name: Ommay Habiba Khatun Bristi  
Email: amk1006788@student.hamk.fi  
Date: 17.03.2026  

---

# Part 1: Introduction to Virtualization Concepts

## Virtualization
Virtualization is the process of creating virtual versions of computing resources such as operating systems, storage, and networks. It enables multiple virtual environments to run on a single physical machine, improving resource utilization and flexibility.

## Hypervisor
A hypervisor is a software layer that enables virtualization by allowing multiple virtual machines (VMs) to share the same physical hardware. It manages system resources and ensures isolation between virtual machines.

## Virtual Machines (VMs)
Virtual Machines are software-based emulations of physical computers. Each VM runs its own operating system and applications, behaving like an independent system with dedicated virtual hardware.

## Containers
Containers are lightweight virtualization environments that package applications together with their dependencies. They run on the host operating system and share the host kernel while maintaining isolated user spaces.

## Difference Between VM and Container

| VM | Container |
|----|----------|
| Full OS | Shared OS |
| Heavy | Lightweight |
| Slow start | Fast start |
| Strong isolation | Process isolation |

## Summary
Virtual machines provide full system isolation but require more resources, while containers are lightweight, faster, and more efficient but share the host kernel. The choice depends on use case and resource requirements.

---

# Part 2: Multipass Virtualization

## Install Multipass
```bash
sudo snap install multipass
multipass version
```
![](img/Archive/multipass%20inst%20v.png)
Explanation: Installs Multipass and verifies installation.

---

## Create VM
```bash
multipass launch
multipass list
multipass info relieving-kagu
```
![](img/Archive/launch.png)
![](img/Archive/Multipass%20list.png)
![](img/Archive/info%20name%20r.png)

Explanation: Creates and checks VM status.

---

## Access VM
```bash
multipass shell relieving-kagu
```
![](img/Archive/shell.png)
Explanation: Opens VM terminal.

---

## Create File
```bash
multipass exec relieving-kagu -- bash -c "echo 'Hello' > hello.txt"
multipass exec relieving-kagu -- cat hello.txt
```
![](img/Archive/multi%20cat%20he%20w.png)
Explanation: Creates and reads file inside VM.

---

## Stop & Delete
```bash
multipass stop relieving-kagu
multipass delete relieving-kagu
multipass purge
```
![](img/Archive/multipass%20stop%20d%20p.png)
Explanation: Stops and removes VM.

---
## Cloud-init Configuration

Created a cloud-init configuration file.

### Command
```
nano cloud-init.yml
```

### Configuration
```yaml
#cloud-config
users:
  - name: ommayb
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']

packages:
 - git
 - curl
 - vim
 - htop
 - nano

runcmd:
 - echo "Cloud-init is working!" > /home/ommayb/welcome.txt
 - apt update && apt upgrade -y
```
![](img/Archive/nano%20ommayb.png)
### Explanation
Cloud-init automates VM setup such as installing packages and creating users.
---

## Launching VM with Cloud-init

Started a VM using the configuration file.

### Command
```
multipass launch --name ommayb --cloud-init cloud-init.yml
```
![](img/Archive/ommayb%20cloud%20init.png)
### Explanation
This creates a VM with automatic configuration applied during startup.

## Accessing the New VM

Entered the new VM.

### Command
```
multipass shell ommayb
```
![](img/Archive/shell%20ommayb.png)

---

## Verifying Cloud-init Execution

Checked if cloud-init worked correctly.

### Command
```
sudo cat /home/ommayb/welcome.txt
```

### Expected Output
```
Cloud-init is working!
```
![](img/Archive/ommayb%20welcome%20txt.png)
### Explanation
Confirms that cloud-init executed successfully.

## Shared Folder Between Host and VM

Created and mounted a shared folder.

### Commands
```
mkdir ~/host_machine
multipass mount ~/host_machine ommayb:/home/ubuntu/shared_folder
```

### Explanation
Allows file sharing between host system and VM.

## Creating a File in Host Machine

Created a test file on host.

### Command
```
echo "Hello from the host!" > ~/host_machine/hostfile.txt
```

## Verifying File Inside VM

Checked the shared file inside VM.

### Commands
```
multipass shell ommayb
ls /home/ubuntu/shared_folder
cat /home/ubuntu/shared_folder/hostfile.txt
```
### Expected Output
```
Hello from the host!
```
![](img/Archive/hostfile.png)
### Explanation
Confirms successful file sharing between host and VM.

## Part 3: Install and Configure LXD / LXC

This section demonstrates installation and basic usage of LXD containers.

---

### Step 1 – Install Snap

**Command**
```
sudo apt install snap -y
```
![](img/snap-y%20inst.png)
**Explanation**  
Installs Snap package manager required for LXD installation.

---

### Step 2 – Install LXD

**Command**
```
sudo snap install lxd
```
![](img/lxd%20inst.png)
**Explanation**  
Installs LXD for managing Linux containers.
---

### Step 3 – Check LXD Version

**Command**
```
lxd --version
```
![](img/lxd%20v.png)
**Explanation**  
Displays LXD version to confirm installation.

---

### Step 4 – Add User to LXD Group

**Command**
```
sudo usermod -aG lxd $USER
newgrp lxd
```
![](img/sudo%20user%20-aG.png)
**Explanation**  
Allows the user to manage containers without sudo.

---

### Step 5 – Initialize LXD

**Command**
```
lxd init
```
![](img/lxc%20init.png)
**Explanation**  
Initializes and configures LXD (storage, network, etc.).

**Configuration Used**
- Clustering → no  
- Storage → yes  
- Backend → dir  
- Network bridge → yes  
- IPv4 → auto  
- IPv6 → auto  
- LXD over network → no  

---

### Step 6 – Verify Configuration

**Commands**
```
lxc profile list
lxc network list
lxc storage list
```
![](img/lxc%20prof.png)
![](img/lxc%20net.png)
![](img/lxc%20storage.png)
**Explanation**  
Verifies LXD configuration including profiles, networks, and storage.

---

### Step 7 – List Images

**Command**
```
lxc image list images:
```
![](img/lxc%20img%20list.png)
**Explanation**  
Lists available container images.

---

### Step 8 – Create Container

**Command**
```
lxc launch ubuntu:24.04 demo-container
```

**Explanation**  
Creates and starts a new container.

---

### Step 9 – Check Container

**Command**
```
lxc list
```
![](img/lxc%20cont%20list.png)
**Explanation**  
Displays container status (RUNNING).

---

### Step 10 – Access Container

**Command**
```
lxc exec demo-container -- bash
```
![](img/cont%20bash.png)
**Explanation**  
Accesses the container shell environment.

# Part 4: Docker

## Install Docker
```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```
![](img/sudo%20get%20doc.png)
Explanation: Installs Docker using official script.

---

## Verify
```bash
docker --version
```
![](img/doc%20v.png)
Explanation: Confirms installation.

---

## Add User
```bash
sudo usermod -aG docker $USER
newgrp docker
```
Explanation: Runs Docker without sudo.

---

## Test Docker
```bash
docker run hello-world
```
![](img/doc%20-ag.png)
Explanation: Tests Docker installation.

---

# Part 5: Snap and Snapcraft

## Snap
Snap packages applications with dependencies.

## Snapcraft
Snapcraft is used to build Snap packages.

## Install Snapcraft
```bash
sudo snap install snapcraft --classic
```
Explanation: Installs Snap creation tool.

---

## Create Snap (Basic)
```bash
mkdir my-app
cd my-app
nano snapcraft.yaml
snapcraft
```
Explanation: Creates and builds a Snap package.

---

# Optional: CPU Virtualization Check

```bash
cat /proc/cpuinfo
grep vmx /proc/cpuinfo
sudo apt install cpu-checker
kvm-ok
```
Explanation: Checks CPU virtualization support.

---

# Conclusion

This assignment demonstrated virtualization using Multipass, LXD, Docker, and Snap.

---

# Thank You
