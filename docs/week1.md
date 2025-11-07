# Week 1 – System Planning and Distribution Selection

## Objectives
- Plan and visualise the dual-system architecture (server + workstation).  
- Select a Linux server distribution and justify your choice.  
- Configure networking between both systems.  
- Gather and document baseline system specifications via CLI commands.  

---

## 1. System Architecture Diagram
*(Insert your diagram or screenshot of VirtualBox/network setup here.)*  
Describe how the two systems connect:

| Component | OS / Version | Purpose | Network IP | Notes |
|------------|---------------|----------|-------------|-------|
| Server | Ubuntu Server 24.04 LTS (headless) | Primary system | 192.168.56.102 | SSH access only |
| Workstation | Ubuntu Desktop / Windows host | Administrative client | 192.168.56.101 | SSH client & monitoring tools |

Explain your design choices (network type, resources, IP scheme).

---

## 2. Distribution Selection Justification
| Distribution | Advantages | Disadvantages | Decision |
|--------------|-------------|----------------|-----------|
| **Ubuntu Server 24.04 LTS** | LTS support, active community, wide package availability | Slightly heavier than Debian | ✅ Chosen |
| Debian 12 | Stable and lightweight | Older software versions | — |
| CentOS Stream 9 | RHEL compatibility for enterprise use | More complex SELinux management | — |

Briefly justify why your final choice best supports your coursework goals.

---

## 3. Workstation Configuration
Describe your workstation setup (VM vs host).  
Include evidence that the SSH client is installed and configured.

Example commands:
```bash
ssh -V
ifconfig

