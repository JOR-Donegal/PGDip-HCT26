# High Performance Computing

Since the syllabus was last updated, artificial intelligence and machine learning have become a huge component of modern data centres. I want to discuss briefly how we approach building HPC clusters. This is not intended to be exhaustive but describes the kind of work we've done in this area in the past five years using NVidia GPUs. Many years ago, we played with [Beowulf Clusters]( https://beowulf.org/overview/faq.html) and many of the concepts are still valid.

## Facilities
You already know from discussions in the popular press that artificial intelligent workloads take a lot of power! Just as a rough guide, I have one cluster with three fairly beefy servers! Lots of DRAM, lots of CPU, and four N100 GPUs. When operating fully under load, this cluster uses c. 4kW. This is probably the smallest HPC cluster we will ever build!
Remember our basic rules update to centre design.

1. I'm using two 6 kW UPS on two separate power lines, a typical A+B power supply arrangement.
2. I need two 32A single phase sockets to power these UPS.
3. My peak load to the UPS will only ever be (6000/230) c. 26A overall but the equipment load will be 17A.
4. I will need air conditioning to allow for c. 4kW plus headroom.

All the above are ballpark estimates and it is important to have headroom. I will provision any system to 60% only if possible, this may entail customer debate! I also use simplest cases here. In earlier notes I discuss power factor, I only buy equipment with PF=1.

## Overview

A starting point should be; what is it you want to do?

Nvidia natively uses Cuda and C/C++. This may be inaccessible to anyone who is not a computer scientist. 
In scientific computing, most of us will use [Conda]( https://docs.conda.io/projects/conda/en/latest/user-guide/getting-started.html) to write code in Python. There is an expectation that nobody will use elevated privileges normal work. We recommend users create virtual environments in Conda to allow them to have full control of dependencies.

## Cluster Environment

A typical architecture will have a __Head Node__ with a complex configuration but no GPU. Other nodes in the cluster are referred to as __Worker Nodes__. They are provisioned from the Head Node using PXEboot and are not normally accessed separately. Some sort of cluster management software may be used and we use [Bright]( https://developer.nvidia.com/bright-cluster-manager). One advantage of this architecture is that head nodes can be added as required, where the cluster must be scaled up.

## Users

If you have more than a handful of users, the environment becomes more complex. My own preference is to create users in Active Directory, and use that as my back end for all services. Administrators have a local Linux account on the head node, with privileges assigns manually. Ordinary users login with only normal user privileges. It is important to tightly control Linux user and group ID, we will need this later to integrate with an NFS file share. 

## File Share

When we built shared multiuser Linux systems, we want to keep the root file system clean and tidy. Users have a home folder and that's where most of the trouble will arise. I'm normally going to create a separate storage facility, typically using NFS on a SAN or NAS. This will mount automatically when the user logs in, and any user will only have access to their own share. It is important to either enforce quotes or too closely police user storage. In NFS we track users based on user ID. On large projects we might want to have group folders, and we could track those based on group IDs. This sounds complicated, but it's a fairly standard setup on multiuser Linux systems.

## Job Scheduling

It's hard to believe, but the largest systems I've built look like old fashioned batch processing from the 1950s. The normal workflow would be to write my code in a Conda virtual environment with my data on the NFS share. After testing, I write a script file with parameters for the job. How much CPU do I need? How many GPU's? Are there any other critical parameters? And what Conda script do I want to run?
When all of this looks about right, I submit the script to the batch processing system. On systems we're using at present, we use the [Slurm Workload Manager]( https://slurm.schedmd.com/overview.html). As an ordinary user you can control the tasks you have submitted. As an administrator I can be prioritise work, or bump jobs from the task queue.
