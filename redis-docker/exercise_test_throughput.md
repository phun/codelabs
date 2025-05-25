# Testing Redis Throughput

This exercise demonstrates how to test Redis throughput using IO threads and the redis-benchmark tool.

## Prerequisites

- Redis server running (from our Docker setup)
- Basic understanding of Redis commands

## Understanding IO Threads

Redis 6.0+ introduced IO threads, which can improve performance by handling read/write operations in parallel. By default, Redis uses a single thread for all operations.

## Testing Throughput

### 1. Start Redis with IO Threads

Our Redis container is configured to use IO threads through command line arguments in the docker-compose.yml:

```yaml
services:
  redis:
    build:
      context: .
      dockerfile: Dockerfile
    ports:
      - "6379:6379"
    volumes:
      - redis_data:/data
    command: redis-server --io-threads 4 --io-threads-do-reads yes --appendonly yes
```

### 2. Using redis-benchmark

The `redis-benchmark` tool is included with Redis and can be used to test throughput. Here are some example commands:

#### Basic Throughput Test
```bash
# Test SET operations
docker exec -it redis-docker-redis-1 redis-benchmark -t set -n 100000

# Test GET operations
docker exec -it redis-docker-redis-1 redis-benchmark -t get -n 100000

# Test multiple operations
docker exec -it redis-docker-redis-1 redis-benchmark -t set,get -n 100000
```

#### Advanced Testing
```bash
# Test with 50 parallel clients
docker exec -it redis-docker-redis-1 redis-benchmark -t set,get -n 100000 -c 50

# Test with pipelining (16 commands per request)
docker exec -it redis-docker-redis-1 redis-benchmark -t set,get -n 100000 -P 16

# Test with specific data size (1000 bytes)
docker exec -it redis-docker-redis-1 redis-benchmark -t set,get -n 100000 -d 1000
```

### 3. Comparing Performance

To compare performance with and without IO threads:

1. First, test without IO threads:
```bash
# Stop current container
docker-compose down

# Start without IO threads (modify docker-compose.yml to remove IO thread arguments)
docker-compose up -d

# Run benchmark
docker exec -it redis-docker-redis-1 redis-benchmark -t set,get -n 100000 -c 50
```

2. Then test with IO threads:
```bash
# Stop container
docker-compose down

# Start with IO threads (restore IO thread arguments in docker-compose.yml)
docker-compose up -d

# Run benchmark
docker exec -it redis-docker-redis-1 redis-benchmark -t set,get -n 100000 -c 50
```

## Understanding the Results

The benchmark output shows:
- Requests per second
- Latency statistics
- Throughput in MB/s

Example output:
```
====== SET ======
  100000 requests completed in 2.00 seconds
  50 parallel clients
  3 bytes payload
  keep alive: 1
  host configuration "save": 3600 1 300 100 60 10000
  host configuration "appendonly": yes
  multi-thread: yes

Latency by percentile distribution:
0.000% <= 0.103 milliseconds (cumulative count 1)
50.000% <= 0.207 milliseconds (cumulative count 50023)
75.000% <= 0.303 milliseconds (cumulative count 75018)
87.500% <= 0.407 milliseconds (cumulative count 87509)
93.750% <= 0.503 milliseconds (cumulative count 93755)
96.875% <= 0.607 milliseconds (cumulative count 96877)
98.438% <= 0.703 milliseconds (cumulative count 98438)
99.219% <= 0.807 milliseconds (cumulative count 99219)
99.609% <= 0.903 milliseconds (cumulative count 99609)
99.805% <= 1.007 milliseconds (cumulative count 99805)
99.902% <= 1.103 milliseconds (cumulative count 99902)
99.951% <= 1.207 milliseconds (cumulative count 99951)
99.976% <= 1.303 milliseconds (cumulative count 99976)
99.988% <= 1.407 milliseconds (cumulative count 99988)
99.994% <= 1.503 milliseconds (cumulative count 99994)
99.997% <= 1.607 milliseconds (cumulative count 99997)
99.998% <= 1.703 milliseconds (cumulative count 99998)
99.999% <= 1.807 milliseconds (cumulative count 99999)
100.000% <= 1.903 milliseconds (cumulative count 100000)

Summary:
  throughput summary: 50000.00 requests per second
  latency summary (msec):
          avg       min       p50       p95       p99       max
        0.207     0.104     0.207     0.407     0.703     1.903
```

## Exercise Tasks

1. Run the basic throughput tests and record the results
2. Compare performance with different numbers of IO threads (2, 4, 8)
3. Test with different client counts (10, 50, 100)
4. Test with different pipeline sizes (1, 16, 32)
5. Create a table comparing the results

## Tips for Accurate Testing

1. Run tests multiple times and take averages
2. Ensure no other heavy processes are running
3. Test with different data sizes
4. Monitor system resources during tests
5. Consider network latency if testing remotely

## Further Reading

- [Redis IO Threads Documentation](https://redis.io/topics/io-threads)
- [redis-benchmark Documentation](https://redis.io/topics/benchmarks)
- [Redis Performance Optimization](https://redis.io/topics/optimization) 
