# Understanding Container Images

## 1. What is a Container Image:

A container image, interchangeably referred to as Docker image or OCI image, serves as a read-only package containing all the essentials for running an application. This comprehensive package includes the application's code, dependencies, a minimal set of operating system components, and associated metadata.

A single container image can be used to initiate one or more containers. These images are obtained by pulling them from a registry, with Docker Hub being the most prevalent, although alternative registries are available.

The structure of container images is based on multiple layers stacked upon one another, collectively forming a unified object. Within the image lies a streamlined operating system along with all the requisite files and dependencies essential for the application's execution. Container images are designed to be swift and resource-efficient, characterized by their small size.

Once a container is initiated from an image, a mutual dependency is established between the two entities. The image cannot be deleted as long as there is an active container derived from it. The removal of the image is only permissible after ensuring that the last container associated with it has been halted and dismantled.
