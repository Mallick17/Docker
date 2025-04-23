# CMD vs ENTRYPOINT in Dockerfiles
The CMD and ENTRYPOINT instructions in a Dockerfile define what command runs when a container starts. They work together but have distinct roles.

**Key Differences between `CMD` and `ENTRYPOINT`** in a table:

| **Instruction** | **Override Behavior**                            | **Use Case**                                |
|-----------------|--------------------------------------------------|---------------------------------------------|
| **CMD**         | Fully replaced by `docker run` arguments.        | Default commands or parameters.             |
| **ENTRYPOINT**  | Arguments are appended; command stays fixed.     | Containers acting as specific executables.  |

![image](https://github.com/user-attachments/assets/aae2bcba-5e7e-4a8c-84fc-9ebb4eb6e000)

### `CMD`
**Purpose**: Provides default commands or parameters for a container. These can be overridden when running docker run.
- **`CMD`** sets default arguments for the container and can be overridden by parameters to `docker run`. 

#### Forms:
- **Exec Form**: ["executable", "param1", "param2"] (preferred for clean process handling).
- **Shell Form**: command param1 param2 (runs inside a shell).

#### Behavior: 
- If multiple CMD instructions exist, only the last one applies. Arguments in docker run replace the CMD.

#### Example:
```dockerfile
CMD ["echo", "Hello, World!"]
```

- Running `docker run myimage` outputs `Hello, World!`, but `docker run myimage ls runs ls` instead.

### ENTRYPOINT
**Purpose**: Sets the primary command, making the container act like an executable. Arguments in docker run are appended to ENTRYPOINT.
- **`ENTRYPOINT`** configures a fixed executable that always runs when the container starts, optionally appending arguments from `CMD` or `docker run`.  
- Combining `ENTRYPOINT` (exec form) with `CMD` allows setting a base executable with default arguments that users can override as needed. 

#### Forms:
- **Exec Form**: ["executable", "param1", "param2"] (preferred for clean process handling).
- **Shell Form**: command param1 param2 (runs inside a shell).

#### Behavior: 
- The command is fixed, but parameters can be customized via CMD or docker run arguments.

#### Example:
```dockerfile
ENTRYPOINT ["echo", "Hello"]
CMD ["World"]
```
- `docker run myimage` outputs `Hello World`.
- `docker run myimage Universe` outputs `Hello Universe`.

---

## 🧪 Example Scenarios

### **1. Using `CMD` Alone**
**Dockerfile:**
```Dockerfile
FROM ubuntu
CMD ["echo", "Hello from CMD"]
```

**Run:**
```bash
docker build -t cmd-example .
docker run cmd-example
# Output: Hello from CMD

docker run cmd-example echo "Overridden"
# Output: Overridden
```
- `CMD` was replaced by the new arguments.

---

### **2. Using `ENTRYPOINT` Alone**
**Dockerfile:**
```Dockerfile
FROM ubuntu
ENTRYPOINT ["echo"]
```

**Run:**
```bash
docker build -t entrypoint-example .
docker run entrypoint-example "Hello from ENTRYPOINT"
# Output: Hello from ENTRYPOINT
```
- `ENTRYPOINT` stays fixed. Arguments get appended.

---

### **3. Combining `ENTRYPOINT` + `CMD`**
**Dockerfile:**
```Dockerfile
FROM ubuntu
ENTRYPOINT ["echo"]
CMD ["Default message"]
```

**Run:**
```bash
docker build -t combo-example .
docker run combo-example
# Output: Default message

docker run combo-example "Custom message"
# Output: Custom message
```
- You get default behavior if no arguments passed, and override when needed.

---
