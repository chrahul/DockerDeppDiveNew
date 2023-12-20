
# Docker Data Management

## Introduction

In the realm of cloud-native and microservices applications, stateful applications that persist data play a crucial role. This chapter explores how Docker handles applications dealing with persistent and non-persistent data.

### Non-Persistent Data

For non-persistent data, each Docker container is assigned its own storage, tightly coupled with the container's lifecycle. This storage is automatically created and linked to the writable container layer. Changes made within the container are stored in this layer. However, deleting the container also deletes the storage and associated data.

Since each container has its writable container layer, multiple containers can share access to the same underlying image while maintaining their own data state.

![image](https://github.com/chrahul/DockerDeppDiveNew/assets/14847377/ae426877-c839-4288-b158-4f6565e928f1)


The major difference between a container and an image is the top writable layer. All writes to the container that add new or modify existing data are stored in this writable layer. When the container is deleted, the writable layer is also deleted. The underlying image remains unchanged.

Because each container has its own writable container layer, and all changes are stored in this container layer, multiple containers can share access to the same underlying image and yet have their own data state.

![image](https://github.com/chrahul/DockerDeppDiveNew/assets/14847377/016e2185-ba0c-45ab-9626-925332a6ae75)



### Persistent Data

Persistent data includes crucial information that needs to be retained, such as customer records, financial data, research results, audit logs, and specific application log data. Docker provides solutions for both persistent and non-persistent data.

#### Volumes

- **Definition:** Volumes are external storage entities in Docker that exist independently of the container lifecycle.
- **Shared Access:** Multiple containers can share access to the same underlying image while preserving their own distinct data state within volumes.
- **Data Retention:** Volumes persist even if the associated container is removed, ensuring that essential data is retained beyond the lifespan of individual containers.

#### Examples of Persistent Data Use Cases

- *Customer Records:* Storing customer information that needs to persist across container restarts.
- *Financial Data:* Maintaining financial records that are critical and should survive the container's lifecycle.
- *Audit Logs:* Preserving audit logs for compliance and analysis purposes.

By leveraging volumes for persistent data and the container layer for non-persistent data, Docker provides a flexible and scalable approach to managing different types of data in containerized applications. This separation enables efficient handling of both disposable and valuable data.

```

You can copy and paste this content into a new Markdown file (e.g., `docker_data_management.md`) and then commit it to your GitHub repository.
