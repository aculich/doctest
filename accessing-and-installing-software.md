[Overview](#Overview)  | [Usage Examples](#Examples)  | [Provided Software](#Software_Provided)  | [Chaining Modules](#Chaining) | [Installing Your Own](#Installing)

### [1. Overview]() {#overview}

To access much of the software available on the Savio cluster - ranging from compilers and interpreters to statistical analysis and visualization software, and much more - you'll use [Environment Module commands](#Examples).

These commands allow you to display a list of many of the [software packages provided on the cluster](#Software_Provided), as well as to conveniently load and unload different packages and their associated runtime environments, as you need them.

As a quick overview, Environment Modules are used to manage users’ runtime environments dynamically on the Savio cluster. This is accomplished by loading and unloading modulefiles which contain the application specific information for setting a user’s environment, primarily the shell environment variables, such as *PATH*, *LD\_LIBRARY\_PATH*, etc. Modules are useful in managing different applications, as well as different versions of the same application, in a cluster environment.

Finally, in addition to the software provided on the Savio cluster, you're also welcome to [install your own software](#Installing).

### [2. Environment Modules Usage Examples]() {#environment-modules-usage-examples}

Below are some of the Environment Module commands that you'll be using most frequently. All of these commands begin with module and are followed by a subcommand. (In this list of commands, a vertical bar (“|”) means “or”, e.g., module add and module load are equivalent. And you'll need to substitute actual modulefile names for *modulefile*, *modulefile1*, and *modulefile2* in the examples below.)

-   module avail - List all available modulefiles in the current MODULEPATH. (This is the command to use when you want to see the list of software that you can use on Savio via Environment Module commands.)
-   module list - List loaded modules. (This shows you what software you currently have available in your environment.)
-   module add|load *modulefile* ... - Load modulefile(s) into the shell environment. (This allows you to add more software packages to your environment.)
-   module rm|unload *modulefile* ... - Remove modulefile(s) from the shell environment.
-   module swap|switch \[*modulefile1*\] *modulefile2* - Switch loaded *modulefile1* with *modulefile2*.
-   module show|display *modulefile* ... - Display configuration information about the specified modulefile(s).
-   module whatis \[*modulefile* ...\] - Display summary information about the specified modulefile(s).
-   module purge - Unload all loaded modulefiles.

For more detailed usage instructions for the **module** command, please run man module on the cluster.

Below are representative examples of how to use these commands. Depending on which system you have access to and when you are reading this instruction, what you see here could be different from the actual output from the system that you work on. On systems like Savio, where a hierarchical structure is used, some modulefiles will only be available after their root modulefile is loaded. (For instance, modulefiles for various Python packages will only become available after you've loaded Python itself. Similarly, R packages, libraries for C compilers, and the like, will only become available after their respective parent modules have been loaded.)

It can be helpful to try out each of the following examples in sequence, to more fully understand how environment modules work. Commands you'll enter are shown in **bold**, followed by samples of output you might see:

    [casey@n0000 ~]$ module avail

    ---- /global/software/sl-6.x86_64/modfiles/tools ----
    cmake/2.8.11.2  gnuplot/4.6.0  octave/3.4.3  paraview/3.12.0  r/3.0.1  texlive/2013

    ---- /global/software/sl-6.x86_64/modfiles/langs ----
    gcc/4.4.7  intel/2013.5.192  intel/2013_sp1.2.144  pgi/13.10  python/2.6.6

    ---- /global/software/sl-6.x86_64/modfiles/intel/2013.5.192 ----
    acml/5.3.1-intel  atlas/3.10.1-intel  fftw/2.1.5-intel  fftw/3.3.3-intel  lapack/3.4.2-intel  mkl/2013.5.192  openmpi/1.6.5-intel
    ...

    [casey@n0000 ~]$ module list
    No Modulefiles Currently Loaded.

    [casey@n0000 ~]$ module load intel
        

    [casey@n0000 ~]$ module list

    Currently Loaded Modulefiles:
      1) intel/2013_sp1.4.211

    [casey@n0000 ~]$ module load openmpi mkl

    [casey@n0000 ~]$ module list
        Currently Loaded Modulefiles:
      1) intel/2013_sp1.4.211   3) mkl/2013_sp1.4.211
      2) openmpi/1.6.5-intel

    [casey@n0000 ~]$ module unload openmpi
    [casey@n0000 ~]$ module list
    Currently Loaded Modulefiles:
      1) intel/2013.5.192   2) mkl/2013.5.192

    [casey@n0000 ~]$ module switch mkl acml
    [casey@n0000 ~]$ module list
    Currently Loaded Modulefiles:
      1) intel/2013.5.192   2) acml/5.3.1-intel

    [casey@n0000 ~]$ module show mkl
    -------------------------------------------------------------------
    /global/software/sl-6.x86_64/modfiles/intel/2013.5.192/mkl/2013.5.192:

    module-whatis   This module sets up MKL 2013.5.192 in your environment.
    setenv                MKL_DIR /global/software/sl-6.x86_64/modules/langs/intel/2013.5.192/mkl
    prepend-path     CPATH /global/software/sl-6.x86_64/modules/langs/intel/2013.5.192/mkl/include
    prepend-path     CPATH /global/software/sl-6.x86_64/modules/langs/intel/2013.5.192/mkl/include/fftw
    prepend-path     FPATH /global/software/sl-6.x86_64/modules/langs/intel/2013.5.192/mkl/include
    prepend-path     FPATH /global/software/sl-6.x86_64/modules/langs/intel/2013.5.192/mkl/include/fftw
    prepend-path     INCLUDE /global/software/sl-6.x86_64/modules/langs/intel/2013.5.192/mkl/include
    prepend-path     INCLUDE /global/software/sl-6.x86_64/modules/langs/intel/2013.5.192/mkl/include/fftw
    prepend-path     LD_LIBRARY_PATH /global/software/sl-6.x86_64/modules/langs/intel/2013.5.192/mkl/lib/intel64
    prepend-path     LIBRARY_PATH /global/software/sl-6.x86_64/modules/langs/intel/2013.5.192/mkl/lib/intel64
    prepend-path     MANPATH /global/software/sl-6.x86_64/modules/langs/intel/2013.5.192/man/en_US
    -------------------------------------------------------------------

    [casey@n0000 ~]$ module whatis mkl
    mkl                  : This module sets up MKL 2013.5.192 in your environment.

    [casey@n0000 ~]$ module purge  
    [casey@n0000 ~]$ module list
    No Modulefiles Currently Loaded.

    [casey@n0000 ~]$ module avail

    ---- /global/software/sl-6.x86_64/modfiles/tools ----
    cmake/2.8.11.2  gnuplot/4.6.0  octave/3.4.3  paraview/3.12.0  r/3.0.1  texlive/2013

    ---- /global/software/sl-6.x86_64/modfiles/langs ----
    gcc/4.4.7  intel/2013.5.192  intel/2013_sp1.2.144  pgi/13.10  python/2.6.6
    ...

    [casey@n0000 ~]$ module load python
    [casey@n0000 ~]$ module avail

    ---- /global/software/sl-6.x86_64/modfiles/tools ----
    cmake/2.8.11.2  gnuplot/4.6.0  octave/3.4.3  paraview/3.12.0  r/3.0.1  texlive/2013

    ---- /global/software/sl-6.x86_64/modfiles/langs ----
    gcc/4.4.7  intel/2013.5.192  intel/2013_sp1.2.144  pgi/13.10  python/2.6.6

    ---- /global/software/sl-6.x86_64/modfiles/python/2.6.6 ----
    ipython/0.12  matplotlib/1.1.0  numpy/1.6.1  scipy/0.10.0

