# Week 4 - **Initial System Configuratoin & Security Implmentation**


 ## Overview
This week focused on implementing foundational security controls on the Ubuntu Server. 
All configuration tasks were performed remotely via SSH from the workstation, in line 
with professional server administration practices. Key-based SSH authentication was 
configured, insecure access methods were disabled, a non-root administrative user was 
created, and a firewall was deployed to restrict network access.


------------------------------------------------------------------------------------------

## SSH Key-Based Authentication

To improve SSH security, key-based authentication was configured. This prevents 
password-based brute-force attacks and ensures only authorised devices can access 
the server.

##
<img width="1310" height="880" alt="public key ss" src="https://github.com/user-attachments/assets/7738e7c8-557f-4a86-8bc8-b57387edc781" />

The `ssh-keygen` command was executed on the workstation using PowerShell to generate 
an Ed25519 key pair. The private key remains on the workstation, while the public key 
is installed on the server.


##
<img width="1390" height="626" alt="direct login to powershell no password required" src="https://github.com/user-attachments/assets/1e5b7961-4553-457a-a717-c8b783eae65f" />


This screenshot demonstrates a successful SSH connection to the server without being 
prompted for a password, confirming that key-based authentication is working correctly.



<img width="1376" height="1546" alt="public key output SS" src="https://github.com/user-attachments/assets/c7b253b2-ae1d-4a6b-be95-7b2fe776fa25" />

This shows that a key was added.

----------------------------------------------------------------------------------------
## SSH Hardening

The SSH service was hardened to reduce the attack surface by disabling insecure 
authentication methods and restricting privileged access.

## Before Editing
<img width="1430" height="1360" alt="before changing sshd config " src="https://github.com/user-attachments/assets/31649e3b-6e6a-42e6-acd6-06420e6382c1" />

After editing SSh config file
<img width="1108" height="370" alt="week 4 sshconfig" src="https://github.com/user-attachments/assets/f01672b3-9453-4a97-a70f-565fc4a6c698" />


#
The SSH configuration file (`/etc/ssh/sshd_config`) was modified to disable password 
authentication and root login, while explicitly enabling public key authentication. 
These changes enforce secure access and follow best security practices.


## 
<img width="1404" height="228" alt="week 4 verifying active ssh " src="https://github.com/user-attachments/assets/f7165850-02a3-475d-8eea-22e922508029" />

Key changes included:
- `PasswordAuthentication no`
- `PermitRootLogin no`
- `PubkeyAuthentication yes`

##
## SSH Key troubleshooting
### SSH Key Authentication Troubleshooting

After disabling password-based authentication, SSH access initially failed with a `Permission denied (publickey)` error. This behaviour was expected, as SSH becomes strictly dependent on valid key-based authentication once passwords are disabled.

Verbose SSH debugging (`ssh -v`) was used from the workstation to identify which public key was being offered during authentication. The server logs confirmed that the offered key did not match the authorised public key stored on the server.

The issue was resolved by reinstalling the correct workstation public key into the server’s `authorized_keys` file and enforcing SSH-compliant file ownership and permissions. Following this correction, key-based SSH access was restored successfully without requiring a password.

##

<img width="876" height="38" alt="week 4 permission" src="https://github.com/user-attachments/assets/137981f7-5b5e-4cc7-907a-a1bb1e3b685a" />

##
<img width="1066" height="82" alt="week 4 permission denied" src="https://github.com/user-attachments/assets/e443f78c-29dd-4a6d-97b8-c997ada6c481" />

permission denied shows issues encountered justies troubleshooting steps

##
<img width="1232" height="138" alt="week 4 ssh -vking" src="https://github.com/user-attachments/assets/80fbc669-9d5b-4b97-87fd-b97ef533e510" />
##

<img width="1396" height="74" alt="week 4 offering public kety" src="https://github.com/user-attachments/assets/131955c2-18e6-49e8-b844-5b58d9c9d53b" />
shows analytical troubleshooting


##

### SSH Key Permissions Verification

After correcting the authorised public key, SSH file permissions and ownership were verified to ensure compliance with OpenSSH security requirements. The `.ssh` directory was restricted to the user only, preventing other users from reading or modifying SSH configuration files. The `authorized_keys` file was configured with strict permissions to ensure that only the account owner can modify authorised public keys.

This step was necessary because OpenSSH will refuse key-based authentication if file permissions are overly permissive, as a protection against unauthorised access and privilege escalation.

<img width="1104" height="150" alt="week 4 troubleshooting ls ocmmands" src="https://github.com/user-attachments/assets/39cc73b2-a913-44cd-88d3-25d7da7cc33a" />



