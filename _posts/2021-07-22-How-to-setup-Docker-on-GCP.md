---
layout: post
title: How to setup Docker on a GCP VM?
published: true
---

Recently, I decided to learn about Docker and how it can be used to run applications. Discovering this has since opened up my mind how we can make best use of our hardware's capacity.

In this tutorial, I will walkthrough the steps of getting Docker setup on a GCE instance on Google Cloud. By the end of this tutorial, you should have a VM setup with Docker installed to run your containerized applications.

Before you get started, this tutorial assumes you have a Google Cloud account and a project already setup.

# Step 0

## Log onto the GCP console and navigate to Compute Engine

# Step 1

## Create a VM instance

Once you've navigated to Compute Engine, click on the 'CREATE INSTANCE' button on the top.

# Step 3

## SSH into the instance

# Step 4

## Make sure you have no versions of Docker installed

```bash
$ sudo apt-get remove docker docker-engine docker.io containerd runc
```

# Step 6








