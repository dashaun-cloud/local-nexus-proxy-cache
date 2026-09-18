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

## Client Configuration

Templates for pointing Maven and Gradle at the local Nexus live in `client-config/`. Copy the relevant one and replace `maven-group` with the name of the Nexus group repository you created (the group repo proxies your team's remotes, e.g. Maven Central).

### Maven

```bash
cp client-config/maven/settings.xml ~/.m2/settings.xml
```

Edit `~/.m2/settings.xml` and set the `url` to your group repository, e.g. `http://localhost:8081/repository/maven-group`. All Maven repositories are mirrored through the local Nexus.

### Gradle

```bash
cp client-config/gradle/init.gradle ~/.gradle/init.gradle
```

Edit `~/.gradle/init.gradle` and set the `url` to your group repository. This prepends the local Nexus repository to every project's repositories.

If your Nexus requires authentication, uncomment the `<server>` / `credentials` blocks in the templates.

## Security

For production use, ensure you:
- Change the default admin password
- Configure proper network security
- Use HTTPS in production