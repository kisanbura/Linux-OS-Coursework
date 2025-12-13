# Week 5 – Advanced Security and Monitoring Infrastructure

## Overview
This week focused on implementing advanced security controls and building automation to verify security posture and monitor system performance remotely. The server is still administered headlessly using SSH from the workstation, following the coursework’s remote administration constraint.

---

## Mandatory Access Control (AppArmor)

### What I did
I verified that AppArmor is enabled and enforcing security profiles on the Ubuntu server.

### What the command does
The `aa-status` command displays whether AppArmor is active, how many profiles are loaded, and whether they are running in enforce mode.

### Why this matters
AppArmor limits what applications can access even if they are compromised, reducing the impact of potential exploits.

<img width="1160" height="194" alt="sudo aa status checking aa status" src="https://github.com/user-attachments/assets/577367ef-89bd-4e69-858f-ed80f0084de2" />
##

<img width="1420" height="596" alt="sudo aa status output" src="https://github.com/user-attachments/assets/27de31ad-0cc5-47c7-b660-9a00666daf33" />

##

-----------------------------------------------------------------------------------------


## Automatic Security Updates

### What I did
I enabled unattended security updates to ensure the system automatically applies critical patches.

### What the commands do
The `unattended-upgrades` package installs the automatic update service.  
`dpkg-reconfigure unattended-upgrades` enables it, and viewing the configuration file confirms it is active.

### Why this matters
Automatic updates reduce the window of exposure to known vulnerabilities by applying security patches without manual intervention.



##
installing unattended upgrades
<img width="1314" height="218" alt="sudo apt install unattended upgrades installing unattended upgrades" src="https://github.com/user-attachments/assets/7f4cb4dc-6992-4278-80dd-b3d09191f688" />




##

<img width="1150" height="42" alt="enables automatic update  sudo dpkg" src="https://github.com/user-attachments/assets/92190b40-37dd-499c-9272-600fa2cd73b1" />


enables automatic update
##

verifying configuration automatic updates
<img width="1132" height="118" alt="verifies configuration cat automatic updates" src="https://github.com/user-attachments/assets/92708e28-e6b7-4ee2-92ab-db97e67404fb" />

-----------------------------------------------------------------------------------------

## Intrusion Prevention with Fail2Ban

### What I did
I installed and enabled Fail2Ban to protect the SSH service from brute-force login attempts.

### What the commands do
Fail2Ban monitors authentication logs and automatically blocks IP addresses that generate repeated failed login attempts. The SSH jail confirms that SSH protection is active.

### Why this matters
This reduces the risk of unauthorised access by limiting repeated authentication attempts over time.

### Evidence

<img width="1424" height="934" alt="installing fail2ban" src="https://github.com/user-attachments/assets/8955f941-6b17-4383-82db-209b7fe67e43" />
installing fail2ban

##
<img width="1410" height="156" alt="fail2ban enabling" src="https://github.com/user-attachments/assets/b3cc504f-b557-4f3c-9fbb-6941edf686ad" />

activating fail2ban

##

starting

<img width="920" height="36" alt="starting fail2ban" src="https://github.com/user-attachments/assets/7fbe8300-da1a-4059-8af4-d7e615dd34ee" />
##

<img width="1396" height="412" alt="fail2ban status is active running" src="https://github.com/user-attachments/assets/d23f7d7d-001c-4038-bfa7-5636d672bc2b" />

fail2ban service running
##

fail2ban ssh jail active
<img width="1254" height="432" alt="sudo fail2ban client status sshd ssh jail" src="https://github.com/user-attachments/assets/53aad501-06c4-4db7-b331-d42af2b0cee9" />

------------------------------------------------------------------------------------------

## Security Baseline Verification Script

### What I did
I created and executed a script to automatically verify that all implemented security controls remain active.

### What the script does
The script checks SSH configuration, firewall rules, AppArmor status, automatic updates, and Fail2Ban service status in a single automated run.

### Why this matters
Automating security checks improves reliability and allows quick verification after system changes or reboots.

### Evidence

creating script 
<img width="896" height="78" alt="creating script nano secuirty baseline" src="https://github.com/user-attachments/assets/d3859be4-6827-40f5-a596-c78ab0a812d8" />

##
security baselie script inside nano 
<img width="1418" height="1070" alt="seucirty baseline script inside nano" src="https://github.com/user-attachments/assets/e62b81b9-66fa-4c0f-85cf-6e987ee6c597" />


##
making script exectuable
<img width="896" height="42" alt="chmod making secuiry baseline executable" src="https://github.com/user-attachments/assets/08b48088-9334-4dae-a2cc-e09037192487" />

##  
running script
<img width="776" height="46" alt="running scriptt  secuirtybaseline" src="https://github.com/user-attachments/assets/23e45b87-bf2c-4391-a0b3-043ba0c6a099" />

##
script output
<img width="1396" height="1408" alt="script output " src="https://github.com/user-attachments/assets/e515ea67-d1fc-41c7-8174-83ddfd44c5a2" />

##

<img width="1374" height="716" alt="script output 2" src="https://github.com/user-attachments/assets/5da0494a-5ac7-4139-9d4c-60b68c1c8a79" />

-----------------------------------------------------------------------------------
## Remote Monitoring Script

### What I did
I created a workstation-side monitoring script that connects to the server via SSH and retrieves live performance metrics.

### What the script does
The script remotely executes commands such as `uptime`, `free -h`, `df -h`, and `ps` to collect system performance data without logging into the server interactively.

### Why this matters
Remote monitoring reflects professional system administration practices and supports performance analysis without direct server access.

### Evidence
creating script on powersehll
<img width="1050" height="46" alt="creating monitoring script powershell" src="https://github.com/user-attachments/assets/24aea6e1-9c98-446c-a13b-563d2543cd41" />
##
monitoring script
<img width="1092" height="720" alt="monitoring script " src="https://github.com/user-attachments/assets/456da718-00d7-4f8b-addb-3031f5ba3f07" />

##

allowing powershell scripts

<img width="1414" height="78" alt="allowing powershell scripts" src="https://github.com/user-attachments/assets/fefcb145-8326-404d-8d41-d7e1ab90192c" />


##
running monitoring script
<img width="790" height="46" alt="running the monitorscript powershell" src="https://github.com/user-attachments/assets/557d4e1c-c1b8-4b0e-8940-1d623f6b4efc" />
##


output of monitoring script
<img width="1420" height="1148" alt="output of monitoring script" src="https://github.com/user-attachments/assets/3b0b323b-5d2e-4f4f-8cb5-e9803b8d4bca" />


---------------------------------------------------------------------------------------

## Reflection
Week 5 focused on strengthening system security and improving automation. AppArmor enforced Mandatory Access Control, unattended upgrades reduced patching delays, and Fail2Ban protected against brute-force SSH attacks. Creating automated scripts for security verification and remote monitoring improved reliability and demonstrated professional command-line and system administration practices.



