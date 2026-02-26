# local-nexus-proxy-cache

Docker Compose setup for running a local Nexus proxy and cache.

## Features

- Runs Sonatype Nexus 3 in a Docker container
- Persists data in a local volume
- Accessible on port 8081

## Usage

1. Start the service:
   ```bash
   docker-compose up -d
   ```

2. Access Nexus at http://localhost:8081

3. Stop the service:
   ```bash
   docker-compose down
   ```

## Configuration

The data directory `nexus-data` will be created automatically and persists between runs.

## Security

For production use, ensure you:
- Change the default admin password
- Configure proper network security
- Use HTTPS in production