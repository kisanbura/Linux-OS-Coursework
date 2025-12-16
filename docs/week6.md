## Week 6 - Performance Evaluation and Analysis

##
# Overview

This week focused on evaluating operating system performance under different workloads and analysing how configuration choices and hardware constraints affect system behaviour. Controlled performance tests were conducted to measure CPU, memory, disk I/O, and network performance. Baseline results were compared against stressed conditions, followed by targeted optimisation and re-testing to evaluate measurable improvements.

All tests were executed via SSH from the workstation, maintaining headless server administration.
-------------------------------------------------------------------------------------------

## Testing Methodology
#Approach

Performance evaluation followed a structured methodology:
1.Measure baseline performance under idle conditions
2.Apply workload-specific stress tests
3.Monitor system behaviour using CLI tools
4.Identify performance bottlenecks
5.Apply optimisations
6.Re-test and compare results

This approach ensures results are reproducible and supports quantitative analysis.

-----------------------------------------------------------------------------------------
# Baseline Performance measuremetns (idle system)
Commands used

What the commands do?

uptime - reports system load averages
free -h - shows memory usage in human-readable format
df -h / - shows memory usage in human-readable format
iostat - reports CPU and disk I/O activity

##

<img width="1272" height="84" alt="uptime command" src="https://github.com/user-attachments/assets/20c03a30-b869-4117-88d7-1805bd4d43d3" />

uptime  output

##

<img width="1424" height="224" alt="free -h powershell" src="https://github.com/user-attachments/assets/e6ea85d7-7e30-4353-88a3-2a9a8f8ed46e" />

free -h output

##
<img width="992" height="110" alt="df -h  disk space usage" src="https://github.com/user-attachments/assets/d207d55c-8d40-4dc7-b450-b76414a47809" />

df -h output

##

<img width="1836" height="1010" alt="iostat" src="https://github.com/user-attachments/assets/f37ac08d-65dd-4673-bd80-28acde9e38f4" />

iostat output


##
Analysis

Baseline results showed low load averages, high available memory, and minimal disk activity. These measurements represent normal operating conditions and provide a reference point for comparison with stressed workloads.
-----------------------------------------------------------------------------------------

##CPU Performance Testing

# Commands Used

stress-ng --cpu 2 --timeout 60 --metrics-brief
uptime
top

##
What the commands do

- stress-ng --cpu generates sustained CPU load using worker threads

- uptime displays load average changes during CPU stress

- top shows real-time CPU usage and active processes


##
Installing stress-ng

<img width="1404" height="234" alt="sudo apt install stress ng " src="https://github.com/user-attachments/assets/5786874e-5af5-4d65-ab4a-fd00507fdf45" />
##


<img width="1426" height="520" alt="stress-ng command" src="https://github.com/user-attachments/assets/f67bcded-8b81-412b-bccc-491a06e84f9d" />
Stress-ng Testing memory

##
<img width="1246" height="88" alt="uptime increased significantly after test" src="https://github.com/user-attachments/assets/2284778d-7f32-4dab-82ec-92b350fcd668" />
uptime out increased after test

##

<img width="1380" height="254" alt="top comamnd" src="https://github.com/user-attachments/assets/05cf09f0-f8a8-4771-bcd5-07151c7301bc" />

top output


<img width="1400" height="1418" alt="top command 2" src="https://github.com/user-attachments/assets/73bcfc11-714d-45e5-b049-a4f6fcf06ba9" />

shows realtime cpu usage
##

Analysis

During CPU stress testing, load averages increased significantly relative to baseline, indicating CPU saturation. This demonstrates how the Linux scheduler manages CPU-bound workloads and prioritises competing processes under sustained load.

----------------------------------------------------------------------------------------
## Memory Perforamnce Testing

# Commands Used
- stress-ng --vm 1 --vm-bytes 75% --timeout 60 --metrics-brief
- free -h

  ##
  What the commands do

stress-ng --vm allocates large blocks of memory

--vm-bytes 75% consumes most available RAM

free -h monitors memory availability and usage
##

<img width="1408" height="554" alt="stress-ng testing memory performanc test" src="https://github.com/user-attachments/assets/b21f8352-61e9-4a8d-af32-ff3ab1a7382d" />

testing memory

##
<img width="1406" height="272" alt="free -h monitoring memory after test" src="https://github.com/user-attachments/assets/eb71f468-5d2a-4950-ab09-b0c1676984bf" />

free -h output 

##
Analysis

Memory pressure significantly reduced available RAM and increased memory utilisation. This highlights how the operating system manages virtual memory and balances RAM usage under constrained conditions.

----------------------------------------------------------------------------------------
## Disk I/O Performance Testing

 fio --name=randwrite --ioengine=libaio --rw=randwrite --bs=4k --size=200M --numjobs=1 --runtime=60 --group_reporting

iostat

What the commands do

- fio performs random disk write operations

- iostat monitors disk throughput and latency

## 
<img width="2174" height="1172" alt="fio  monitoring disk io perforamance" src="https://github.com/user-attachments/assets/b1684253-42cd-43ed-883f-04f6261b05f7" />

fio monitoring disk io performance

<img width="2022" height="194" alt="fio monitoring disk performance 2" src="https://github.com/user-attachments/assets/b682c736-82c8-43bc-a8cb-3488d9db6af3" />

##

<img width="1848" height="920" alt="iostat monitoring disk perforamnce" src="https://github.com/user-attachments/assets/9b5e621f-3039-48e6-bb09-68e62bd01c24" />

