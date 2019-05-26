---
title: "Docker 기본 명령어 사용법"
date: 2019-05-26 15:20:00
categories: Devops
---

Docker 기본 사용법을 알아보자. (node.js 웹 앱의 도커라이징)

Dockerfile : 도커안에 이미지를 만들때(빌드할때) 설정값들을 사전에 정의하는 파일

-- FROM : 어떤 이미지를 사용해서 빌드할 것인지 정의. 빌드할때는 가장 먼저 로컬에서 해당 이미지가 있는지 알아보고 없으면 `Docker Hub`에서 이미지를 가져 온다. (예, node:10)

-- WORKDIR : 이미지 안에 어플리케이션 코드를 넣기 위한 디렉터리를 생성해야 하는데 해당 디렉터리를 만들어 주는 역할을 한다. (예, /usr/src/app)

-- COPY : 파일을 이미지에 추가하는 명령어. (예, package*.json ./). 예로 구성된 node:10은 기본적으로 node.js와 NPM이 설치되어 있다. 그래서 package.json, package-lock.json 파일을 `./` 현재 경로에서 복사해서 이미지에 추가할 수 있다.

-- RUN : 

-- EXPOSE : 

-- CMD : 

.dockerignore : 필요없는 파일이나 디렉터리를 해당 파일에 지정해주면 제외가 된다. nodejs 로 구축할때는 아래와 같은 파일이나 디렉터리를 제외시켜 로컬 모듈과 디버깅 로그를 복사하는 것을 막아서 이미지 내에서 설치한 모듈을 덮어쓰지 않게 한다.
```
node_modules
npm-debug.log
```

이미지 빌드하기
```
$ docker build -t 이름 .
```

완료했으면 성공적으로 이미지가 빌드 되었는지 이미지 목록을 조회하면 된다.
```
$ docker images
```