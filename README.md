# Docker Development Environments

This repository contains Docker configurations for setting up local development environments for various services.

## Available Services

### Redis
A local Redis instance using Docker. Located in the `redis-docker` directory.

Key features:
- Redis 8.0.1 running on Alpine Linux
- Data persistence enabled (AOF)
- Exposed on port 6379

[View Redis Setup Details](redis-docker/README.md)

### MySQL
A local MySQL instance using Docker. Located in the `mysql-docker` directory.

Key features:
- MySQL 8.0
- Pre-configured database and user
- Data persistence using Docker volumes
- Exposed on port 3306

[View MySQL Setup Details](mysql-docker/README.md)

## Prerequisites

- Docker
- Docker Compose

### Installation on macOS/Linux (using Homebrew)

If you're using macOS or Linux with Homebrew installed, you can install Docker and Docker Compose with:

```bash
# Install Docker Desktop (includes Docker Engine and Docker Compose)
brew install --cask docker

# After installation:
# 1. Open Docker Desktop from your Applications folder
# 2. Wait for it to start up (you'll see the Docker icon in your menu bar)
# 3. Accept the terms and conditions when prompted
```

## Usage

Each service has its own directory with specific instructions. Navigate to the service directory you want to use and follow the instructions in its README.md file.

### Quick Start

1. Choose a service (Redis or MySQL)
2. Navigate to its directory:
   ```bash
   cd redis-docker    # for Redis
   # or
   cd mysql-docker    # for MySQL
   ```
3. Start the service:
   ```bash
   docker-compose up -d
   ```
4. Follow the specific instructions in the service's README.md for testing and usage

## Stopping Services

To stop a service, navigate to its directory and run:
```bash
docker-compose down
```
