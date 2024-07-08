---
layout: post
title: "Introduction to Kubernetes"
published: false
---

I'm a bit late to the party, but I've recently started learning Kubernetes.

I don't think anyone in tech hasn't heard about Kubernetes, but as a refresher, Kubernetes is a container orchestration tool used for maintaining a fleet of containers.

In this blog, I'll go over the essence of Kubernetes as I picked-up through the Udemy Course [Kubernetes for the Absolute Beginner](https://www.udemy.com/course/learn-kubernetes/) by _Mumshad Mannambeth_.

## What Problem is Kubernetes Solving?

The birth of containers allowed people to package-up applications and run them across different sets of environments, without worrying too much about the underlying infrastructure. For the most part, this solved the problem of: *"it works on my machine"*, i.e. developers could write some code, package it up in a Docker container and have it deployed to an environment with fundamentally no additional tweaking. 

This works for a simple CRUD application with a basic frontend, backend and DB; however, modern application demands are often more complex than this. In particular, the question became: *"how can we manage and maintain the deployment of containerized applications at scale?"*

This is where Kubernetes comes into the picture. At it's core, Kubernetes is solving the problem of container orchestration; that is deployment of containerized services, the linkages between them and the scaling of these services based on demand.

## Setting up Kubernetes Locally

If you're on a Mac, you can setup Kubernetes locally to get an understanding of it's core concepts.

**Prerequisites**

1. Have Docker installed
2. Have Homebrew package manager installed

### Installing `kubectl`

The first thing you'll have to do is install `kubectl`. This is a CLI tool used to run commands against Kubernetes clusters.

1. Run the installation command:

   ```shell
   brew install kubectl
   ```

2. Test to ensure the version you installed is up-to-date:

   ```shell
   kubectl version --client
   ```

### Installing `minikube`

minikube is local Kubernetes, intended for learning Kubernetes concepts.

1. Run the installation command:

   ```shell
   brew install minikube
   ```

2. Run Docker on your machine

3. Confirm `minikube` working by starting your cluster

   ```shell
   minikube start
   ```

## Core Concepts of Kubernetes

This section explains some of the core concepts/components of Kubernetes. At first these terms appear overwhelming, but you will see how they aren't.

### PODs

PODs are the smallest unit in Kubernetes that represent an application. On first thought, you may be inclined to think that a POD is a container; however, this isn't the case.

A POD is a wrapper for one or more containers, which contains not only working application but also some metadata.

### Nodes

A Node is a worker machine in Kubernetes, and may be either a virtual or a physical machine, depending on the cluster. Each Node is managed by the control plane.

A Node can have multiple pods, and the Kubernes control plane automatically handles scheduling the pods across Nodes in the cluster.

### ReplicaSet

A ReplicaSet is a Kubernetes resource used to maintain a specified number of identical pod replicas within a cluster.

The intention behind ReplicaSets is to provide _High Availability_ - ensuring that PODs are running at all times.

### Deployments

A Deployment represents the desired state for your application pods and ReplicaSets.

### Services

Services enable applications to connect together or to users. It is an object on the Node, which listens to a port and forwards that request to a POD.

## Kubernetes on Cloud

Kubernetes can be run on a traditional on-premise stack or in the cloud; however, it is commonly known to be used in a cloud environment.

All of the major cloud providers have a managed offering for deploying Kubernetes in the cloud. This reduces the effort required by individuals to set this up themselves; and can focus on deployment.

## Conclusion

## Further Reading

- [Introduction to Kubernetes: what problems does it solve?](https://wkrzywiec.medium.com/introduction-to-kubernetes-what-problems-does-it-solve-8a72400cfb2e)
