## Week 1 — System Planning & Initial Setup
##
# 1. System Architecture Diagram

<img width="1766" height="742" alt="architecture diagram screenshoit" src="https://github.com/user-attachments/assets/b4afb5d7-08b4-402f-ad3e-88cc3721f4da" />

##

This architecture separates the workstation and server roles, ensuring that administrative access occurs over SSH rather than console interaction. The host-only network isolates management traffic, reducing exposure while still allowing controlled access for administration.


##

# 2. Distribution Selection Justification

Chosen server distribution: Ubuntu Server LTS
Alternative considered: Debian

# Justification:

Ubuntu offers excellent documentation and strong community support.
Easy package management with apt.

Compatible with coursework tools.

Debian is more stable but slower with updates.

Ubuntu is better for beginners and aligns with industry practice.



-----------------------------------------------------------------------------------------

# 3. Workstation Configuration Decision

Chosen workstation option: Option B — Host Machine

Reasons:

Windows PowerShell already includes SSH client.

No need to run another VM.

Lower resource usage.

Easier workflow (copy/paste, browser available).

Matches required “dual-system” architecture.


-----------------------------------------------------------------------------------------
# 4. Network Configuration Documentation
VirtualBox Network Setup

Adapter 1 (NAT): Internet access
<img width="1554" height="936" alt="Ss Adapter 1 Nat" src="https://github.com/user-attachments/assets/4e5b041a-0a1b-4291-a54f-f1a456a85768" />
##

Adapter 2 (Host-Only Adapter – vboxnet0): Secure internal SSH network
<img width="1554" height="926" alt="ss Adapter 2 host only" src="https://github.com/user-attachments/assets/59e24172-f5cc-44e0-9f73-25d40e24d663" />
##

Server Network Output

From ip addr command:

enp0s8 = 192.168.56.3/24 (Host-Only Network)

<img width="1418" height="1014" alt="ip addr screenshot" src="https://github.com/user-attachments/assets/a292e48d-4465-46cc-878d-3fbcef892265" />


-----------------------------------------------------------------------------------------

5. **System Specifications**
Kernel Info (uname -a)

- This output confirms the kernel version and architecture, which is relevant for compatibility with performance and security tools.

<img width="2302" height="222" alt="uname  -a ss" src="https://github.com/user-attachments/assets/e8b12e47-5aae-4e4b-a0c0-fac5a04e3f06" />

-------------------------------------------------------------------------------------------------------------
Memory Info (free -h)
- This shows available and used memory, providing a baseline for later performance testing.

<img width="1846" height="218" alt="free -h ss" src="https://github.com/user-attachments/assets/e5429694-fb81-49ad-a9e4-66e39741a9cf" />

--------------------------------------------------------------------------------------------------------------------------------------
Disk Info (df -h)
- This shows available and used memory, providing a baseline for later performance testing.

<img width="1496" height="404" alt="df -h ss" src="https://github.com/user-attachments/assets/b35e0b3a-51fe-4b8e-b447-97d5181a63fc" />


-----------------------------------------------------------------------------------------------------------------------------------------
Network Info (ip addr)

<img width="2248" height="606" alt="ip addr screenshot powershell" src="https://github.com/user-attachments/assets/a2b00ed5-d72b-46ae-9492-8e53ba3bd83d" />

-------------------------------------------------------------------------------------------------------------------------------------------------------
Release Info (lsb_release -a)
<img width="936" height="316" alt="lsb_release -a ss" src="https://github.com/user-attachments/assets/398e31c8-acd4-4169-b34a-ff21d0032018" />

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------

6. ## Reflection

This week I set up my Ubuntu Server VM and successfully connected to it using SSH from my host computer. I configured VirtualBox with both NAT and a Host-Only adapter and verified that the server received the correct IP address. I also collected system information using various Linux commands and created an architecture diagram. I initially encountered an issue where the host-only adapter was disabled and the VM did not receive an IP address, but fixing the adapter settings resolved the problem. Through this process I gained confidence in VirtualBox networking and remote administration.
