# Task 2: DevOps — Product Catalogue

## Overview

This project implements a product catalogue REST API using Node.js, Express, TypeScript, PostgreSQL, and Prisma. The application is containerized with Docker and deployed to Kubernetes with scalable infrastructure and automated CI/CD.

## Technology Stack

* Node.js
* Express.js
* TypeScript
* PostgreSQL
* Prisma ORM
* Docker
* Kubernetes / Minikube
* NGINX Ingress
* GitHub Actions

## API Versions

### v1.0.0

Provides:

* `GET /health`
* `GET /products`

### v1.1.0

Adds:

* `GET /products/search?keyword=keyboard`

### v2.0.0

Enhances the search API with query parameters, pagination, validation, and error handling.

## Project Features

* Product catalogue management.
* PostgreSQL database with Prisma ORM.
* Multi-stage Docker build.
* Container health checks.
* Separate Kubernetes namespaces for each version.
* CPU and memory resource limits.
* Horizontal Pod Autoscaler.
* NGINX Ingress for version-based routing.
* Git version tags.
* GitHub Actions CI/CD pipeline.
* Integration tests.

## Local Setup

### 1. Install dependencies

```bash
npm install
```

### 2. Configure environment variables

Create a `.env` file:

```env
DATABASE_URL="postgresql://postgres:password@localhost:5432/catalogue_db"
PORT=3000
```

### 3. Set up the database

```bash
npx prisma generate
npx prisma migrate dev
npm run prisma:seed
```

### 4. Start the application

```bash
npm run dev
```

The application runs at:

`http://localhost:3000`

## Docker Setup

Build the image:

```bash
docker build -t product-catalogue:v2.0.0 .
```

Run the container:

```bash
docker run --env-file .env -p 3000:3000 product-catalogue:v2.0.0
```

Check the health endpoint:

```bash
curl http://localhost:3000/health
```

## Kubernetes Deployment

The Kubernetes manifests are located in the `kubernetes/` directory.

Deploy the namespaces, applications, services, HPA, and Ingress:

```bash
kubectl apply -f kubernetes/
```

Check running resources:

```bash
kubectl get pods -A
kubectl get services -A
kubectl get ingress -A
```

The application versions are routed using:

* `/v1`
* `/v1.1`
* `/v2`

## CI/CD Pipeline

GitHub Actions automates:

1. Installing dependencies.
2. Running tests.
3. Building Docker images.
4. Pushing images to Docker Hub or a private registry.
5. Deploying to Kubernetes.
6. Running integration tests after deployment.

Configure the required registry credentials and Kubernetes secrets in GitHub Actions.

## Version Management

The project uses semantic versioning:

* `v1.0.0`
* `v1.1.0`
* `v2.0.0`

Version history is maintained in `CHANGELOG.md`.

## Documentation

* `CHANGELOG.md` — Version history.
* `SYSTEM_DESIGN.md` — Architecture and design decisions.
* `Dockerfile` — Container build instructions.
* `kubernetes/` — Kubernetes deployment manifests.
* `.github/workflows/` — CI/CD pipeline configuration.

## Testing

Run the application tests:

```bash
npm test
```

## License

This project was developed as part of a backend and DevOps assignment.
