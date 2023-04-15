# `docker`

## List containers

```bash
docker ps -a
```

## Postgres

```bash
sudo docker run --name postgres -e POSTGRES_PASSWORD=postgres -p 5432:5432 -d postgres
```

## PgAdmin 4

```bash
sudo docker run --name pgadmin -e 'PGADMIN_LISTEN_PORT=5050' -e PGADMIN_DEFAULT_EMAIL=example.com -e PGADMIN_DEFAULT_PASSWORD=admin -p 5050:5050 -d dpage/pgadmin4
```
