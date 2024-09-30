---
description: Containerize and develop Bun applications using Docker.
keywords: getting started, bun
title: Bun language-specific guide
linkTitle: Bun
toc_min: 1
toc_max: 2
---

The Bun getting started guide teaches you how to create a containerized Bun application using Docker. In this guide, you'll learn how to:

> **Acknowledgment**
>
> Docker would like to thank [Pradumna Saraf](https://twitter.com/pradumna_saraf) for his contribution to this guide.

Like Node.js, Bun is a JavaScript runtime that is designed to run on the server. Bun is a comparatively lightweight runtime that is designed to be fast and efficient. Now we have a options in the JavaScript ecosystem to choose from like Node.js, Deno, and Bun.

## Why develop with Bun and Docker?

It's great to have multiple options in the JavaScript ecosystem to choose from. But as the number of runtimes increases, it becomes challenging to manage the different runtimes and their dependencies. This is where Docker comes in. Creating and destroying containers on demand is a great way to manage the different runtimes and their dependencies. Also, as it's fairly a new runtime, getting a consistent development environment for Bun can be challenging. Docker can help you set up a consistent development environment for Bun.

## What will you learn?

* Containerize and run a Bun application using Docker
* Set up a local environment to develop a Bun application using containers
* Configure a CI/CD pipeline for a containerized Bun application using GitHub Actions
* Deploy your containerized application locally to Kubernetes to test and debug your deployment

## Prerequisites

Some basic understanding of Bun and JavaScript is assumed. If you are new to the runtime, the [Bun website](https://bun.sh/) is a great place to explore. You must have familiarity with Docker concepts like containers, images, and Dockerfiles. If you are new to Docker, you can start with the [Docker basics](/get-started/docker-concepts/the-basics/what-is-a-container.md) guide.

After completing the Bun getting started modules, you should be able to containerize your own Bun application based on the examples and instructions provided in this guide.

Start by containerizing an existing Bun application.

{{< button text="Containerize a Bun app" url="containerize.md" >}}