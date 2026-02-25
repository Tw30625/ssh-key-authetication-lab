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
## Skills Demonstrated
- Linux sytem adminstration
- SSH configuration and hardening
- Network troubleshooting
- file permission management
- Virtual machine lab environment setup
