# Week 10

Containers revolutionized software development by providing a lightweight, efficient, and portable solution for packaging applications and their dependencies, running under a single operating system kernel. They are thus more lightweight than Virtual Machines (VMs). VMs can also provide isolated, independent application environments, but they have considerable overhead compared to containers. This week we will examine some container theory and practice, using Docker.

## Study

You can create containers with nothing more than a Linux instance. Linux Containers (LXC) allow you to run a full instance of the underlying system as a container. Do some [background reading](https://linuxcontainers.org/) and when you have time, play with the technology.
I could use Proxmox to host these containers and have the full management front end to work with.

Docker is probably the most popular container environment, it is based on the idea that each container is based on a reusable image and an application is made up of many containers, where each is responsible for a single component. To allow for some standardization, the [Open Container Initiative was established](https://opencontainers.org/).

## Practical Work

Practice exercises in [Docker](https://jor-donegal.github.io/Docker26/). These can be carried out on any Linux instance.

