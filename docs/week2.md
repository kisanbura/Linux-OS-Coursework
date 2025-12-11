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
