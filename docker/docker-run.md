[Reference](https://docs.docker.com/engine/reference/run/#general-form)

```shell
sudo docker run \
    -d \
    -p 80:80 \
    --name proxy \
    -v /some/host/path:/container/dest:rw \
    - /container/path \
    nginx:stable-alpine \
    nginx -g 'daemon off;'
```
