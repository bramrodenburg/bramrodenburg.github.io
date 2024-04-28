---
layout: post
title:  "Building a K8s Clone!"
date:   2024-04-28 14:15:15 +0200
categories: [go, k8s]
---

I am a person that likes to learn by doing. In this case, I want to learn [Go](https://go.dev) and more on distributed systems. So I decided to build a [Kubernetes (K8s)](https://kubernetes.io/) clone. Well not really a clone; more a **very, very, simplified** version of it.

What I hope to have in the end is a piece of software that runs workloads across multiple machines. These workloads will be Docker containers. A user can submit these workloads either from the command line or a web interface. The software should figure out the best way to run these workloads across the machines, do monitoring and potentially rerun them if they fail.

I haven't really yet read up on any literature on distrubted orchestrators, but on a high-level this is what I currently have in mind:

### High-level architecture

![High-level architecture](/assets/high-level-architecture.svg)

**Manager**: 
The manager \[1\] runs workloads submitted by users. It schedules these workloads across the cluster and monitors them.

**Worker**: 
The worker accepts workloads from the manager and then schedules and runs them on the node the worker is running on.

**Task**:
A task \[2\] represents one or more Docker containers that should run together on a node.

**Web GUI**:
A web user interface that users can interact with. Users will be able to submit workloads and monitor the status of the cluster and corresponding workloads.

**Console**:
Similar to the Web GUI, but then a command line interface.

### Learning Go

I already played around with Go in the past. I have the book [The Go Programming Language](https://www.gopl.io/) at home, though I actually prefer the online book [Learn Go with tests](https://quii.gitbook.io/learn-go-with-tests). I guess that has to do with the fact I prefer learning by doing.

While writing the code for this project, I want to try doing that using test driven development (TDD). Basically meaning that I will:
1. Write a failing test and see it fail.
2. Write the smallest amount of code required to make the tests pass.
3. Refactor and repeat.

### A few words before ending this post

Before ending this post, I should mention that my inspiration for doing this comes from Juraj Majerik and Tim Boring. Juraj wrote a series of blog posts on [builing an Uber clone](https://jurajmajerik.com/blog/start-here/), and Tim actually wrote a book called [Build an Orchestrator in Go (from Scratch)](https://www.manning.com/books/build-an-orchestrator-in-go-from-scratch). Oh and I actually became of a father of twins this year, so lets see how much time I will be able to spend on this project :-)

### Notes

\[1\]: Kubernetes separates this into an API server, a manager and a scheduler. I'm not clear yet what all the responsibilities of the manager will be, so I might actually split the manager component later on, once I have put more thought into it.

\[2\]: What I call a task is basically a pod on Kubernetes.

