# Docker Networking and Linking
Docker networking enables containers to communicate with each other and external systems. The default setup uses bridge networks, but other options exist.

##  Networking Types
### Bridge Network
- Default for standalone containers. Containers on the same bridge network communicate using container names as hostnames.

- **Syntax**: `docker network create <name>`.

#### Example:
```bash
docker network create mynetwork
docker run -d --name app1 --network mynetwork nginx
docker run -d --name app2 --network mynetwork busybox
```
- `app2` can ping `app1` by name.

Example: 2 Create isolated networks with:
```bash
docker network create -d bridge my-net
docker run --network=my-net -itd --name=container3 busybox
```  
- Containers on the same network can communicate by name or IP.

### Host Network
Containers use the host’s network, removing isolation. Useful for performance but less secure.

### Overlay Network
For multi-host communication in Docker Swarm.

### None
Disables networking for isolated containers.

### Legacy Container Linking
- **Definition**: An older method using `--link` to connect containers. Replaced by user-defined bridge networks for better flexibility.
- **Recommendation**: Use custom bridge networks instead of `--link`.
- The `--link` flag creates environment variables and `/etc/hosts` entries for connecting containers, but is now considered legacy in favor of user‑defined networks. 


## Port Mapping
Expose container ports on the host to enable external access:  
- **Syntax** 
```bash
docker run -p <host-port>:<container-port> <image>
```  
Example:  
```bash
docker run -p 8080:80 httpd
``` 
- Access the container’s web server at localhost:8080
