# Kubernetes DevOps Project

This project demonstrates a producer-consumer system using RabbitMQ on Kubernetes. The system is designed to showcase various DevOps practices, including Dockerization, Helm chart deployment, and monitoring with Prometheus.

## Project Components

1. **RabbitMQ**: A message broker used to facilitate communication between the producer and consumer.
2. **Producer**: Sends messages to RabbitMQ.
3. **Consumer**: Receives messages from RabbitMQ and exposes metrics to Prometheus.

## Prerequisites

- Kubernetes cluster
- Helm installed
- Docker installed
- Prometheus and Grafana (optional for advanced monitoring)

## Deployment Instructions

### 1. Build Docker Images

Build the Docker images for both the producer and consumer services:

```bash
docker build -t <dockerhub_username>/producer:latest producer/
docker build -t <dockerhub_username>/consumer:latest consumer/

docker push <dockerhub_username>/producer:latest
docker push <dockerhub_username>/consumer:latest
```

### 2. Deploy RabbitMQ, Producer, and Consumer using Helm

Deploy RabbitMQ, Producer, and Consumer services using Helm:

```bash
helm upgrade --install rabbitmq ./helm-charts/rabbitmq --namespace default
helm upgrade --install producer ./helm-charts/producer --namespace default
helm upgrade --install consumer ./helm-charts/consumer --namespace default

```

### 3. Access the Consumer Metrics

Access the consumer metrics by port-forwarding the service:

```bash
kubectl port-forward svc/consumer 9422:9422 --namespace default
```

Open your browser and navigate to `http://localhost:9422/metrics` to view the consumer metrics.

Access the RabbitMQ management UI by port-forwarding the service:

```bash
kubectl port-forward svc/rabbitmq 15672:15672 --namespace default
```

Open your browser and navigate to `http://localhost:15672` to view the RabbitMQ management UI.
Use the default credentials: `guest`/`guest`.


### 4. Clean Up

To delete the deployed services, run the following Helm commands:

```bash
helm uninstall rabbitmq --namespace default
helm uninstall producer --namespace default
helm uninstall consumer --namespace default

```