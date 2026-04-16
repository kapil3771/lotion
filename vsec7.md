# Kubernetes AI Deployment using Minikube (Beginner Friendly)

## Aim

Set up a local Kubernetes cluster using Minikube and deploy & scale a
Dockerized AI application.

------------------------------------------------------------------------

## Step 1: Install Docker

``` bash
sudo apt update
sudo apt install docker.io -y
sudo systemctl start docker
sudo systemctl enable docker
```

``` bash
sudo usermod -aG docker $USER
newgrp docker
```

``` bash
docker --version
docker ps
```

------------------------------------------------------------------------

## Step 2: Install kubectl

``` bash
sudo snap install kubectl --classic
kubectl version --client
```

------------------------------------------------------------------------

## Step 3: Install Minikube

``` bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
minikube version
```

------------------------------------------------------------------------

## Step 4: Start Cluster

``` bash
minikube start
kubectl get nodes
```

------------------------------------------------------------------------

## Step 5: Create Project

``` bash
mkdir ai-kubernetes
cd ai-kubernetes
```

------------------------------------------------------------------------

## Step 6: Create AI App

``` bash
nano app.py
```

``` python
from flask import Flask, request, jsonify
app = Flask(__name__)

@app.route('/')
def home():
    return "AI Model Running Successfully"

@app.route('/predict', methods=['POST'])
def predict():
    data = request.json['number']
    return jsonify({'result': data * 2})

app.run(host="0.0.0.0", port=5000)
```

------------------------------------------------------------------------

## Step 7: Requirements File

``` bash
nano requirements.txt
```

    flask

------------------------------------------------------------------------

## Step 8: Dockerfile

``` bash
nano Dockerfile
```

``` dockerfile
FROM python:3.10
WORKDIR /app
COPY . .
RUN pip install -r requirements.txt
EXPOSE 5000
CMD ["python","app.py"]
```

------------------------------------------------------------------------

## Step 9: Build Image

``` bash
eval $(minikube docker-env)
docker build -t ai-model .
```

------------------------------------------------------------------------

## Step 10: Deployment

``` bash
nano deployment.yaml
```

``` yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: ai-model-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: ai-model
  template:
    metadata:
      labels:
        app: ai-model
    spec:
      containers:
        - name: ai-container
          image: ai-model
          imagePullPolicy: Never
          ports:
            - containerPort: 5000
```

``` bash
kubectl apply -f deployment.yaml
kubectl get pods
```

------------------------------------------------------------------------

## Step 11: Service

``` bash
nano service.yaml
```

``` yaml
apiVersion: v1
kind: Service
metadata:
  name: ai-model-service
spec:
  type: NodePort
  selector:
    app: ai-model
  ports:
    - port: 5000
      targetPort: 5000
      nodePort: 30007
```

``` bash
kubectl apply -f service.yaml
kubectl get services
```

------------------------------------------------------------------------

## Step 12: Access App

``` bash
minikube service ai-model-service
```

------------------------------------------------------------------------

## Step 13: Scale

``` bash
kubectl scale deployment ai-model-deployment --replicas=5
kubectl get pods
```

------------------------------------------------------------------------

## Step 14: Dashboard

``` bash
minikube dashboard
```

------------------------------------------------------------------------

## Output

Application deployed and scaled successfully on Kubernetes.

------------------------------------------------------------------------

## Memory Commands

``` bash
minikube start
docker build -t ai-model .
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
minikube service ai-model-service
```
