# Amazon Web Services :: Elastic Cloud Compute

## EC2 Instances

### EC2 Instance Pricing Models

- [On-Demand](https://aws.amazon.com/ec2/pricing/on-demand/)
- [Reserved Instances](https://aws.amazon.com/ec2/pricing/reserved-instances/)
    - Standard (70-80%)
    - Convertible (~50%)
    - Scheduled
- [Spot Instances](https://aws.amazon.com/ec2/pricing/spot-instances/)
- [Dedicated Hosts](http://aws.amazon.com/ec2/dedicated-hosts/) 

Note: Per Second Billing (On-Demand, Reserved & Spot)

### EC2 Instance Type
#### General Purpose (T2, M3, M4, M5)
- T2
    - Burstable CPU (Baseline: 20% of CPU Core)
    - Lowest Cost
    - EBS-Only
    - ! Dedicated Host, ! Dedicated Instance, ! Scheduled Instances
    - Limit: 20 per region
    - *Use Case:* Websites and web applications, development environments, build servers, code repositories, micro services, test and staging environments, and line of business applications. 
- M3
    - SSD Storage
- M4
    - EBS-optimized by default at no additional cost
    - Support for Enhanced Networking
    - *Use Case:* Small and mid-size databases, data processing tasks that require additional memory, caching fleets, and for running backend servers for SAP, Microsoft SharePoint, cluster computing, and other enterprise applications.
- M5
    - EBS-optimized by default and higher EBS performance on smaller instance sizes
    - Up to 25 Gbps network bandwidth using Enhanced Networking
    - Requires HVM AMIs that include drivers for ENA and NVMe
    - Powered by the new light-weight Nitro system, a combination of dedicated hardware and lightweight hypervisor
    - *Use Case:* Small and mid-size databases, data processing tasks that require additional memory, caching fleets, and for running backend servers for SAP, Microsoft SharePoint, cluster computing, and other enterprise applications.
#### Compute Optimized
- C3
    - Local SSD-backed instance storage, with EBS optimization available for low additional fee
    - Support Enhanded Networking when used in Amazon VPCs and HVM AMIs
- C4
    - Default EBS-optimized for increased storage performance at no additional cost
    - Higher networking performance with Enhanced Networking supporting Intel 82599 VF
    - Requires Amazon VPC, Amazon EBS and 64-bit HVM AMIs
    - *Use Case:* High performance front-end fleets, web-servers, batch processing, distributed analytics, high performance science and engineering applications, ad serving, MMO gaming, and video-encoding.
- C5
    - Up to 25 Gbps of network bandwidth using Elastic Network Adapter (ENA)-based Enhanced Networking
    - EBS optimized by default
    - Requires HVM AMIs that include drivers for ENA and NVMe
    - *Use Case:* High performance web servers, scientific modelling, batch processing, distributed analytics, high-performance computing (HPC), machine/deep learning inference, ad serving, highly scalable multiplayer gaming, and video encoding.
#### Memory Optimized
- R3
    - SSD Storage
    - Support for Enhanced Networking
    - *Use Case:* We recommend R3 instances for high performance databases, distributed memory caches, in-memory analytics, genome assembly and analysis, Microsoft SharePoint, and other enterprise applications.
- R4
    - EBS-Only
    - DDR4 Memory
    - Support for Enhanced Networking
    - *Use Case:* High performance databases, data mining & analysis, in-memory databases, distributed web scale in-memory caches, applications performing real-time processing of unstructured big data, Hadoop/Spark clusters, and other enterprise applications.
- X1
    - One of the lowest price per GiB of RAM
    - Up to 1,952 GiB of DRAM-based instance memory
    - SSD storage and EBS-optimized by default and at no additional cost
    - *Use Case:* In-memory databases (e.g. SAP HANA), big data processing engines (e.g. Apache Spark or Presto), high performance computing (HPC). Certified by SAP to run Business Warehouse on HANA (BW), Data Mart Solutions on HANA, Business Suite on HANA (SoH), Business Suite S/4HANA.
- X1e
    - One of the lowest price per GiB of RAM
    - Up to 3,904 GiB of DRAM-based instance memory
    - SSD storage and EBS-optimized by default and at no additional cost
    - *Use Case:* High performance databases, in-memory databases (e.g. SAP HANA) and memory intensive applications. x1e.32xlarge instance certified by SAP to run next-generation Business Suite S/4HANA, Business Suite on HANA (SoH), Business Warehouse on HANA (BW), and Data Mart Solutions on HANA on the AWS cloud.
#### Accelerated Computing
- F1
    - Xilinx Virtex UltraScale+ VU9P FPGAs
    - *Use Case:* Genomics research, financial analytics, real-time video processing, big data search and analysis, and security.
- G3
    - NVIDIA Tesla M60 GPUs, each with 2048 parallel processing cores and 8GiB of video memory
    - *Use Case:* 3D visualizations, graphics-intensive remote workstation, 3D rendering, application streaming, video encoding, and other server-side graphics workloads.
- P2
    - High-performance NVIDIA K80 GPUs, each with 2,496 parallel processing cores and 12GiB of GPU memory
    - *Use Case:* Machine learning, high performance databases, computational fluid dynamics, computational finance, seismic analysis, molecular modeling, genomics, rendering, and other server-side GPU compute workloads.
- P3
    - Up to 8 NVIDIA Tesla V100 GPUs, each pairing 5,120 CUDA Cores and 640 Tensor Cores
    - *Use Case:* Machine/Deep learning, high performance computing, computational fluid dynamics, computational finance, seismic analysis, speech recognition, autonomous vehicles, drug discovery.
#### Storage Optimized
- D2
    - HDD storage
    - Consistent high performance at launch time
    - High disk throughput
    - Support for Enhanced Networking
    - *Use Case:* Massively Parallel Processing (MPP) data warehousing, MapReduce and Hadoop distributed computing, distributed file systems, network file systems, log or data-processing applications
- I3
    - High Random I/O performance and High Sequential Read throughput
    - Up to 25 Gbps of network bandwidth using Elastic Network Adapter (ENA)-based Enhanced Networking
    - NVMe (Non-Volatile Memory Express) SSD
    - *Use Case:* NoSQL databases (e.g. Cassandra, MongoDB, Redis), in-memory databases (e.g. Aerospike), scale-out transactional databases, data warehousing, Elasticsearch, analytics workloads.
- H1
    - Up to 16TB of HDD storage
    - High disk throughput
    - ENA enabled Enhanced Networking up to 25 Gbps
    - *Use Case:* MapReduce-based workloads, distributed file systems such as HDFS and MapR-FS, network file systems, log or data processing applications such as Apache Kafka, and big data workload clusters.
### Amazon Machine Images
- Provide information required to launch an instance
- Provides:
    - A template for the root volume (OS, apps)
    - Launch permissions (Which AWS account can use the AMI)
    - A block device mapping (which volumes to attach)

### EC2 Virtualization
- HVM (Mostly used, provides the biggest advantages, some instance types: HVM)
- PV (Used to perform better [disk, network] but are no longer so due to HVM using PV drivers)
## EBS
- Volumes are like Virtual Disks
- 99.999% availability
- Volume sizes and type can be changed on the fly
- Volumes must be in the same AZ
- To move a volume from one AZ/Region to another you must take a snapshot or image, then copy it.

#### SSD-backed storage
- For transactional workloads, such as databases and boot volumes (performance depends primarily on IOPS)
- General Purpose (GP2)
- Provisioned IOPS (IO1)
- Better under small random I/O
- IOPS: I/O cap 256 KiB, 

#### HDD-backed storage
- For throughput intensive workloads, such as MapReduce and log processing (performance depends primarily on MB/s)
- Cold HDD (SC1)
- Throughput Optimized HDD (ST1)
- Magnetic (standard)
- Better under secuential operations
- IOPS: I/O cap 1,024 KiB, 

#### Considerations on SSD / HDD
- Volume Queue Length is the amount of pending I/O requests for a device
- Latency is the end-to-end client time of an I/O operation, from client send to request completed (write or read)


#### EBS Optimized Instances
- Optimized configuration stack
- Dedicated capacity for EBS I/O

#### Instance Store

```
# /tmp/test = EBS-SSD
# /mnt/test = instance-store

root@ip-10-0-2-6:~# dd bs=1M count=256 if=/dev/zero of=/tmp/test
256+0 records in
256+0 records out
268435456 bytes (268 MB) copied, 3.26957 s, 82.1 MB/s
root@ip-10-0-2-6:~# dd bs=1M count=256 if=/dev/zero of=/tmp/test
256+0 records in
256+0 records out
268435456 bytes (268 MB) copied, 3.61336 s, 74.3 MB/s
root@ip-10-0-2-6:~# dd bs=1M count=256 if=/dev/zero of=/tmp/test
256+0 records in
256+0 records out
268435456 bytes (268 MB) copied, 3.31484 s, 81.0 MB/s
root@ip-10-0-2-6:~# dd bs=1M count=256 if=/dev/zero of=/mnt/test
256+0 records in
256+0 records out
268435456 bytes (268 MB) copied, 0.291084 s, 922 MB/s
root@ip-10-0-2-6:~# dd bs=1M count=256 if=/dev/zero of=/mnt/test
256+0 records in
256+0 records out
268435456 bytes (268 MB) copied, 0.29238 s, 918 MB/s
root@ip-10-0-2-6:~# dd bs=1M count=256 if=/dev/zero of=/mnt/test
256+0 records in
256+0 records out
268435456 bytes (268 MB) copied, 0.291242 s, 922 MB/s
```

## Snapshots
- Snapshots are point in time copies of a volume
- First Snapshot takes a while while the following increments are almost instant
- Ideally stop the instance or detach the volume if possible
- Snapshots exist in S3
- Snapshots of encrypted volumes are encrypted and viceversa
- Encrypted snapshots cannot be shared
- You can create an AMI from an encrypted snapshot and you can have EC2 instances with encrypted root devices.
#### Initialization (Pre-warming)

- Volumes restored from Snapshots require initialization to restore volume performance
