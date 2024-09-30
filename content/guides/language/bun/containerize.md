---
title: Containerize a Bun application
linkTitle: Containerize your app
weight: 10
keywords: bun, containerize, initialize
description: Learn how to containerize a Bun application.
aliases:
  - /language/bun/containerize/
---

## Prerequisites

* You have a [Git client](https://git-scm.com/downloads). The examples in this section use a command-line based Git client, but you can use any client.

## Overview

This section walks you through containerizing and running a Bun application.

## Get the sample application

Clone the sample application to use with this guide. Open a terminal, change directory to a directory that you want to work in, and run the following command to clone the repository:

```console
$ git clone https://github.com/Pradumnasaraf/bun-docker.git
```

You should now have the following contents in your `bun-docker`
directory.

```text
├── bun-docker/
│ ├── compose.yml
│ ├── Dockerfile
│ ├── LICENSE
│ ├── server.js
│ └── README.md
```

In the Dockerfile if you look closely, you will see in `FROM` instruction, we are using `oven/bun` as the base image instead of `bun`. This is because the official DOCKER image for Bun is not available yet, unlike Node. So, we are using the `oven/bun` image which is a custom image created by the company itself. This image is available on the Docker Hub. You can find the image [here](https://hub.docker.com/r/oven/bun).

```dockerfile
# Use the Bun image as the base image
FROM oven/bun:latest

# Set the working directory in the container
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . .

# Expose the port on which the API will listen
EXPOSE 3000

# Run the server when the container launches
CMD ["bun", "server.js"]
```

To give you a brief overview of Dockerfile apart from the `FROM` instruction, we are setting the working directory in the container to `/app`, copying the contents of the current directory to the `/app` directory in the container, exposing the port 3000, so that the API can be accessed from outside the container, and finally running the server when the container launches.

To learn more about the files in the repository, see the following:
 - [Dockerfile](/reference/dockerfile.md)
 - [.dockerignore](/reference/dockerfile.md#dockerignore-file)
 - [compose.yml](/reference/compose-file/_index.md)

## Run the application

Inside the `bun-docker` directory, run the following command in a
terminal.

```console
$ docker compose up --build
```

Open a browser and view the application at [http://localhost:3000](http://localhost:3000). You will see a message `{"Status" : "OK"}` in the browser.

In the terminal, press `ctrl`+`c` to stop the application.

### Run the application in the background

You can run the application detached from the terminal by adding the `-d`
option. Inside the `bun-docker` directory, run the following command
in a terminal.

```console
$ docker compose up --build -d
```

Open a browser and view the application at [http://localhost:3000](http://localhost:3000).


In the terminal, run the following command to stop the application.

```console
$ docker compose down
```

For more information about Compose commands, see the [Compose CLI
reference](/reference/cli/docker/compose/_index.md).

## Summary

In this section, you learned how you can containerize and run your Bun
application using Docker.

Related information:
 - [Docker Compose overview](/manuals/compose/_index.md)

## Next steps

In the next section, you'll learn how you can develop your application using
containers.

{{< button text="Develop your application" url="develop.md" >}}
