# Docker Voting App

__The Kubernetes Way__

  1. [voting-app (python)](#voting-app-python)
  1. [in-memory DB (redis)](#in-memory-db-redis)
  1. [db (PostgreSQL)](#db-postgresql)
  1. [worker (.NET)](#worker-net)
  1. [result-app (NodeJS)](#result-app-nodejs)

__The Docker Way__

  1. [in-memory DB (redis)](#in-memory-db-redis-1)
  1. [db (PostgreSQL)](#db-postgresql-1)
  1. [voting-app (python)](#voting-app-python-1)
  1. [result-app (NodeJS)](#result-app-nodejs-1)
  1. [worker (.NET)](#worker-net-1)

## The Kubernetes Way

Run kubectl commands on GCP or AWS in the following sequence.

### voting-app (python)

```
kubectl create -f voting-app-pod.yml
kubectl create -f voting-app-service.yml
```

### in-memory DB (redis)

```
kubectl create -f redis-pod.yml
kubectl create -f redis-service.yml
```

### db (PostgreSQL)

```
kubectl create -f postgres-pod.yml
kubectl create -f postgres-service.yml
```

### worker (.NET)

No service here because no other components rely on the worker pod.

```
kubectl create -f worker-app-pod.yml
```

### result-app (NodeJS)

```
kubectl create -f result-app-pod.yml
kubectl create -f result-app-service.yml
```

## The Docker Way

Run docker commands in the following sequence with --links

### in-memory DB (redis)

```
docker run -d --name=redis redis
```

### db (PostgreSQL)

```
docker run -d --name-db postgres:9.4
```

### voting-app (python)

```
docker run -d --name=vote -p 5000:80 --link redis:redis voting-app
```

### result-app (NodeJS)

```
docker run -d --name=result -p 5001:80 --link db:db result-app
```

### worker (.NET)

```
docker run -d --name=worker --link db:db --link redis:redis worker
```
