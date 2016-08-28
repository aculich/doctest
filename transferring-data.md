This is an overview of how to transfer data to or from the Savio high
performance computing cluster at the University of California, Berkeley.

When transferring data using file transfer software, you should connect
only to Savio's Data Transfer Node, `dtn.brc.berkeley.edu`. (Note: if
you're using Globus Connect, you'll instead connect to the Globus
endpoint `ucb#brc`)

After connecting to Savio's Data Transfer Node, you can transfer files
directly into (and/or copy files directly from) your Home directory,
Group directory (if applicable), and Scratch directory on Savio.

#### Medium- to large-sized data transfers {#medium--to-large-sized-data-transfers}

When transferring a large number of files and/or large files, we
recommend you use:

-   **Globus Connect (formerly Globus Online)**: This method allows you
    to make unattended transfers which are fast and reliable. For basic
    instructions, see [Using Globus Connect with
    Savio](http://research-it.berkeley.edu/services/high-performance-computing/using-globus-connect-savio).

You can additionally use GridFTP or BBCP for this purpose ...

#### Small-sized data transfers {#small-sized-data-transfers}

When transferring a modest number of smaller-sized files, you can also
use:

-   **SFTP**: For basic instructions, see [Using SFTP with Savio via
    FileZilla](http://research-it.berkeley.edu/services/high-performance-computing/using-sftp-savio-filezilla).
-   **SCP**: For basic instructions, see [Using SCP with
    Savio](http://research-it.berkeley.edu/services/high-performance-computing/using-scp-savio).

You can additionally use protocols like FTPS and tools like Rsync for
this purpose ...

#### Transfers to/from repositories under version control {#transfers-tofrom-repositories-under-version-control}

When your code and/or data are stored in repositories under version
control, client software is available on Savio for accessing them via:

-   **Git**
-   **Mercurial**
-   **Subversion**

See [Accessing and Installing
Software](http://research-it.berkeley.edu/services/high-performance-computing/accessing-and-installing-software)
for information on finding and loading this software via Savio's
Environment Modules.

#### Transfers to/from specific systems {#transfers-tofrom-specific-systems}

-   **Box**: For basic instructions, see: [Transferring Data Between
    Savio and Your UC Berkeley Box
    account](http://research-it.berkeley.edu/services/high-performance-computing/transferring-data-between-savio-and-your-uc-berkeley-box-account).

Additional tutorials for transferring files to/from Google Drive, Amazon
Web Services (AWS) S3, and other popular data storage sites are in
planning or development. If you have any interest in working on or
testing one of these, or have suggestions for other data transfer
tutorials, please contact us at <brc-hpc-help@berkeley.edu>.
