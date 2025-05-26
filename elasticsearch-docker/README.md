# Local Elasticsearch Docker Setup

This directory contains the necessary files to run a local Elasticsearch instance using Docker.

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

## Running Elasticsearch

To start the Elasticsearch server:

```bash
docker-compose up -d
```

To stop the server:

```bash
docker-compose down
```

## Connection Details

- Host: localhost
- Port: 9200
- Security: Disabled (for development purposes)

## Features

- Elasticsearch 8.12.1
- Single node setup
- Data persistence using Docker volumes
- Memory limit set to 512MB
- Exposed on standard Elasticsearch port (9200)

## Testing the Setup

### 1. Check Cluster Health

```bash
curl http://localhost:9200/_cluster/health
```

### 2. Create an Index

```bash
curl -X PUT "http://localhost:9200/my-index"
```

### 3. Add a Document

```bash
curl -X POST "http://localhost:9200/my-index/_doc" \
     -H "Content-Type: application/json" \
     -d '{"title": "Test Document", "content": "This is a test document"}'
```

### 4. Search Documents

```bash
curl "http://localhost:9200/my-index/_search?q=test"
```

## Exercise: Basic CRUD Operations

1. Create an index:
   ```bash
   curl -X PUT "http://localhost:9200/books"
   ```

2. Add a document:
   ```bash
   curl -X POST "http://localhost:9200/books/_doc" \
        -H "Content-Type: application/json" \
        -d '{
          "title": "The Great Gatsby",
          "author": "F. Scott Fitzgerald",
          "year": 1925
        }'
   ```

3. Get the document:
   ```bash
   curl "http://localhost:9200/books/_search?q=Gatsby"
   ```

4. Update the document:
   ```bash
   curl -X POST "http://localhost:9200/books/_update/1" \
        -H "Content-Type: application/json" \
        -d '{
          "doc": {
            "year": 1926
          }
        }'
   ```

5. Delete the document:
   ```bash
   curl -X DELETE "http://localhost:9200/books/_doc/1"
   ```

## Monitoring

You can check the status of the container:

```bash
docker-compose ps
```

View logs:

```bash
docker-compose logs elasticsearch
```

## Further Reading

- [Elasticsearch Documentation](https://www.elastic.co/guide/en/elasticsearch/reference/current/index.html)
- [Elasticsearch REST API](https://www.elastic.co/guide/en/elasticsearch/reference/current/rest-apis.html)
- [Elasticsearch Docker Guide](https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html) 
