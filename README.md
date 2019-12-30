# Docker Voting App #

## The Kubernetes Way

Run kubectl commands on GCP or AWS in the following sequence.

### voting-app (python)

```
kubectl create -f voting-app-pod.yml --record
kubectl create -f voting-app-service.yml --record
```

### in-memory DB (redis)

```
kubectl create -f redis-pod.yml --record
kubectl create -f redis-service.yml --record
```

### db (PostgreSQL)

```
kubectl create -f postgres-pod.yml --record
kubectl create -f postgres-service.yml --record
```

### worker (.NET)

No service here because no other components rely on the worker pod.

```
kubectl create -f worker-app-pod.yml --record
```

### result-app (NodeJS)

```
kubectl create -f result-app-pod.yml --record
kubectl create -f result-app-service.yml --record
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
