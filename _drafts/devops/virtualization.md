---
layout: post
title: "Virtualization"
category: jekyll update
---

- Bare metal server: It is also called single tenant server. The physical server host a single tenant. The OS is directly installed into the physical server. It is opposite of hypervisor server.
- Hypervisor: Hypervisor is a software the can house multiple guest OS. There is type-1 hypervisor that is installed directly into the physical server and there is type-2 hypervisor that is installed over a host operating system. Some hypervisor example are VMware’s ESXi & vSpere, Microsoft’s Hyper-V etc. KVM lets you turn linux machine into a hypervisor.

![need_update virtualization]({{ site.base_url}}/_images/virtualization.png)