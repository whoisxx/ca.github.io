---
title: "Nodejs Express 어플리케이션 Elastic Beanstalk으로 배포하기"
date: 2019-06-08 17:15:00
categories: AWS ElasticBeanstalk nodejs
---

Docker 환경에서 구성한 Nodejs 어플리케이션을 AWS Elastic Beanstalk에 배포해보자.

Requirement
* AWS IAM 배포할 수 있는 API key (Access key, Secret Key)
* AWS CLI 설치
* AWS EB 설치
* Docker로 구성된 Nodejs 환경(example : https://github.com/studyjjm/jadenodejs)


이 포스트에서는 위에 정의한 requirement가 설치된 이후에 과정부터 진행한다.

1. 먼저 aws configure 를 해준다. IAM에서 생성한 access key, master key를 입력하고 본인이 편한 환경 서울이나 미국 등 환경을 설정해준다.

2. nodejs 어플리케이션이 있는 디렉터리로 이동한다.

3. 일라스틱 빈스톡 환경임을 명시해준다.
```
$ eb init
```

여기서 배포할 어플리케이션이 자리잡을 region과 이름, 형태를 구축해준다. 
(ap-northeast-2, DockerandNodejs, Docker, SSH 사용한다고 설정했다.)

이후에 ls -al로 해당 디렉터리를 확인해보면 .elasticbeanstalk이라는 디렉터리가 생성된 것을 확인할 수 있다.

4. 어플리케이션 첫 배포
```
$ eb create
```

여기서 환경 이름, DNS CNAME, load balancer type 등을 정의할 수 있고 이후에 몇분을 기다면 첫 배포가 완료된다.

