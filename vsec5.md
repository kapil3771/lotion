# Dockerized AI Model using Ollama (Gemma 2B)

## Aim

To create a Docker container for a pretrained AI model and test it
locally for consistent performance.

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

## Step 2: Fix Permissions (Optional)

``` bash
sudo usermod -aG docker $USER
newgrp docker
```

------------------------------------------------------------------------

## Step 3: Create Project Folder

``` bash
mkdir ai-docker
cd ai-docker
```

------------------------------------------------------------------------

## Step 4: Create Dockerfile

``` bash
nano Dockerfile
```

Paste:

    FROM ollama/ollama
    CMD ["serve"]

------------------------------------------------------------------------

## Step 5: Build Docker Image

``` bash
docker build -t my-ai-model .
```

------------------------------------------------------------------------

## Step 6: Run Container

``` bash
docker run -d -p 11434:11434 --name mycontainer my-ai-model
```

------------------------------------------------------------------------

## Step 7: Pull Model Inside Container (IMPORTANT)

``` bash
docker exec -it mycontainer ollama pull gemma:2b
```

------------------------------------------------------------------------

## Step 8: Run Model (Optional)

``` bash
docker exec -it mycontainer ollama run gemma:2b
```

------------------------------------------------------------------------

## Step 9: Test

Type:

    What is AI?

------------------------------------------------------------------------

## Output

The Docker container runs Ollama server successfully and executes the
Gemma 2B model inside the container.

------------------------------------------------------------------------

## Viva Points

-   Docker ensures consistent environment\
-   Ollama provides pretrained LLM\
-   Model runs inside container\
-   No host installation required\
-   Fully containerized AI deployment

------------------------------------------------------------------------

## Memory Commands

``` bash
docker build -t my-ai-model .
docker run -d -p 11434:11434 my-ai-model
docker exec -it mycontainer ollama pull gemma:2b
```
