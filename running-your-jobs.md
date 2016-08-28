[Overview](#Overview) | [Key options to set](#Key-options) | [Basic job submission](#Basic-job-submission) | [Job submission with specific resource requirements](#Job-submission-with-specific-resource-requirements) | [Additional job submission options](#Additional-job-submission-options) | [Finding output](#Finding-output) | [Charges for running jobs](#Charges) | [Migration](#Migration)

Overview
========

To submit and run jobs, cancel jobs, and check the status of jobs on the Savio cluster, you'll use the Simple Linux Utility for Resource Management (SLURM), an open-source resource manager and job scheduling system. (SLURM manages jobs, job steps, nodes, partitions (groups of nodes), and other entities on the cluster.)

There are several basic SLURM commands you'll likely use often:

-   `sbatch` - Submit a job to the batch queue system, e.g., `sbatch myjob.sh`, where `myjob.sh` is a SLURM job script. (On this page, you can find both a simple, [introductory example of a job script](#Basic-job-submission), as well as [many other examples of job scripts](#Job-submission-with-specific-resource-requirements) for specific types of jobs you might run. Adapting and modifying one of these examples is the quickest way to get started with running batch jobs.)
-   `srun` - Submit an interactive job to the batch queue system
-   ``` scancel``  ```- Cancel a job, e.g., `scancel 123`, where 123 is a job ID
-   `squeue` - Check the current jobs in the batch queue system, e.g., `squeue -u $USER` to view your own jobs
-   `sinfo` - View the current status of the queues

The remainder of this page provides more details about using the SLURM scheduler:

-   Learn about the [key options](#Key-options) you'll need to set when running your jobs.
-   See [examples](#Basic-job-submission) of basic interactive and batch job submission.
-   See [examples](#Job-submission-with-specific-resource-requirements) of how to request specific computational resources in terms of the number of nodes or cores or computational tasks required. (These options are of particular importance when doing parallel computation.)
-   See [additional options](#Additional-job-submission-options) when submitting a job, including time limits, memory requirements, etc.
-   Learn where [output](#Finding-output) from your batch jobs can be found.
-   Find out [how much it costs](#Charges) to run your jobs.
-   See the [Migration](#Migration) tables for examples of how to transition from Torque/PBS to SLURM.

Key options to set when submitting your jobs
============================================

When submitting a job, the two key options required are the **account** you are submitting under and the **partition** you are submitting to. Under some circumstances, a **Quality of Service (QoS)** is also expected, along with the partition.

-   **Account**: Each job must be submitted as part of an account, which determines which resources you have access to and how your use will be charged. Note that this account name, which you will use in your SLURM job script files, is different from your Linux account name on the cluster. For instance, for a hypothetical example user `lee` who has access to both the `physics` condo and to a Faculty Computing Allowance, their available accounts for running jobs on the cluster might be named `co_physics` and `fc_lee`, respectively. (See below for a command that you can run to find out what account name(s) you can use in your own job script files.)
-   **Partition**: Each job must be submitted to a particular partition. A partition can also be considered to be a job queue that comes with a set of constraints, such as job size limit, time limit, etc. Jobs submitted within a partition will be allocated to that partition's set of compute nodes based on the scheduling policy, until all resources within that partition are exhausted. Currently, on the Savio cluster, partitions are also associated with specific types of computational resources on which you can request your job be run, such as older or newer generations of standard compute nodes, "big memory" nodes, nodes with Graphics Processing Units (GPUs), etc. (See below for a command that you can run to find out what partitions you can use in your own job script files.)
-   **QoS**: A QoS is a classification that determines what kind of resources your job can use. For instance, there is a QoS option that you can select for running test jobs when you're debugging your code, which further constrains the resources available to your job and thus may reduce its cost. As well, Condo users can select a "lowprio" QoS which can make use of unused resources on the cluster, in exchange for these jobs being subject to termination when needed, in order to free resources for higher priority jobs. (See below for a command that you can run to find out what QoS options you can use in your own job script files.)

You can view the accounts you have access to, partitions you can use, and the QoS options available to you using the ``` sacct``mgr ``` command:

`sacctmgr -p show associations user=`$USER

This will return output such as the following for a hypothetical example user `lee` who has access to both the `physics` condo and to a Faculty Computing Allowance. Each line of this output indicates a specific combination of an account, a partition, and QoSes that you can use in a job script file, when submitting any individual batch job:

`Cluster|Account|User|Partition|...|QOS|Def QOS|GrpTRESRunMins|brc|co_physics|lee|savio2_gpu|...|savio_lowprio|savio_lowprio||brc|co_physics|lee|savio2_htc|...|savio_lowprio|savio_lowprio||brc|co_physics|lee|savio2_bigmem|...|savio_lowprio|savio_lowprio||`
`brc|co_physics|lee|savio2|...|savio_lowprio,physics_normal|physics_normal||`
`brc|co_physics|lee|savio|...|savio_lowprio|savio_lowprio||brc|co_physics|lee|savio_bigmem|...|savio_lowprio|savio_lowprio||`
`...brc|fc_lee|lee|savio2_gpu|...|savio_debug,savio_normal|savio_normal||`
`brc|fc_lee|lee|savio2_htc|...|savio_debug,savio_normal|savio_normal||`
`brc|fc_lee|lee|savio2_bigmem|...|savio_debug,savio_normal|savio_normal||`
`brc|fc_lee|lee|savio2|...|savio_debug,savio_normal|savio_normal||brc|fc_lee|lee|savio|...|savio_debug,savio_normal|savio_normal||brc|fc_lee|lee|savio_bigmem|...|savio_debug,savio_normal|savio_normal||`

The `Account`, `Partition`, and `QOS` fields indicate which partitions and QoSes you have access to under each of your account(s). The `Def QoS` field identifies the default QoS that will be used if you do not explicitly identify a QoS when submitting a job. Thus as per the example above, if the user `lee` submitted a batch job using their `fc_lee` account, they could submit their job to either the `savio2_gpu`, `savio2`\_htc, `savio2_bigmem`, `savio2`, `savio`, or `savio_bigmem` partitions. (And when doing so, they could also choose either the `savio_debug` or `savio_normal` QoS, with a default of `savio_normal` if no QoS was specified.)

If you are running your job in a condo, be sure to note which of the line(s) of output associated with the condo account (those beginning with "co\_" ) have their `Def QoS` being a lowprio QoS and which have a normal QoS. Those with a normal QoS (such as the line highlighted in **boldface text** in the above example) are the QoS to which you have priority access, while those with a lowprio QoS are those to which you have only low priority access. Thus, in the above example, the user `lee` should select the `co_physics` account and the `savio2` partition when they want to run jobs with normal priority, using the resources available via their condo membership.

You can find more details on the various partitions and QoS options, as well as on low priority jobs, in the [Scheduler section of the User Guide](http://research-it.berkeley.edu/services/high-performance-computing/user-guide#Scheduler).

In addition to the key options of account, partition, and QoS, your job script files can also contain [options to request various numbers of cores, nodes, and/or computational tasks](#Job-submission-with-specific-resource-requirements). And there are a variety of [additional options](#Additional-job-submission-options) you can specify in your batch files, if desired, such as the maximum amount of wall clock time your job should be allowed to run. These are all described further below.

Basic job submission
====================

This section provides an overview of how to run your jobs in batch (i.e., non-interactive or background) mode and in interactive mode.

### Batch jobs

When you want to run one of your jobs in batch (i.e. non-interactive or background) mode, you'll enter an `sbatch` command. As part of that command, you will also specify the name of, or filesystem path to, a SLURM job script file; e.g., `sbatch myjob.sh`

A job script specifies where and how you want to run your job on the cluster, and ends with the actual command(s) needed to run your job. The job script file looks much like a standard shell script (`.sh`) file, but also includes one or more lines that specify options for the SLURM scheduler; e.g.

`#SBATCH --some-option-here`

Although these lines start with hash signs (`#`), and thus are regarded as comments by the shell, they are nonetheless read and interpreted by the SLURM scheduler.

Here is a simple example of a job script file that includes the required account and partition options. It will launch the application named `a.out`, which will be run unattended for up to 30 seconds on one of the compute nodes in the `partition_name` partition:

`#!/bin/bash`
`# Job name:`
`#SBATCH --job-name=test`
`#`
`# Account:`
`#SBATCH --account=account_name`
`#`
`# Partition:`
`#SBATCH --partition=partition_name`
`#`
`# Wall clock limit:`
`#SBATCH --time=00:00:30`
`#`
`## Command(s) to run:`
`./a.out`

In this and other examples, `account_name` and `partition_name` are placeholders for actual values you will need to provide. See [Key options to set](#Key-options), above, for information on what values to use for `account_name` and `partition_name` in your own job script fies.

See [Job submission with specific resource requirements](#Job-submission-with-specific-resource-requirements), below, for a set of example job script files, each illustrating how to run a specific type of job.

See [Finding output](#Finding-output) to learn where output from running your batch jobs can be found. If errors occur when running your batch job, this is the first place to look for these.

### Interactive jobs

In some instances, you may need to use software that requires user interaction, rather than running programs or scripts in batch mode. To do so, you must first start an instance of an interactive shell on a Savio compute node, within which you can then run your software on that node. To run such an interactive job on a compute node, you'll use `srun`. Here is a basic example that launches an interactive 'bash' shell on that node, and includes the required account and partition options:

`[user@ln001 ~]$ srun --pty -A account_name -p partition_name bash`

Once your job starts, the Linux prompt will change and indicate you are on a compute node rather than a login node:

`srun: job 669120 queued and waiting for resourcessrun: job 669120 has been allocated resources[user@n0047 ~]$ `

Job submission with specific resource requirements
==================================================

This section provides a set of example job scripts, showing the key SLURM scheduler options, for a variety of the kinds of jobs you might submit on Savio. When submitting parallel code, you usually need to specify the number of tasks, nodes, and CPUs to be used by your job in various ways. For any given use case, there are generally multiple ways to set the options to achieve the same effect; these examples try to illustrate what we consider to be best practices.

The key options for parallelization are:

-   `--nodes` (or `-N`): indicates the number of nodes to use
-   `--ntasks-per-node`: indicates the number of tasks (i.e., processes one wants to run on each node)
-   `--cpus-per-task` (or `-c`): indicates the number of cpus to be used for each task

In addition, in some cases it can make sense to use the `--ntasks` (or `-n`) option to indicate the total number of tasks and let the scheduler determine how many nodes and tasks per node are needed. In general --cpus-per-task will be 1 except when running threaded code.  

Note that if the various options are not set, SLURM will in some cases infer what the value of the option needs to be given other options that are set and in other cases will treat the value as being 1. So some of the options set in the example below are not strictly necessary, but we give them explicitly to be clear.

Finally, remember that nodes are assigned for exclusive access by your job, except in the "savio2\_htc" and "savio2\_gpu" partitions. So, if possible, you generally want to set SLURM options and write your code to use all the cores on the nodes assigned to your job (e.g., 20 cores per node in the "savio" partition and 24 in the "savio2" partition).

In the examples below, when you see "(example)" that indicates that how you set the option will depend on the characteristics of your specific job.

Individual files with the contents of each of the example job scripts which follow are also available from [GitHub](https://github.com/ucberkeley/brc-draft-documentation).

### 1. Threaded/OpenMP job script

`#!/bin/bash`
`# Job name:`
`#SBATCH --job-name=test`
`#`
`# Account:`
`#SBATCH --account=account_name`
`#`
`# Partition:`
`#SBATCH --partition=partition_name`
`#`
`# Request one node:`
`#SBATCH --nodes=1`
`#`
`# Specify one task:`
`#SBATCH --ntasks-per-node=1`
`#`
`# Number of processors for single task needed for use case (example):`
`#SBATCH --cpus-per-task=4`
`#`
`# Wall clock limit:`
`#SBATCH --time=00:00:30`
`#`
`## Command(s) to run (example):`
`export OMP_NUM_THREADS=$SLURM_CPUS_PER_TASK`
`./a.out`

Here `--cpus-per-task` should be no more than the number of cores on a Savio node in the partition you request. You may want to experiment with the number of threads for your job to determine the optimal number, as computational speed does not always increase with more threads. Note that if --cpus-per-task is fewer than the number of cores on a node, your job will not make full use of the node. Strictly speaking the `--nodes` and --ntasks-per-node arguments are optional here because they default to 1.

### 2. Simple multi-core job script (multiple processes on one node)

`#!/bin/bash`
`# Job name:`
`#SBATCH --job-name=test`
`#`
`# Account:`
`#SBATCH --account=account_name`
`#`
`# Partition:`
`#SBATCH --partition=partition_name`
`#`
`# Request one node:`
`#SBATCH --nodes=1`
`#`
`# Specify number of tasks for use case (example):`
`#SBATCH --ntasks-per-node=20`
`#`
`# Processors per task:`
`#SBATCH --cpus-per-task=1`
`#`
`# Wall clock limit:`
`#SBATCH --time=00:00:30`
`#`
`## Command(s) to run (example):`
`./a.out`

This job script would be appropriate for multi-core R, Python, or MATLAB jobs. In the commands that launch your code and/or within your code itself, you can reference the `SLURM_NTASKS` environment variable to dynamically identify how many tasks (i.e., processing units) are available to you.

Here the number of CPUs used by your code at at any given time should be no more than the number of cores on a Savio node.

For a way to run many individual jobs on one or more nodes (more jobs than cores), see the Tips & Tricks entry regarding use of a [mini-scheduler script](http://research-it.berkeley.edu/services/high-performance-computing/tips-using-brc-savio-cluster#q-how-to-run-high-throughput-computing-htc-type-of-jobs-how-to-run-multiple-jobs-on-the-same-node-).

### 3. MPI job script

`#!/bin/bash`
`# Job name:`
`#SBATCH --job-name=test`
`#`
`# Account:`
`#SBATCH --account=account_name`
`#`
`# Partition:`
`#SBATCH --partition=partition_name`
`#`
`# Number of MPI tasks needed for use case (example):`
`#SBATCH --ntasks=40`
`#`
`# Processors per task:`
`#SBATCH --cpus-per-task=1`
`#`
`# Wall clock limit:`
`#SBATCH --time=00:00:30`
`#`
`## Command(s) to run (example):`
`module load openmpi`
`mpirun ./a.out`

As noted in the introduction, for all partitions except for "savio2\_htc" and "savio2\_gpu", you probably want to set the number of tasks to be a multiple of the number of cores per node in that partition, thereby making use of all the cores on the node(s) to which your job is assigned.

This example assumes that each task will use a single core; otherwise there could be resource contention amongst the tasks assigned to a node.

### 4. Alternative MPI job script

`#!/bin/bash`
`# Job name:`
`#SBATCH --job-name=test`
`#`
`# Account:`
`#SBATCH --account=account_name`
`#`
`# Partition:`
`#SBATCH --partition=partition_name`
`#`
`# Number of nodes needed for use case:`
`#SBATCH --nodes=2`
`#`
`# Tasks per node based on number of cores per node (example):`
`#SBATCH --ntasks-per-node=20`
`#`
`# Processors per task:`
`#SBATCH --cpus-per-task=1`
`#`
`# Wall clock limit:`
`#SBATCH --time=00:00:30`
`#`
`## Command(s) to run (example):`
`module load openmpi`
`mpirun ./a.out`

This alternative explicitly specifies the number of nodes, tasks per node, and CPUs per task rather than simply specifying the number of tasks and having SLURM determine the resources needed. As before, one would generally want the number of tasks per node to equal a multiple of the number of cores on a node, assuming only one CPU per task.

### 5. Hybrid OpenMP+MPI job script

`#!/bin/bash`
`# Job name:`
`#SBATCH --job-name=test`
`#`
`# Account:`
`#SBATCH --account=account_name`
`#`
`# Partition:`
`#SBATCH --partition=partition_name`
`#`
`# Number of nodes needed for use case (example):`
`#SBATCH --nodes=2`
`#`
`# Tasks per node based on --cpus-per-task below and number of cores`
`#   per node (example):`
`#SBATCH --ntasks-per-node=4`
`#`
`# Processors per task needed for use case (example):`
`#SBATCH --cpus-per-task=5`
`#`
`# Wall clock limit:`
`#SBATCH --time=00:00:30`
`#`
`## Command(s) to run (example):`
`module load openmpi`
`export OMP_NUM_THREADS=$SLURM_CPUS_PER_TASK`
`mpirun ./a.out`

Here we request a total of 8 (=2x4) MPI tasks, with 5 cores per task.  This would make use of all the cores on two, 20-core nodes in the "savio" partition.

### 6. Jobs scheduled on a per-core basis (jobs that use fewer cores than available on a node)

`#!/bin/bash`
`# Job name:`
`#SBATCH --job-name=test`
`#`
`# Account:`
`#SBATCH --account=account_name`
`#`
`# Partition:`
`#SBATCH --partition=savio2_htc`
`#`
`# Number of tasks needed for use case (example):`
`#SBATCH --ntasks=4`
`#`
`# Processors per task:`
`#SBATCH --cpus-per-task=1`
`#`
`# Wall clock limit:`
`#SBATCH --time=00:00:30`
`#`
`## Command(s) to run (example):`
`./a.out`

In the "savio2\_htc" pool you are only charged for the actual number of cores used, so the notion of making best use of resources by saturating a node is not relevant.

### 7. GPU job script

`#!/bin/bash`
`# Job name:`
`#SBATCH --job-name=test`
`#`
`# Account:`
`#SBATCH --account=account_name`
`#`
`# Partition:`
`#SBATCH --partition=savio2_gpu`
`#`
`# Number of nodes:`
`#SBATCH --nodes=1`
`#`
`# Number of tasks (one for each GPU desired for use case) (example):`
`#SBATCH --ntasks=1`
`#`
`# Processors per task (please always specify total number of processors twice of number of GPUs):`
`#SBATCH --cpus-per-task=2`
`#`
`#Number of GPUs, this can be in the format of "gpu:[1-4]", or "gpu:K80:[1-4] with the type included`
`#SBATCH --gres=gpu:1`
`#`
`# Wall clock limit:`
`#SBATCH --time=00:00:30`
`#`
`## Command(s) to run (example):`
`./a.out`

Each GPU node has four GPUs, but the "savio2\_gpu" nodes are scheduled by core. To help us effectively manage the use of the multiple GPUs, we ask that you request two CPUs for each GPU you will use, hence --cpus-per-task=2.

Additional job submission options
=================================

Here are some additional options that you can incorporate as needed into your own scripts. These are introduced one-by-one, below, in `boldface text`. (For the full set of available options, please see the [SLURM documentation on the sbatch command](http://slurm.schedmd.com/sbatch.html).)

### Job Script with Exclusive Usage of Nodes

`#!/bin/bash`
`# Job name:`
`#SBATCH --job-name=test`
`#`
`# Account:`
`#SBATCH --account=account_name`
`#`
`# Partition:`
`#SBATCH --partition=partition_name`
`#`
`# Processors:`
`#SBATCH --nodes=2`
`#SBATCH --exclusive`
`#`
`# Wall clock limit:`
`#SBATCH --time=00:00:30`
`#`
`## Command(s) to run:`
`a.out`

### Job script with Email Notification

`#!/bin/bash`
`# Job name:`
`#SBATCH --job-name=test`
`#`
`# Account:`
`#SBATCH --account=account_name`
`#`
`# Partition:`
`#SBATCH --partition=partition_name`
`#`
`# Wall clock limit:`
`#SBATCH --time=00:00:30`
`#`
`# Mail type:`
`#SBATCH --mail-type=all`
`#`
`# Mail user:`
`#SBATCH --mail-user=jessie.doe@berkeley.edu`
`#`
`## Command(s) to run:`
`./a.out`

### Job Script with Memory Requirement

`#!/bin/bash`
`# Job name:`
`#SBATCH --job-name=test`
`#`
`# Account:`
`#SBATCH --account=account_name`
`#`
`# Partition:`
`#SBATCH --partition=partition_name`
`#`
`# Memory:`
`#SBATCH --mem-per-cpu=2G`
`#`
`# Wall clock limit:`
`#SBATCH --time=00:00:30`
`#`
`## Command(s) to run:`
`./a.out`

### Job Script with QoS

`#!/bin/bash`
`# Job name:`
`#SBATCH --job-name=test`
`#`
`# Account:`
`#SBATCH --account=account_name`
`#`
`# Partition:`
`#SBATCH --partition=partition_name`
`#`
`# QoS:`
`#SBATCH --qos=qos_name`
`#`
`# Wall clock limit:`
`#SBATCH --time=00:00:30`
`#`
`## Command(s) to run:`
`./a.out`

### Job Script with Job Array

`#!/bin/bash`
`# Job name:`
`#SBATCH --job-name=test`
`#`
`# Account:`
`#SBATCH --account=account_name`
`#`
`# Partition:`
`#SBATCH --partition=partition_name`
`#`
`# Indexes:`
`#SBATCH --array=0-31`
`#`
`# Wall clock limit:`
`#SBATCH --time=00:00:30`
`#`
`## Command(s) to run:`
`./a.out`

Finding output from running batch jobs
======================================

Note that output from running a SLURM batch job is, by default, placed in a log file named `slurm-$SLURM_JOBID.out`, where the job's actual ID is substituted for `$SLURM_JOBID`; e.g. `slurm-478012.out` This file will be created in your current directory; e.g. the directory from within which you entered the sbatch command. Also by default, both command output and error output (to stdout and stderr, respectively) is combined in this file.

 You can modify several of these default behaviors, if you wish, via various [sbatch options](http://slurm.schedmd.com/sbatch.html) in the job script file.

Charges for running jobs
========================

When running your SLURM batch or interactive job under a [Faculty Computing Allowance](http://research-it.berkeley.edu/services/high-performance-computing/faculty-computing-allowance) account (i.e. a scheduler account whose name begins with `fc_`, as per [Key options to set when running your jobs](#Key-options)), that Allowance will be charged a number of [Service Units](http://research-it.berkeley.edu/services/high-performance-computing/service-units-savio), based on how many cores your job used, the duration of the time that it used them, and the type of computing nodes on which your job was run.

For more information on these charges, please see [Service Units on Savio](http://research-it.berkeley.edu/services/high-performance-computing/service-units-savio).

When running your job under a [Condo](http://research-it.berkeley.edu/services/high-performance-computing/condo-cluster-program) account (i.e. a scheduler account whose name begins with `co_`), no charges will apply.

Migrating from Torque/PBS to SLURM
==================================

The purpose of this section is to help users who are familiar with Torque/PBS to migrate to the SLURM environment more efficiently. For users coming from other schedulers, such as Platform LSF, SGE/OGE, Load Leveler, please use [this link](http://slurm.schedmd.com/rosetta.pdf) to find a quick reference.

Table 1 lists the common tasks that you can perform in Torque/PBS and the equivalent ways to perform those tasks in SLURM.

<table style="width:99%;">
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Task</p></td>
<td><p>Torque/PBS</p></td>
<td><p>SLURM</p></td>
</tr>
<tr class="even">
<td><p>Submit a job</p></td>
<td><p>qsub myjob.sh</p></td>
<td><p>sbatch myjob.sh</p></td>
</tr>
<tr class="odd">
<td><p>Delete a job</p></td>
<td><p>qdel 123</p></td>
<td><p>scancel 123</p></td>
</tr>
<tr class="even">
<td><p>Show job status</p></td>
<td><p>qstat</p></td>
<td><p>squeue</p></td>
</tr>
<tr class="odd">
<td><p>Show expected job start time</p></td>
<td><p>- (showstart in Maui/Moab)</p></td>
<td><p>squeue --start</p></td>
</tr>
<tr class="even">
<td><p>Show queue info</p></td>
<td><p>qstat -q</p></td>
<td><p>sinfo</p></td>
</tr>
<tr class="odd">
<td><p>Show job details</p></td>
<td><p>qstat -f 123</p></td>
<td><p>scontrol show job 123</p></td>
</tr>
<tr class="even">
<td><p>Show queue details</p></td>
<td><p>qstat -Q -f &lt;queue&gt;</p></td>
<td><p>scontrol show partition &lt;partition_name&gt;</p></td>
</tr>
<tr class="odd">
<td><p>Show node details</p></td>
<td><p>pbsnode n0000</p></td>
<td><p>scontrol show node n0000</p></td>
</tr>
<tr class="even">
<td><p>Show QoS details</p></td>
<td><p>- (mdiag -q &lt;QoS&gt; in Maui/Moab)</p></td>
<td><p>sacctmgr show qos &lt;QoS&gt;</p></td>
</tr>
</tbody>
</table>

Table 2 lists the commonly used options in the batch job script for both Torque/PBS (qsub) and SLURM (sbatch/srun/salloc).

<table style="width:99%;">
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Option</p></td>
<td><p>Torque/PBS</p></td>
<td><p>SLURM</p></td>
</tr>
<tr class="even">
<td><p>Declares the time after which the job is eligible for execution.</p></td>
<td><p>-a date_time</p></td>
<td><p>--begin=&lt;time&gt;</p></td>
</tr>
<tr class="odd">
<td><p>Defines the account string associated with the job.</p></td>
<td><p>-A account_string</p></td>
<td><p>-A, --account=&lt;account&gt;</p></td>
</tr>
<tr class="even">
<td><p>Defines the path to be used for the standard error stream of the batch job.</p></td>
<td><p>-e [hostname:][path_name]</p></td>
<td><p>-e, --error=&lt;filename pattern&gt;</p></td>
</tr>
<tr class="odd">
<td><p>Specifies that a user hold be applied to the job at submission time.</p></td>
<td><p>-h</p></td>
<td><p>-H, --hold</p></td>
</tr>
<tr class="even">
<td><p>Declares that the job is to be run &quot;interactively&quot;.</p></td>
<td><p>-I</p></td>
<td><p>srun -u bash -i</p></td>
</tr>
<tr class="odd">
<td><p>Declares if the standard error stream of the job will be merged with the standard output stream of the job.</p></td>
<td><p>-j oe / -j eo</p></td>
<td><p>default behavior</p></td>
</tr>
<tr class="even">
<td><p>Requests a number of nodes be allocated to this job.</p></td>
<td><p>-l nodes=number</p></td>
<td><p>-n, --ntasks=&lt;number&gt; / -N, --nodes=&lt;minnodes[-maxnodes]&gt;</p></td>
</tr>
<tr class="odd">
<td><p>Specifies the number of processors per node requested.</p></td>
<td><p>-l nodes=number:ppn=number</p></td>
<td><p>--ntasks-per-node=&lt;ntasks&gt; / --tasks-per-node=&lt;n&gt;</p></td>
</tr>
<tr class="even">
<td><p>Specifies the node feature.</p></td>
<td><p>-l nodes=number:gpu</p></td>
<td><p>-C, --constraint=&quot;gpu&quot;</p></td>
</tr>
<tr class="odd">
<td><p>Requests a specific list of node names.</p></td>
<td><p>-l nodes=node1+node2</p></td>
<td><p>-w, --nodelist=&lt;node name list&gt; / -F, --nodefile=&lt;node file&gt;</p></td>
</tr>
<tr class="even">
<td><p>Specifies the real memory required per node in Megabytes.</p></td>
<td><p>-l mem=mem</p></td>
<td><p>--mem=&lt;MB&gt;</p></td>
</tr>
<tr class="odd">
<td><p>Specifies the minimum memory required per allocated CPU in Megabytes.</p></td>
<td><p>no equivalent</p></td>
<td><p>--mem-per-cpu=&lt;MB&gt;</p></td>
</tr>
<tr class="even">
<td><p>Requests a quality of service for the job.</p></td>
<td><p>-l qos=qos</p></td>
<td><p>--qos=&lt;qos&gt;</p></td>
</tr>
<tr class="odd">
<td><p>Sets a limit on the total run time of the job allocation.</p></td>
<td><p>-l walltime=time</p></td>
<td><p>-t, --time=&lt;time&gt;</p></td>
</tr>
<tr class="even">
<td><p>Defines the set of conditions under which the execution server will send a mail message about the job.</p></td>
<td><p>-m mail_options (a, b, e)</p></td>
<td><p>--mail-type=&lt;type&gt; (type = BEGIN,  END,  FAIL, REQUEUE, ALL)</p></td>
</tr>
<tr class="odd">
<td><p>Declares the list of users to whom mail is sent by the execution server when it sends mail about the job.</p></td>
<td><p>-M user_list</p></td>
<td><p>--mail-user=&lt;user&gt;</p></td>
</tr>
<tr class="even">
<td><p>Specifies that the job has exclusive access to the nodes it is executing on.</p></td>
<td><p>-n</p></td>
<td><p>--exclusive</p></td>
</tr>
<tr class="odd">
<td><p>Declares a name for the job.</p></td>
<td><p>-N name</p></td>
<td><p>-J, --job-name=&lt;jobname&gt;</p></td>
</tr>
<tr class="even">
<td><p>Defines the path to be used for the standard output stream of the batch job.</p></td>
<td><p>-o path</p></td>
<td><p>-o, --output=&lt;filename pattern&gt;</p></td>
</tr>
</tbody>
</table>

<table style="width:99%;">
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Defines the destination of the job.</p></td>
<td><p>-q destination</p></td>
<td><p>-p, --partition=&lt;partition_names&gt;</p></td>
</tr>
<tr class="even">
<td><p>Declares whether the job is rerunnable.</p></td>
<td><p>-r y|n</p></td>
<td><p>--requeue</p></td>
</tr>
<tr class="odd">
<td><p>Declares the shell that interprets the job script.</p></td>
<td><p>-S path_list</p></td>
<td><p>no equivalent</p></td>
</tr>
<tr class="even">
<td><p>Specifies the task ids of a job array.</p></td>
<td><p>-t array_request</p></td>
<td><p>-a, --array=&lt;indexes&gt;</p></td>
</tr>
<tr class="odd">
<td><p>Allows for per job prologue and epilogue scripts.</p></td>
<td><p>-T script_name</p></td>
<td><p>no equivalent</p></td>
</tr>
<tr class="even">
<td><p>Defines the user name under which the job is to run on the execution system.</p></td>
<td><p>-u user_list</p></td>
<td><p>--uid=&lt;user&gt;</p></td>
</tr>
<tr class="odd">
<td><p>Expands the list of environment variables that are exported to the job.</p></td>
<td><p>-v variable_list</p></td>
<td><p>--export=&lt;environment variables | ALL | NONE&gt;</p></td>
</tr>
<tr class="even">
<td><p>Declares that all  environment variables in the qsub command's environment are to be exported to the batch job.</p></td>
<td><p>-V</p></td>
<td><p>--export=&lt;environment variables | ALL | NONE&gt;</p></td>
</tr>
<tr class="odd">
<td><p>Defines the working directory path to be used for the job.</p></td>
<td><p>-w path</p></td>
<td><p>-D, --workdir=&lt;directory&gt;</p></td>
</tr>
<tr class="even">
<td><p>This job may be scheduled for execution at any point after jobs jobid have started  execution.</p></td>
<td><p>-W depend=after:jobid[:jobid...]</p></td>
<td><p>-d, --dependency=after:job_id[:jobid...]</p></td>
</tr>
<tr class="odd">
<td><p>This job may be scheduled  for execution only after jobs jobid have terminated with no errors.</p></td>
<td><p>-W depend=afterok:jobid[:jobid...]</p></td>
<td><p>-d, --dependency=afterok:job_id[:jobid...]</p></td>
</tr>
<tr class="even">
<td><p>This job may be scheduled for execution only after jobs jobid have terminated with errors.</p></td>
<td><p>-W depend=afternotok:jobid[:jobid...]</p></td>
<td><p>-d, --dependency=afternotok:job_id[:jobid...]</p></td>
</tr>
<tr class="odd">
<td><p>This job may be scheduled for execution after jobs jobid have terminated, with or without errors.</p></td>
<td><p>-W depend=afterany:jobid[:jobid...]</p></td>
<td><p>-d, --dependency=afterany:job_id[:jobid...]</p></td>
</tr>
<tr class="even">
<td><p>This job can begin execution after any previously launched jobs sharing the same job name and user have terminated.</p></td>
<td><p>no equivalent</p></td>
<td><p>-d, --dependency=singleton</p></td>
</tr>
<tr class="odd">
<td><p>Defines the group name under which the job is to run on the execution system.</p></td>
<td><p>-W group_list=g_list</p></td>
<td><p>--gid=&lt;group&gt;</p></td>
</tr>
<tr class="even">
<td><p>Allocates resources for the job from the named reservation.</p></td>
<td><p>-W x=FLAGS:ADVRES:staff.1</p></td>
<td><p>--reservation=&lt;name&gt;</p></td>
</tr>
<tr class="odd">
<td><p>Enables X11 forwarding.</p></td>
<td><p>-X</p></td>
<td><p>srun --pty [command]</p></td>
</tr>
</tbody>
</table>

Table 3 lists the commonly used environment variables in Torque/PBS and the equivalents in SLURM.

<table style="width:99%;">
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Environment Variable For</p></td>
<td><p>Torque/PBS</p></td>
<td><p>SLURM</p></td>
</tr>
<tr class="even">
<td><p>Job ID</p></td>
<td><p>PBS_JOBID</p></td>
<td><p>SLURM_JOB_ID / SLURM_JOBID</p></td>
</tr>
<tr class="odd">
<td><p>Job name</p></td>
<td><p>PBS_JOBNAME</p></td>
<td><p>SLURM_JOB_NAME</p></td>
</tr>
<tr class="even">
<td><p>Node list</p></td>
<td><p>PBS_NODELIST</p></td>
<td><p>SLURM_JOB_NODELIST / SLURM_NODELIST</p></td>
</tr>
<tr class="odd">
<td><p>Job submit directory</p></td>
<td><p>PBS_O_WORKDIR</p></td>
<td><p>SLURM_SUBMIT_DIR</p></td>
</tr>
<tr class="even">
<td><p>Job array ID (index)</p></td>
<td><p>PBS_ARRAY_INDEX</p></td>
<td><p>SLURM_ARRAY_TASK_ID</p></td>
</tr>
<tr class="odd">
<td><p>Number of tasks</p></td>
<td><p>-</p></td>
<td><p>SLURM_NTASKS</p></td>
</tr>
</tbody>
</table>


