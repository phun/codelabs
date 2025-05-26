# Local Kafka Docker Setup

This directory contains the necessary files to run a local Kafka instance using Docker.

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

## Running Kafka

To start the Kafka server and Zookeeper:

```bash
docker-compose up -d
```

To stop the services:

```bash
docker-compose down
```

## Connection Details

- Kafka Broker: localhost:9092
- Zookeeper: localhost:2181

## Features

- Kafka 7.5.3 (Confluent Platform)
- Zookeeper 7.5.3
- Single broker setup
- Data persistence using Docker volumes
- Exposed on standard Kafka and Zookeeper ports

## Testing the Setup

### 1. Create a Topic

```bash
docker exec -it kafka-docker-kafka-1 kafka-topics --create \
    --topic test-topic \
    --bootstrap-server localhost:9092 \
    --partitions 1 \
    --replication-factor 1
```

### 2. List Topics

```bash
docker exec -it kafka-docker-kafka-1 kafka-topics --list \
    --bootstrap-server localhost:9092
```

### 3. Produce Messages

```bash
docker exec -it kafka-docker-kafka-1 kafka-console-producer \
    --topic test-topic \
    --bootstrap-server localhost:9092
```

### 4. Consume Messages

```bash
docker exec -it kafka-docker-kafka-1 kafka-console-consumer \
    --topic test-topic \
    --bootstrap-server localhost:9092 \
    --from-beginning
```

## Exercise: Basic Message Flow

1. Open two terminal windows
2. In the first terminal, start the consumer:
   ```bash
   docker exec -it kafka-docker-kafka-1 kafka-console-consumer \
       --topic test-topic \
       --bootstrap-server localhost:9092 \
       --from-beginning
   ```
3. In the second terminal, start the producer:
   ```bash
   docker exec -it kafka-docker-kafka-1 kafka-console-producer \
       --topic test-topic \
       --bootstrap-server localhost:9092
   ```
4. Type messages in the producer terminal and watch them appear in the consumer terminal

## Monitoring

You can check the status of the containers:

```bash
docker-compose ps
```

View logs:

```bash
# Kafka logs
docker-compose logs kafka

# Zookeeper logs
docker-compose logs zookeeper
```

## Further Reading

- [Kafka Documentation](https://kafka.apache.org/documentation/)
- [Confluent Platform Documentation](https://docs.confluent.io/platform/current/overview.html)
- [Kafka Console Producer/Consumer](https://kafka.apache.org/documentation/#basic_ops_console_producer) 
