
# Understanding Docker Images

A Docker image is like a box that holds everything needed for a computer program to work. This box includes the program itself, the things it needs to run, and some basic computer stuff. If you have this box with the program inside, all you need is a computer that can run Docker to make the program work.

Similar to how you have templates or images for virtual machines (like AMIs or ISOs), a Docker image is a kind of template for running software, but it's designed for a different type of environment compared to traditional virtual machines.

## Layers and Efficiency

Images consist of several layers stacked together to form a single entity. These images include a streamlined operating system (OS) and all the necessary files and dependencies for running an application. Containers are designed to be quick and efficient, resulting in compact image sizes, whereas AMI/ISO images tend to be significantly larger in size.

Images are like small packages for computer programs. Each package is designed to run one program, and it only has the stuff that program needs to work. It doesn't have extra things. For example, think of it like this: when you buy a toy, you don't need six different toys in the box, just the one you wanted. So, these packages are like that – they only have what the program needs.

These packages also don't have something called a "kernel," which is like the brain of the computer. Instead, they use the brain of the computer they are put on. So, many programs can share the same brain without any problems.

So, in simple words, these packages are very focused on making one program work, and they don't have extra stuff or their own brain. They only have what's necessary for that program to run.

## Image Sizes

The official Alpine Linux Docker image is incredibly tiny at around 5MB, showcasing how small Docker images can be. In comparison, the official Ubuntu Docker image is larger at about 40MB, but both are stripped down to only include what's essential.

## How to Get these Images

When you first install Docker, there are no images on your computer. You can either download images from Docker Hub or make your own custom images.

### What is Docker Hub?

Docker Hub is a cloud-based service that serves as a central repository for Docker containers. It allows developers to store, share, and access container images, making it easier to distribute and deploy applications using Docker containers. Docker Hub provides both public and private repositories for container images.

To search for images on Docker Hub, you can use the following command:

```shell
$ docker search alpine
```

To pull an image from Docker Hub, you can use the "docker image pull" command:

```shell
$ docker image pull redis:latest
```

You can list all the images on your system using:

```shell
$ docker image ls
```

### Naming and Tagging Images

Images are stored in central locations known as image registries, which facilitate easy sharing and retrieval. Docker Hub (https://hub.docker.com) is the most popular registry, but others, such as third-party registries and secure on-premises registries, also exist. It's important to note that the Docker client primarily uses Docker Hub by default.

Naming and Tagging is straightforward. To address images from official repositories, you simply need to specify the repository name and tag, separated by a colon (:). When using the "docker image pull" command with an image from an official repository, the format is:

```shell
$ docker image pull <repository>:<tag>
```

For example:

```shell
$ docker image pull mongo:4.2.6
```

You can also filter images, such as finding dangling images:

```shell
$ docker image ls --filter dangling=true
```

A dangling image is one that has lost its tag and is shown as "<none>:<none>" in listings. This often happens when creating a new image with a tag that's already in use. Docker replaces the tag on the existing image with the new one, resulting in the previous image becoming "dangling" without a tag.

To list images with a specific reference or tag, you can use:

```shell
$ docker image ls --filter=reference="*:latest"
```

### Displaying Image Information

You can use the following command to list all images and display only the repository, tag, and size:

```shell
docker image ls --format '{{.Repository}}:{{.Tag}} {{.Size}}'
```

This command uses the `--format` flag to specify the output format and selects the repository, tag, and size fields to display.

### Examining Image Layers

You can also examine the layers of an image by using the "docker image inspect" command. Here's an example of inspecting the "ubuntu:latest" image:

```shell
docker image inspect ubuntu:latest
```

This command provides detailed information about the image, including its layers and configuration.

These concepts should help you understand Docker images and how to work with them effectively.




