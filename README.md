# Docker User Profile Demo

A tutorial user profile application with plain HTML/JavaScript, an Express backend, MongoDB, and a Mongo Express administration UI.

## Requirements

Docker with Docker Compose. The supplied Dockerfile uses the historical Node 13 Alpine image; review its compatibility before maintaining this demo.

## Getting started

```sh
docker build -t my-app:1.0 .
docker compose -f docker-compose.yaml up -d mongodb mongo-express
```

The Compose file points its application service at a historical private ECR image. To use your local build, create an untracked override file and start the application with both files:

```yaml
# compose.local.yaml
services:
  my-app:
    image: my-app:1.0
```

```sh
docker compose -f docker-compose.yaml -f compose.local.yaml up -d my-app
```

## Project structure

| Path | Purpose |
| --- | --- |
| `app/server.js` | Express profile endpoints, port 3000 |
| `app` | Frontend and Node dependency manifest |
| `docker-compose.yaml` | MongoDB and Mongo Express services |
| `Dockerfile` | Application container build |
| `Jenkinsfile` | Example pipeline |

## Configuration and limitations

Run the application UI at port 3000; Compose publishes Mongo Express on port 8080. The server currently uses the Docker-only hostname `mongodb`, the `my-db` database, and the `users` collection. Its local MongoDB URL is declared but not used, so simply running `node server.js` on the host does not provide working profile requests. The example contains tutorial credentials/connection strings; keep it isolated and replace them before non-demo use.

## Development and validation

Exercise `/get-profile` and `/update-profile` with a disposable database. Build the demo image with `docker build -t my-app:1.0 .` from the repository root. No meaningful automated npm test suite is documented.

## License

No root-level license file is included. Check source-specific notices and obtain permission before redistribution or reuse.
