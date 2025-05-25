# Local MySQL Docker Setup

This directory contains the necessary files to run a local MySQL instance using Docker.

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

## Running MySQL

To start the MySQL server:

```bash
docker-compose up -d
```

To stop the MySQL server:

```bash
docker-compose down
```

## Connection Details

- Host: localhost
- Port: 3306
- Root Password: root
- Database: mydb
- Username: user
- Password: password

## Features

- MySQL 8.0
- Data persistence using Docker volumes
- Pre-configured database and user
- Native password authentication enabled
- Exposed on standard MySQL port (3306)

## Testing the Connection

You can test the connection using the MySQL CLI:

```bash
docker exec -it mysql-docker-mysql-1 mysql -uuser -ppassword mydb
```

Then try some basic commands:
```sql
SHOW TABLES;
CREATE TABLE test (id INT, name VARCHAR(50));
INSERT INTO test VALUES (1, 'Hello MySQL');
SELECT * FROM test;
```

## Using MySQL Workbench or Other Clients

You can connect to the MySQL server using any MySQL client with these credentials:
- Host: localhost
- Port: 3306
- Username: user
- Password: password
- Database: mydb 
