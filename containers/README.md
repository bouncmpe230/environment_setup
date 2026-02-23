# Docker Container Instructions

This guide explains how to use the Spring 26 development container either by building it directly with Docker or using VS Code's Dev Containers feature.

## Method 1: Building with Docker directly

To build and run the Docker container using the terminal:

1. Navigate to the spring26 directory:
   ```bash
   cd containers/spring26
   ```

2. Build the Docker image:
   ```bash
   docker build -t spring26-dev .
   ```

3. Run the container:
   ```bash
   docker run -it --rm spring26-dev
   ```

## Method 2: Using VS Code Dev Containers

For a more integrated development experience, you can use VS Code's Dev Containers feature:

1. Install the prerequisites:
   - [VS Code](https://code.visualstudio.com/)
   - [Docker Desktop](https://www.docker.com/products/docker-desktop)
   - [Dev Containers extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)

2. Open this project in VS Code

3. When prompted, click "Reopen in Container" or:
   - Press `F1` or `Ctrl+Shift+P`
   - Type "Dev Containers: Reopen in Container"
   - Press Enter

VS Code will build the container and create a fully configured development environment automatically.

## Additional Notes

- The Dev Container configuration is defined in `.devcontainer/devcontainer.json`
- The Docker configuration is defined in `containers/spring25/Dockerfile`
- Any changes to these files will require rebuilding the container


## Multi-architecture build and Dockerhub 



```bash
docker buildx create --name multiarch-builder --use
docker buildx inspect --bootstrap
```

```bash
docker login 
```


```bash
docker buildx build \
  --platform linux/amd64,linux/arm64 \
  -t <your-dockerhub-username>/cmpe230-spring26:v1 \
  -t <your-dockerhub-username>/cmpe230-spring26:latest \
  --push \
  .
```
