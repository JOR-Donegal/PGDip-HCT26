# Week 4
The most common Authentication, Authorization and Accounting (AAA) infrastructure we find in modern enterprise and data centres is Microsoft's _Active Directory_ (AD). It's useful for centralizing information in an SME, but it's essential for any infrastructure that needs to scale. Once the site goes beyond a trivial size, its security information becomes unmanageable unless we centralize it. This week we are going to work on some of the theory and terminology behind having a local AD infrastructure.

In practical exercises this week, build the core services for a basic SME site using Active Directory. This should have two domain controllers, each having redundant AD, DNS, DHCP. One of the controllers should be set to synchronize time to a source of NTP. Plan the site as if it has no Internet connectivity.

## Study
1. Read through my theory material on [Active Directory](https://johnoraw.gitbook.io/active-directory-1/)

## Practical Work
2. Build Authentication, Authorization and Accounting (AAA) infrastructure for an SME site, the walkthrough at this [link](https://jor-donegal.github.io/AAA-SME26/) was updated to Windows Server 2025.

## Later study
As public cloud emerged and became a viable platform for core services, many of us moved one of our domain controllers to public cloud. From a contingency and disaster recovery perspective, this was perfect; assuming you were confident about security. 

This developed into pure cloud-based applications, like _Azure Active Directory_. In previous notes, I have used the acronym _Authentication, Authorization, and Accounting_ (AAA). You will also come across _Identity and Access Management_ (IAM) used to describe these systems. 

Due to the pace of change in public cloud, I do not write notes for these topics, I point you in the direction and get you to do some background study. As a point in case, Azure Active Directory is now called _Entra ID_!

In your own time, do some background reading and after completion of the taught modules, use your Azure subscription to evaluate this.
