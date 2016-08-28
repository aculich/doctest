Welcome to the Savio cluster. You should have received an email with
information about your account and a link to the cluster [User
Guide](http://research-it.berkeley.edu/services/high-performance-computing/user-guide).

For an overview of hardware, software, and more on Savio, please see the
[System
Overview](http://research-it.berkeley.edu/services/high-performance-computing/system-overview).

**Passwords**. You'll need to generate and enter a one-time password
each time you that you log in. You'll use an application called Google
Authenticator to generate these passwords, which you can install and run
on your smartphone, and/or tablet. For instructions on setting up and
using Google Authenticator, see [Logging into
Savio](http://research-it.berkeley.edu/services/high-performance-computing/logging-savio).

**Logging in**. You'll use your favorite SSH client program to log into
the cluster via hpc.brc.berkeley.edu. E.g., from the command line (where
you'll substitute your actual Savio username for myusername):

$ ssh myusername@hpc.brc.berkeley.edu

**File storage**. Once you log in, you'll be in your home directory
(/global/home/users/*myusername*), with a 10 GB storage limit. You also
have access to a personal scratch directory
(/global/scratch/*myusername*), through which you'll share Savio's
Global Scratch storage area with other cluster users. Within that
scratch area you can store vast amounts of data, but you should always
regard it as temporary storage. (In addition to home and scratch
directories, some Savio users may also have access to a group directory,
shared with their collaborators.) Your home, scratch, and (if relevant)
group directories are all equally accessible from Savio's login,
compute, and data transfer nodes.

**Running your jobs**. When you log into Savio, you'll land on one of
several login/front-end nodes. Here you can edit scripts, compile
programs etc. However, you should not be running any applications or
tasks on the login nodes, which are shared with many other Savio users.
Instead, use the SLURM job scheduler to submit jobs that will be run on
one or more of Savio's hundreds of compute nodes. You'll use SLURM
commands like sbatch to submit your jobs, sinfo to view their status,
and scancel to cancel them. Whenever you run sbatch, you'll point it at
a SLURM job script, a small file that specifies where and how you want
to run your job on the cluster and what command(s) you want your job to
execute. If you need to run jobs interactively, there's also an srun
command available. See [Running Your
Jobs](http://research-it.berkeley.edu/services/high-performance-computing/running-your-jobs)
for more information on submitting and running your jobs via SLURM.

**Accessing or installing software**. Lot of software packages and tools
are already built and available on Savio. You can list these and
load/unload them via Environment Module commands. By default, SLURM and
Warewulf commands are already added to your path, starting out. At a
shell prompt, enter module list to see what you're currently accessing,
module avail to see what additional software is available, and one or
more module load *modulename* or module unload *modulename* commands to
set up your environment. For more information on accessing software via
Environment Module commands - as well as on installing your own
software, if needed - please see [Accessing and Installing
Software](http://research-it.berkeley.edu/services/high-performance-computing/accessing-and-installing-software).

**Transfering data**. To transfer data from other computers into - or
out of - your directories on Savio, you can use protocols and tools like
SCP, STFP, FTPS, and Rsync. If you're transferring lots of data, the
web-based Globus Connect tool is typically your best choice: it can
perform fast, reliable, unattended transfers. Whenever you transfer
data, you'll need to connect to Savio's dedicated Data Transfer Node,
dtn.brc.berkeley.edu. For more information on getting your data onto and
off of Savio, please see [Transferring
Data](http://research-it.berkeley.edu/services/high-performance-computing/transferring-data).

**For more information**. You might also refer to the [Tips &
Tricks](http://research-it.berkeley.edu/services/high-performance-computing/tips-using-brc-savio-cluster)
page for more helpful information on how to use the Savio cluster. And
don't forget the main [User
Guide](http://research-it.berkeley.edu/services/high-performance-computing/user-guide)
- it's packed with information you'll need.  
  
It's possible that you still have questions about topics that we have
not covered here. For additional help, support, or information, please
see [Getting
Help](http://research-it.berkeley.edu/services/high-performance-computing/getting-help).

 
