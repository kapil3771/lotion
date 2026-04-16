# Kubernetes Auto-Scaling AI App (Minikube) - Beginner Friendly

## Aim

To implement auto-scaling for an AI application on Kubernetes and
monitor its health and performance.

------------------------------------------------------------------------

## Step 1: Start Minikube

``` bash
minikube start --driver=docker
kubectl get nodes
```

------------------------------------------------------------------------

## Step 2: Create Project Folder

``` bash
mkdir ai-k8s-app
cd ai-k8s-app
```

------------------------------------------------------------------------

## Step 3: Create AI Application

``` bash
nano app.py
```

``` python
from flask import Flask, request, jsonify
app = Flask(__name__)

@app.route("/")
def home():
    return "AI Model Running in Kubernetes"

@app.route("/predict", methods=["POST"])
def predict():
    data = request.json["number"]
    return jsonify({"result": data * 2})

app.run(host="0.0.0.0", port=5000)
```

------------------------------------------------------------------------

## Step 4: Create requirements.txt

``` bash
nano requirements.txt
```

    flask

------------------------------------------------------------------------

## Step 5: Create Dockerfile

``` bash
nano Dockerfile
```

``` dockerfile
FROM python:3.9
WORKDIR /app
COPY . .
RUN pip install -r requirements.txt
EXPOSE 5000
CMD ["python","app.py"]
```

------------------------------------------------------------------------

## Step 6: Connect Docker to Minikube

``` bash
eval $(minikube docker-env)
```

------------------------------------------------------------------------

## Step 7: Build Image

``` bash
docker build -t ai-model .
docker images
```

------------------------------------------------------------------------

## Step 8: Create Deployment

``` bash
nano deployment.yaml
```

``` yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: ai-app
spec:
  replicas: 2
  selector:
    matchLabels:
      app: ai-app
  template:
    metadata:
      labels:
        app: ai-app
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

## Step 9: Create Service

``` bash
nano service.yaml
```

``` yaml
apiVersion: v1
kind: Service
metadata:
  name: ai-service
spec:
  type: NodePort
  selector:
    app: ai-app
  ports:
    - port: 5000
      targetPort: 5000
      nodePort: 30007
```

``` bash
kubectl apply -f service.yaml
kubectl get svc
```

------------------------------------------------------------------------

## Step 10: Access App

``` bash
minikube service ai-service
```

------------------------------------------------------------------------

## Step 11: Enable Metrics Server

``` bash
minikube addons enable metrics-server
kubectl top pods
```

------------------------------------------------------------------------

## Step 12: Enable Auto Scaling

``` bash
kubectl autoscale deployment ai-app --cpu-percent=50 --min=2 --max=5
kubectl get hpa
```

------------------------------------------------------------------------

## Step 13: Generate Load

``` bash
for i in {1..50}; do curl $(minikube service ai-service --url); done
```

------------------------------------------------------------------------

## Step 14: Monitor Scaling

``` bash
kubectl get pods
kubectl top pods
kubectl top nodes
```

------------------------------------------------------------------------

## Step 15: Debug (Optional)

``` bash
kubectl logs <pod-name>
kubectl describe pod <pod-name>
```

------------------------------------------------------------------------

## Output

AI application deployed, auto-scaled, and monitored successfully.

------------------------------------------------------------------------

## Memory Commands

``` bash
minikube start
docker build -t ai-model .
kubectl apply -f deployment.yaml
kubectl autoscale deployment ai-app
kubectl get hpa
```
