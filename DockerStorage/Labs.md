To create a GitHub Markdown (`.md`) file based on the information provided about Docker storage, you can follow this structure:

```markdown
# Docker Storage

## Introduction

Docker containers have two primary ways of managing data: non-persistent storage and persistent storage. Here, we'll explore these storage options and how to use them effectively.

### Non-Persistent Data

To deal with non-persistent data, Docker provides each container with its own non-persistent storage. This storage is tightly coupled to the container's lifecycle, meaning that deleting the container also deletes the storage and any data stored on it.

### Persistent Data

For persistent data, Docker containers need to use volumes. Volumes are separate objects with lifecycles independent of containers. This means that even if you delete a container, the volume will remain intact.

Containers and volumes are designed to work together to manage data effectively.

## Immutability

Containers are designed to be immutable, meaning they are read-only. It's recommended not to change the configuration of a running container. Instead, create a new container with the necessary fixes or updates and replace the old container.

However, some applications require a read-write filesystem to function properly, and Docker accommodates this requirement by adding a thin writable layer on top of the read-only image that containers are based on.

This writable layer allows all read/write operations but is tied to the container's lifecycle, which can be problematic for important data that needs to persist.

## Writable Container Layer

The writable container layer is an integral part of a container and enables read/write operations. It's created when the container is created and deleted when the container is deleted. This makes it unsuitable for storing critical data that needs to persist.

The management of this writable layer is handled by a storage driver on the Docker host.

## Storage Drivers

The storage driver, not to be confused with a volume driver, manages the writable container layer on each Docker host. When using Docker in production on Linux, it's essential to choose the correct storage driver that matches the Linux distribution on your Docker host.

The writable container layer can be found on the Docker host under various names, including local storage, ephemeral storage, and graphdriver storage. The location varies depending on the host's operating system.

- Linux Docker hosts: `/var/lib/docker/<storage-driver>/...`
- Windows: Windows only has one driver, which is configured by default.
- Red Hat/Ubuntu: The recommended driver is overlay2.

## Containers and Persistent Data

Volumes are the recommended way to persist data in Docker containers for several reasons:

1. **Independence**: Volumes are independent objects not tied to the lifecycle of a container.
2. **Specialized Storage**: Volumes can be mapped to specialized external storage systems.
3. **Data Sharing**: Volumes enable multiple containers on different Docker hosts to access and share the same data.

## Managing Volumes

You can create and manage volumes independently of containers. Here are some common commands for managing volumes:

### Create a Volume

```shell
$ docker volume create myvol
```

### List Volumes

```shell
$ docker volume ls
```

### Inspect a Volume

```shell
$ docker volume inspect myvol
```

### Remove a Volume

```shell
$ docker volume rm myvol
```

## Starting a Container with a Volume

To start a container with a volume, you can use either of the following commands:

```shell
$ docker run -d --name devtest -v myvol2:/app nginx:latest
$ docker run -d --name devtest --mount source=myvol2,target=/app nginx:latest
```

To inspect a container:

```shell
$ docker inspect devtest
```

To stop and remove a container:

```shell
$ docker container stop devtest
$ docker container rm devtest
```

To remove the associated volume:

```shell
$ docker volume rm myvol2
```

## Sharing Data Between Machines

Sharing data between Docker hosts can be achieved by using Docker Swarm or Kubernetes, which provide mechanisms for distributing data across a cluster of machines.

For more information on Docker storage, refer to the [official Docker documentation](https://docs.docker.com/storage/).

```

You can copy and paste this Markdown content into a GitHub Markdown (`.md`) file in your repository to create documentation about Docker storage. Make sure to format it as needed and add any additional sections or formatting as per your requirements.
