1. Build and Run with Docker

First, I created a Dockerfile for the Next.js app and built the image:

docker build -t gittu1912/nextjs-blog .


To test it locally:

docker run -p 3000:3000 gittu1912/nextjs-blog


The app runs on http://localhost:3000
.

2. Push Image to Docker Hub

I pushed the image to Docker Hub so it can be pulled by Kubernetes:

docker push gittu1912/nextjs-blog:latest


Note: My Docker Hub credentials are stored securely as GitHub Action secrets to automate builds and pushes.

3. Deploy on Kubernetes (Minikube)

I installed Minikube locally on Ubuntu to run Kubernetes clusters:

minikube start


Then I created a Deployment and Service for my app.

deployment.yaml

apiVersion: apps/v1
kind: Deployment
metadata:
  name: nextjs-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nextjs
  template:
    metadata:
      labels:
        app: nextjs
    spec:
      containers:
        - name: nextjs-container
          image: gittu1912/nextjs-blog:latest
          ports:
            - containerPort: 3000
---
apiVersion: v1
kind: Service
metadata:
  name: nextjs-service
spec:
  selector:
    app: nextjs
  ports:
    - protocol: TCP
      port: 80
      targetPort: 3000
  type: LoadBalancer


Apply the deployment:

kubectl apply -f deployment.yaml

4. Check Pods and Service

Verify pods are running:

kubectl get pods


Check the service:

kubectl get svc


If using Minikube, open the app in your browser:

minikube service nextjs-service

5. Access the App

Once the service is running, open the external IP or Minikube URL to see the Next.js blog live locally 🚀

6. CI/CD Automation (Optional)

Using GitHub Actions, I configured the workflow to:

Build the Docker image.

Push it to Docker Hub using credentials stored in GitHub Secrets.

Deploy to Kubernetes automatically (if needed).