iostat disk performance monitoring
##

Analysis

Disk I/O testing revealed increased write latency during random operations, reflecting the performance characteristics of virtualised storage. This demonstrates the impact of I/O patterns on disk performance in VM environments.

----------------------------------------------------------------------------------------

## Network Performance Testing

# Commands Used
iperf3 -s
iperf3 -c 127.0.0.1

##
What the commands do

iperf3 -s starts a network test server

iperf3 -c measures TCP throughput between client and server

##
<img width="1664" height="808" alt="iperf3 -s testing networking performance 2" src="https://github.com/user-attachments/assets/19ddcaca-e939-4a96-9011-43622e2ec859" />

iperff3 -s 

##
<img width="1532" height="750" alt="iperf3 -c 127 0 0 1" src="https://github.com/user-attachments/assets/b10d8e96-9a08-4ed9-b061-7ea399e9ed0f" />

iperf3 -c

##
What the commands do

iperf3 -s starts a network test server

iperf3 -c measures TCP throughput between client and server

----------------------------------------------------------------------------------------

## Performance Optimisation - Memory Management
# Optimisation Applied

Kernel swappiness was reduced to minimise unnecessary swapping.

**Commands Used**
sudo sysctl vm.swappiness=10
sudo nano /etc/sysctl.conf
sysctl vm.swappiness
##

What the commands do ?

sysctl vm.swappiness=10 reduces swap aggressiveness

Persisting the value ensures the change survives reboots

Verification confirms the optimisation is active


## 

<img width="894" height="118" alt="sudo sysctl vm swapiness reduces aggresive swapping improves performance" src="https://github.com/user-attachments/assets/2b85ae27-680d-4f9f-bc7d-7309bd6e96ac" />

sudo sysctl vm 

##

<img width="834" height="44" alt="sudo nano etcsystctl   entering conf file" src="https://github.com/user-attachments/assets/069f3a84-2183-41b5-8625-c1cf6dc4337b" />

sudo nano etc conf
##
<img width="1416" height="1448" alt="vm swapiness=10 conf" src="https://github.com/user-attachments/assets/e02fd500-d0e7-4e5e-9ce7-36a5b4938243" />
adding vm.swapiness=10 conf


<img width="1380" height="296" alt="vm swapiness=10con 2" src="https://github.com/user-attachments/assets/9fce07fb-1c4c-4114-8c75-125a78079402" />

##
<img width="814" height="68" alt="sysctl vm swappiness veryifying sysctl vm" src="https://github.com/user-attachments/assets/be13c00f-29d0-4cd0-87f0-8defe43d859d" />

confirms optimisation is active systcl

---------------------------------------------------------------------------------------
## Retesing After OPtimisation - Memory Teste

Commands Used
stress-ng --vm 1 --vm-bytes 75% --timeout 60 --metrics-brief
free -h

##
<img width="2072" height="488" alt="stress-ng rerun memory test after optiimsaiation" src="https://github.com/user-attachments/assets/a3ba8da5-c28b-49f3-ac21-1022e11f438e" />

output after optimisation
##

<img width="1552" height="160" alt="free -h monitoring memory after optimisation re running" src="https://github.com/user-attachments/assets/098c9538-508d-44a7-b2a4-2f6f0e89c88d" />

after optimisation output

##
# Analysis
After optimisation, swap usage was reduced and available memory was utilised more efficiently. The system remained more responsive under memory pressure, demonstrating measurable performance improvement.


---------------------------------------------------------------------------------------
## Retesing after Optimsation - CPU Test

##
Commands Used
stress-ng --cpu 2 --timeout 60 --metrics-brief
uptime


##

<img width="1412" height="534" alt="stress-ng command retesting cpu test re run" src="https://github.com/user-attachments/assets/2677cf10-ebf7-44b8-a2a4-c6600a441875" />

##


<img width="1206" height="78" alt="uptime command retesting cpu test rerun output" src="https://github.com/user-attachments/assets/da5b4fa8-40f6-4988-ab93-b1c95c124100" />

output after optimisation
----------------------------------------------------------------------------------------
## Before v After Comparison


| Test Area | Metric         | Before Optimisation | After Optimisation |
| --------- | -------------- | ------------------- | ------------------ |
| Memory    | Available RAM  | Lower               | Higher             |
| Memory    | Swap usage     | Increased           | Reduced            |
| CPU       | Load stability | Variable            | Stable             |

----------------------------------------------------------------------------------------
##Trade-Off Analysis (LO5)
#Trade-off 1: Performance vs Stability

Reducing swappiness improves performance by avoiding excessive swapping; however, under extreme memory pressure it may increase the risk of out-of-memory conditions.

Trade-off 2: Virtualisation vs Hardware Control

CPU frequency scaling could not be modified within the virtual machine due to hypervisor constraints, highlighting a trade-off between virtualisation flexibility and direct hardware-level optimisation.

Trade-off 3: Disk Throughput vs Latency

Random disk writes improved throughput realism but increased latency, demonstrating the balance between I/O performance and responsiveness.
----------------------------------------------------------------------------------------
## Reflection

Week 6 demonstrated how operating system performance varies significantly under different workloads and configuration choices. Quantitative testing revealed clear differences between idle and stressed conditions, while targeted optimisation improved memory responsiveness. Hardware constraints imposed by virtualisation highlighted realistic trade-offs faced in cloud and VM-based deployments, reinforcing the importance of context-aware performance tuning.
