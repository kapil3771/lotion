# Docker Compose AI Web App (Ollama + WebUI + MongoDB)

## Aim

To use Docker Compose to run a multi-container AI web application with
AI model, frontend, and database.

------------------------------------------------------------------------

## Step 1: Install Docker (Ubuntu)

``` bash
sudo apt update
sudo apt install docker.io -y
sudo systemctl start docker
sudo systemctl enable docker
docker --version
```

------------------------------------------------------------------------

## Step 2: Install Docker Compose

``` bash
sudo apt install docker-compose -y
docker-compose --version
```

------------------------------------------------------------------------

## Step 3: Fix Permissions

``` bash
sudo usermod -aG docker $USER
newgrp docker
```

------------------------------------------------------------------------

## Step 4: Create Project Folder

``` bash
mkdir ai-compose
cd ai-compose
```

------------------------------------------------------------------------

## Step 5: Create docker-compose.yml

``` bash
nano docker-compose.yml
```

Paste:

``` yaml
services:
  ollama:
    image: ollama/ollama
    container_name: ollama
    ports:
      - "11434:11434"
    command: serve
    restart: unless-stopped

  webui:
    image: ghcr.io/open-webui/open-webui:main
    container_name: webui
    ports:
      - "3000:8080"
    environment:
      - OLLAMA_BASE_URL=http://ollama:11434
    depends_on:
      - ollama
    restart: unless-stopped

  db:
    image: mongo:latest
    container_name: mongo_db
    ports:
      - "27017:27017"
    restart: unless-stopped
```

------------------------------------------------------------------------

## Step 6: Start Containers

``` bash
docker-compose up -d
```

------------------------------------------------------------------------

## Step 7: Verify Containers

``` bash
docker ps
```

Expected: - ollama - webui - mongo_db

------------------------------------------------------------------------

## Step 7.1: Restart WebUI (Important)

``` bash
docker restart webui
```

------------------------------------------------------------------------

## Step 8: Pull AI Model

``` bash
docker exec -it ollama ollama pull gemma:2b
```

------------------------------------------------------------------------

## Step 9: Open Web App

Open browser: http://localhost:3000

------------------------------------------------------------------------

## Step 10: Test

Type: What is AI?

------------------------------------------------------------------------

## Optional: Check Database

``` bash
docker exec -it mongo_db mongosh
```

------------------------------------------------------------------------

## Output

The Docker Compose setup successfully runs multiple containers including
an AI model (Ollama), frontend (WebUI), and database (MongoDB). The
system was tested via browser and produced correct responses.

------------------------------------------------------------------------

## Viva Points

-   Docker Compose manages multiple containers
-   Ollama provides pretrained AI model
-   WebUI is frontend interface
-   MongoDB acts as database
-   Containers communicate via internal network

------------------------------------------------------------------------

## Memory Commands

``` bash
docker-compose up -d
docker exec -it ollama ollama pull gemma:2b
docker restart webui
```
