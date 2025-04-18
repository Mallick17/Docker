# Mounts and Volumes in Docker
Containers are ephemeral, meaning data is lost when they stop unless persisted. Docker offers volumes and bind mounts for data persistence.
- Docker supports various types of storage mounts to persist and share data:

**Docker Storage Options Comparison Table**:

| **Type**         | **Managed By** | **Portability** | **Best For**                            | **Example Command**                                                                 |
|------------------|----------------|------------------|-----------------------------------------|--------------------------------------------------------------------------------------|
| **Volumes**       | Docker          | High             | Production, persistent data storage     | `docker run -v mydata:/app/data myapp`                                              |
| **Bind Mounts**   | User (Host OS)  | Low              | Development, local file syncing/testing | `docker run -v /home/user/app:/app myapp`                                           |
| **tmpfs Mounts**  | Host Memory     | None             | Ephemeral, in-memory temporary storage  | `docker run --tmpfs /app/cache myapp` or `docker run --mount type=tmpfs,dst=/tmp`  |


### 4.1 Volumes
Volumes are managed by Docker and stored in a host directory under Docker’s control. They are the preferred mechanism for persisting container data. 
- Docker-managed storage for persisting data, stored in `/var/lib/docker/volumes` on the host.
- **Creation**: Use `docker volume create <name>` or let Docker create one during `docker run`.
- **Mount with**: Use `-v <volume_name>:<container_path>` or `--mount` in `docker run`.
```bash
docker run --mount type=volume,src=<volume-name>,dst=<mount-path>
# or
docker run --volume <volume-name>:<mount-path>
# or
docker volume create mydata
# or
docker run -v mydata:/app/data myimage
``` 
- **Advantages**: Portable, easy to back up, and isolated from the host’s filesystem. Preferred for production.
- **Use Case**: Storing database data that persists across container restarts.

### 4.2 Bind Mounts
Bind mounts map a host directory or file into a container, allowing direct access to the host filesystem.  
- Maps a host file or directory to a container path, like `/host/path:/container/path`.
Specify with:  
```bash
docker run --mount type=bind,src=<host-path>,dst=<container-path>
# or
docker run -v /home/user/code:/app myimage
``` 
- **Use Case**: Editing code on the host while testing in a container.
- **Advantages**: Useful for development, as host changes reflect immediately in the container.
- **Drawbacks**: Tied to the host’s filesystem, less portable than volumes.



### 4.3 tmpfs Mounts
Temporary file storage mounts (`tmpfs`) store data in the host’s memory for short‑lived use cases.  
Use:  
```bash
docker run --mount type=tmpfs,dst=<container-path>
``` 
