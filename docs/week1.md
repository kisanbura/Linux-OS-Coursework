Week 1 — System Planning & Initial Setup
1. System Architecture Diagram

<img width="1766" height="742" alt="architecture diagram screenshoit" src="https://github.com/user-attachments/assets/b4afb5d7-08b4-402f-ad3e-88cc3721f4da" />





2. Distribution Selection Justification

Chosen server distribution: Ubuntu Server LTS
Alternative considered: Debian

Justification:

Ubuntu offers excellent documentation and strong community support.
Easy package management with apt.

Compatible with coursework tools.

Debian is more stable but slower with updates.

Ubuntu is better for beginners and aligns with industry practice.





3. Workstation Configuration Decision

Chosen workstation option: Option B — Host Machine

Reasons:

Windows PowerShell already includes SSH client.

No need to run another VM.

Lower resource usage.

Easier workflow (copy/paste, browser available).

Matches required “dual-system” architecture.



4. Network Configuration Documentation
VirtualBox Network Setup

Adapter 1 (NAT): Internet access
<img width="1554" height="936" alt="Ss Adapter 1 Nat" src="https://github.com/user-attachments/assets/4e5b041a-0a1b-4291-a54f-f1a456a85768" />


Adapter 2 (Host-Only Adapter – vboxnet0): Secure internal SSH network
<img width="1554" height="926" alt="ss Adapter 2 host only" src="https://github.com/user-attachments/assets/59e24172-f5cc-44e0-9f73-25d40e24d663" />


Server Network Output

From ip addr command:

enp0s8 = 192.168.56.3/24 (Host-Only Network)

(Insert ip addr screenshot)

5. System Specifications (CLI Evidence)
Kernel Info (uname -a)

(Insert screenshot)

Memory Info (free -h)

(Insert screenshot)

Disk Info (df -h)

(Insert screenshot)

Network Info (ip addr)

(Insert screenshot)

Release Info (lsb_release -a)

(Insert screenshot)

6. Reflection

Example reflection you can copy:

This week I set up my Ubuntu Server VM and successfully connected to it using SSH from my host computer. I configured VirtualBox with both NAT and a Host-Only adapter and verified that the server received the correct IP address. I also collected system information using various Linux commands and created an architecture diagram. I initially encountered an issue where the host-only adapter was disabled and the VM did not receive an IP address, but fixing the adapter settings resolved the problem. Through this process I gained confidence in VirtualBox networking and remote administration.
