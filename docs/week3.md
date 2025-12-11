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


-------------------------------------------------------------------------------------------
**Application Seleetion Matrix**

| Application   | Workload Type                 | Reason for Selection                                                                              |
| ------------- | ----------------------------- | ------------------------------------------------------------------------------------------------- |
| **stress-ng** | CPU-intensive / RAM-intensive | Provides configurable CPU and memory stress for reproducible load conditions.                     |
| **fio**       | Disk I/O-intensive            | Industry-standard tool for benchmarking sequential and random disk read/write performance.        |
| **iperf3**    | Network-intensive             | Measures bandwidth, throughput, and latency between server and workstation.                       |
| **nginx**     | Server workload               | Lightweight web server suitable for performance analysis, benchmarking, and HTTP request testing. |
