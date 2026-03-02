# ssh-key-authetication-lab
Implementation of secure SSH key-based authetication between Kali Linux and Debian, including custom port hardening (2222), strict .ssh permission controls, and verified passwordless ecrypted remote access.

## Project Overview
This lab demonstrates secure SSH key-based authentication between two linux virtual machines (kali and Debian).
The objective was to configure encryted, passwordless remote access using ed25519 keys, enforced proper file permissions, and validate secure communication pver a non-default SSH port (2222).

## Lab Architecture 
Kali Linux (192.168.56.102)
-> SSH (ed25519 key, Port 2222)
-> Debian Server (192.168.56.101)
Both systems were hosted in VirtualBox using internal netork.

## Configuration Steps
## Install OpenSSH Server (Debian) 
bash
sudo apt install openssh-server

Change SSH Port
edit/etc/ssh/sshd_config:
Port 2222

Restart SSH:
bash
sudo systemctl restart ssh

Generate SSH Key (Kali)
bash
ssh-keygen -t ed25519

Copy Public Key Debien
bash
ssh-copy-id -i ~/.ssh/id_ed25519.pub -p 2222 debian@192.168.56.101

Set Proper Permissions (Debian)
bash 
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys

Validated Passwordless Logins
bash
ssh -p 2222 debian@192.168.56.101
---
## Security Concepts Demonstrated
-Asymmetric key authentication (ed25519)
-Encrypted remote communication (SSH)
-Principle of least priviledge via file permissions
-Reduced attacks surface using non-default SSH port
-Authetication troubleshooting and validation

## Troubleshooting
Issues encountered:
-Permission denied (publickey)
-Incorrect file permissions
-SSH context confusion between Vms
-Host fingerprint validation prompt

ALL issues were resolved through verification of:
- ~/.ssh permissions
- authorized_keys integrity
- SSH service status
- Correct machine context

- ## Implementation Walkthrough

### 1. ED25519 Key Generation (Kali)
![Key Generation](screenshots/01-key-generation.png)

Generated a secure ED25519 key pair on Kali Linux for passwordless authentication.

---

### 2. Public Key Deployment
![Key Deployment](screenshots/02-key-deployment.png)

Deployed the public key to the Debian server using ssh-copy-id over custom port 2222.

---

### 3. SSH Hardening Configuration
![SSH Hardening](screenshots/03-ssh-config-hardening.png)

Modified sshd_config to:
- Change default port to 2222
- Disable root login
- Disable password authentication
- Enforce key-based authentication

---

### 4. SSH Service Restart & Verification
![Service Verification](screenshots/04-ssh-service-verification.png)

Restarted the SSH service and verified it is active and listening on port 2222.

---

### 5. Successful Passwordless Login
![Passwordless Login](screenshots/05-passwordless-login-success.png)

Validated secure remote access from Kali to Debian using key-based authentication with no password prompt.

## Skills Demonstrated
- Linux sytem adminstration
- SSH configuration and hardening
- Network troubleshooting
- file permission management
- Virtual machine lab environment setup
