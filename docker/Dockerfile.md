# Dockerfile

docker image 생성을 위한 스크립트

## docker build
`Dockerfile`이 있는 폴더에서 `docker build` 명령을 이용하여 빌드함
```shell
sudo docker build --tag my-image:v1.0 .
```

만약 Dockerfile이 다른 폴더에 있는 경우, `build`명령의 마지막에 `.`이 아닌 Dockerfile이 있는 경로를 기록   
만약 파일 이름이 Dockerfile이 아니라면 `--file` 옵션을 이용하여 파일명 지정
```shell
sudo docker build --tag my-image:v1.0 --file Dockerfile.dev
```

## Dockerfile 구성
```dockerfile
#build stage
# base image 지정. as ...을 이용하여 stage이름을 지정
FROM gradle:jdk-alpine as build-stage

# 작업 dir 지정. 이후 명령은 이 dir을 기준으로 실행.
WORKDIR /home/gradle/project

USER root

# image 내부에서 명령을 실행
RUN apk update

# 이미지에서 사용할 환경변수 지정
ENV GRADLE_USER_HOME /home/gradle/project

# 현재 폴더의 내용을 image의 특정 경로로 복사
COPY . /home/gradle/project

# image 내부에서 gradlew 명령 실행
RUN ./gradlew build

#production stage
# 작업대상 이미지를 변경함. docker build stage가 추가됨
FROM java:jre-alpine

# 작업 dir 지정
WORKDIR /home/gradle/project 

# container가 8080 포트를 listen함을 기록
EXPOSE 8080 # 

# 파일을 현재 이미지로 복사. --from을 이용하여 이전 stage에서부터 파일을 복사하도록 함
COPY --from=build-stage /home/gradle/project/build/libs/project-0.0.1-SNAPSHOT.jar .

# default 실행명령을 지정. /bin/bash -c java $JAVA_OPTS ...
ENTRYPOINT java $JAVA_OPTS -jar project-0.0.1-SNAPSHOT.jar
```

## 그 외 사용되는 명령
### ADD
`ADD <src> <dest>`   
Image에 파일을 추가한다. URL은 다운로드 후 추가하고, 압축파일이면 압축해제 후 추가한다.
### LABEL
`LABEL "some.label.key"="some label value"`   
Image에 메타데이터를 추가한다.
### USER
`USER <user>[:<group>]`   
`RUN`, `CMD`, `ENTRYPOINT`등 명령을 수행할 사용자를 지정한다.
### ARG
`ARG <name>[=<default>]`   
`docker build` 수행 시 `--build-arg <name>=<value>` 형태로 파라미터를 전달
### CMD
`CMD nginx -g daemon off;` 혹은 `CMD ["nginx", "-g", "daemon off;"]`   
전자를 shell form, 후자를 exec form 이라고 함. Image 실행 시 실행되는 default 값

#### CMD vs. ENTRYPOINT
[docs.docker.com](https://docs.docker.com/engine/reference/builder/#understand-how-cmd-and-entrypoint-interact) 참고   
* `CMD` 혹은 `ENTRYPOINT` 둘 중 하나는 반드시 있어야 함.
* `shell form`으로 작성된 경우 `/bin/sh -c` 뒤에 명령이 추가되어 실행됨
* `ENTRYPOINT`가 `shell form`으로 작성된 경우 `CMD`를 무시함
* `ENTRYPOINT`가 `exec form`으로 작성된 경우, `CMD`를 `ENTRYPOINT`의 파라미터로 사용.   
  (`CMD`가 `shell form`이면 `/bin/sh -c`를 포함하여 파라미터로 사용)
