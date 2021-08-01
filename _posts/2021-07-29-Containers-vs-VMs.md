---
layout: post
title: "Simple Explained: Containers and VMs"
published: false
---

I've been learning about the cloud recently and keep coming across the term virtualization. The idea of virtualization comes in two flavours: containerization and virtual machines (VMs).

Essentially, virtualization came about to solve one key problem; efficency. Before we can understand this concept, we have to take a look at the history of serving applications.

# A time before Virtualization

In the past, when a business wanted to host an application they had to procure a physical server. The business had to speculate the demand for the application upfront, before making the purchase. As such, they were likely to buy a high end server which costs a lot of money. 

Besides this, they would also incur monthly expenses like energy, workforce and licenses. After spending all this money, they might realise that only a fraction of capacity is used. However, there was no way to allocate or make use of the resources that weren't needed. This is where Virtual Machines come in.

<p align="center">
<br>
<img src="../images/containers_and_vms/server.png" />
</p>

# Virtual Machines

The industry realised that having one server per application was rigid, clunky and expensive. As such, in the late 1990s, VMware came out with a product which would solve this issue.

Virtualization, enabled by VMware would allow organisations to squeeze more from their physical servers. Essentially, this technology virtualises the hardware of the physical server allowing the emulation of multiple computers on a single device.

For example, we can divide a server's resources into 3 VMs and have a seperate application running on each VM. Each VM is isolated from the other and has the required resources to perform its given task. This enabled better hardware utilization but created a lot of overhead due to the necessary OS installation.

<!-- This means that we are virtualizing the underlying hardware allowing us to divide up our resources.

From a cloud perspective, when you spin up an instance, you are getting a VM with resources from a physical server shared amongst many other users. -->

<p align="center">
<br>
<img src="../images/containers_and_vms/vms.png" />
</p>

# Containers




In contrast, containers aim to virtualize the operating system, only containing the application and its libraries and dependencies.

Containers are small, fast, and portable because they do not include a guest OS in every instance. 

Containers allow us to make even better use of our resources as we don't have to predefine the amount of resources we will need.

From a cloud perspective, this gives us the flexibility to ship our code between different cloud providers with relative ease.

<p align="center">
<br>
<img src="../images/containers_and_vms/container.png" width="500" height="500"/>
</p>

# Final Thoughts

Both VMs and Containers have their place. In the cloud, containers are usually used on top of VMs, which if you think about it can allow you to make more effective use of an instance.

I don't believe you can say that one is better than the other but they both can be used for different cases. Containers have allowed us to make some processes more efficient.