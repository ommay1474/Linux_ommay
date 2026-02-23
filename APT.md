# linux-Apt

# APT & System Updates Assignment

## Student Information
- Name: Ommay Habiba Khatun Bristi  
- Student Email: amk1006788@student.hamk.fi   
- Date: 23/02/2026

---

# Part 1: Understanding APT & System Updates

## 1. Check APT Version

Command:
```
apt --version
```

![APT Version](img/apt%20part%201.1.png)

**Explanation:**  
This command displays the installed version of the APT package manager.

---

## 2. Update Package List

Command:
```
sudo apt update
```

![apt update](img/apt%20part%201.2.png)

**Explanation:**  
This command refreshes the local package index from repositories.  
It prepares the system for upgrading.

---

## 3. Upgrade Installed Packages

Command:
```
sudo apt upgrade -y
```

![apt upgrade](img/apt%20part%201.3.png)

**Difference between `update` and `upgrade`:**

- `update` → Refreshes package lists.
- `upgrade` → Installs available updates.

---

## 4. View Pending Updates

Command:
```
apt list --upgradable
```

![upgradable](img/apt%20part%201.4.png)

**Explanation:**  
After upgrading, no packages were left pending.

---

# Part 2: Installing & Managing Packages

## 5. Search for a Package

Command:
```
apt search image editor
```

![search](img/apt%20part%202.1.png)
![search](img/apt%20part%202.2.png)

**Selected package:** `kimagemapeditor`

---

## 6. View Package Details

Command:
```
apt show kimagemapeditor
```

![show](img/apt%20part%202.3.png)

**Details observed:**

- Version: 4:23.08.5-0ubuntu3  
- Repository: universe  
- Dependencies listed under "Depends"

---

## 7. Install the Package

Command:
```
sudo apt install kimagemapeditor -y
```

![install](img/apt%20part%202.4.png)

### Verify Installation

Command:
```
apt list --installed | grep kimagemapeditor
```

![installed](img/apt%20part%202.5.png)

**Result:**  
The package was successfully installed.

---

# Part 3: Removing & Cleaning Packages

## 9. Remove the Package

Command:
```
sudo apt remove kimagemapeditor -y
```

![remove](img/apt%20part%203.1.png)

**Result:**  
The package was removed and disk space was freed.

---

## 10. Purge Configuration Files

Command:
```
sudo apt purge kimagemapeditor -y
```

![purge](img/apt%20part%203.2.png)

**Difference between `remove` and `purge`:**

- `remove` → Removes program files but keeps configuration files.
- `purge` → Removes program files and configuration files.

---

## 11. Remove Unnecessary Dependencies

Command:
```
sudo apt autoremove -y
```

![autoremove](img/apt%20part%203.3.png)

**Explanation:**  
Removes automatically installed packages that are no longer required.

---

## 12. Clean Cached Files

Command:
```
sudo apt clean
```

![clean](img/apt%20part%203.4.png)

**Explanation:**  
Deletes cached `.deb` files from `/var/cache/apt/archives` to free disk space.

---

# Part 4: Managing Repositories & Troubleshooting

## 13. List APT Repositories

Command:
```
cat /etc/apt/sources.list
```

![sources](img/apt%20part%204.1.png)

In Ubuntu 24.04, repositories are stored using the deb822 format in:

```
/etc/apt/sources.list.d/ubuntu.sources
```

![sources](img/apt%20part%204.2.png)
![sources](img/apt%20part%204.3.png)

Observed components:

- main  
- universe  
- restricted  
- multiverse  
- noble-security  
- noble-updates  

---

## 14. Add Universe Repository

Command:
```
sudo add-apt-repository universe
```

![add-universe](img/apt%20part%204.4.png)

The universe repository component was successfully enabled.

---

## 15. Simulate Installation Failure

Command:
```
sudo apt install fakepackage
```

![fake-error](img/apt%20part%204.5.png)

**Error Message:**
```
E: Unable to locate package fakepackage
```

### Troubleshooting Steps:

- Verify package spelling.
- Run `sudo apt update`.
- Search for the correct package using `apt search`.
- Check if required repositories are enabled.

---

# Conclusion

This assignment demonstrated how to:

- Update and upgrade packages
- Install and remove software
- Manage repositories
- Clean unused packages
- Troubleshoot installation errors

All commands were executed on a local Ubuntu system with real screenshots attached.

# Bonus Challenge

## Hold a Package

Command:
```
sudo apt-mark hold kimagemapeditor
```
![Again Installed](img/Bonus%20part%201.1.png)
![Hold](img/Bonus%20part%201.2.png)

This command prevents the package from being upgraded.

Verify:
```
apt-mark showhold
```
![Showhold](img/Bonus%20part%201.3.png)

## Unhold the Package

Command:
```
sudo apt-mark unhold kimagemapeditor
```
![Unhold](img/Bonus%20part%201.4.png)

This command allows the package to be upgraded again.

### Why hold a package?

A package may be held to:
- Prevent automatic updates
- Avoid compatibility issues
- Maintain system stability