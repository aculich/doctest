[Compute](#Compute) | [Login Nodes](#Login_Nodes) | [Storage](#Storage) | [Interconnect](#Interconnect) | [Data Transfer](#Data_Transfer) | [System Software](#System_Software)  | [Application Software](#Application_Software)

The **Savio** institutional cluster forms the foundation of the Berkeley Research Computing (BRC) Institutional/Condo Cluster. As of August 2016, the system consists of 331 compute nodes in various configurations to support a wide diversity of research applications, with a peak performance of 306 teraFLOPS per second, and offers approximately 1 Petabyte of high-speed parallel storage. Savio was launched in May 2014, and is named after Mario Savio, a political activist and a key member of the Berkeley Free Speech Movement.

![](/sites/default/files/SAVIO%20Overview.jpeg)

[]()

**Compute** {#compute}
-----------

![](/sites/default/files/DellBlade.jpg)**Savio0**: Savio0 is the first generation of compute nodes purchased in 2014. Each node is a Dell PowerEdge C6220 server blade equipped with two Intel Xeon 10-core Ivy Bridge processors (20 cores per node) on a single board configured as an SMP unit. The core frequency is 2.5 GHz and supports 8 floating-point operations per clock period with a peak performance of 20.8 GFLOPS/core or 400 GFLOPS/node. Turbo mode enables processor cores to operate at 3.3 Ghz when sufficient power and cooling are available. 164 compute nodes are configured with 64 GB of 1866 Mhz DDR3 memory and 4 compute nodes are configured as "BigMem" nodes with 512 GB of 1600 Mhz DDR3 memory.

**Savio2:** Savio2 is the 2nd generation of compute for the Savio cluster purchased in 2015. The new general compute pool consists of 136 ea. Lenovo NeXtScale nx360m5 nodes equipped with two Intel Xeon 12-core Haswell processors (24 cores per node) on a single board configured with an SMP unit. The core frequency is 2.3 Ghz and supports 16 floating-point operations per clock period. 132 compute nodes are configured with 64 GB of 2133 Mhz DDR4 memory and 4 compute nodes are configured as "BigMem" nodes with 128 GB of 2133 Mhz DDR4 memory.

**Savio2 HTC**: Purchased as part of the 2nd generation of compute for Savio, the HTC pool is available for users needed to do High-Throughput Computing or serial compute jobs. The pool consists of 12 ea. Lenovo NeXtScale nx360m5 nodes equipped with faster 3.4 Ghz clock speed, but fewer - 12 instead of 24 - core count Intel Haswell processors and 128 GB of 2133 Mhz DDR4 memory to better facilitate serial workloads.

**Savio2 GPU**: Also purchased as part of the 2nd generation of compute for Savio, the Savio2 GPU nodes are intended for researchers using graphics processing units (GPUs) for computation or image processing. The pool consists of 15 ea. Finetec Computer Supermicro 1U nodes, each equipped with 2 ea. Intel Xeon 4-core 3.0 Ghz Haswell processors (8 total) and 2 ea. Nvidia K80 dual-GPU accelerator boards (4 GPUs total per node). Each GPU offers 2,496 NVIDIA CUDA cores.

[]()

**Login Nodes** {#login-nodes}
---------------

When users login to Savio, they will ssh to hpc.brc.berkeley.edu. This will make a connection through the BRC firewall and they will land on one of the 4 interactive Login Nodes. Users should use the Login Nodes to prepare their jobs to be run - editing files and compiling applications, etc. - and for submitting their jobs via the scheduler. These 4 Login Nodes have the same specifications as some of the general compute nodes, but the Login Nodes are shared and are not to be used for directly running computations (instead, submit your jobs via the scheduler, to be run on one or more of the cluster's hundreds of [Compute Nodes](#Compute)), nor for transferring data (instead, use the cluster's [Data Transfer Node](#Data_Transfer)).

[]()

**Storage** {#storage}
-----------

The cluster uses a two-tier storage strategy. Each user is allotted 10 GB of backed up home directory storage which is hosted by IST's storage group on Network Appliance NFS servers. These servers provide highly available and reliable storage for users to store their persistent data needed to run their compute jobs. A second storage system available to users is a high performance 885 TB Lustre parallel filesystem, provided by a Data Direct Networks Storage Fusion Architecture 12KE storage platform, that is available as Global Scratch. Users with computations that have moderate to heavy I/O storage demands should use Global Scratch when needing to write and read temporary files during the course of a job. There are no limits on the use of Global Scratch; however, this filesystem is NOT backed up and it will be periodically purged of older files in order to insure that there is sufficient working space for users running current calculations.

[]()

**Interconnect** {#interconnect}
----------------

The interconnect for the cluster is a 56Gb/s Mellanox FDR infiniband fabric configured as a two-level fat tree. Edge switches will accommodate up to 24 compute nodes and will have 8 uplinks into the core infiniband switch fabric to achieve a 3:1 blocking factor to provide excellent, cost-effective network performance for MPI and parallel filesystem traffic. A second gigabit ethernet fabric will be used for access to interactive login and compute nodes and for Home Directory storage access.

[]()

**Data Transfer** {#data-transfer}
-----------------

The data transfer node (DATA-XFER) is a BRC server dedicated to performing transfers between data storage resources such as the NFS Home Directory storage and Global Scratch Lustre Parallel Filesystem; and remote storage resources at other sites. High speed data transfers are facilitated by a direct connection to CENIC via UC Berkeley's new Science DMZ network architecture. This server, and not the Login Nodes, should be used for large data transfers so as not to impact the interactive performance for other users on the Login Nodes. Users needing to transfer data to and from Savio should ssh from the Login Nodes or their own computers to the Data Transfer Node, dtn.brc.berkeley.edu, before doing their transfers, or else connect directly to that node from file transfer software running on their own computers.

**File Transfer Software**  
For smaller files you can use Secure Copy (SCP) or Secure FTP (SFTP) to transfer files between Savio and another host. For larger files BBCP and GridFTP provide better transfer rates. In addition, Globus Connect - a user-friendly, web-based tool that is especially well suited for large file transfers - makes GridFTP transfers trivial, so users do not have to learn command line options for manual performance tuning. Globus Connect also does automatic performance tuning and has been shown to perform comparable to - or even better (in some cases) than - expert-tuned GridFTP. The Globus endpoint name for the BRC DTN server is ucb\#brc

**Restrictions**  
In order to keep the data transfer nodes performing optimally for data transfers, we request that users restrict interactive use of these systems to tasks that are related to preparing data for transfer or are directly related to data transfer of some form or fashion.  Examples of intended usage would be running Python scripts to download data from a remote source, running client software to load data from a file system into a remote database, or compressing (gzip) or bundling (tar) files in preparation for data transfer. Examples of work that should not be done on the data transfer nodes include running a database on the server to do data processing, or running tests that saturate the nodes' resources. The goal in all this is to maintain data transfer systems that have adequate memory and CPU available for interactive user data transfers.

[]()

**System Software** {#system-software}
-------------------

Operating System: Scientific Linux 6  
Cluster Provisioning: [Warewulf Cluster Toolkit](http://warewulf.lbl.gov/trac)  
Infinband Stack: OFED  
Message Passing Library: OpenMPI  
Compiler: Intel  
Job Scheduler: SLURM with [NHC](http://go.lbl.gov/nhc/)  
Software management: Environment Modules  
Data Transfer: [Globus Connect](https://www.globus.org/)

[]()

**Application Software** {#application-software}
------------------------

See [Accessing and Installing Software](http://research-it.berkeley.edu/services/high-performance-computing/accessing-and-installing-software) for an overview of the types of application software, tools, and utilities provided on Savio.
