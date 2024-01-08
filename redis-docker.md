Sharing this for other users:

## Volume

```shell
docker volume create redis-data
```

## Running

```shell
docker run -d \
  -h redis \
  -e REDIS_PASSWORD=redis \
  -v redis-data:/data \
  -p 6379:6379 \
  --name redis \
  --restart always \
  redis:latest /bin/sh -c 'redis-server --appendonly yes --requirepass ${REDIS_PASSWORD}'
```
or
```shell
docker run -d \
  -h redis \
  -v redis-data:/data \
  -p 6379:6379 \
  --name redis \
  --restart always \
  redis:latest redis-server --appendonly yes --requirepass "redis"
```

## Remove

```shell
docker rm -f redis
docker volume rm redis-data
```

_Originally posted by @brunowego in https://github.com/docker-library/redis/issues/176#issuecomment-497411473_
            
