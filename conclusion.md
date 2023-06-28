---
layout: default
title: Conclusion
nav_order: 5
---

# Conclusion

Throughout this learning module, we learned the basics of using Docker. You learned the several Docker commands that allow you to:
- Publish a port
- Run a container in a detached mode
- List running containers
- Stop a running container
- Name a container
- Restart a container
- Remove stopped containers
- List images
- Remove images
- Purge unused or dangling images, container, volumes and networks

You also learned how to use Docker Compose to perform container orchestration and simplify the container creation and running processes. We covered creating and running docker images as well as using Docker Compose to create development and production Docker images.

While we only scratched the surface of what you can do with Docker, we hope that this learning module provided you with the basic knowledge needed to get started with Docker containers. 

We recommend the following resources if you want to learn more about Docker:
- [Official Docker Documentation](https://docs.docker.com/)
- [A Docker Tutorial for Beginners](https://docker-curriculum.com/)

## Alternatives

Docker is one of the most popular containerization platforms, but it is not the only one. There are multiple other platforms that you can use to create and run containers.

![apptainer-logo](assets/img/apptainer-logo.png)

**Apptainer** (formerly known as Singularity) is a container platform created for High-Performance Computing (HPC) and High Throughput Computing (HTC) use cases. As an enterprise-based container framework, Docker is meant to provide a containerization solution that fits well in the models of the industry, i.e., where system administrators with root privilege install and run applications, each in its own container. This solution is not compatible with the HPC/HTC use case that requires complex applications to run exhaustively using all the available resources and without any special privilege.
Apptainer allows users to build and run containers (including support for Docker images) with just a few steps in most cases, and its design emphasizes the following features:
- Single-file based container images, facilitating the distribution, archiving and sharing.
- Ability to run without any root privileges thus making it safer for large computer centers with shared resources.
- Defaults to running as the current user outside the container thus preserving the permissions in the environment. 
- Simple integration with resource managers and distributed computing frameworks because it defaults to running as a regular application (instead of a background process).
- Prioritizes security and addresses many of the security flaws that can be found in Docker containers.
- Compatibility with Docker images for seamless container migration and sharing. 

If you are interested in learning more about Apptainer, we recommend consulting the following resources:
- [Compute Ontario Summer School - Apptainer Slides](https://mcmasteru365.sharepoint.com/:b:/r/sites/Daves-RSDTeam/Shared%20Documents/RSD%20Team/General/Workshops/apptainer.pdf?csf=1&web=1&e=UfY4kK)
- [Computer Ontario Summer School - Apptainer Recording](https://mcmasteru365.sharepoint.com/:v:/r/sites/Daves-RSDTeam/Shared%20Documents/RSD%20Team/General/Workshops/apptainer-recording.mp4?csf=1&web=1&e=HUBNGj)
- [Apptainer Documentation (alliancecan.ca)](https://docs.alliancecan.ca/wiki/Apptainer)
- [Official Apptainer Documentation](http://apptainer.org/docs/)

## Complementary Software 

### Kubernetes

![kubernetes-logo](assets/img/kubernetes-logo.png)

Kubernetes, or k8s, is an open source platform that automates Linux container operations. Kubernetes is often used to automate the processes involved in deploying and scaling containerized applications. Kubernetes allows users to cluster groups of hosts running Linux containers in addition to helping them easily and efficiently manage those clusters.

Kubernetes assesses the available compute resources and the resource requirements of each container to organize and schedule running these containers on virtual machines. Kubernetes allows users to group containers into pods, which are the basic operational unit for Kubernetes.

Kubernetes also monitors the running environment and compares it against the desired state. It performs automated health checks on services and restarts containers that have failed or stopped. Kubernetes only makes services available when they are running and ready.

Kubernetes is not an alternative to Docker given that it cannot create containers on its own, but it can be used in conjunction with Docker or other containerization platforms to automate container operations, manage infrastructure resources and perform automated health check on running services.