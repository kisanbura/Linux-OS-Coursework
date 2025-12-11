Week 2 - Security Planning and Testing Methodology 

1. Performance Testing Plan

   ## 
To evaluate the performance of my Ubuntu Server VM, I will use a remote monitoring approach where all measurements are taken through the SSH connection from my workstation. I will measure CPU, memory, disk I/O, network throughput, and application response time under different workloads.

##
Monitoring Tools:

CPU: top, htop, vmstat, mpstat

Memory: free -h, vmstat

Disk: iostat, df -h, and benchmarking tools such as fio

Network: ping, iperf3, ss, nload

Service response: curl, ab

##

Testing Methodology:
1. Baseline Measurement: Capture system statistics while the server is idle.
Load Testing: Run CPU-intensive, memory-intensive, disk, network, and server application workloads.
2. Bottleneck Identification: Analyse which hardware or OS components become saturated during tests.
3. ptimisation Testing: Apply configuration optimisations and compare results.
4. All tests will be executed remotely to simulate real-world server administration conditions.
--------------------------------------------------------------------------------------


2. Security Configuration Checklist

| Security Area                        | Planned Configuration                                                                                                               |
| ------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------- |
| **SSH Hardening**                    | Enable key-based authentication; disable password authentication; disable root login; restrict SSH access to the host-only network. |
| **Firewall Configuration**           | Configure `ufw` to deny all incoming traffic except SSH from my workstation IP.                                                     |
| **User & Privilege Management**      | Create a non-root administrative user; apply least-privilege principles; restrict sudo access.                                      |
| **Automatic Security Updates**       | Enable unattended security upgrades to ensure the server remains updated.                                                           |
| **Mandatory Access Control**         | Configure AppArmor (default on Ubuntu) to enforce profiles and restrict application permissions.                                    |
| **Intrusion Detection & Prevention** | Install and configure Fail2Ban to monitor SSH login attempts and ban malicious IPs.                                                 |
| **Network Security Measures**        | Disable unnecessary services; review listening ports; ensure no insecure services are running.                                      |

   
