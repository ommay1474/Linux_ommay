## Student Information
- Name: Ommay Habiba Khatun Bristi  
- Student Email: amk1006788@student.hamk.fi   
- Date: 20/02/2026

---

# Linux Firewall Configuration Report

## Introduction

In this assignment, I configured a firewall on my Ubuntu virtual machine using UFW (Uncomplicated Firewall).  
The purpose of this task was to improve the network security of the server by allowing only necessary services and blocking all other unwanted traffic.

A firewall is an important security component that controls incoming and outgoing network traffic based on defined rules.

---

## 1. Checking Firewall Status

First, I checked the current firewall status:

```bash
sudo ufw status verbose
```

Initially, the firewall was inactive.

---

## 2. Setting Default Security Policies

I configured the default policies as follows:

```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
```

Explanation:

- All incoming connections are denied by default.  
  This prevents unauthorized access to the server.
- All outgoing connections are allowed.  
  This allows the server to access updates and external services.

This setup follows the principle of least privilege.

---

## 3. Allowing Required Services

The assignment required OpenSSH, HTTP, and HTTPS to be allowed.

### Allow OpenSSH

```bash
sudo ufw allow ssh
```

This rule allows remote administration of the server.

### Limit SSH Connections

```bash
sudo ufw limit ssh
```

This rule limits repeated SSH connection attempts.  
It helps prevent brute-force attacks and reduces the risk of SYN flood and connection-based attacks.

### Allow HTTP

```bash
sudo ufw allow http
```

This allows users to access the web server using port 80.

### Allow HTTPS

```bash
sudo ufw allow https
```

This allows secure web traffic using port 443.

Only necessary services are exposed to the network.

---

## 4. Logging Configuration

To log firewall activity, I enabled high logging:

```bash
sudo ufw logging high
```

Explanation:

- Blocked connections are logged.
- Suspicious or repeated attempts are recorded.
- This helps monitor unauthorized access attempts.
- Logging improves visibility and helps detect attacks.

---

## 5. Enabling the Firewall

After configuring all rules, I enabled the firewall:

```bash
sudo ufw enable
```

The firewall is now:

- Active
- Enabled on system startup

This ensures protection remains active even after reboot.

---

## 6. Preventing SYN Flood and Other Attacks

SYN flood is a type of denial-of-service attack that overloads a server with connection requests.

The following rule helps reduce this risk:

```bash
sudo ufw limit ssh
```

This limits repeated connection attempts from the same IP address.

Other common attacks that can be reduced with this configuration:

- Brute-force SSH attacks
- Port scanning attempts
- Unauthorized remote access
- Basic denial-of-service attempts

Because all incoming traffic is denied by default, only explicitly allowed services can be accessed.

---

## 7. Verifying the Configuration

Finally, I verified the firewall configuration:

```bash
sudo ufw status verbose
```

The final configuration shows:

- Status: active
- Logging: on (high)
- Default: deny (incoming), allow (outgoing)
- 22/tcp: LIMIT IN
- 80/tcp: ALLOW IN
- 443/tcp: ALLOW IN

This confirms that only required services are accessible.

---

## Conclusion

In this assignment, I successfully configured a secure firewall using UFW on my Ubuntu server.

The firewall:

- Blocks all incoming traffic by default
- Allows only SSH, HTTP, and HTTPS
- Limits SSH connections to reduce brute-force and SYN flood attacks
- Logs firewall activity
- Starts automatically when the server boots

This configuration significantly improves the overall network security of the system while keeping required services accessible.

