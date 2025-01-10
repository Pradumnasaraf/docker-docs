---
title: Containerize a Deno application
linkTitle: Containerize your app
weight: 10
keywords: deno, containerize, initialize
description: Learn how to containerize a Deno application.
aliases:
  - /language/deno/containerize/
---

## Prerequisites

* You have a [Git client](https://git-scm.com/downloads). The examples in this section use a command-line based Git client, but you can use any client.

## Overview

For a JavaScript application, Node.js has been the de-facto runtime. Recent years have seen a rise in new alternative runtimes in the ecosystem, including [Deno website](https://deno.land/). Similar to Node.js, Deno is a JavaScript runtime. Even though Deno is a new runtime, it has gained popularity due to its security features and performance improvements.

Why develop Deno applications with Docker? Having multiple runtimes to choose
from is great. But as the number of runtimes increases, it becomes challenging
to manage the different runtimes and their dependencies consistently across
environments. This is where Docker comes in. Creating and destroying containers
on demand is a great way to manage the different runtimes and their
dependencies. Also, as it's fairly a new runtime, getting a consistent
development environment for Deno can be challenging. Docker can help you set up
a consistent development environment for Deno.

## Get the sample application

Clone the sample application to use with this guide. Open a terminal, change
directory to a directory that you want to work in, and run the following
command to clone the repository:

```console
$ git clone https://github.com/Pradumnasaraf/deno-docker.git
```

You should now have the following contents in your `deno-docker` directory.

```text
├── deno-docker/
│ ├── compose.yml
│ ├── Dockerfile
│ ├── LICENSE
│ ├── server.ts
│ └── README.md
```

## Understand the sample application

The sample application is a simple Deno application that uses the Oak framework to create a simple API that returns a JSON response. The application listens on port 8000 and returns a message `{"Status" : "OK"}` when you access the application in a browser.

```typescript
// server.ts
import { Application, Router } from "https://deno.land/x/oak@v12.0.0/mod.ts";

const app = new Application();
const router = new Router();

// Define a route that returns JSON
router.get("/", (context) => {
  context.response.body = { Status: "OK" };
  context.response.type = "application/json";
});

app.use(router.routes());
app.use(router.allowedMethods());

console.log("Server running on http://localhost:8000");
await app.listen({ port: 8000 });
```

## Create a Dockerfile

In the Dockerfile, you'll notice that the `FROM` instruction uses `denoland/deno:latest`
as the base image. This is the official image for Deno. This image is [available on the Docker Hub](https://hub.docker.com/r/denoland/deno).

```dockerfile
# Use the official Deno image
FROM denoland/deno:latest

# Set the working directory
WORKDIR /app

# Copy server code into the container
COPY server.ts .

# Set permissions (optional but recommended for security)
USER deno

# Expose port 8000
EXPOSE 8000

# Run the Deno server
CMD ["run", "--allow-net", "server.ts"]
```

Aside from specifying `denoland/deno:latest` as the base image, the Dockerfile

- Sets the working directory in the container to `/app`
- Copies `server.ts` into the container.
- Sets the user to `deno` to run the application as a non-root user.
- Exposes port 8000 to allow traffic to the application.
- Runs the Deno server using the `CMD` instruction.
- The `--allow-net` flag is used to allow network access to the application. The `server.ts` file uses the Oak framework to create a simple API that listens on port 8000.

## Run the application

Make sure you are in the `deno-docker` directory. Run the following command in a terminal to build and run the application.

```console
$ docker compose up --build
```

Open a browser and view the application at [http://localhost:8000](http://localhost:8000). You will see a message `{"Status" : "OK"}` in the browser.

In the terminal, press `ctrl`+`c` to stop the application.

### Run the application in the background

You can run the application detached from the terminal by adding the `-d`
option. Inside the `bun-docker` directory, run the following command
in a terminal.

```console
$ docker compose up --build -d
```

Open a browser and view the application at [http://localhost:8000](http://localhost:8000).


In the terminal, run the following command to stop the application.

```console
$ docker compose down
```

## Summary

In this section, you learned how you can containerize and run your Bun
application using Docker.

Related information:

 - [Dockerfile reference](/reference/dockerfile.md)
 - [.dockerignore file](/reference/dockerfile.md#dockerignore-file)
 - [Docker Compose overview](/manuals/compose/_index.md)
 - [Compose file reference](/reference/compose-file/_index.md)

## Next steps

In the next section, you'll learn how you can develop your application using
containers.
