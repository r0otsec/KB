---
tags:
  - technologies
date: 2023-09-1
---
- Open source platform.
- Used to develop, ship, and run apps in isolated environments (`containers`).
- Containers are:
	- self-contained, portable, fast.
	- package an app and all its dependencies.
	- runs the same regardless of environment.
# Key Components

- `Image`: template for creating containers.
- `Container`: instance of an image running.
- `Dockerfile`: script to build custom image.
- `Registry`: remote image storage (e.g. Docker Hub).
- `Volume`: persistent storage outside container lifecycle.
- `Network`: isolated networks for container comms.
# Basic Workflow Example

- Write a `Dockerfile`.
- Build an image:
	- `docker build -t myapp .`
- Run a container:
	- `docker run -d -p 8080:80 myapp`
- Push to registry (optional):
	- `docker push myuser/myapp:latest`
- Example Dockerfile includes:

```dockerfile
FROM python:3.11-slim

WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .

CMD ["python", "app.py"]
```
# Commands

- Common commands:
	- `docker ps` - list running containers
	- `docker build -t myimage .` - build image from dockerfile
	- `docker run -d -p 8080:80 myimage` - run container from image
	- `docker logs <container ID>` - view container logs
	- `docker exec -it <container ID> /bin/bash` - enter container shell
	- `docker stop <ID>; docker rm <ID>` - stop and remove container
# Volume & Data Persistence

- Data inside containers is ephemeral - to persist:
	- `docker run -v /host/path:/container/path ...`
- For named volumes:
	- `docker volume create mydata`
	- `docker run -v mydata:/data ...`
# Networking

- Containers can talk to internet by default.
- Docker creates bridge network automatically.
- To isolate:
	- `docker network create isolated_net`
	- `docker run --network=isolated_net`