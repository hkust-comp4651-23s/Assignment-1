# COMP4651 Assignment 01: EC2 Measurement (5 marks)

### Deadline: 23:59, Feb 28, Tuesday

---

### Name: Kan, Wan On
### Student Id: 20701753

### Email: wokan@connect.ust.hk

---



## Question 1: Measure the EC2 CPU and Memory performance

1. (1 mark) Report the name of measurement tool used in your measurements (you are free to choose *any* open source measurement software as long as it can measure CPU and memory performance). Please describe your configuration of the measurement tool, and explain why you set such a value for each parameter. Explain what the values obtained from measurement results represent (e.g., the value of your measurement result can be the execution time for a scientific computing task, a score given by the measurement tools or something else).

    > I used SysBench, a benchmarking tool to measure the performance of computer hardware. It is a method to access the CPU and memory performance. I used sysbench becuase it is open public in Github and easy to access.
    > For CPU test, I adopted an experiment in calculations of prime numbers up to a specified value. I set 10000 to be that specified value because it is feasible to be measured within 10 second. Also, I specified the number of used threads to be 4, so that it can estimate the multi-threading performance in a reasonable setting, etc 4. The computing performance can be measured by the total number of events can be handled. It reviews how many tasks the machine can accomplish within a given period, hence indicates how powerful the CPU is.
    > For Memory test, I test how long the machine we will take to write data within a specified value of size. I take the size to be 10Gb. Similarly, the total number of events will be the tool to compare the performance of memory. It implies how powerful the memory device is in terms of writing speed.

2. (1 mark) Run your measurement tool on general purpose `t2.small`, `t3.medium`, and `c3.large` Linux instances, respectively, and find the performance differences among these instances. Launch all the instances in the **N. Virginia** region. Does the performance of EC2 instances increase commensurate with the increase of the number of vCPUs and memory resource?

    In order to answer this question, you need to complete the following table by filling out blanks with the measurement results corresponding to each instance type.

    | Size        | CPU performance | Memory performance |
    | ----------- | --------------- | ------------------ |
    | `t2.small`  |     9097        |      5018689       |
    | `t3.medium` |    16166        |      10485760      |
    | `c3.large`  |    14200        |      7626072       |

    > Region: `N. Virginia`. Use `Ubuntu Server 20.04 LTS (HVM)` as AMI.
    > From t2.small to t3.medium, we can observe that both the CPU performance and memory performance can be improved with the increased number of vCPUs from 1 to 2 and the increased number of RAM from 1Gb to 2Gb.
    > However, for t3.medium to c3.large, the CPU performance and memory performance of c3.large is not as good as t3.medium, even with the same number of vCPUs and slightly smaller RAM from 4Gb to 3.75Gb.

## Question 2: Measure the EC2 Network performance

1. (1 mark) The metrics of network performance include **TCP bandwidth** and **round-trip time (RTT)**. Within the same region, what network performance is experienced between instances of the same type and different types? In order to answer this question, you need to complete the following table.

    | Type                      | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | `t2.small` - ``t2.small`` |       988      |  0.666   |
    | `t3.medium` - `t3.medium` |      4741      |  0.195   |
    | `c3.large` - `c3.large`   |       619      |  0.258   |
    | `t2.small` - `c3.large`   |       620      |  0.570   |
    | `t3.medium` - `c3.large`  |       614      |  0.649   |
    | `t3.medium` - `t2.small`  |       980      |  0.694   |

    > Region: `N. Virginia`. Use `Ubuntu Server 20.04 LTS (HVM)` as AMI. You should launch **6** instances in total.

2. (1 mark) What about the network performance for instances deployed in different regions? In order to answer this question, you need to complete the following table.

    | Connection                | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | N. Virginia - Oregon      |     24.9       |   62.612 |
    | N. Virginia - N. Virginia |     4741       |   0.195  |
    | Oregon - Oregon           |     3860       |   0.256  |

    > Region: `N. Virginia`/`Oregon`. Use `Ubuntu Server 20.04 LTS (HVM)` as AMI. All instances are `t3.medium`.
    
3. (1 mark) Is network performance consistent over time? You can do measurements at different times of a day and compare the results. Please give at least 2 possible reasons why network performance is inconsistent.

    > My first experiment is recorded at HKT 17:30, while I repeat the case `t3.medium` - `t3.medium` in later time (HKT 20:30). Compared to the orginal RTT (0.195ms), it has been extended to 0.269ms. RTT measures how long it takes a network request to go from its begining point to its destination and return, in terms milliseconds (ms). It means the network performance is not consistent over time.
    > There are two causes that might be responsible. The local area network (LAN) traffic is the first factor that might choke the connection over time. In this case, a sudden spike in network consumption demand during US business hours may result in a surge in LAN traffic. Second, there may be variations in the server response time. In this scenario, the server can see a considerable increase in the number of requests, which causes each request's response time to lengthen.

