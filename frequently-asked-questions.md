\[TOC\]

General FAQs {#general-faqs}
------------

### Q. How can I access the Faculty Computing Allowance application (Requirements Survey) and Additional User Request forms? I'm seeing a "You need permission" error. {#q.-how-can-i-access-the-faculty-computing-allowance-application-requirements-survey-and-additional-user-request-forms-im-seeing-a-you-need-permission-error.}

A. Starting in late March 2016, you will now need to [authenticate via CalNet](https://calnetweb.berkeley.edu/calnet-me) to access the online forms for applying for a Faculty Computing Allowance, and for requesting additional user accounts on the Savio cluster.  
  
When accessing either form, you may encounter the error message, "You need permission. This form can only be viewed by users in the owner's organization", under either of these circumstances:

<span colspan="2"><span style="word-wrap:break-word;display:block">1. If you haven't already successfully logged in via CalNet. (If you don't have a CalNet ID, please work with a UCB faculty member or other researcher who can access the form on your behalf.)</span></span>2. If you've logged in via CalNet, but you're also simultaneously connected, in your browser, to a non-UCB Google account; for instance, to access a personal Gmail account. (If so, the easiest way to access the online forms might be to use a second browser on your computer, one in which you aren't already logged into a Google account. As an alternative, you can log out of both accounts in your primary browser, before accessing these forms.)

### Q. Can I get root access to my compute nodes? {#q.-can-i-get-root-access-to-my-compute-nodes}

A. Unfortunately, that is not possible. All the compute nodes download the same operating system image from the master node and load the image into RAM disk, so changes to the operating system on the compute node would not be persistent.

### Q. Do you allow users to NFS mount their own storage onto the compute nodes? {#q.-do-you-allow-users-to-nfs-mount-their-own-storage-onto-the-compute-nodes}

A. No. We NFS mount storage across all compute nodes so that data is available independent of which compute nodes are used; however, medium to large clusters can place a very high load on NFS storage servers and many, including Linux-based NFS servers, cannot handle this load and will lock up. A non-responding NFS mount can hang the entire cluster, so we can't risk allowing outside mounts.

### Q. How can I acknowledge the Savio Cluster in my presentations or publications? {#q.-how-can-i-acknowledge-the-saviocluster-in-my-presentations-or-publications}

A. You can use the following sentence in order to acknowledge computational and storage services associated with the Savio Cluster:

> *"This research used the Savio computational cluster resource provided by the Berkeley Research Computing program at the University of California, Berkeley (supported by the UC Berkeley Chancellor, Vice Chancellor for Research, and Chief Information Officer)."*

Acknowledgements of this type are an important factor in helping to justify ongoing funding for, and expansion of, the cluster. As well, we encourage you to [tell us how BRC impacts your research](https://docs.google.com/a/berkeley.edu/forms/d/e/1FAIpQLSdqhh2A77-l8N3eOcOzrH508UKfhIvPn8h5gLDUJ9XrRLvA5Q/viewform) (Google Form), at any time!

Condo Cluster Computing Program FAQs {#condo-cluster-computing-program-faqs}
------------------------------------

### Q. What are the benefits of participating in the Condo cluster program? {#q.-what-are-the-benefits-of-participating-in-the-condo-cluster-program}

A. A major incentive for researchers to participate is that they only have to purchase their compute nodes, and support of the compute nodes is provided for free in exchange for their unused compute cycles. In addition to receiving professional systems administration support, researchers will be able to leverage the use of the HPC infrastructure (firewalled subnet, login nodes, commercial compiler, parallel filesystem, etc.) when they use their compute nodes. This infrastructure is provided for free and saves researchers from having to purchase and create any of these components on their own.

### Q. What are the support costs for participating in the Condo program? {#q.-what-are-the-support-costs-for-participating-in-the-condo-program}

A. The monthly cluster support, colocation and network fees are waived for researchers who buy into the Condo. Essentially, the institution waives those costs in exchange for excess compute cycles. Each user of the system receives a 10GB storage allocation which includes backups, and use of the shared parallel scratch filesystem is at no cost. Users needing more storage for persistent data can purchase additional allocations at current [rates](https://ist.berkeley.edu/services/is/san).

### Q. How do I purchase compute nodes for the Condo program? {#q.-how-do-i-purchase-compute-nodes-for-the-condo-program}

A. Contact [HPC Services manager Gary Jung](mailto:gmjung@berkeley.edu?subject=Inquiry%20regarding%20BRC%20Condo%20participation). Our team will work with you to understand your application and to determine if the Condo cluster would be a suitable platform. We will provide an estimate of the costs of the compute node and associated infiniband network equipment and then work with your Procurement buyer to specify the correct items to order. Participants are expected to contribute the compute node, infiniband cable, and infiniband switch (or cover the cost of a fraction of a switch).

### Q. How do I get access to my nodes? {#q.-how-do-i-get-access-to-my-nodes}

A. We will set up a floating reservation equivalent to the number of nodes that you contribute to the Condo to provide priority access to you and your users. You can determine the run time limits for your reservation. If you are not using your reservation, then other users will be allowed to run jobs on unused nodes. If you submit a job to run when all nodes are busy, your job will be given priority over all other waiting jobs to run, but your job will have to wait until nodes become free in order to run. We do not do pre-emptive scheduling where running jobs are killed in order to give immediate access to priority jobs.

### Q. I need dedicated or immediate access to my nodes. Can you accommodate that? {#q.-i-need-dedicated-or-immediate-access-to-my-nodes.-can-you-accommodate-that}

A. The basic premise of Condo participation is to facilitate the sharing of unused resources. Dedicating or reserving compute resources works counter to sharing, so this is not possible in the Condo model. As an alternative, PIs can purchase nodes and set them up as a Private Pool in the Condo environment, which will allow a researcher to tailor the access and job queues to meet their specific needs. Private Pool compute nodes will share the HPC infrastructure along with the Condo cluster; however, researchers will have to cover the support costs for BRC staff to manage their compute nodes. Rates for Private Pool compute nodes will be determined at a later date.

### Q. How do I "burst" onto more nodes? {#q.-how-do-i-burst-onto-more-nodes}

A. There are two ways to do this. First, Condo users can access more nodes via Savio's preemptable, [low-priority quality of service option](http://research-it.berkeley.edu/services/high-performance-computing/user-guide#Low_Priority){.toc-filter-processed}. Second, faculty can obtain a [Faculty Computing Allowance](http://research-it.berkeley.edu/services/high-performance-computing/faculty-computing-allowance), and their users can then submit jobs to the General queues to run on the compute nodes provided by the institution. (Use of these nodes is subject to the current job queue policies for general institutional access.)
