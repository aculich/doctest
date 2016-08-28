\[TOC\]

### Q. How do I know which partition, account, and QoS I should use when submitting my job?

**A.** SLURM provides a command you can run to check on the partitions, accounts and Quality of Service (QoS) options that you're permitted to use. Please run the "**sacctmgr show associations user=$USER**" command to find this information for your job submission. You can also add the "-p" option to this command to get a parsable output, i.e., "**sacctmgr -p show associations user=$USER**".

### Q. How can I check on my Faculty Computing Allowance (FCA) usage?

**A.** Savio provides a "**check\_usage.sh**" command line tool you can use to check cluster usage for the current user and for all the Faculty Computing Allowance (FCA) accounts that user is associated with. Simply running "**check\_usage.sh**", without any arguments, will report usage since the most recent reset/introduction date (normally June 1st of each year). You can also check usage during a specified time period via start and end date options: "**-s YYYY-MM-DD**" and "**-e YYYY-MM-DD**". Run "**check\_usage.sh -h**" for more information and additional options.

The [Service Units (SUs)](http://research-it.berkeley.edu/services/high-performance-computing/service-units-savio) field is now color-coded: green means your account has used less than 50% of the allowance; yellow means your account has used more than 50% but less than 100% of the allowance; red means your account has used more than 100% of usage (and has likely been disabled). Note if you specify the starttime and/or endtime with "-s" and/or "-e" option(s) you will not get the color coded output.

A couple of output samples from running this command line tool with user and account options, respectively, along with some tips on interpreting that output:

`$ check_usage.sh -u myusernameUsage for USER myusername [2016-06-01T00:00:00, 2016-08-17T18:18:37]: 38 jobs,1311.40 CPUHrs, 984.43 SUs`

Usage from June 1, 2016 through the early evening of August 17, 2016 by the 'myusername' cluster user consists of 38 jobs run, using approximately 1,311 CPU hours, and resulting in usage of approximately 984 Service Units. (The total number of [Service Units](http://research-it.berkeley.edu/services/high-performance-computing/service-units-savio) is less than the total number of CPU hours, because some jobs were run on older or otherwise less expensive hardware pools (partitions) which cost less than one Service Unit per CPU hour.)

`$ check_usage.sh -a fc_myprojectnameUsage for ACCOUNT fc_myprojectname [2016-06-01T00:00:00, 2016-08-17T18:19:15]: 156jobs, 85263.80 CPUHrs, 92852.12 (200000) SUs`

Usage from June 1, 2016 through the early evening of August 17, 2016 by all cluster users of the Faculty Computing Allowance account 'fc\_myprojectname'  consists of 156 jobs run, using a total of approximately 85,263 CPU hours, and resulting in usage of approximately 92,852 Service Units. (The total number of [Service Units](http://research-it.berkeley.edu/services/high-performance-computing/service-units-savio) is greater than the total number of CPU hours, because some jobs were run on hardware pools (partitions) which cost more than one Service Unit per CPU hour.) The total Faculty Computing Allowance allocation for this account is 200,000 Service Units, so there are approximately 107,148 Service Units still available for running jobs during the remainder of the current Allowance year (June 1 to May 31): 200,000 total Service Units granted, less 92,852 used to date. The total of 92,852 Service Units used to date is colored green, because this account has used less than 50% of its total Service Units available to date.

### Q. How can I use $SLURM\_JOBID in my output and/or error log filenames?

**A.** SLURM uses a different way to manage SLURM-specific environment variables, which is in turn different than PBS or other job schedulers. Before you use a SLURM environment variable, please check its scope of availability by entering "man sbatch" or "man srun".

To use the JOBID as part of the output file name, it takes a filename pattern instead of any of the environment variables. Please "man sbatch" for details. As a quick reference, the proper syntax is "**--output=%j.out**".

### Q. When is my job going to start to run?

**A.** In most cases you should be able to get an estimate of when your job is going to start by running the command "**squeue --start -j $your\_job\_id**". However under the following two circumstances you may get a "N/A" as the reported START\_TIME.

-   You did not specify the run time limit for the job with "--time" option. This will block the job from being back filled.
-   The job that's currently running and blocking your job from starting didn't specify the run time limit with "--time" option.

Thus, as the best practice to improve the scheduler efficiency and to obtain a more accurate estimate of the start time, it is highly recommended to always use "--time" to specify a run time limit for your jobs. It is also worth noting that the start time is only an estimate based on the current jobs queued in the scheduler. If there are new jobs submitted later with higher priorities this estimate will be updated spontaneously as well. So this estimate should only be used as a reference instead of a guaranteed start time.

### Q. Why is my job not starting to run?

**A.** Lots of reasons could cause the job to not start at your expected time:

-   The first action that you should take to troubleshoot it is to get an estimate of the start time with "**squeue --start -j $your\_job\_id**". If the start time is reasonable and you are satisfied with the estimated start time you can stop here.
-   If you would like to troubleshoot further you can then run "**sinfo -p $partition**" to see if the resources that you are requesting are currently allocated to other jobs or not. If you used node features make sure you only check the resources that match the node feature that you requested (all the node features are documented on your cluster's webpage).
-   If you see enough resources available but your job is still not showing a reasonable start time, please run "**sprio**" to see if there are jobs with higher priorities that are currently blocking your job.
-   If there are no higher priority jobs blocking the resources that you requested please check if there's any reservation on the resources that you requested with "**scontrol show reservations**".
-   For FCA users you may also want to check whether your have used up all of your allowance or not with "**check\_usage.sh**".

If, after going through all of these steps, you are still puzzled by why your job is not starting, please feel free to [contact us](http://research-it.berkeley.edu/services/high-performance-computing/getting-help).

### Q. How can I check my job's running status?

**A.** If you suspect your job is not running properly, or you simply want to understand how much memory or how much CPU the job is actually using on the compute nodes, RIT provides a script "wwall" to check that. "**wwall -j $your\_job\_id**" provides a snapshot of node status that the job is running on. "**wwall -j $your\_job\_id -t**" provides a text-based user interface (TUI) to monitor the node status when the job progresses.

### Q. How can I run High-Throughput Computing (HTC) type of jobs? (How can I run multiple jobs on the same node?)

**A.** If you have a set of common tasks that you would like to perform on the cluster, and these tasks share the characteristics of short duration and a decent number of them, they fall into the category of High-Throughput Computing (HTC). Typical applications such as parameter/configuration scanning, divide and conquer approach can all be categorized like this. Resolving an HTC problem isn't easy on a traditional HPC cluster with time and resource limits. However, within the room that one can maneuver, there are still some options available.

Here we demonstrate one approach by using the "ht\_helper.sh" (HT Helper) script that RIT provides. The idea of the "**ht\_helper.sh**" script is to fire an FIFO mini scheduler within a real scheduler allocation (SLURM or PBS), then cycle through all the tasks within the real scheduler allocation by using the mini scheduler. These tasks could be either serial or parallel.

The following are the usage instructions for this "ht\_helper.sh" script:

``` rteindent1
[joe@ln000 ]$ ht_helper.sh -h
Usage: /global/home/groups/allhands/bin/ht_helper.sh [-dhkv] [-f hostfile]
       [-m modules] [-n # of processors per task] [-o ompi options]
       [-p # of parallel tasks] [-s sleep] [-t taskfile]
    -d    dump task stdout/stderr to files
    -f    provide a hostfile with list of processors, one per line
    -h    this help page
    -k    keep intermediate files (for debugging purpose)
    -m    provide environment modules to be loaded for tasks (comma separated)
    -n    provide number of processors per task
    -o    provide ompi options, e.g., "-mca btl openib,sm,self"
    -p    provide number of parallel tasks
    -s    interval between checks (default to 60s)
    -t    provide a taskfile with list of tasks, one per line (required)
          task could be a binary executable, or a script with the proper shebang,
          or a script string starts with something similar to "sh -c", e.g.,
              /bin/sh -c "echo task 0; hostname; sleep 5"
              /foo/bar/mytask0
          NOTE: if you have multiple steps for one task, you are not
              able to simply do "echo task 0; hostname; sleep 5",
              instead you will need to use the above "sh -c" trick,
              or use another script as a substitute
    -v    verbose mode
```

To use the helper script you will need to prepare one taskfile and one job script file. The taskfile will contain all the tasks that you need to run. If a self identifier is desired for each task, environment variable "$HT\_TASK\_ID" can be used in the taskfile, or any of the subsequent scripts. The taskfile takes three types of input as showed in the usage page. If you are running MPI type of tasks, please make sure not to have the mpirun command in the taskfile, instead you only need to input the actual executable and input options. If mpirun command line options are required please provide them via the "-o" option. For users running parallel tasks, please make sure to turn off CPU affinity settings, if any, to avoid conflicts and serious oversubscription of CPUs. The next important parameter is the "-n" option - how many processors/cpus you want to allocate for each task, the default value is "1" for serial tasks if not provided. If you are running short-duration tasks (less than a few minutes), you may also want to reduce the default mini scheduler check interval from 60 seconds to a smaller value with the "-s" option. If you are running within an SLURM or PBS allocation, please do not specify the hostfile with "-f" option which may conflict with the default allocation. To get familiar with using this helper script, you may want to turn on "-d" (dump output from each task to an individual file), "-k" (keep intermediate files), and "-v" (verbose mode) options so that you can better understand how it works. After you are familiar with the process, you can choose which options to use, we recommend "-d" and "-v". For the job script file it will look similar to a job script for a parallel job, except that you want to run command "ht\_helper.sh" on the taskfile that was just prepared instead of anything else.

Here's an example of it in production, demonstrating running an 8-task job within a 4-CPU allocation.

**taskfile:**

``` rteindent1
#!/bin/bash
hostname
date
/path/to/myscript.sh
whoami
uname -a
pwd
sh -c "echo task $HT_TASK_ID; hostname; sleep 5"
echo $((1+1))
```

**SLURM job script:**

``` rteindent1
#!/bin/bash
#SBATCH --job-name=test
#SBATCH --partition=savio
#SBATCH --account=ac_abc
#SBATCH --qos=savio_debug
#SBATCH --ntasks=4
#SBATCH --time=00:10:00
ht_helper.sh -t taskfile -n1 -s1 -dvk
```

As well, the Savio cluster now also offers [High Throughput Computing nodes](http://research-it.berkeley.edu/blog/16/05/19/high-throughput-computing-pool-savio-cluster), which may be suitable for some of these types of HTC tasks.

### Q. How can I run Hadoop jobs?

**A.** The Hadoop framework and an auxiliary script are provided to help users to run Hadoop jobs on the HPC clusters in Hadoop On Demand (HOD) fashion. The auxiliary script "**hadoop\_helper.sh**" is located in /global/home/groups/allhands/bin/hadoop\_helper.sh and can be used interactively or from a job script. Please note that this script only provides functions to help to build a Hadoop environment, so it should never be run directly. The proper way to use it is to source it from your current environment by running "**source /global/home/groups/allhands/bin/hadoop\_helper.sh**" (only bash is supported right now). After that please run "**hadoop-usage**" to see how to run Hadoop jobs. You will need to run "**hadoop-start**" to initialize an HOD environment and run "**hadoop-stop**" to destroy the HOD environment after your Hadoop job completes.

The example below shows how to use it interactively.

``` rteindent1
[joe@ln000 ~]$ srun -p savio -A ac_abc --qos=savio_debug -N 4 -t 10:0 --pty bash
[joe@ln000 ~]$ module load java hadoop
[joe@n0000 ~]$ source /global/home/groups/allhands/bin/hadoop_helper.sh
[joe@n0000 ~]$ hadoop-start
starting jobtracker, ...
[joe@n0000 bash.738294]$ hadoop jar $HADOOP_DIR/hadoop-examples-1.2.1.jar pi 4 10000
Number of Maps  = 4
...
Estimated value of Pi is 3.14140000000000000000
[joe@n0000 bash.738294]$ hadoop-stop
stopping jobtracker
...
```

The example below shows how to use it in a job script:

``` rteindent1
#!/bin/bash
#SBATCH --job-name=test
#SBATCH --partition=savio
#SBATCH --account=ac_abc
#SBATCH --qos=savio_debug
#SBATCH --nodes=4
#SBATCH --time=00:10:00

module load java hadoop
source /global/home/groups/allhands/bin/hadoop_helper.sh

# Start Hadoop On Demand
hadoop-start

# Example 1
hadoop jar $HADOOP_DIR/hadoop-examples-1.2.1.jar pi 4 10000

# Example 2
mkdir in
cp /foo/bar in/
hadoop jar $HADOOP_DIR/hadoop-examples-1.2.1.jar wordcount in out

# Stop Hadoop On Demand
hadoop-stop
```

### Q. How can I run Spark jobs?

**A.** The Spark framework and an auxiliary script are provided to help users to run Spark jobs on the HPC clusters in Spark On Demand (SOD) fashion. The auxiliary script "**spark\_helper.sh**" is located in /global/home/groups/allhands/bin/spark\_helper.sh and can be used interactively or from a job script. Please note that this script only provides functions to help to build a Spark environment, so it should never be run directly. The proper way to use it is to source it from your current environment by running "**source /global/home/groups/allhands/bin/spark\_helper.sh**" (only bash is supported right now). After that please run "**spark-usage**" to see how to run Spark jobs. You will need to run "**spark-start**" to initialize an SOD environment and run "**spark-stop**" to destroy the SOD environment after your Spark job completes.

The example below shows how to use it interactively:

``` rteindent1
[joe@ln000 ~]$ srun -p savio -A ac_abc --qos=savio_debug -N 4 -t 10:0 --pty bash
[joe@ln000 ~]$ module load java spark
[joe@n0000 ~]$ source /global/home/groups/allhands/bin/spark_helper.sh
[joe@n0000 ~]$ spark-start
starting org.apache.spark.deploy.master.Master, ...

[joe@n0000 bash.738307]$ spark-submit --master $SPARK_URL $SPARK_DIR/examples/src/main/python/pi.py
Spark assembly has been built with Hive
...
Pi is roughly 3.147280
...

[joe@n0000 bash.738307]$ pyspark $SPARK_DIR/examples/src/main/python/pi.py
WARNING: Running python applications through ./bin/pyspark is deprecated as of Spark 1.0.
...
Pi is roughly 3.143360
...

[joe@n0000 bash.738307]$ spark-stop
...
```

The example below shows how to use it in a job script:

``` rteindent1
#!/bin/bash
#SBATCH --job-name=test
#SBATCH --partition=savio
#SBATCH --account=ac_abc
#SBATCH --qos=savio_debug
#SBATCH --nodes=4
#SBATCH --time=00:10:00

module load java spark
source /global/home/groups/allhands/bin/spark_helper.sh

# Start Spark On Demand
spark-start

# Example 1
spark-submit --master $SPARK_URL $SPARK_DIR/examples/src/main/python/pi.py

# Example 2
spark-submit --master $SPARK_URL $SPARK_DIR/examples/src/main/python/wordcount.py /foo/bar

# PySpark Example
pyspark $SPARK_DIR/examples/src/main/python/pi.py

# Stop Spark On Demand
spark-stop
```

### Q. What does the \#error "This Intel &lt;math.h&gt; is for use with only the Intel compilers!" mean?

**A.** You likely are seeing this error because you have an Intel compiler module loaded in your environment, but you are trying to build your application with a GCC compiler. Please unload any Intel compiler module(s) from your current environment and rebuild with GCC. (See [Accessing and Installing Software](http://research-it.berkeley.edu/services/high-performance-computing/accessing-and-installing-software) for instructions on unloading modules.)

### Q. My code uses C++11 features. Do any compilers on the cluster support that?

**A.** C++11 (formerly known as C++0x) features have been partially supported by Intel's C++ compilers, beginning with version 11.x, and are fully supported in the 2015.x series. For more details please refer to [Intel's C++11 features support page](https://software.intel.com/en-us/articles/c0x-features-supported-by-intel-c-compiler). Note: to support the full set of C++11 features, GCC 4.8 and above is also needed. Please follow this guidance when compiling your C++ code with C++11 features on the cluster:

-   Start by loading the environment module for the default version of the Intel compilers via `module load intel`. Compile the code with "icpc -std=c++11 some\_file" (replacing "some\_file" with the actual name of your C++11 source code file).
-   If the command above finishes successfully you can stop here. Otherwise please check [Intel's C++11 features support page](https://software.intel.com/en-us/articles/c0x-features-supported-by-intel-c-compiler) to learn whether the C++11 features your code uses are supported by the default version of the Intel compilers. If not, please switch to the cluster's environment module that provides a higher version of the Intel compilers. To do so, enter "module switch intel intel/xxxx.yy.zz" (replacing "xxxx.yy.zz" with that higher version number; enter "module avail" to find that number, if needed).
-   If your code uses the C++11 Standard Template Library (STL), you’ll also need to load the GCC/4.8.5 software module as a driver; its header files provide support for the C++11 STL. To do so, enter "module load gcc/4.8.5" before compiling your code.