...

**NOTE: Python modulefiles will become available only after the “*python*” modulefile is loaded. The same is the case for R packages, libraries for C compilers, etc.: they will only become available after their respective parent modules are loaded.**  
 

### [3. Software Provided on Savio](){#Software_Provided} {#software-provided-on-savio}

Research IT provides and maintains a set of system level software modules. The purpose is to provide an ecosystem that most users can rely on to accomplish their research and studies. The range of applications and libraries that Research IT supports highly depend on the use case and the frequency of how often a support request is received.

For a detailed and up-to-date list of software provided on the cluster, run the module avail command, as described in [the usage examples above](#Examples).

(Note: if you're interested in whether a particular C library, Python module, R package, or the like is provided on the cluster, make sure that you first load the parent software itself – such as the Intel or GCC compilers, Python, or R – before checking the list of provided software, as that list is dynamically adjusted based on your current environment.)

Currently the following categories of applications and libraries are supported, with some key examples of each shown below:

-   Development Tools
-   Data processing and Visualization Tools
-   Typesetting and Publishing Tools
-   Miscellaneous Tools (examples not yet listed below)  
     

Category

Application/Library Name

Development Tools

Editor/IDE

Emacs, Vim, cmake, cscope, ctags

SCM

Subversion, Git, Mercurial

Debugger/Profiler/Tracer

GDB, gprof, Valgrind, TAU, Allinea DDT

Languages/Platforms

GCC, Intel, Perl, Python, Java, Boost, CUDA, UPC, Open MPI, PVM, TBB, MPI4Py, IPython, R, MATLAB (license required), Octave, Julia

Math Libraries

ACML, MKL, ATLAS, FFTW, FFTW3, GSL, LAPACK, ScaLAPACK, NumPy, SciPy

IO Libraries

HDF5, NetCDF, NCO, NCL

Data processing and Visualization Tools

Data Processing/Visualization

Gnuplot, Grace, Graphviz, ImageMagick, MATLAB (license required), Octave, ParaView, R, VisIt, VMD, yt, Matplotlib

Typesetting and Publishing Tools

Typesetting

TeX Live, Ghostscript, Doxygen

 

### [4. Chaining Software Modules]() {#chaining-software-modules}

Environment Modules also allow a user to optionally integrate their own application environment together with the system-provided application environment, by allowing different categories of modulefiles to be chained together. This provides a common interface for simplicity, while still maintaining diversity and flexibility:

-   The first category of the modulefiles are provided and maintained by Research IT, which include the commonly used applications and libraries, such as compilers, math libraries, I/O libraries, data processing and visualization tools, etc. We use a hierarchical structure to maintain the cleanness without losing the flexibility of it.  
     
-   The second category of the modulefiles are automatically chained for the group of users who belong to the same group on the cluster, if the modulefiles exist in the designated directory. This allows the same group of users to share some of the common applications that they use for collaboration and saves spaces. Normally the user group maintains these modulefiles. But Research IT can also provide assistance under support agreement and on a per request basis.  
     
-   The third category of the modulefiles can also be chained on demand by a user if the user chooses to use Environment Modules to manage user specific applications as well. To do that, user needs to append the location of the modulefiles to the environment variable *MODULEPATH*. This can be done in one of the following ways:

    1). For bash users, please add the following to ~/.bashrc:

        export MODULEPATH=$MODULEPATH:/location/to/my/modulefiles

    2). For csh/tcsh users, please add the following to ~/.cshrc:

        setenv MODULEPATH "$MODULEPATH":/location/to/my/modulefiles

