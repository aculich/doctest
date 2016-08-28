[Login](#Login) | [Data Transfer](#Data_Transfer) | [Hardware](#Hardware) | [Storage](#Storage) | [Scheduler](#Scheduler) | [Software](#Software)

### [Login Procedure]() {#login-procedure}

The SAVIO cluster uses One Time Passwords (OTP) for login authentication. You will need to download and configure the Google Authenticator application on a tablet, and/or smart phone (Android or iOS) to generate these one time passwords. Please see [Logging into Savio](http://research-it.berkeley.edu/services/high-performance-computing/logging-savio)for instructions on installing and configuring Google Authenticator.

-   Login Protocol: ssh
-   Login Server: hpc.brc.berkeley.edu

### [Data Transfer]() {#data-transfer}

To transfer data to or from the SAVIO cluster, connect to the cluster's Data Transfer Node. For instructions, please see [Transferring Data](http://research-it.berkeley.edu/services/high-performance-computing/transferring-data).

-   Data Transfer Node: dtn.brc.berkeley.edu
-   Globus Endpoint Name: ucb\#brc

### [Hardware Configuration]() {#hardware-configuration}

Please refer to the following table with the hardware configuration of each generation of nodes. A high performance Lustre file system is also available as scratch space to all users.

<table style="width:99%;">
<colgroup>
<col width="11%" />
<col width="11%" />
<col width="11%" />
<col width="11%" />
<col width="11%" />
<col width="11%" />
<col width="11%" />
<col width="11%" />
<col width="11%" />
</colgroup>
<thead>
<tr class="header">
<th>Partition</th>
<th>Nodes</th>
<th>Node List</th>
<th>CPU Model</th>
<th># Cores/Node</th>
<th>Memory/Node</th>
<th>Infiniband</th>
<th>Speciality</th>
<th>Scheduler Allocation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>savio</td>
<td>164</td>
<td>n0[000-095].savio1<br />
n0[100-167].savio1</td>
<td>Intel Xeon E5-2670 v2</td>
<td>20</td>
<td>64 GB</td>
<td>FDR</td>
<td>-</td>
<td>By Node</td>
</tr>
<tr class="even">
<td>savio_bigmem</td>
<td>4</td>
<td>n0[096-099].savio1</td>
<td>Intel Xeon E5-2670 v2</td>
<td>20</td>
<td>512 GB</td>
<td>FDR</td>
<td>BIGMEM</td>
<td>By Node</td>
</tr>
<tr class="odd">
<td>savio2_htc</td>
<td>20</td>
<td><p>n0[000-011].savio2<br />
n0[215-222].savio2</p></td>
<td>Intel Xeon E5-2643 v3</td>
<td>12</td>
<td>128 GB</td>
<td>FDR</td>
<td>HTC</td>
<td>By Core</td>
</tr>
<tr class="even">
<td>savio2_gpu</td>
<td>15</td>
<td>n0[012-026].savio2</td>
<td>Intel Xeon E5-2623 v3</td>
<td>8</td>
<td>64 GB</td>
<td>FDR</td>
<td>4x Nvidia K80</td>
<td>By Core</td>
</tr>
<tr class="odd">
<td>savio2</td>
<td>136</td>
<td>n0[027-162].savio2</td>
<td>Intel Xeon E5-2670 v3</td>
<td>24</td>
<td>64 GB</td>
<td>FDR</td>
<td>-</td>
<td>By Node</td>
</tr>
<tr class="even">
<td>savio2_bigmem</td>
<td>4</td>
<td>n0[163-166].savio2</td>
<td>Intel Xeon E5-2670 v3</td>
<td>24</td>
<td>128 GB</td>
<td>FDR</td>
<td>-</td>
<td>By Node</td>
</tr>
</tbody>
</table>

### [Storage and Backup]() {#storage-and-backup}

SAVIO cluster users are entitled to access the following storage systems. Please be sure to use these filesystems correctly. Users should not use their HOME directory for heavy I/O activity during job runs.

<table style="width:323%;">
<colgroup>
<col width="90%" />
<col width="20%" />
<col width="80%" />
<col width="80%" />
<col width="11%" />
<col width="42%" />
</colgroup>
<thead>
<tr class="header">
<th>Name</th>
<th>Location</th>
<th>Quota</th>
<th>Backup</th>
<th>Allocation</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>HOME</td>
<td>/global/home/users/</td>
<td>10 GB</td>
<td>Yes</td>
<td>Per User</td>
<td>HOME directory for permanent data</td>
</tr>
<tr class="even">
<td>GROUP</td>
<td>/global/home/groups/</td>
<td>200 GB</td>
<td>No</td>
<td>Per Group</td>
<td>GROUP directory for shared data (Condo only)</td>
</tr>
<tr class="odd">
<td>SCRATCH</td>
<td>/global/scratch/</td>
<td>none</td>
<td>No</td>
<td>Per User</td>
<td>SCRATCH directory with Lustre FS</td>
</tr>
</tbody>
</table>

### [Scheduler Configuration]() {#scheduler-configuration}

The SAVIO cluster uses [SLURM](http://research-it.berkeley.edu/services/high-performance-computing/running-your-jobs) as the scheduler to manage jobs on the cluster. Please see [Running Your Jobs](http://research-it.berkeley.edu/services/high-performance-computing/running-your-jobs) for instructions on using the scheduler, as well as taking note of crucial additional details, below.

Three different models are supported when running jobs on the Savio cluster through the scheduler:

-   Condo model - Faculty and principal investigators can join the [Condo program](http://research-it.berkeley.edu/services/high-performance-computing/condo-cluster-program) by purchasing compute nodes which are contributed to the cluster. Users from the condo group are granted ongoing, no cost use of compute resources for running their jobs, up to the amount contributed. Condo users can also access larger amounts of compute resources at no cost via Savio's preemptable, [low-priority quality of service option](#Low_Priority).
-   Faculty Computing Allowance (FCA) model - This program provides qualified faculty and principal investigators with up to 200K [Service Units](http://research-it.berkeley.edu/services/high-performance-computing/service-units-savio) on the SAVIO cluster at no cost, during each annual application period. Please see [Faculty Computing Allowance](http://research-it.berkeley.edu/services/high-performance-computing/faculty-computing-allowance) for more details.
-   Memorandum of Understanding (MOU) model - If you use your entire Faculty Computing Allowance for a year and need additional compute time on Savio, please contact us at brc-hpc-help@berkeley.edu. We can help you set up an MOU, through which you can pay for additional blocks of compute time at a rate that is highly competitive with those of other compute providers.

Depending on the specific group(s) to which a user belongs, s/he may have access to one or more of the models described above. Therefore, it is highly recommended that all users become familiar with the following scheduler configuration on the SAVIO cluster to use its resources in an efficient manner:

-   The partition name “savio” or “savio\_bigmem” (“--partition=savio” or “--partition=savio\_bigmem”) is needed in all cases.
-   The designated account that was assigned to the user is needed in all cases (*e.g.*, --account=**fc\_{PUT\_YOUR\_ACCOUNT\_HERE}**).
-   The appropriate Quality of Service (QoS) selection is also required; the specific QoS which applies to each user will depend on his/her project(s) and the model under which the job should run:
    -   To run jobs with the condo model, the proper condo QoS (*e.g.*, --qos=**{PUT\_YOUR\_CONDO\_NAME\_HERE}**\_normal) should be used.
    -   To run jobs with the FCA model, the proper FCA QoS (*e.g.*, --qos=**savio**\_normal) should be used.
    -   To run jobs with the MOU model, the proper MOU QoS (*e.g.*, --qos=**savio**\_normal, or --qos=**savio**\_debug) should be used.
-   A standard fair-share policy with a decay half-life of 14 days (2 weeks) is enforced.

##### Configuration Details {#configuration-details}

<table style="width:96%;">
<colgroup>
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
</colgroup>
<thead>
<tr class="header">
<th>Partition</th>
<th>Nodes</th>
<th>Node<br />
Features</th>
<th>Shared</th>
<th><a href="http://research-it.berkeley.edu/services/high-performance-computing/service-units-savio">SU/CORE Hour<br />
Ratio</a></th>
<th>Account</th>
<th>QoS</th>
<th>QoS Limit</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>savio</td>
<td>164</td>
<td>savio</td>
<td>Exclusive</td>
<td>0.75</td>
<td><table>
<tbody>
<tr class="odd">
<td>ac_*<br />
fc_*<br />
pc_*</td>
</tr>
<tr class="even">
<td>co_*</td>
</tr>
</tbody>
</table></td>
<td><table>
<tbody>
<tr class="odd">
<td>savio_debug</td>
</tr>
<tr class="even">
<td>savio_normal</td>
</tr>
<tr class="odd">
<td><a href="#Savio_Condo">Condo QoS</a></td>
</tr>
<tr class="even">
<td>savio_lowprio</td>
</tr>
</tbody>
</table></td>
<td><table>
<tbody>
<tr class="odd">
<td>4 nodes max per job<br />
4 nodes in total<br />
00:30:00 wallclock limit</td>
</tr>
<tr class="even">
<td>24 nodes max per job<br />
72:00:00 wallclock limit</td>
</tr>
<tr class="odd">
<td><a href="#Savio_Condo">Savio Condo QoS Conf</a></td>
</tr>
<tr class="even">
<td>24 nodes max per job<br />
72:00:00 wallclock limit</td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td>savio_<br />
bigmem</td>
<td>4</td>
<td>savio_<br />
bigmem<br />
or<br />
savio_<br />
m512</td>
<td>Exclusive</td>
<td>1.67</td>
<td><table>
<tbody>
<tr class="odd">
<td>ac_*<br />
fc_*<br />
pc_*</td>
</tr>
<tr class="even">
<td>co_*</td>
</tr>
</tbody>
</table></td>
<td><table>
<tbody>
<tr class="odd">
<td>savio_debug</td>
</tr>
<tr class="even">
<td>savio_normal</td>
</tr>
<tr class="odd">
<td><a href="#Savio_Bigmem_Condo">Condo QoS</a></td>
</tr>
<tr class="even">
<td>savio_lowprio</td>
</tr>
</tbody>
</table></td>
<td><table>
<tbody>
<tr class="odd">
<td>4 nodes max per job<br />
4 nodes in total<br />
00:30:00 wallclock limit</td>
</tr>
<tr class="even">
<td>24 nodes max per job<br />
72:00:00 wallclock limit</td>
</tr>
<tr class="odd">
<td><a href="#Savio_Bigmem_Condo">Savio Bigmem Condo QoS Conf</a></td>
</tr>
<tr class="even">
<td>24 nodes max per job<br />
72:00:00 wallclock limit</td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="odd">
<td>savio2_<br />
htc</td>
<td>20</td>
<td>savio2_<br />
htc</td>
<td>Shared</td>
<td>1.20</td>
<td><table>
<tbody>
<tr class="odd">
<td>ac_*<br />
fc_*<br />
pc_*</td>
</tr>
<tr class="even">
<td>co_*</td>
</tr>
</tbody>
</table></td>
<td><table>
<tbody>
<tr class="odd">
<td>savio_debug</td>
</tr>
<tr class="even">
<td>savio_normal</td>
</tr>
<tr class="odd">
<td><a href="#Savio2_HTC_Condo">Condo QoS</a></td>
</tr>
<tr class="even">
<td>savio_lowprio</td>
</tr>
</tbody>
</table></td>
<td><table>
<tbody>
<tr class="odd">
<td>4 nodes max per job<br />
4 nodes in total<br />
00:30:00 wallclock limit</td>
</tr>
<tr class="even">
<td>24 nodes max per job<br />
72:00:00 wallclock limit</td>
</tr>
<tr class="odd">
<td><a href="#Savio2_HTC_Condo">Savio2 HTC Condo QoS Conf</a></td>
</tr>
<tr class="even">
<td>24 nodes max per job<br />
72:00:00 wallclock limit</td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td>savio2_<br />
gpu</td>
<td>15</td>
<td>savio2_<br />
gpu</td>
<td>Shared</td>
<td>2.67</td>
<td><table>
<tbody>
<tr class="odd">
<td>ac_*<br />
fc_*<br />
pc_*</td>
</tr>
<tr class="even">
<td>co_*</td>
</tr>
</tbody>
</table></td>
<td><table>
<tbody>
<tr class="odd">
<td>savio_debug</td>
</tr>
<tr class="even">
<td>savio_normal</td>
</tr>
<tr class="odd">
<td><a href="#Savio2_GPU_Condo">Condo QoS</a></td>
</tr>
<tr class="even">
<td>savio_lowprio</td>
</tr>
</tbody>
</table></td>
<td><table>
<tbody>
<tr class="odd">
<td>4 nodes max per job<br />
4 nodes in total<br />
00:30:00 wallclock limit</td>
</tr>
<tr class="even">
<td>24 nodes max per job<br />
72:00:00 wallclock limit</td>
</tr>
<tr class="odd">
<td><a href="#Savio2_GPU_Condo">Savio2 GPU Condo QoS Conf</a></td>
</tr>
<tr class="even">
<td>24 nodes max per job<br />
72:00:00 wallclock limit</td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="odd">
<td>savio2</td>
<td>136</td>
<td>savio2</td>
<td>Exclusive</td>
<td>1.00</td>
<td><table>
<tbody>
<tr class="odd">
<td>ac_*<br />
fc_*<br />
pc_*</td>
</tr>
<tr class="even">
<td>co_*</td>
</tr>
</tbody>
</table></td>
<td><table>
<tbody>
<tr class="odd">
<td>savio_debug</td>
</tr>
<tr class="even">
<td>savio_normal</td>
</tr>
<tr class="odd">
<td><a href="#Savio2_Condo">Condo QoS</a></td>
</tr>
<tr class="even">
<td>savio_lowprio</td>
</tr>
</tbody>
</table></td>
<td><table>
<tbody>
<tr class="odd">
<td>4 nodes max per job<br />
4 nodes in total<br />
00:30:00 wallclock limit</td>
</tr>
<tr class="even">
<td>24 nodes max per job<br />
72:00:00 wallclock limit</td>
</tr>
<tr class="odd">
<td><a href="#Savio2_Condo">Savio2 Condo QoS Conf</a></td>
</tr>
<tr class="even">
<td>24 nodes max per job<br />
72:00:00 wallclock limit</td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td>savio2_<br />
bigmem</td>
<td>4</td>
<td>savio2_<br />
bigmem<br />
or<br />
savio2_<br />
m128</td>
<td>Exclusive</td>
<td>1.20</td>
<td><table>
<tbody>
<tr class="odd">
<td>ac_*<br />
fc_*<br />
pc_*</td>
</tr>
<tr class="even">
<td>co_*</td>
</tr>
</tbody>
</table></td>
<td><table>
<tbody>
<tr class="odd">
<td>savio_debug</td>
</tr>
<tr class="even">
<td>savio_normal</td>
</tr>
<tr class="odd">
<td><a href="#Savio2_Bigmem_Condo">Condo QoS</a></td>
</tr>
<tr class="even">
<td>savio_lowprio</td>
</tr>
</tbody>
</table></td>
<td><table>
<tbody>
<tr class="odd">
<td>4 nodes max per job<br />
4 nodes in total<br />
00:30:00 wallclock limit</td>
</tr>
<tr class="even">
<td>24 nodes max per job<br />
72:00:00 wallclock limit</td>
</tr>
<tr class="odd">
<td><a href="#Savio2_Bigmem_Condo">Savio2 Bigmem Condo QoS Conf</a></td>
</tr>
<tr class="even">
<td>24 nodes max per job<br />
72:00:00 wallclock limit</td>
</tr>
</tbody>
</table></td>
</tr>
</tbody>
</table>

**NOTE:** To check which account and/or QoS that a user is allowed to use, please run "sacctmgr -p show associations user=$USER".

##### [Savio Condo QoS Configurations]() {#savio-condo-qos-configurations}

<table style="width:99%;">
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>Account</th>
<th>QoS</th>
<th>QoS Limit</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>co_acrb</td>
<td>acrb_normal</td>
<td>8 nodes max per group</td>
</tr>
<tr class="even">
<td>co_aiolos</td>
<td>aiolos_normal</td>
<td>12 nodes max per group<br />
24:00:00 wallclock limit</td>
</tr>
<tr class="odd">
<td>co_astro</td>
<td><table>
<tbody>
<tr class="odd">
<td>astro_debug</td>
</tr>
<tr class="even">
<td>astro_normal</td>
</tr>
</tbody>
</table></td>
<td><table>
<tbody>
<tr class="odd">
<td>4 nodes max per group<br />
4 nodes max per job<br />
00:30:00 wallclock limit</td>
</tr>
<tr class="even">
<td>32 nodes max per group<br />
16 nodes max per job</td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td>co_dlab</td>
<td>dlab_normal</td>
<td>4 nodes max per group</td>
</tr>
<tr class="odd">
<td>co_nuclear</td>
<td>nuclear_normal</td>
<td>24 nodes max per group</td>
</tr>
<tr class="even">
<td>co_praxis</td>
<td>praxis_normal</td>
<td>4 nodes max per group</td>
</tr>
<tr class="odd">
<td>co_rosalind</td>
<td>rosalind_normal</td>
<td>8 nodes max per group<br />
4 nodes max per job per user</td>
</tr>
</tbody>
</table>

##### [Savio Bigmem Condo QoS Configurations]() {#savio-bigmem-condo-qos-configurations}

 

##### [Savio2 HTC Condo QoS Configurations]() {#savio2-htc-condo-qos-configurations}

| Account      | QoS                   | QoS Limit             |
|--------------|-----------------------|-----------------------|
| co\_rosalind | rosalind\_htc\_normal | 8 nodes max per group |

##### [Savio2 GPU Condo QoS Configurations]() {#savio2-gpu-condo-qos-configurations}

| Account  | QoS               | QoS Limit             |
|----------|-------------------|-----------------------|
| co\_acrb | acrb\_gpu\_normal | 36 GPUs max per group |

##### [Savio2 Condo QoS Configurations]() {#savio2-condo-qos-configurations}

| Account      | QoS              | QoS Limit              |
|--------------|------------------|------------------------|
| co\_biostat  | biostat\_normal  | 8 nodes max per group  |
| co\_chemqmc  | chemqmc\_normal  | 12 nodes max per group |
| co\_dweisz   | dweisz\_normal   | 8 nodes max per group  |
| co\_econ     | econ\_normal     | 2 nodes max per group  |
| co\_hiawatha | hiawatha\_normal | 40 nodes max per group |
| co\_lihep    | lihep\_normal    | 4 nodes max per group  |
| co\_mrirlab  | mrirlab\_normal  | 4 nodes max per group  |
| co\_planets  | planets\_normal  | 4 nodes max per group  |
| co\_stat     | stat\_normal     | 2 nodes max per group  |
| co\_bachtrog | bachtrog\_normal | 4 nodes max per group  |

[Savio2 Bigmem Condo QoS Configurations](){#Savio2_Bigmem_Condo}

| Account    | QoS                    | QoS Limit             |
|------------|------------------------|-----------------------|
| co\_laika  | laika\_normal          | 4 nodes max per group |
| co\_dweisz | dweisz\_bigmem\_normal | 4 nodes max per group |
| co\_aiolos | aiolos\_bigmem\_normal | 4 nodes max per group |

##### [Low Priority Jobs]() {#low-priority-jobs}

All condo contributors (account name starts with "co\_") are entitled to use the extra resource that is available on the SAVIO cluster (across all partitions). The is done through a low priority QoS "savio\_lowprio" and your account is automatically subscribed to this QoS during the account creation stage. You do not need to request for it explicitly. By using this QoS you are no longer limited by your condo size. What this means to users is that you will now have access to the broader compute resource which is limited by the size of partitions. However this QoS does not get a priority as high as the general QoSs, such as "savio\_normal" and "savio\_debug", or all the condo QoSs, and it is subject to preemption when all the other QoSs become busy. Thus it has two implications:

1.  When system is busy, any job that is submitted with this QoS will be pending and yield to other jobs with higher priorities.
2.  When system is busy and there are higher priority jobs pending, scheduler will preempt jobs that are running with this lower priority QoS. Preempted jobs can choose whether the job should be simply killed, or be automatically requeued after it's killed, at submission time. Please note that, since preemption could happen at any time, it would be very beneficial if your job is capable of checkpointing/restarting by itself, when you choose to requeue the job. Otherwise, you may need to verify data integrity manually before you want to run the job again.

##### [Job Script Examples]() {#job-script-examples}

For many examples of job script files that you can adapt and use for running your own jobs, please see [Running Your Jobs](http://research-it.berkeley.edu/services/high-performance-computing/running-your-jobs).

### [Software Configuration]() {#software-configuration}

The SAVIO cluster uses [Environment Modules](http://research-it.berkeley.edu/services/high-performance-computing/accessing-and-installing-software) to manage the cluster-wide software installation.
