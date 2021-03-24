
## docker-compose up
```shell
sudo docker-compose \
     -f docker-compose.yaml \
     -f docker-compose.dev.yaml \
     up \
     -d --build \
     service-name
```

## docker-compose down
```shell
sudo docker-compose \
     down
```

## docker-compose build
```shell
sudo docker-compose \
     build \
     service-name
```

## docker-compose config
```shell
sudo docker-compose \
     -f docker-compose.yaml \
     -f docker-compose.dev.yaml \
     config
```

### docker-compose logs
```shell
sudo docker-compose \
     logs \
     -f \
     service-name
```
## docker-compose ps
```shell
sudo docker-compose \
     ps \
     --filter key=val
```

## docker-compose push
```
sudo docker-compose \
     push \
     service-name
```
