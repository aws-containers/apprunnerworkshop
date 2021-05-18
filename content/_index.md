---
title: 'AWS App Runner Workshop'
chapter: true
weight: 1
---

# AWS App Runner Workshop

![aws app runner](/images/app-runner.png)

AWS App Runner is a new service that provides customers with a fast, simple, and secure way to deploy applications on AWS without managing any infrastructure. Customers simply provide their source code or container image and App Runner will automatically build and deploy the application, load balance network traffic, automatically scale up or down based on demand, monitor health of the application, and deliver encryption.

In this workshop, we will launch a simple Node.js web service using GitHub, switch this to using a Dockerfile, and finally add a database for querying.

### Prerequisites

This workshop will require:

- A [GitHub account](https://github.com/join) on which you can create a repository
- [Docker Deskop](https://www.docker.com/products/docker-desktop) running on your own computer
- An AWS account with console access