<img width="1130" height="320" alt="week 4 troubleshooting 4 " src="https://github.com/user-attachments/assets/e75af53d-1026-4cff-8f77-a35686311ff4" />




##
After fix succesful login without password
<img width="1336" height="770" alt="week 4 succesful loginwithout password" src="https://github.com/user-attachments/assets/70f70900-16e1-4e8e-af78-830e3538f56d" />

### Trade-off: Security vs Usability in SSH Authentication

A key trade-off identified during SSH hardening was between security and usability. Disabling password-based authentication significantly reduces the risk of brute-force attacks and credential compromise; however, it also increases the risk of administrator lockout if SSH keys are misconfigured. This trade-off was accepted because key-based authentication provides stronger cryptographic security and aligns with industry best practices for server administration. The risk was mitigated by retaining console access via the virtual machine and validating configuration changes using `sshd -T` before closing active sessions.

----------------------------------------------------------------------------------------

## Non-Root Administrative User

A dedicated non-root administrative user was created to follow the principle of least 
privilege and avoid routine use of the root account.

## 

<img width="1434" height="794" alt="adding new user admin1 " src="https://github.com/user-attachments/assets/b43c7922-171a-4e6a-bba8-1616b44e3b0d" />

The `adduser` command was used to create a new administrative user via an SSH session. 
This user was added to the `sudo` group, allowing administrative tasks to be performed 
without logging in as root.


##
<img width="1420" height="1012" alt="admin login in powershell 2" src="https://github.com/user-attachments/assets/7b4ff5ba-bb08-4718-b98e-fd00d17dda87" />

admin login

##

<img width="1020" height="106" alt="admin1 performing sudo" src="https://github.com/user-attachments/assets/ee1391ed-c131-4c25-994e-b30e02fbf16d" />

This screenshot confirms that the new administrative user can successfully execute 
commands with elevated privileges using `sudo`.

------------------------------------------------------------------------------------------------

## Firewall Configuration

A host-based firewall was configured using UFW to restrict incoming network traffic 
and allow SSH access only from the authorised workstation.

<img width="1386" height="854" alt="firewall activation" src="https://github.com/user-attachments/assets/0e6cbf65-6812-40e0-a877-5c4de54f3d35" />

##

<img width="1258" height="426" alt="sudo ufw status verbose" src="https://github.com/user-attachments/assets/c6e6cb77-ec06-48d6-967a-7c8ef17604b6" />



checks firewall stauts
##

got ip from ipconfig 
<img width="1466" height="476" alt="ipconfig get ip from powershell" src="https://github.com/user-attachments/assets/12e585d0-d91b-43fb-9fc7-f6c83cbe0ff2" />


The firewall was configured to deny all incoming connections by default and allow 
outgoing traffic. SSH access was explicitly permitted only from the workstation’s 
host-only IP address, significantly reducing exposure to unauthorised access.


### Trade-off: Network Security vs Accessibility

Restricting SSH access to a single trusted workstation IP significantly reduces the network attack surface but limits flexibility when administrative access is required from other locations. This trade-off prioritises security over convenience, reflecting real-world server deployment practices where access is tightly controlled. The limitation was accepted because the system operates within an isolated VirtualBox network, and administrative access requirements are predictable.

-------------------------------------------------------------------------------------


## Remote Administration Evidence

The following commands demonstrate that the server is being managed remotely via SSH, 
with active services and enforced security controls.

##
whaomi 
<img width="504" height="78" alt="whoami" src="https://github.com/user-attachments/assets/5613d69b-8583-42fd-863a-31f86d763264" />
##

hostname 
<img width="492" height="76" alt="hostname" src="https://github.com/user-attachments/assets/faa0fdaf-232d-4a5a-b52c-dc987f13ddf6" />

##
uptime

<img width="1294" height="80" alt="uptime" src="https://github.com/user-attachments/assets/f16cd377-7281-458b-b49f-2ecfab3bb29c" />
##

systemctl status ssj
<img width="1426" height="538" alt="sudo systemctl status ssh" src="https://github.com/user-attachments/assets/fc77f4fa-f27b-4baa-98fe-f27412ccc11e" />

Commands such as `whoami`, `hostname`, `uptime`, and `systemctl status ssh` confirm 
successful remote administration, system identity, service availability, and uptime.

----------------------------------------------------------------------------------------
## Reflection

This week highlighted the importance of secure remote administration in modern 
operating systems. Implementing SSH hardening, key-based authentication, and firewall 
rules significantly reduced the system’s attack surface. Creating a non-root 
administrative user reinforced the principle of least privilege. Performing all tasks 
via SSH mirrored real-world server management practices and improved confidence in 
command-line system administration.















