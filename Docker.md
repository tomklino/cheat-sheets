# Docker cheat sheet

* log into a container

```bash
docker exec -it <container-name> /bin/bash
```

* get ip of container

```bash
docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' <container-name>
```

* run a container with environment variables

```bash
docker run --name <name-of-container> --env <environment-variable>=<value-for-variable> -d <docker-image-name>
```
