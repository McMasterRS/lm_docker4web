---
layout: default
title: Installation
parent: Part 1 - Docker
nav_order: 1
---

## Disclaimer

Keep in mind that there are multiple ways to setup and install Docker in your system. It is best to refer to the [official Docker installation guideline](https://docs.docker.com/engine/install/). In this tutorial, we will present an installation example on Ubuntu Linux with the `apt` package manager.  

## Installing Docker

Before installing the Docker Engine, you will need to set up the Docker repository:  

1. In the Ubuntu's terminal window, update the `apt` package index and install packages that allow `apt` to use a repository over HTTPS:  

    ```bash
    apt-get update && apt-get install ca-certificates curl gnupg
    ```

2. Add Docker's official GPG key:  

    ```bash
    install -m 0755 -d /etc/apt/keyrings
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
    chmod a+r /etc/apt/keyrings/docker.gpg
    ```

3. Use the following command to set up the repository:  

    ```bash
    echo \
    "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
    "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
    sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    apt-get update
    ```

Next, to install the Docker Engine, containerd and Docker Compose, simply run the following command:  

```bash
apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
