---
title: Run Data API builder using a container
description: This document contains details about running Data API builder using a container.
author: anagha-todalbagi
ms.author: atodalbagi
ms.service: data-api-builder
ms.topic: run-dab-using-container
ms.date: 04/06/2023
---

# Running Data API builder for Azure Databases using a container

With Docker, you can run Data API builder using a container from `mcr.microsoft.com/azure-databases/data-api-builder`:

```sh
docker run -it -v <configuration-file>:/App/<configuration-file> -p 5000:5000 mcr.microsoft.com/azure-databases/data-api-builder:<tag> --ConfigFileName <configuration-file>
```

The proceeding command makes the following assumptions:

- Let's say you are in the directory: `C:\data-api-builder` folder
- The configuration file you want to use in the `samples` folder and is named `my-sample-dab-config.json`
- You want to use the latest release, this can be identified from the [Releases](https://github.com/Azure/data-api-builder/releases) page. For Example, If you would like to use the image with the tag `0.5.34`, run the following command:

```bash
docker run -it -v "c:\data-api-builder\samples:/App/samples" -p 5000:5000 mcr.microsoft.com/azure-databases/data-api-builder:0.5.34 --ConfigFileName ./samples/my-sample-dab-config.json
```

You may also use one of the provided 'docker-compose.yml' files, available in the `docker` folder:

```shell
docker compose -f "./docker-compose.yml" up
```

When using your own Docker compose file, make sure you update your docker-compose file to point to the configuration file you want to use.

**NOTE:**

When running a Data API builder container in Docker, you'll see that only the HTTP endpoint is mapped. If you want your Docker container to support HTTPS for local development, you'll need to provide your own SSL/TLS certificate and private key files required for SSL/TLS encryption and expose the HTTPS port. 

A reverse proxy can also be used to enforce that clients connect to your server over HTTPS to ensure that the communication channel is encrypted before forwarding the request to your container.
Some of useful reverse proxies for https implementation:

* Nginx
* Envoy,etc

