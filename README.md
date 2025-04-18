# Docker Networking and Linking
Docker networking enables containers to communicate with each other and external systems. The default setup uses bridge networks, but other options exist.
| **Topic**            | **Quick Analogy**                                |
|----------------------|--------------------------------------------------|
| Bridge Network       | Like private LAN – talk by name or IP            |
| Host Network         | Container lives on your machine’s network        |
| Overlay Network      | Virtual network over many Docker hosts           |
| None Network         | No internet or LAN – like airplane mode          |
| Legacy Linking       | Old-style direct line – not flexible anymore     |

---

##  Networking Types
### Bridge Network (Default)
- Default for standalone containers. Containers on the same bridge network communicate using container names as hostnames.

- **Syntax**: `docker network create <name>`.

#### Example 1: Create and Connect Containers
```bash
docker network create mynetwork

docker run -d --name web --network mynetwork nginx
docker run -it --rm --name client --network mynetwork busybox
```

From inside `client` container:
```bash
ping web
```
- You can ping or access `web` by name.

---

#### Example 2: Isolated App Communication
```bash
docker network create -d bridge app-net

docker run -itd --name app1 --network app-net busybox
docker run -itd --name app2 --network app-net busybox
```
- Containers `app1` and `app2` can communicate using their names.

#### Example 3: One Container Exposes a Web Server
```bash
docker network create web-net

docker run -d --name backend --network web-net python:3 \
python -m http.server

docker run -it --rm --network web-net curlimages/curl \
curl backend:8000
```
- Curl container successfully connects to Python’s HTTP server.

---

### Host Network
Containers use the host’s network, removing isolation. Useful for performance but less secure.
#### Example:
```bash
docker run --rm --network host nginx
```
- Nginx listens directly on the host's ports (like port 80).
> 🔒 Note: Not available on Docker Desktop for Mac/Windows due to virtualization.

---

### Overlay Network (Swarm Mode)
Used for **multi-host container networking** in a Docker Swarm cluster.

#### Example:
```bash
docker swarm init
docker network create -d overlay my-overlay

docker service create --name web --network my-overlay nginx
```
- Nginx service spans multiple hosts and stays connected via `my-overlay`.

---

### None
Creates a container **with no networking**. Disables networking for isolated containers.
#### Example:
```bash
docker run -d --network none --name isolated alpine sleep 1000
```
- Container has no access to other containers or internet.

---

### Legacy Container Linking
- **Definition**: An older method using `--link` to connect containers. Replaced by user-defined bridge networks for better flexibility.
- **Recommendation**: Use custom bridge networks instead of `--link`.
- The `--link` flag creates environment variables and `/etc/hosts` entries for connecting containers, but is now considered legacy in favor of user‑defined networks. 
#### Example:
```bash
docker run -d --name db mongo
docker run -it --link db:dbclient busybox
```
- `dbclient` can now access `db` using environment variables or hostname.

Instead of linking, **create a network**:
```bash
docker network create backend-net
docker run -d --name db --network backend-net mongo
docker run -it --network backend-net busybox
```

---

## Port Mapping
Expose container services to the **host machine** or **external access**
- **Syntax** 
```bash
docker run -p <host-port>:<container-port> <image>
```  
#### Example: Expose Port
```bash
docker run -d -p 8080:80 nginx
```
- Access via `http://localhost:8080`

#### Example: Map Multiple Ports
```bash
docker run -d -p 3000:3000 -p 9229:9229 node-app
```

---
