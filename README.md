# Docker Voting App #

Run docker commands in the following sequence with --links

<!-- MarkdownTOC style="ordered" -->

1. [in-memory DB \(redis\)](#in-memory-db-redis)
1. [db \(PostgreSQL\)](#db-postgresql)
1. [voting-app \(python\)](#voting-app-python)
1. [result-app \(NodeJS\)](#result-app-nodejs)
1. [worker \(.NET\)](#worker-net)

<!-- /MarkdownTOC -->

## in-memory DB (redis) ##

```
docker run -d --name=redis redis
```

## db (PostgreSQL) ##

```
docker run -d --name-db postgres:9.4
```

## voting-app (python) ##

```
docker run -d --name=vote -p 5000:80 --link redis:redis voting-app
```

## result-app (NodeJS) ##

```
docker run -d --name=result -p 5001:80 --link db:db result-app
```

## worker (.NET) ##

```
docker run -d --name=worker --link db:db --link redis:redis worker
```
