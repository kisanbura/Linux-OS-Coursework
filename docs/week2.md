

## Week 2 - Security Planning and Testing Methodology 

1. **Performance Testing Plan**

   ## 
To evaluate the performance of my Ubuntu Server VM, I will use a remote monitoring approach where all measurements are taken through the SSH connection from my workstation. I will measure CPU, memory, disk I/O, network throughput, and application response time under different workloads.

This approach reflects real-world server administration, where performance monitoring is performed remotely without direct console access.

##
Monitoring Tools:

CPU: top, htop, vmstat, mpstat - These tools provide both real-time and statistical views of processor usage.

Memory: free -h, vmstat - These tools allow monitoring of memory allocation, availability, and pressure, helping to identify potential swapping or memory exhaustion issues.

Disk: iostat, df -h, and benchmarking tools such as fio - fio allows controlled synthetic workloads, while iostat observes real-time I/O behaviour

Network: ping, iperf3, ss, nload - These tools measure latency, bandwidth, and active connections, allowing identification of network performance limitations and connectivity issues.

Service response: curl, ab - These tools simulate client requests and measure response times, allowing evaluation of application-level performance under load.

##

Testing Methodology:
1. Baseline Measurement: Capture system statistics while the server is idle.
Load Testing: Run CPU-intensive, memory-intensive, disk, network, and server application workloads.
2. Bottleneck Identification: Analyse which hardware or OS components become saturated during tests.
3. ptimisation Testing: Apply configuration optimisations and compare results.
4. All tests will be executed remotely to simulate real-world server administration conditions.
--------------------------------------------------------------------------------------


 2. **Security Configuration Checklist**

| Security Area                        | Planned Configuration                                                                                                               |
| ------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------- |
| **SSH Hardening**                    | Enable key-based authentication; disable password authentication; disable root login; restrict SSH access to the host-only network. |
| **Firewall Configuration**           | Configure `ufw` to deny all incoming traffic except SSH from my workstation IP.                                                     |
| **User & Privilege Management**      | Create a non-root administrative user; apply least-privilege principles; restrict sudo access.                                      |
| **Automatic Security Updates**       | Enable unattended security upgrades to ensure the server remains updated.                                                           |
| **Mandatory Access Control**         | Configure AppArmor (default on Ubuntu) to enforce profiles and restrict application permissions.                                    |
| **Intrusion Detection & Prevention** | Install and configure Fail2Ban to monitor SSH login attempts and ban malicious IPs.                                                 |
| **Network Security Measures**        | Disable unnecessary services; review listening ports; ensure no insecure services are running.                                      |


-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
   
3. **Threat Model identifying**
                                                        
| Threat                        | Description                                                               | Mitigation Strategy                                                                                                        |
| ----------------------------- | ------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| **Brute-force SSH Attacks**   | Attackers attempt to guess SSH passwords through repeated login attempts. | Enable key-based authentication, disable password logins, restrict SSH to the host-only network, and configure Fail2Ban.   |
| **Privilege Escalation**      | An attacker who gains limited access may attempt to become root.          | Use non-root administrative accounts, restrict sudo access, enforce AppArmor profiles, and ensure secure file permissions. |
| **Unpatched Vulnerabilities** | Outdated packages can contain known exploits that attackers may target.   | Enable automatic security updates and regularly apply patches.                                                             |
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
These security and performance plans directly informed later implementation decisions in Weeks 4–7. For example, the threat model guided SSH hardening and firewall restrictions, while the performance methodology was applied during structured testing in Week 6.

-----------------------------------------------------------------------------------------
### Reflection

Week 2 focused on planning rather than implementation, which highlighted the importance of designing security and performance strategies before making system changes. Developing a security checklist and threat model helped clarify how different attack vectors map to specific operating system controls such as SSH hardening, firewalls, and automatic updates. Creating a structured performance testing methodology ensured that later testing would be reproducible and meaningful rather than ad hoc. This planning phase reinforced the idea that effective system administration relies on preparation and risk assessment as much as technical execution and also this structured planning approach reduced configuration errors and improved confidence when implementing security and performance changes in later weeks.

