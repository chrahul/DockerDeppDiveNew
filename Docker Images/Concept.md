
Images

The aim is to give you a solid understanding of what Docker images are, how to perform basic operations, and how they work under-the-hood.

Image, Docker image, container image, and OCI image all mean the same thing. We’ll use the terms interchangeably.

#1: What is a container image:
-------------------------

A container image, often referred to as Docker image or OCI image, serves as a read-only package encompassing all the essentials for running an application. This comprehensive package includes the application's code, its dependencies, a minimal set of operating system components, and associated metadata.

Notably, a single container image can be leveraged to initiate one or more containers. These images are obtained by pulling them from a registry, with Docker Hub being the most prevalent, although alternative registries are available.

The structure of container images is based on multiple layers that are stacked upon one another, collectively forming a unified object. Within the confines of an image lies a streamlined operating system along with all the requisite files and dependencies essential for the application's execution. Designed to be swift and resource-efficient, container images are characterized by their small size.



Once a container has been initiated from an image, a mutual dependency is established between the two entities. The image cannot be deleted as long as there is an active container derived from it. The removal of the image is only permissible after ensuring that the last container associated with it has been halted and dismantled.


#2:Size of the images:
------------------------

The primary purpose of a container is to facilitate the execution of a single application or service. As a result, it exclusively encompasses the code and dependencies required for the specific application, excluding any extraneous components. This focus on essentials ensures that container images are compact and devoid of non-essential elements.

Notably, container images do not incorporate a kernel, as containers share the host's kernel during execution. Typically, an image includes only essential filesystem components and fundamental constructs related to the operating system. It's worth noting that Windows-based images are often larger compared to their Linux counterparts, reflecting the inherent differences in the structure and functioning of the Windows operating system.

3:Understanding Docker Images and Layers
---------------------------------------------

In Docker, an image is essentially a composite of interconnected, read-only layers, with each layer containing one or more files. Let's explore the concept using the example of pulling the latest Nginx image:

```bash
$ docker pull nginx:latest
$ docker inspect nginx:latest
```

The output of the `docker inspect` command reveals a series of SHA256 hashes representing individual layers:

```json
"Layers": [
  "sha256:92770f546e065c4942829b1f0d7d1f02c2eb1e6acf0d1bc08ef0bf6be4972839",
  "sha256:8ae474e0cc8f5a81405b04143604f78bfac4756c523e276a36921a8c4da36567",
  "sha256:f5525891d9e9b43a95b4aa1f79405087922489eb300864a2683262aae0fa5b3a",
  "sha256:66283570f41bca3619443d121a79e810b8a72849b5329319993e538d563b3e2f",
  "sha256:c2d3ab485d1b375fdd309458d69d93f8eb9aba8472e928efa32d9e5eda631440",
  "sha256:cddc309885a283a35ef142af78bc6f2e9c9db10e1981c4ea9cfb2c00b83e68ff",
  "sha256:0d0e9c83b6f775d68c7517aabf39ec9123ffca29672e3c3f83c5af7fc6aa242b"
]
```

Here's a breakdown of Docker image layers:

1. **Base Layer:**
   The initial layer, often derived from a foundational image like Ubuntu 22:04, serves as the base for subsequent changes.

2. **Adding Packages:**
   Installing packages adds a new layer on top of the base layer. Each layer represents a set of changes or additions.

3. **Adding Source Code:**
   Subsequent layers may include source code files. Each layer builds upon the previous, creating a cumulative effect.

As layers are added, the Docker image is essentially a stack of all these layers. Importantly, the order in which layers are added matters. If there are conflicts, where the same file exists in multiple layers, the file in the topmost layer takes precedence.

Docker utilizes a storage driver (e.g., overlay2, devicemapper, btrfs, or zfs) to manage and present these layers as a cohesive, unified filesystem or image.

Efficiency is achieved through layer sharing—multiple images can share common layers, reducing both storage space and enhancing performance. This modular approach facilitates versioning, updates, and efficient use of system resources.


#4: Deleting Images
-------------------------

When you no longer need an image on your Docker host, you can delete it with the docker rmi command. rmi is short for remove image. Deleting an image will remove the image and all of its layers from your Docker host. This means it will no longer show up in docker images

Deleting an image will remove the image and all of its layers from your Docker host. This means it will no longer show up in docker images
commands and all directories on the Docker host containing the layer data will be deleted. However, if an image layer is shared by another image, it won’t be deleted until all images that reference it have been deleted.

$ docker rmi <>

You won’t be able to delete an image if it’s in use by a running container. You’ll need to stop and delete any containers before deleting the image.

$ docker rmi $(docker images -q) -f
