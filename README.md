# Flask Docker GitHub Actions Project

## Overview
This is a Flask web application configured with Docker and automated CI/CD using GitHub Actions. The project demonstrates a robust deployment pipeline with testing, building, and deployment to staging and production environments.

## Features
- Flask web application
- Docker containerization
- MongoDB integration
- Continuous Integration and Continuous Deployment (CI/CD)
- Automated testing
- Staging and Production deployment workflows

## Prerequisites
- Docker
- Docker Compose
- GitHub Account
- DockerHub Account

## Project Structure
```
.
├── .github/workflows/main.yml    # GitHub Actions workflow configuration
├── Dockerfile                    # Docker image build configuration
├── docker-compose.yml            # Docker Compose configuration
└── app/                          # Flask application source code
```

## CI/CD Workflow
The GitHub Actions workflow (`main.yml`) implements the following stages:

### 1. Test Stage
- Runs on every push to `main` and `prod` branches
- Builds and runs tests using Docker Compose
- Ensures code quality before proceeding to build

### 2. Build and Push Stage
- Builds Docker image
- Pushes image to DockerHub
- Tags image with git commit hash or tag

### 3. Deployment Stages
#### Staging Deployment
- Triggered on pushes to `main` branch
- Deploys to a staging EC2 instance
- Sets up Docker network and MongoDB
- Pulls and runs the latest image

#### Production Deployment
- Triggered on version tags (e.g., `v1.0.0`)
- Deploys to production EC2 instance
- Similar setup to staging with production-specific configurations

## Environment Variables
- `MONGO_URI`: MongoDB connection string
- `JWT_SECRET_KEY`: Secret key for JWT authentication
- `MONGO_DB_NAME`: MongoDB database name

## Docker Configuration
- Uses a custom Docker network (`flask-app-network`)
- Persistent MongoDB data volume
- Exposes application on port 8000

## Secrets Configuration
Configure the following secrets in your GitHub repository:
- `DOCKERHUB_USERNAME`: DockerHub username
- `DOCKERHUB_TOKEN`: DockerHub access token
- `EC2_HOST_IP`: Staging EC2 instance IP
- `PROD_EC2_HOST_IP`: Production EC2 instance IP
- `EC2_USER_NAME`: EC2 instance username
- `EC2_SSH_KEY`: SSH private key for EC2 access
- `JWT_SECRET_KEY`: Application JWT secret

## Local Development
1. Clone the repository
2. Create a `.env` file with necessary environment variables
3. Run `docker-compose up --build`

## Deployment
- Pushes to `main` trigger staging deployment
- Version tags (e.g., `v1.0.0`) trigger production deployment

