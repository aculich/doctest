[Planned Outages](#planned-outages) | [Announcements](#announcements) | [Live Status](#live-status)

### **System Status**

All systems are available.

### [Planned Outages](#planned-outages)

There are no planned outages scheduled at this time.

### [Announcements](#announcements)

**July 27, 2016 11:30 PDT -** The Savio cluster's scratch filesystem (/global/scratch) is now back online. Savio's job scheduler has been released from its downtime-related reservations, and jobs are running as scheduled before.

Please note the following changes made during this downtime that directly affect cluster users, as described in earlier announcements:

-   Intel compilers are not loaded by default anymore. Nor is OpenMPI. Please update your login scripts according to your needs, following these changes.
-   You'll use a new method of referring to Graphics Processing Units (GPUs) when requesting them for your jobs; e.g., as described in the GPU job script example in [Running Your Jobs](http://research-it.berkeley.edu/services/high-performance-computing/running-your-jobs).

Feel free to email us at <brc-hpc-help@berkeley.edu> if you need help with anything.

**July 26, 2016 17:45 PDT -** Access to the BRC supercluster is now enabled. Users can now access the login nodes, data transfer node and the data on all the filesystems (except /global/scratch). We finished all the maintenance tasks scheduled for today's downtime except the work on the Scratch filesystem which is still ongoing. We are copying filesystem metadata from the old to a new storage platform and these transfers are scheduled to finish tomorrow morning. Access to data on this (/global/scratch) filesystem will remain blocked until then.

SLURM job queues for the Cortex and Vector clusters have been released and jobs are running as scheduled before. As most of the jobs running in the Savio cluster queues depend on data in the scratch filesystem none of the Savio queues/partitions have been released yet. We expect to release Savio queues and Scratch filesystem sometime early in the morning tomorrow, Wednesday, July 27, 2016.

**July 15, 2016 15:35 PDT -** Savio will be unavailable on **Tuesday, July 26, 2016, from 9:00 am to 5:00 pm** for scheduled maintenance.

This downtime will impact all three clusters (Savio, Cortex, and Vector and all associated condos) in the BRC supercluster infrastructure. Access to login/front-end nodes, compute nodes, scheduler queues and data on the cluster filesystems will be blocked for the duration of the downtime. If you are submitting any jobs to Savio partitions before Tuesday, July 26th, please make sure you request the proper wall clock times so that your jobs finish running before 9:00 am that day, or else they will be waiting in the queue until after the downtime.

After the downtime we will no longer be loading Intel compilers in user environments by default, nor OpenMPI (the version associated with the Intel compilers). Users dependent on Intel compilers will need to explicitly load them (`$ module load intel`). Users who do not need Intel compilers will no longer have to add `module unload intel` to their default login scripts. In addition, the method of requesting GPUs in your job scripts has been changed to use SLURM [generic resource (GRES)](http://slurm.schedmd.com/gres.html) requests; e.g, as described in the GPU job script example in [Running Your Jobs](http://research-it.berkeley.edu/services/high-performance-computing/running-your-jobs). Other than this, no user-noticeable changes will be made.

**July 7, 2016 -** Pledge enrollments are still not available. The vendor is working on the problem, but there is no ETA. New user accounts are on HOLD.

**July 5, 2016 -** Pledge enrollments for One-Time-Password users is not working due to a vendor service problem. This affects new Savio users needing to enroll in Pledge to setup OTP access to Savio and existing users needing to enroll new devices for OTP access to Savio.

**June 26, 2016 13:11 PDT -** Login access to Savio was affected by an outage of the OTP server earlier this AM. The service has now been restored.

**June 5, 2016 12:53 PDT -** Savio's /global/scratch filesystem is back online.

**June 5, 2016 12:04 PDT-** Savio's /global/scratch filesystem is having problems and is unavailable. Investigation is underway. There is currently no ETA for resolution.

**June 1, 2016 10:30 PDT-** We are receiving very intermittent reports of issues with the supercluster's /global/scratch filesystem. We are aware of these reports and are actively seeking further data to help isolate the cause(s) of the problem. Please send any reports of issues to <brc-hpc-help@berkeley.edu>. It would also be very helpful if you can identify the date and time you experienced the issue, the login (or compute) node you're working on (this is typically mentioned in your shell prompt), the paths to any directories or files that are problematic, what command(s) you're attempting to run, and the text of any error messages you've encountered. In that way, we can more rapidly associate your problem experiences with logging and debugging messages.

**May 23, 2016 15:40 PDT** - Today's planned maintenance work has been completed. The /global/scratch filesystem is once again available, and jobs can once again be scheduled.

**May 23, 2016 13:45 PDT** - Update as of 1:45 pm: Today's planned maintenance work is continuing beyond the originally scheduled maintenance window. It is now in the final update step, and is expected to be finished by or before 3:30 pm.

**May 19, 2016 15:30 PDT** - Savio will be unavailable on Monday, May 23, 2016, from 8:00 am to 12:00 noon for scheduled maintenance. This maintenance will address the intermittent issues with the /global/scratch filesystem, described in the announcement of May 9, 2016 (below).

**May 9, 2016 12:00 PDT** - For the past few days we have been experiencing highly intermittent access issues with data on the BRC supercluster's /global/scratch filesystem. It has been very transient, with only some users experiencing these issues and only for short periods of time. We are aware of this and our engineers are actively working with the storage vendor to identify the source and resolve these problems. For those who are experiencing the issue just a simple listing of the files in their folders would appear to be hung without giving any response. If you experience the problem, send us an email to <brc-hpc-help@berkeley.edu> with the path to the folder you are trying to access, as it would give us more data points for debugging.

**April 26, 2016 16:00 PDT** - Pledge service is now back online. Please try to connect now and your Pledge OTP should work. In case you generated a lot of OTPs while the service is offline its possible your Pledge has gone out of sync with the server and your Pledge OTPs might still not work. In this case please re-sync your Pledge app by following the instructions under the last tab on this page:<a href="https://commons.lbl.gov/display/itfaq/Installing+and+Configuring+the+OTP+Token" class="uri" class="uri">https://commons.lbl.gov/display/itfaq/Installing+and+Configuring+the+OTP+Token</a>

**April 26, 2016 14:47 PDT** - We are having some unexpected issues with the One Time Password service today. User attempts to connect/SSH to cluster resources might not be working. We are aware of this message and are working on it. Users with already connected active sessions can continue to use the cluster resources as before. Do not loose your connections. Users trying to start new sessions will not be able to do so. We apologize for this inconvenience and we will update you when things are back to normal. Avoid generating new OTPs from your Pledge applications until new email you or else you might run your Pledge apps out of sync with the servers.

**April 1, 2016 12:30 PDT** - Jobs are flowing normally again. The SLURM scheduler problem was caused by a bug in the scheduler software. An upgrade to the latest version of SLURM has fixed the problem.

**March 31, 2016 17:02 PDT -** We are noticing SLURM job queue issues on the Savio cluster. As users submit jobs to different Savio partitions it looks like some of the jobs are waiting in the queue for more time than needed even when there are free nodes available. This is to tell you that we are aware of this issue and we are working on a fix for this. We apologize for this unexpected behavior and inconvenience. We will update you as we make progress, in the mean time feel free to continue submitting jobs to queues as before.

**March 29, 2016 16:42 PDT -** Savio will be unavailable on Wednesday, March 30, 2016, from 9:00 am to 5:00 pm for scheduled maintenance.

**February 29, 2016 10:23PST -** The issue with I/O errors when running batch jobs has been resolved. The cause was that the scheduler server ran out of disk space.

**February 29, 2016 09:57PST -** Running batch jobs via 'sbatch' is failing with I/O errors. Savio's administrators are investigating.

**February 29, 2016 08:30PST -** Timeout errors with Savio's Data Transfer Node (DTN) have been resolved.

**February 29, 2016 07:45PST -** Savio's administrators are investigating reports of timeout errors when using Savio's Data Transfer Node (DTN).

**January 28, 2016 14:30PST -** SSH logins to Savio's Data Transfer Node (DTN) are once again available.

**January 28, 2016 11:30PST -** SSH logins to Savio's Data Transfer Node (DTN) are currently unavailable. (This problem was first identified at or near 10:15PST.) Estimated resolution is at or before 14:30PST.

**October 9, 2015 15:15PST** - The Savio cluster has been significantly expanded through the addition of a pool of 76 new, second generation compute nodes, each equipped with two 12-core Intel Haswell processors (24 cores total) and 64 GB of memory. Another 28 PI-contributed Condo nodes with the same specifications will be added to this pool shortly, to bring its total count to 104 nodes.

Any cluster user with an active Faculty Computing Allowance can now run jobs on either its second generation Haswell processor nodes, or on its first generation nodes, each of which is equipped with two 10-core Intel Ivy Bridge processors (20 cores total) and 64 GB of memory.

To select one or the other, please specify the appropriate SLURM partition name when submitting your jobs. (For more details, see the [Scheduler section of the Savio User Guide](http://research-it.berkeley.edu/services/high-performance-computing/user-guide#Scheduler).)

**June 11, 2015 8:00PST** - The /global/scratch storage system is back online and the data is intact; however, we are concerned about the stabilty of the storage system. We have a new, higher performance, higher capacity storage system that was scheduled to go online later this month. Because of the instability of the current /global/scratch filesystem, we will copy the data and cut over to the new system now. Savio jobs will be held until this is completed.

**June 9, 2015  3:30PST** - The /global/scratch filesystem is currently offline due to a hardware failure. BRC is working wth the vendor to resolve the issue. Here is no ETA at this time.

**April 24, 2015 6:00 PST** - Power has been restored and all systems are back online.

**April 24, 2015 11:37 PST** - A power outage has affected the BRC compute clusters including SAVIO and private pool clusters Vector and Cortex. At the moment there is no ETA for when systems will be available.

**1/27/2015 11:15 PST **Global Scratch back online.

**1/27/2015 16:05 PST **Global Scratch on SAVIO is down due to a hardware problem so all compute nodes have been taken offline.

**12/23/2014 22:05 PST - Update on Global SCRATCH Problem**
Global SCRATCH is now back online after our emergency maintenance. Unfortunately our attempts did not improve the situation we need to follow up with the storage vendor once again and try this procedure again either on or after December 26, 2014. We will notify all users when this is scheduled again in future.

**12/23/2014 18:54 PST - Emergency Filesystem Maintenance**
We ran into issues with a second attempt at rebuilding the Global SCRATCH filesystem. Our storage vendor has recommended that we immediately take the filesystem (/global/scratch) offline to reset the controllers and disks. Given the importance and priority of making this filesystem reliable we will be doing this in the next several minutes now. SCRATCH filesystem may stay offline for couple of hours and attempts to access (both reads & writes) of data will fail during this time. There are some user jobs running in the queues, if any of those jobs use this filesystem they might fail. Please verify your failed jobs and resubmit them to the queues. Any data transfer sessions currently writing to /global/scratch will also break. Please restart your transfers.

**12/19/2014 - BRC Support during the Holiday Curtailment**
BRC SAVIO cluster will continue to operate during the UC Berkeley Holiday Curtailment December 24, 2014 through Jan 1, 2015 Users experiencing system problems can continue to send email to brc-hpc-help@berkeley.edu to report problems. BRC staff will be monitoring incoming email and trouble tickets, but support will be best-effort and prioritized based on criticality and impact. We wish all users a great Holiday break and a Happy New Year.

**12/12/2014 - SAVIO Global SCRATCH Problem**
SAVIO cluster SCRATCH filesystem (/global/scratch) started having issues from afternoon today, Dec 12th. One of the backend storage controller started labeling some of the disks as failed. BRC engineers having been working on it since this afternoon and as of now the filesystem is back online and users should be able to access all their data. But to bring this RAID filesystem back to it normal condition all the failed disks need to rebuild and that process is going on right now. Until the rebuilding process completes successfully (over the next couple of days) we cannot guarantee total stability of the filesystem. There is some possibility that filesystem does not recover and we experience data loss. As the filesystem is accessible right now we ask all our SAVIO cluster users to review what they have under this SCRATCH filesystem and manually backup any important data immediately to a local storage. Please remember this is a SCRATCH filesystem and there are no system level backups, if data is lost we cannot recover. We highly recommend using [Globus](https://www.globus.org/) for data transfers out of the SAVIO cluster. Our endpoint name is ucb\#brc. If you would prefer to use traditional transfer tools like scp/rsync please login to the dedicated Data Transfer Node (DTN), dtn.brc.berkeley.edu and start your transfers from that node.

### [Live Status](#live-status)


