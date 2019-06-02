---
title: "Docker Compose의 이해"
date: 2019-06-02 17:31:00
categories: docker
---

Dockerfile 파일로 하나의 컨테이너를 구성하는데 필요한 작업을 적어놓을 수 있다면, Docker-compose는 여러개의 컨테이너를 동시에 구성하고 싶을때 사용한다.
이 문서에서는 Node.js 와 MongoDB 두 가지의 컨테이너를 Docker Compose를 사용하여 하나의 파일로 띄울 수 있도록 하는 것을 목표로 한다.

프로젝트하는 디렉터리에 아래처럼 docker-compose.yml 파일을 만듬 (Dockerfile 이 있는 곳)
```
version: "2"
services:
  app:
    container_name: jadeNodeApp
    restart: always
    build: .
    ports:
      - "3000:3000"
    links:
      -mongo
  mongo:
    container_name: mongo
    image: mongo
    volumes:
      - ./data:/data/db
    ports:
      - "27017:27017"
```

* service 이름을 `app` 이라고 정의한다.
* app 이라는 서비스에서 사용할 컨테이너 이름을 `app` 라고 정의한다.
* `restart` : 만약 실패할 경우에 자동으로 다시 실행하도록 설정한다.
* `build` : 현재 경로에 있는 Dockerfile을 사용하여 이미지를 빌드한다. 
* `ports` : 호스트 포트와 컨테이너 포트 매핑.

* 또다른 service 이름을 `mongo` 라고 정의한다(DB용). 이번에는 도커 파일을 사용하는 대신에 도커 허브 레파지토리에서 기본 mongo 이미지를 다운로드 받아보자.
* `volumes` : mongo 디비를 설치하고 세팅할때 /data 디렉터리를 만들어서 사용한 것 처럼, 호스트의 /data 디렉터리와 컨테이너 디렉터리 /data/db를 마운트 한다. (이건 호스트에서 일전에 mongo 설치하면서 더미데이터도 같이 설정해주어야 할듯)
* 'links' : 마지막으로 mongo 컨테이너와 jadeNodeApp 컨테이너가 서로 통신할 수 있도록 연결한다.