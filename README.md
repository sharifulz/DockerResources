Docker — One-Page README

A concise guide for quickly using Docker in this repo.

------------------------------------------------------------------------

🚀 What is Docker?

Docker packages apps and their dependencies into containers so they run
consistently across environments.

Why use it? Portability • Isolation • Fast deployments • Reproducible
builds

------------------------------------------------------------------------

🕰️ Quick History (super short)

-   2013: Open-sourced by Solomon Hykes (dotCloud → Docker, Inc.).
-   2015–2017: Image/Runtime standards move under OCI; Moby project
    created.
-   Today: Docker is the default developer workflow for containers
    (Desktop, CLI, Compose).

------------------------------------------------------------------------

🧩 Core concepts

-   Image: Read-only template (your app + runtime).
-   Container: Running instance of an image.
-   Registry: Remote image store (e.g., Docker Hub, GHCR).
-   Dockerfile: Build recipe for an image.
-   Compose: Multi-container app definition (docker-compose.yml /
    compose.yaml).

------------------------------------------------------------------------

🛠️ Install (summary)

-   Linux: Follow your distro’s “Docker Engine” guide.
-   macOS/Windows: Install Docker Desktop.
    Confirm:

    docker version
    docker info

------------------------------------------------------------------------

🔧 Common commands (copy & use)

Images & Containers

    # Pull / list / remove images
    docker pull nginx:alpine
    docker images
    docker rmi IMAGE_ID

    # Run a container (detached), map port, set name
    docker run -d -p 8080:80 --name web nginx:alpine

    # List / stop / start / remove containers
    docker ps            # running
    docker ps -a         # all
    docker stop web
    docker start web
    docker rm web        # remove (container must be stopped)

Build & Tag

    # Build with a tag
    docker build -t myapp:1.0 .

    # Tag for a registry
    docker tag myapp:1.0 ghcr.io/USER/myapp:1.0

Push & Pull

    docker login ghcr.io
    docker push ghcr.io/USER/myapp:1.0
    docker pull ghcr.io/USER/myapp:1.0

Inspect, Logs, Exec

    docker logs -f web
    docker exec -it web sh          # or bash
    docker inspect web               # JSON metadata
    docker port web                  # published ports

Files, Networks, Volumes

    docker cp web:/usr/share/nginx/html/index.html ./index.html

    docker network ls
    docker network create app-net
    docker run --network app-net ...

    docker volume ls
    docker volume create app-data
    docker run -v app-data:/var/lib/app ...

Clean up

    docker system df
    docker system prune -f           # remove unused data (CAUTION)
    docker image prune -f            # dangling images only

------------------------------------------------------------------------

🧰 Docker Compose (multi-service)

compose.yaml example:

    services:
      api:
        build: .
        ports: ["8080:8080"]
        env_file: .env
