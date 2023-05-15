---
layout: default
title: General Docker Techniques
parent: Part 1 - Docker
nav_order: 2
---

## General Docker Techniques

### Publishing a Port

Containers are isolated environments and as such, the host system cannot access any application running inside the container.  

To allow an external system to access an application running inside a container, you have to publish the appropriate port inside the container to a port on your local network.  

The `--publish` or `-p` option can be added to the run command to perform this port forwarding:  

```bash
docker container run --publish <host port>:<container port> <image>
```

### Running in Detached Mode

Running a Docker image from a terminal window will cause the container to attach itself to the terminal preventing the user from entering additional commands. Hence, you can use the `--detach` or `-d` option to keep the container running in the background.  

### Listing Running Container

Use the `container ls` command to view a list of containers that are currently running:  

```bash
docker container ls
```

Note that the command above only shows containers that are currently running. To view all containers including past ones, add the `--all` or `-a` flag:  

```bash
docker container ls --all
```

### Stopping a Running Container

To stop a container that is currently running in the foreground, simply hit the `Ctrl + C` key combination on your keyboard.  

To stop a container running in detached mode, use the stop command:  

```bash
docker container stop <container identifier>
```

The `<container identifier>` in the previous command and in all future commands shown in this workshop can be the container ID or container name. We'll go over more about naming containers in the next section.  

### Naming Containers

Containers are automatically assigned an ID when you run them. However, you may want to explicitly give your container a name.  

Use the `--name` flag to name containers when running them:  

```bash
docker container run --publish <host port>:<container port> --name <container-name> <image>
```

You can view container names by listing them using the `container ls` command.  

Old named containers can be renamed using the following command:  

```bash
docker container rename <old-name> <new-name>
```

### Restarting a Container

You can use the start command to restart a running container or to start a previously stopped one:  

```bash
docker container start <container identifier>
```

The start command is particularly useful to start containers that were created using the create command:  

```bash
docker container create --publish <host port>:<container port> <image>
```

The command above creates a new container but does not start it. You can use the start command to run a previously created container.  

### Removing Stopped Containers

Stopped containers can still take up a significant amount of space on your system. You may want to remove any containers that you are no longer using the rm command:  

```bash
docker container rm <container identifier>
```

Run the `container ls` command after deleting a container to verify that it has been removed successfully.  

The `--rm` flag can coupled with the run command to delete the container as soon as it finishes executing:  

```bash
docker container run --rm --publish <host port>:<container port> <image>
```

### Listing Images

To view a list of all the existing images on your system, use the following command:  

```bash
docker images -a
```

### Removing Images

You can delete an image using the `rmi` command:  

```bash
docker rmi <image_identifier>
```

Note that the image_identifier can be the image ID or image tag.  

### Purging All Unused or Dangling Images, Containers, Volumes, and Networks

Docker provides a single command that will clean up any resources (images, containers, volumes, and networks) that are dangling (not tagged or associated with a container):  

```bash
docker system prune
```
