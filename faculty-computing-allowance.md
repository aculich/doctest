#### Download the [Faculty Computing Allowance info packet](http://research-it.berkeley.edu/sites/default/files/FCA%20Bundle.pdf). {#download-thefaculty-computing-allowance-info-packet.}

Faculty and PIs wanting to obtain access to Savio for their research
will need to complete the [Requirements
Survey](https://docs.google.com/a/berkeley.edu/forms/d/1rkWi5Og2zqb6Af47djQhtWcpHnd4Cz6li8OfJF4ww8M/viewform) and
include a list of anticipated users as indicated on the form. A
 Savio cluster specific project will be setup using a unique name and
all user accounts will be created under this unique project name. The
project name will also be used to setup (SLURM) scheduler accounts using
which we can enforce allowances, monitor and report cluster usage. Any
UCB researcher who wants to open Savio cluster account associated with
an existing Savio cluster project (or the Savio scheduler account name)
can request by submitting the [Additional User Account Request
Form](https://docs.google.com/a/berkeley.edu/forms/d/1byVN8FjyWSvkDYMvzs6SJM5JFfrK37za50exRSWnCls/viewform).

Accounts are added upon approval of the faculty or PI for the project.
Usernames must be unique and are allocated on a first-come, first served
basis meaning that users may have to choose an alternate username for
their accounts if the one that that originally want has been taken.  For
security reasons, access to Savio will be through the use of two-factor
authentication using Google Authenticator one-time password tokens. This
greatly reduces the risk of a security compromise due to stolen user
credentials.

**Allocations:** There are two different kinds of allocations that
provide compute time on the Savio cluster. Faculty and PIs can request
access to the cluster under either or both of these:

-   **Faculty Computing Allowance**:  This is a new pilot program,
    sponsored jointly by the VCR and CIO, to provide up to 200K [Service
    Units (SUs)](http://research-it.berkeley.edu/services/high-performance-computing/service-units-savio)
    of free compute time per academic year to all qualified UC
    Berkeley faculty/PIs. PIs will go through the standard process of
    applying for access and they can receive an Allowance upon request
    that can be used by their research group. PIs can also pool their
    Allowances if their groups are working together; however, this must
    be specified when the Allowance is initially setup or during the
    annual renewal period. Savio cluster project names for these
    allocations start with a ‘fc\_’ prefix, for example fc\_projectname.
     As mentioned there will be a 200K SU limit enforced on these
    projects where one SU is equivalent to one compute cycle on the
    latest standard hardware. People needing more compute time beyond
    their Allowance should email brc-hpc-help@berkeley.edu to inquire
    about setting up an MOU. Please note that Allowances can be shared
    but are not transferable.
-   **Condo Allocation**: This category of allocation is available to
    Faculty and PIs that purchase standard compute nodes to be added to
    the Savio cluster. The basic premise of Condo Computing is that PIs
    receive free cluster support for their contributed hardware and, in
    exchange, the institution has access to their excess cycles. The
    advantages of this model for PIs are no ongoing support costs; and
    that they can determine and set the scheduler limits on their
    Condo QoS (Quality of Service) according to their needs.
    Savio cluster project names for these allocations start with a
    ‘co\_’ prefix, for example co\_condoname and when users submit jobs
    with this project their jobs get the additional priority boost as
    Condo jobs. There will not be any limit on the compute cycles but a
    limit on the number of nodes available to these projects at any
    given time based on the number of nodes contributed by the Condo.

**Renewing Your Faculty Computing Allowance**

Each year, beginning in May, you can submit an application to renew your
Faculty Computing Allowance.

Renewal applications submitted in May will be processed beginning June
1st. Those submitted and approved later in the year, after May/June,
will receive pro-rated allowances of computing time.

**Viewing the Usage of Your Allowance**

You can view how many Service Units have been used to date under a
Faculty Computing Allowance, or by a particular user account on Savio,
via the [check\_usage.sh
script](http://research-it.berkeley.edu/services/high-performance-computing/tips-using-brc-savio-cluster#q-how-to-check-my-fca-usage-){.toc-filter-processed}.

**Charges for Running Jobs**

Each time a computational job is run on the cluster under a Faculty
Computing Allowance account, charges are incurred against that account,
using abstract measurement units called [Service Units
(SUs)](http://research-it.berkeley.edu/services/high-performance-computing/service-units-savio).
Please see [Service Units on
Savio](http://research-it.berkeley.edu/services/high-performance-computing/service-units-savio)
to learn more about how these charges are calculated.

**Getting More Compute Time When Your Allowance Is Used Up**

Have you exhausted your entire Faculty Computing Allowance? There are a
number of [options for getting more computing time for your
project](http://research-it.berkeley.edu/services/high-performance-computing/options-when-faculty-computing-allowance-exhausted).

**Acknowledgements**  
Please acknowledge Savio in your publications. (Such acknowledgements
are an important factor in helping to justify ongoing funding for, and
expansion of, the cluster.) A sample statement is:  
  
*"This research used the Savio computational cluster resource provided
by the Berkeley Research Computing program at the University of
California, Berkeley (supported by the UC Berkeley Chancellor, Vice
Chancellor for Research, and Chief Information Officer)."*

As well, we encourage you to [tell us how BRC impacts your
research](https://docs.google.com/a/berkeley.edu/forms/d/e/1FAIpQLSdqhh2A77-l8N3eOcOzrH508UKfhIvPn8h5gLDUJ9XrRLvA5Q/viewform) (Google
Form), at any time!
