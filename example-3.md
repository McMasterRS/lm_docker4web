---
layout: default
title: Creating a Docker Image for Production
parent: Part 2 - Docker Compose
nav_order: 4
---

## Creating a Docker Image for Production

Now that we've created Docker images with Docker Compose. What about building a Docker image for a production-ready Next.js application.

### Steps

1. Navigate to the `client` directory.  

    Create a `Dockerfile.prod` using the text editor of your choice and paste the following content:  

    ```Dockerfile
    FROM node:16-alpine AS base

    FROM base AS dependencies
    WORKDIR /client
    COPY package.json package-lock.json /client/
    RUN npm ci

    FROM base AS builder
    WORKDIR /client
    COPY --from=dependencies /client/node_modules/ /client/node_modules/
    COPY . /client
    # to disable telemetry in next.js, uncomment the following line
    # ENV NEXT_TELEMETRY_DISABLED 1
    RUN npm run build

    FROM base AS runner
    WORKDIR /client
    ENV NODE_ENV production
    COPY --from=builder /client/public/ /client/public/
    COPY --from=builder /client/.next/ /client/.next/
    COPY --from=builder /client/node_modules/ /client/node_modules/
    COPY package.json /client/
    EXPOSE 3000
    CMD npm run start
    ```

    In the `Dockerfile` above, we provide instructions to generate production-ready statics files of the Next.js application and start the application in production mode.  

2. Navigate back to `nextjs-nginx-tutorial` directory.  

    Create a `docker-compose.production.yaml` file in the same directory using the text editor of your choice and paste the following content:  

    ```yaml
    services:
        client:
            build:
                context: ./client/
                dockerfile: Dockerfile.prod
            ports:
                - 3000
            volumes:
                - ./client/:/client
                - /client/node_modules

        nginx:
            build:
                context: ./nginx/
                dockerfile: Dockerfile
            ports:
                - "8080:8080"
            depends_on:
                - client
    ```

    In this Compose file, we added extra attributes `context` and `dockerfile` to specify where and which files should `docker-compose` look for the image build instructions.  

3. Run the resulting containers!

    By running the following command:  

    ```bash
    docker-compose -p <container-name> --file docker-compose.production.yaml up --build
    ```