### [5. Installing Your Own]() {#installing-your-own}

In addition to the software provided on the Savio cluster, you are most welcome to install your own software.

First, before installing your own software, be sure to check whether [it may already be provided on the cluster](#Software_Provided).

Second, there are some important considerations of which to be aware when installing your own software on the cluster. Software you install will need to:

-   Run on Scientific Linux 6 (i.e. essentially Red Hat Enterprise Linux 6).
-   Run in command line mode, or - if remote, graphical access is required - provide such access via X Windows (X11).
-   Be capable of installation without <span class="il">root</span>/sudo privileges. (This might sometimes require adding command line options to installation commands or changing values in installation-related configuration files, for instance; see your vendor- or community-provided documentation for instructions.)
-   Be capable of installation in the storage space you have available. (For instance, installable within your 10 GB space provided for your home directory.)
-   If compiled from source, be capable of being built using the compiler suites on Savio, or via user-installed compilers.
-   Be capable of running without the requirement to install <span class="il">database software</span> directly on Savio. (Externally hosted <span class="il">databases</span> are OK.)
-   If commercial or otherwise license-restricted, come with a license that permits cluster usage (multi-core and potentially, multi-node), as well as a license enforcement mechanism (if any) that's compatible with the Savio environment.

As well, if your software has installation dependencies – such as libraries, interfaces, or modules – you can save time and trouble by [checking first whether they are already provided on the cluster](#Software_Provided) before installing them yourself. (Make sure that you've first loaded the relevant compiler, interpreted language, or application before examining the list of provided software, because that list is dynamically adjusted based on your current environment.)

If you have any questions about installing your software on Savio, whether before or during installation, please write us at <brc-hpc-help@berkeley.edu>. Be sure to let us know of any pertinent information regarding the software you're installing, such as URL(s) for its installation guide, list of dependencies, and the like.

 
