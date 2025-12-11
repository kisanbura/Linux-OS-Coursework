Week 3 - **Select Applications for Different Workloads** 

##
1. CPU-Intensive → stress-ng

Used to stress test CPU(s).

2. RAM-Intensive → stress-ng with memory options

Same tool, different flags.

3. Disk I/O-Intensive → fio

Industry-standard disk testing tool.

4. Network-Intensive → iperf3

Used for throughput, bandwidth, network stress.

5. Server Application → nginx

 Lightweight web server for latency and response tests.


--------------------------------------------------------------------------------------------------------------------------------------------------
**Application Seleetion Matrix**

| Application   | Workload Type                 | Reason for Selection                                                                              |
| ------------- | ----------------------------- | ------------------------------------------------------------------------------------------------- |
| **stress-ng** | CPU-intensive / RAM-intensive | Provides configurable CPU and memory stress for reproducible load conditions.                     |
| **fio**       | Disk I/O-intensive            | Industry-standard tool for benchmarking sequential and random disk read/write performance.        |
| **iperf3**    | Network-intensive             | Measures bandwidth, throughput, and latency between server and workstation.                       |
| **nginx**     | Server workload               | Lightweight web server suitable for performance analysis, benchmarking, and HTTP request testing. |


---------------------------------------------------------------------------------------------------------------------------------------------------

**Installation Documentation**
##
Updating Packages:
**sudo apt update**

##

Install CPU & RAM stress tool:
**sudo apt install stress-ng -y**

##

Install Disk Benchmarking tool:
**sudo apt install fio -y**

##

Install Network Performance tool:
**sudo apt install iperf3 -y**

##

Install Web Server:

**Sudo apt install nginx -y**

**sudo systemctl start nginx**

**sudo systemctl enable nginx** 
##
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
**Expected Resource Profiles**

| Application   | Expected CPU Usage                                 | Expected Memory Usage                         | Expected Disk Usage                  | Expected Network Usage                  |
| ------------- | -------------------------------------------------- | --------------------------------------------- | ------------------------------------ | --------------------------------------- |
| **stress-ng** | Very high CPU usage; all cores stressed under load | High memory usage depending on selected tests | Low                                  | Low                                     |
| **fio**       | Low CPU                                            | Low RAM                                       | Very high disk read/write operations | Low                                     |
| **iperf3**    | Low CPU                                            | Low RAM                                       | Low disk                             | Very high network throughput            |
| **nginx**     | Moderate CPU under high load; low when idle        | Low-medium                                    | Low                                  | Medium-high depending on request volume
|

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

*Monitoring Strategy*

All performance monitoring will be performed remotely over SSH from my workstation.
I will use the following tools and commands to measure system performance under different workloads:

CPU & Memory Monitoring

top — real-time CPU and memory usage

htop — improved interactive monitoring

vmstat — process scheduling and memory pressure

mpstat — per-core CPU usage breakdown

Disk I/O Monitoring

iostat — throughput and IOPS

df -h — filesystem space usage

Compare before/after fio runs

Network Monitoring

ping — latency measurement

iperf3 — throughput testing between server and workstation

ss -tulpn — open ports and active connections

Server Performance Monitoring

curl — HTTP response time

ab (ApacheBench) — HTTP load generation for nginx

All monitoring will be executed via SSH to simulate real remote administration in a professional environment.

------------------------------------------------------------------------------------------------------------------------------------------------------------------

*Reflection*

In Week 3, I selected the applications required to test CPU, RAM, disk I/O, network performance, and server response times. I documented installation steps, expected performance characteristics, and my monitoring strategy. This planning phase clarified how different workloads interact with the operating system and gave me a structured approach for the detailed performance testing I will conduct in Week 6.










