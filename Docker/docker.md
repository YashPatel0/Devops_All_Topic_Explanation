# 🐳 Docker Complete Guide – DevOps Edition

> A complete Docker reference for Developers, DevOps Engineers, and Cloud Professionals.

---

# 📌 Table of Contents

- What is Docker?
- Containers Explained
- Monolithic vs Microservices
- Containerization vs Virtualization
- Docker Architecture
- Dockerfile Deep Dive
- Multi-Stage Builds
- Docker Commands (Images & Containers)
- Docker Networking
- Docker Volumes
- Docker Logs & Monitoring
- Docker System Cleanup
- Docker Hub & Image Management
- Docker Compose
- Best Practices
- Interview Important Points

---

# 🚀 What is Docker?

Docker is a containerization platform that allows you to package an application along with all its dependencies into a standardized unit called a **container**.

Containers ensure that applications run consistently across:
- Developer machines
- Testing environments
- Production servers
- Cloud platforms

---

# 📦 In Simple Words

Docker is like a **portable box for software**.

Inside the box:
- Application code
- Runtime
- Libraries
- Dependencies
- Environment settings

You just run the box — no manual setup required.

---

# 🧱 What is a Container?

A container is:

- Lightweight
- Isolated
- Fast to start
- Shares the host OS kernel

Unlike virtual machines, containers do not require a full operating system.

---

# 🏗 Monolithic vs Microservices

## Monolithic Architecture

- Entire application built as a single unit
- All modules tightly coupled
- Single deployment unit
- Hard to scale specific components

## Microservices Architecture

- Application divided into small independent services
- Each service has its own logic and database
- Communicate using APIs
- Easy scaling and independent deployments

Docker is widely used in Microservices architecture.

---

# 🖥 Containerization vs Virtualization

| Feature | Containerization | Virtualization |
|----------|------------------|---------------|
| OS | Shares host OS | Each VM has full OS |
| Speed | Very fast | Slower |
| Resource Usage | Lightweight | Heavy |
| Startup Time | Seconds | Minutes |
| Isolation | Process-level | Full hardware-level |

---

# 🏛 Docker Architecture

Docker uses:

- **Docker Client** → CLI (docker commands)
- **Docker Daemon** → Background service
- **Docker Images** → Blueprint for containers
- **Docker Containers** → Running instances
- **Docker Registry** → Stores images (Docker Hub)

---

# 📄 Dockerfile

A Dockerfile is a text file containing instructions to build a Docker image.

It defines:
- Base image
- Dependencies
- Environment variables
- Application startup command

---

# 🧪 Basic Dockerfile Example

```dockerfile
FROM ubuntu:20.04
RUN apt-get update && apt-get install -y nginx
CMD ["nginx", "-g", "daemon off;"]
```

### Instruction Explanation

- `FROM` → Base image
- `RUN` → Executes commands during build
- `CMD` → Default command at container start

---

# 🧠 Important Dockerfile Instructions

## FROM
Defines base image.

## RUN
Executes commands at build time.

## CMD
Default runtime command.

## ENTRYPOINT
Main executable that always runs.

## COPY
Copies files from local system.

## ADD
Copies files and supports archive extraction.

## WORKDIR
Sets working directory.

## EXPOSE
Documents container port.

## ENV
Sets environment variables.

## ARG
Build-time variables.

## USER
Specifies non-root user (security best practice).

---

# 🏗 Recommended Dockerfile Order

1. FROM
2. LABEL
3. ARG
4. ENV
5. WORKDIR
6. COPY
7. RUN
8. EXPOSE
9. USER
10. CMD / ENTRYPOINT

---

# 🚀 Multi-Stage Dockerfile (Best Practice)

Used to reduce final image size and remove build dependencies.

```dockerfile
# Stage 1: Build
FROM maven:3.9.6-eclipse-temurin-17 AS build
WORKDIR /app
COPY pom.xml .
RUN mvn dependency:go-offline
COPY src ./src
RUN mvn package -DskipTests

# Stage 2: Runtime
FROM eclipse-temurin:17-jre
WORKDIR /app
COPY --from=build /app/target/myapp.jar app.jar
EXPOSE 8080
USER 1001
CMD ["java", "-jar", "app.jar"]
```

✔ Smaller  
✔ More secure  
✔ Production ready  

---

# 🐳 Docker Basic Commands

## Image Commands

```bash
docker images
docker pull nginx
docker build -t myapp .
docker rmi image_id
docker image prune
```

---

## Container Commands

```bash
docker run nginx
docker run -d -p 8080:80 nginx
docker run -it ubuntu /bin/bash
docker ps
docker ps -a
docker stop container_id
docker start container_id
docker restart container_id
docker rm container_id
docker container prune
```

---

# 📊 Logs & Monitoring

```bash
docker logs container_id
docker logs -f container_id
docker stats
docker top container_id
docker inspect container_id
```

---

# 🌐 Docker Networking

Docker supports:

- bridge (default)
- host
- none
- overlay (Swarm)
- macvlan

## Commands

```bash
docker network ls
docker network create mynet
docker network inspect mynet
docker network rm mynet
```

---

# 💾 Docker Volumes

Volumes are used to persist data beyond container lifecycle.

```bash
docker volume ls
docker volume create myvolume
docker run -v myvolume:/data nginx
docker volume inspect myvolume
docker volume rm myvolume
docker volume prune
```

---

# 🧹 Docker System Cleanup

```bash
docker system df
docker system prune
docker system prune -a
```

---

# ☁ Docker Hub

Docker Hub is a cloud registry to store and share Docker images.

## Workflow

1. Build image
2. Tag image
3. Login
4. Push to Docker Hub
5. Pull anywhere

## Example

```bash
docker build -t myapp .
docker tag myapp username/myapp:v1
docker login
docker push username/myapp:v1
```

Pull image:

```bash
docker pull username/myapp:v1
docker run -d username/myapp:v1
```

---

# 📦 Docker Compose

Used to define multi-container applications using YAML.

## docker-compose.yml Example

```yaml
version: '3'
services:
  app:
    image: myapp
    ports:
      - "8080:8080"
  db:
    image: mysql
    environment:
      MYSQL_ROOT_PASSWORD: root
```

## Commands

```bash
docker-compose up
docker-compose up -d
docker-compose down
docker-compose ps
```

---

# 🔐 Docker Best Practices (Important for Interviews)

✔ Use multi-stage builds  
✔ Use minimal base images (alpine, distroless)  
✔ Avoid running containers as root  
✔ Use .dockerignore  
✔ Keep images small  
✔ Scan images for vulnerabilities  
✔ Use specific image tags (avoid latest in production)  

---

# 🎯 Must-Know Interview Topics

- Difference between CMD and ENTRYPOINT
- Difference between COPY and ADD
- Docker vs Kubernetes
- What is multi-stage build?
- How to reduce Docker image size?
- What is Docker networking?
- How volumes work?
- Docker layered architecture

---

⭐ If this repository helped you, consider giving it a star!
