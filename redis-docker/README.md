# Local Redis Docker Setup

This directory contains the necessary files to run a local Redis instance using Docker.

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

## Running Redis

To start the Redis server:

```bash
docker-compose up -d
```

To stop the Redis server:

```bash
docker-compose down
```

## Connection Details

- Host: localhost
- Port: 6379
- No password required by default

## Features

- Redis 8.0.1 running on Alpine Linux
- Data persistence enabled (AOF)
- Data stored in a Docker volume
- Exposed on standard Redis port (6379)

## Testing the Connection

You can test the connection using the Redis CLI:

```bash
docker exec -it redis-docker-redis-1 redis-cli
```

Then try some basic commands:
```
PING
SET test "Hello Redis"
GET test
``` 
