[Overview](#Overview) | [Program Details](#Program%20Details) | [Hardware](#Hardware) | [Condo Contributors](#Condo%20Contributors) | [Faculty Perspectives](#FacultyPerspectives)

**[]()**

**Overview**

BRC manages **Savio** the new high-performance computational cluster for research computing. Designed as a turnkey computing resource, it features flexible usage and business models, and professional system administration. Unlike traditional clusters, **Savio** is a collaborative system wherein the majority of nodes are purchased and shared by the cluster users, known as *condo* owners. In addition to the participant-contributed condo nodes, BRC has a collection of *hotel* nodes which are available to condo owners and to other researchers on a rental basis. The condo and hotel configurations both contain standard two-socket nodes and the hotel configuration also features four 512GB large-memory nodes.

The model for sustaining computing resources** **is premised on faculty and principal investigators purchasing compute nodes (individual servers) from their grants or other available funds which are then added to the cluster. This allows PI-owned nodes to take advantage of the high speed Infiniband interconnect and high performance Lustre parallel filesystem storage associated with **Savio**. Operating costs for managing and housing PI-owned compute nodes are waived in exchange for letting other users make use of any idle compute cycles on the PI-owned nodes. PI owners have priority access to computing resources equivalent to those purchased with their funds, but can access more nodes for their research if needed. This provides the PI with much greater flexibility than owning a standalone cluster.\*\*\*\*\*\*[]()\*\*\*\*\*\*

\*\*\*\*\*\*Program Details\*\*\*\*\*\*

Compute node equipment is purchased and maintained based on a 5-year lifecycle. PIs owning the nodes will be notified during year 4 that the nodes will have to be upgraded before the end of year 5. If the hardware is not upgraded by the end of 5 years, the PI may donate the equipment to **Savio** or take possession of the equipment (removal of the equipment from **Savio** and transfer to another location is at the PI's expense); nodes left in the cluster after five years may be removed and disposed of at the discretion of the BRC program manager

Once a PI has decided to participate, the PI or his designate works with the HPC Services manager and IST teams to procure the desired number of compute nodes and allocate the needed storage. There is a 4-node minimum buy-in for any given compute pool  and all 4 nodes must be the same whether it be the Standard, HTC, Bigmem, or GPU nodes. GPU nodes are the most expensive; therefore, if a group has already purchased the 4-node minimum of any other type of node, they can purchase and add single GPU nodes to their Condo. Generally, procurement takes about three months from start to finish. In the interim, a test condo queue with a small allocation will be set up for the PI's users in anticipation of acquiring the new equipment. Users may submit jobs to the general queues on the cluster using their [Faculty Computing Allowance](http://research-it.berkeley.edu/services/high-performance-computing/faculty-computing-allowance). Jobs are subject to general queue limitations and guaranteed access to contributed cores is not provided until purchased nodes are provisioned.[]()

\*\*\*\*\*\*Hardware Requirements for Condo Participation (Updated March 22, 2016)\*\*\*\*\*\*

*Condo contributors are expected to purchase the compute nodes, and a 2M FDR infiniband cable for each node.*

**General and HTC Compute:** Lenovo system chassis purchased with 4 ea. NeXtScale nx360m5 compute nodes.

**GPU Compute**: Finetec Computer Supermicro 1U node.

General Computing Node

Processors

Dual-socket, 12-core, 2.3GHz Intel Haswell Xeon E5-2670v3 processors (24 cores/node)

Memory

64GB (8 X 8GB) 2133Mhz DDR4 RDIMMs

Interconnect

56Gb/s Mellanox ConnectX3 FDR-14 Infiniband interconnect

Hard Drive

500GB 7.2K RPM SATA HDD (Local swap and log files)

Warranty

5 yrs

Big Memory Computing Node (128 GB RAM)

Processors

Dual-socket, 12-core, 2.3GHz Intel Haswell Xeon E5-2670v3 processors (24 cores/node)

Memory

128GB (8 X 16GB) 2133Mhz DDR4 RDIMMs

Interconnect

56Gb/s Mellanox ConnectX3 FDR-14 Infiniband interconnect

Hard Drive

500GB 7.2K RPM SATA HDD (Local swap and log files)

Warranty

5 yrs

Serial HTC Computing Node

Processors

Dual-socket, 6-core, 3.4GHz Haswell Xeon E5-2643v3 processors (12 cores/node)

Memory

128GB (8 X 16GB) 2133Mhz DDR4 RDIMMs

Interconnect

56Gb/s Mellanox ConnectX3 FDR-14 Infiniband interconnect

Hard Drive

500GB 7.2K RPM SATA HDD (Local swap and log files)

Warranty

5 yrs

GPU Computing Node

Processors

Dual-socket, 4-core, 3.0GHz Haswell Xeon E5-2623v3 processors (8 cores/node)

Memory

64GB (4 X 16GB) 1866Mhz DDR4 RDIMMs

Interconnect

56Gb/s Mellanox ConnectX3 FDR-14 Infiniband interconnect

GPU

2 ea. Nvidia Tesla K80 accelerator boards

Hard Drive

500GB 10K RPM SATA HDD (Local swap and log files)

Warranty

5 yrs

**Network:** Mellanox FDR-14 36-port unmanaged leaf switch is used for every 24 ea. compute nodes.

**Storage:** All institutional and condo users have a 10GB home directory with backups on IST's shared HPC storage infrastructure. Users or projects needing more space for persistent data can purchase additional performance tier storage from IST at the current [rate](https://ist.berkeley.edu/services/is/san) (as of Mar 2014: $0.14/GB plus $0.14/GB for backups). This eliminates the need for PIs to invest in initial purchase of storage hardware. More importantly, this eliminates the issues of having to replace older storage hardware as equipment either fails or is no longer supported by the vendor. 

**Hardware Purchasing**: Prospective condo owners should [contact HPC Services Manager Gary Jung](mailto:gmjung@berkeley.edu?subject=Inquiry%20regarding%20BRC%20Condo%20participation) for current pricing and prior to purchasing any equipment to insure compatibility. BRC will assist with entering a compute node purchase requisition on behalf of UC Berkeley faculty.

**Software**:  Prospective Condo owners should review the software section under [System Overview](http://research-it.berkeley.edu/services/high-performance-computing/system-overview) to confirm that their applications are compatible with Savio's operating system, job scheduler and operating environment.

**[]()Charter Condo Contributers**

[Eliot Quataert](http://astro.berkeley.edu/faculty-profile/eliot-quataert), Theoretical Astrophysics Center, Berkeley Astronomy Department  
[Eugene Chiang](http://astro.berkeley.edu/faculty-profile/eugene-chiang), Berkeley Astronomy Department  
[Chris McKee](http://astro.berkeley.edu/faculty-profile/chris-mckee), Berkeley Astronomy Department  
[Richard Klein](http://astro.berkeley.edu/faculty-profile/richard-klein), Berkeley Astronomy Department  
[Uros Seljak](http://physics.berkeley.edu/?textonly=0&option=com_dept_management&Itemid=312&task=view&id=3319), Physics Department  
[Jon Arons](http://astro.berkeley.edu/faculty-profile/jon-arons), Berkeley Astronomy Department  
[Ron Cohen](http://chem.berkeley.edu/faculty/cohen/index.php), Department of Chemistry, Department of Earth and Planetary Science  
[John Chiang](http://climate.geog.berkeley.edu/~jchiang/Lab/Home.html), Department of Geography and Berkeley Atmospheric Sciences Center  
[Fotini Katopodes Chow](http://www.ce.berkeley.edu/people/faculty/Chow?destination=people%2Ffaculty%2FChow), Department of Civil and Environmental Engineering  
[Jasmina Vujic](http://www.nuc.berkeley.edu/people/jasmina_vujic), Department of Nuclear Engineering  
[Jasjeet Sekhon](http://sekhon.berkeley.edu/), Department of Political Science and Statistics  
[Rachel Slaybaugh](http://www.nuc.berkeley.edu/people/rachel-slaybaugh), Nuclear Engineering  
[Massimiliano Fratoni](http://www.nuc.berkeley.edu/people/massimiliano_fratoni), Nuclear Engineering  
[Hiroshi Nikaido,](http://mcb.berkeley.edu/faculty/all/nikaidoh) Molecular and Cell Biology  
[Donna Hendrix,](http://qb3.berkeley.edu/administration/) Computation Genomics Research Lab  
[Justin McCrary,](http://dlab.berkeley.edu/people/justin-mccrary-faculty-director) Director D-Lab  
[Alan Hubbard,](http://hubbard.berkeley.edu/) Professor and Head of Biostatistics Division, School of Public Health  
[Mark van der Laan,](https://www.stat.berkeley.edu/~laan/) Professor of Biostatistics and Statistics, School of Public Health  
[Michael Manga,](http://seismo.berkeley.edu/~manga/) Department of Earth and Planetary Sciences  
[Jeff Neaton](http://physics.berkeley.edu/people/faculty/jeffrey-neaton), Physics  
[Eric Neuscamman](http://chemistry.berkeley.edu/faculty/chem/neuscamman), College of Chemistry  
[M. Alam Reza](http://www.me.berkeley.edu/people/faculty/m-reza-alam), Mechanical Engineering  
[Elaine Tseng](http://profiles.ucsf.edu/elaine.tseng), UCSF School of Medicine  
[Julius Guccione](http://www.surgery.ucsf.edu/faculty/adult-cardiothoracic-surgery/julius-m-guccione,-jr,-phd.aspx), UCSF Department of Surgery  
[Ryan Lovett](http://statistics.berkeley.edu/ryan-lovett), Statistical Computing Facility  
[ ]()

**Faculty Perspectives**

**UC Berkeley Professor of Astrophysics Eliot Quataert** speaks at the BRC Program Launch (22 May 2014) on the need for local high performance computing (HPC) clusters, distinct from national resources such as NSF, DOE (NERSC), and NASA.

 

**UC Berkeley Professor of Integrated Biology Rasmus Nielsen** speaks at the BRC Progam Launch (22 May 2014) about the transformative effect of using HPC in genomics research.

 

 
