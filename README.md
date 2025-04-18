# Mounts and Volumes in Docker
Containers are ephemeral, meaning data is lost when they stop unless persisted. Docker offers volumes and bind mounts for data persistence.
- Docker supports various types of storage mounts to persist and share data:

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
