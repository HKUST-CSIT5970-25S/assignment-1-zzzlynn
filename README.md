[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/IAASVEAZ)
# CSIT5970 Assignment-1: EC2 Measurement (2 questions, 4 marks)

### Deadline: 11:59PM, Feb, 28, Friday

---

### Name: ZHANG, yining
### Student Id: 21075709
### Email: yzhangsu@connect.ust.hk

---

## Question 1: Measure the EC2 CPU and Memory performance

1. (1 mark) Report the name of measurement tool used in your measurements (you are free to choose *any* open source measurement software as long as it can measure CPU and memory performance). Please describe your configuration of the measurement tool, and explain why you set such a value for each parameter. Explain what the values obtained from measurement results represent (e.g., the value of your measurement result can be the execution time for a scientific computing task, a score given by the measurement tools or something else).

    > The measurement tool used in my measurements is Phoronix Test Suite.
    > 
    > The configuration of Phoronix Test Suite: 
    > 
    > For CPU performance: Compression rate. I set the value because it can show the speed when CPU performs instructions. The result is in MIPS which means the amount of instructions that CPU can perform per second. Higher MIPS values indicate better instruction performance.
    > 
    > For memory performance: RAMspeed(Copy integer). I set this value because it can show the bandwidth. The result is in MB/s. Higher bandwidth indicates better memory performance.

2. (1 mark) Run your measurement tool on general purpose `t2.micro`, `t2.medium`, and `c5d.large` Linux instances, respectively, and find the performance differences among these instances. Launch all the instances in the **US East (N. Virginia)** region. Does the performance of EC2 instances increase commensurate with the increase of the number of vCPUs and memory resource?

    In order to answer this question, you need to complete the following table by filling out blanks with the measurement results corresponding to each instance type.

    | Size        | CPU performance(MIPS) | Memory performance(MB/s)|
    | ----------- | --------------------- | ----------------------- |
    | `t2.micro`  |       3711            |       10799.61          |
    | `t2.medium` |       9749            |       19010.54          |
    | `c5d.large` |       7910            |       14469.62          |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI.

    > The performance of Amazon EC2 instances does not always increase linearly with the number of vCPUs and memory resources. 
    > 
    > `t2.micro` instance has 2 GB memory and 1 vCPUs. `t2.micro` instance has 4 GB memory and 2 vCPUs.`c5d.large` instance has 4 GB memory and 2 vCPUs. From the results, we can see doubling the number of vCPUs does not double the CPU performance when comparing `t2.micro` and `t2.medium`. Doubling the number of memory resources does not double the memory performance when comparing `t2.micro` and `c5d.large`.

## Question 2: Measure the EC2 Network performance

1. (1 mark) The metrics of network performance include **TCP bandwidth** and **round-trip time (RTT)**. Within the same region, what network performance is experienced between instances of the same type and different types? In order to answer this question, you need to complete the following table.

    | Type                      | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | `t3.medium` - `t3.medium` |     4200       |   0.205  |
    | `m5.large` - `m5.large`   |     4910       |   0.168  |
    | `c5n.large` - `c5n.large` |     4950       |   0.178  |
    | `t3.medium` - `c5n.large` |     2800       |   0.573  |
    | `m5.large` - `c5n.large`  |     2250       |   0.621  |
    | `m5.large` - `t3.medium`  |     4420       |   0.330  |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. Note: Use private IP address when using iPerf within the same region. You'll need iPerf for measuring TCP bandwidth and Ping for measuring Round-Trip time.
    
    > Within the same region, network performance between instances of the same type is generally consistent and predictable. It has highest network performance with the lowest latency. The TCP bandwidth varies by instance size. RTT is typically less than 1 ms.
    >
    > Network performance between instances of the different type depends on the capabilities of the instances. Instances with similar network performance is similar to same-type instances, as both instances have comparable network capabilities(`m5.large` - `t3.medium`). Instances with different network performance is limited by the instance with the lower network performance(`t3.medium` - `c5n.large`).
    > RTT is higher compared to same-type instances. 

2. (1 mark) What about the network performance for instances deployed in different regions? In order to answer this question, you need to complete the following table.

    | Connection                | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | N. Virginia - Oregon      |     34.7       |   61.816 |
    | N. Virginia - N. Virginia |     4920       |   0.202  |
    | Oregon - Oregon           |     4960       |   0.162  |
 
    > Region: US East (N. Virginia), US West (Oregon). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. All instances are `c5.large`. Note: Use public IP address when using iPerf within the same region.
    
    > TCP bandwidth between instances in different regions is typically lower than within the same region. RTT is much higher than within the same region.
