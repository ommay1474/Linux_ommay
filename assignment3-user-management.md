# Assignment 3 – User Management and File Permissions

## Student Information
- Name: Ommay Habiba Khatun Bristi  
- Student Email: amk1006788@student.hamk.fi   
- Assignment: 3 – User management  
- Platform: Ubuntu Linux VM (Azure)
- Date: 30/01/2026

---

## Task Description
The task is to create users and use the created users to test file access permissions.  
All steps were performed on a Linux Virtual Machine.

---

## Step 1: Create the **Tupu** user using `adduser`

Command:
```bash
sudo adduser tupu
```

This command:
- Creates user `tupu`
- Creates home directory `/home/tupu`
- Creates a group named `tupu`
- Sets password and user information

Verification:
```bash
groups tupu
```

---

## Step 2: Create the **Lupu** user using `useradd`

Create group:
```bash
sudo groupadd lupu
```

Create user:
```bash
sudo useradd -m -d /home/lupu -s /bin/bash -g lupu lupu
```

Set password:
```bash
sudo passwd lupu
```

Verification:
```bash
id lupu
```

---

## Step 3: Create the **Hupu** system user with login disabled

Command:
```bash
sudo useradd --system --shell /bin/false hupu
```

Verification:
```bash
getent passwd hupu
```

This confirms that `hupu` is a system user and cannot log in.

---

## Step 4: Add **Tupu** and **Lupu** to the sudo group

Commands:
```bash
sudo usermod -aG sudo tupu
sudo usermod -aG sudo lupu
```

Verification:
```bash
groups tupu
groups lupu
```

Both users are confirmed members of the `sudo` group.

---

## Step 5: Create `/opt/projekti` directory with restricted access

### Create project group
```bash
sudo groupadd ommayb_projekti
```

### Add users to the group
```bash
sudo usermod -aG ommayb_projekti tupu
sudo usermod -aG ommayb_projekti lupu
```

### Create directory
```bash
sudo mkdir /opt/projekti
```

### Set ownership
```bash
sudo chown root:ommayb_projekti /opt/projekti
```

### Set permissions with setgid
```bash
sudo chmod 2770 /opt/projekti
```

### Verification
```bash
ls -ld /opt/projekti
```

The permissions confirm:
- Only `tupu` and `lupu` can access the directory
- Other users have no permissions
- Files created inside inherit the group automatically

---

## Conclusion
All users were created successfully according to the assignment instructions.  
File permissions were configured so that only `tupu` and `lupu` have access to `/opt/projekti`.  
The system user `hupu` was created with login disabled, fulfilling all requirements.
