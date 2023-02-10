---
id: k15avpde27cy35vrrbvgfbx
title: Compose
desc: ''
updated: 1675682163130
created: 1675681078931
---

## Tips

Example for create a good docker-compose.yaml.

```yaml
version: '3.8'
services:

  postgres:
    image: postgres:14.4
    container_name: postgres
    restart: on-failure:2
    ports:
      - "5432:5432"
    volumes:
      - pgdata:/var/lib/postgresql/data
    environment:
      - POSTGRES_USER=admin
      - POSTGRES_PASSWORD=utileadmin
      - POSTGRES_MULTIPLE_DATABASES=keycloak,node
    networks:
      - example
    healthcheck:
      test: [ "CMD", "pg_isready" ]
      interval: 30s
      timeout: 20s
      retries: 3

  keycloak:
    image: jboss/keycloak:16.1.1
    container_name: keycloak
    restart: on-failure:2
    ports:
      - "8070:8080"
    depends_on:
      - postgres
    environment:
      - KEYCLOAK_USER=admin
      - KEYCLOAK_PASSWORD=admin
      - DB_VENDOR=postgres
      - DB_ADDR=postgres
      - DB_DATABASE=keycloak
      - DB_USER=keycloak
      - DB_PASSWORD=keycloak
    networks:
      - example

networks:
  example:


volumes:
  pgdata:
```

Build with and env file

```bash
docker-compose build --build-args $(cat envfile)
```