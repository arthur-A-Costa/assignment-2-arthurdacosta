# Git and Docker Starter Application

This repository contains a small Python web application used to practice Git, GitHub, and Docker workflows.

## Application

The application listens on port 8000 and returns a text response when accessed over HTTP.

## Verification

The running application should be verified using an HTTP request to port 8000.

## Usage

### Build the Application

Build the Docker image:

    docker build -t git-docker-app:test .

### Run the Application

Run the container and expose application port 8000 on host port 8080:

    docker run -d --name app-test -p 8080:8000 git-docker-app:test

### Test the Application

Verify that the application responds:

    curl http://localhost:8080

The response should include the application's health status.

### Stop and Remove the Container

    docker stop app-test
    docker rm app-test

### Docker Network Verification

Create a Docker network:

    docker network create app-net

Run the application on that network:

    docker run -d --name app-test --network app-net git-docker-app:test

Test container-to-container communication by name:

    docker run --rm --name network-test --network app-net curlimages/curl:8.5.0 http://app-test:8000

Clean up:

    docker rm -f app-test
    docker network rm app-net
