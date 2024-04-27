pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        sh '''#!/bin/bash

# Define variables
DOCKER_IMAGE="your-docker-image-name"
DOCKER_TAG="latest"
DOCKERFILE_PATH="src/emailservice/Dockerfile"
WORKSPACE_PATH="/home/email_server"
REGISTRY_URL="cmupro7"  # Set this to your Docker registry URL if you want to push the image
REGISTRY_CREDENTIALS="new@12345"  # Add your Docker registry credentials

# Build the Docker image using the Dockerfile
echo "Building Docker image: $DOCKER_IMAGE:$DOCKER_TAG..."
docker build -t "$DOCKER_IMAGE:$DOCKER_TAG" -f "$DOCKERFILE_PATH" "$WORKSPACE_PATH"

# Optionally push the Docker image to a registry
if [ ! -z "$REGISTRY_URL" ]; then
    echo "Pushing Docker image to registry: $REGISTRY_URL..."
    # Login to the Docker registry
    docker login -u "$REGISTRY_USERNAME" -p "$REGISTRY_PASSWORD" "$REGISTRY_URL"
    # Tag the Docker image
    docker tag "$DOCKER_IMAGE:$DOCKER_TAG" "$REGISTRY_URL/$DOCKER_IMAGE:$DOCKER_TAG"
    # Push the Docker image
    docker push "$REGISTRY_URL/$DOCKER_IMAGE:$DOCKER_TAG"
    # Logout of the Docker registry
    docker logout "$REGISTRY_URL"
fi

echo "Artifact build and deployment completed."
'''
      }
    }

  }
}