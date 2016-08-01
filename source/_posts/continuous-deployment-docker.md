---
title: Docker를 이용한 지속적 배포 환경 구축
categories:
  - DevEnv
  - Docker
tags:
  - Docker
  - DevOps
  - CD
date: 2016-07-19 21:33:46
thumbnail: http://www.jsitech.com/wp-content/uploads/2015/11/DockerLogo.png
---

<img src="https://d21ii91i3y6o6h.cloudfront.net/gallery_images/from_proof/1026/large/1396373089/docker.png">

```bash
✝  ~/Documents/github/docker_compose_django  vim Dockerfile
✝  ~/Documents/github/docker_compose_django  vim requirements.txt
✝  ~/Documents/github/docker_compose_django  vim docker-compose.yml
✝  ~/Documents/github/docker_compose_django  docker-compose run web django-admin.py startproject composeexample .
ERROR: yaml.scanner.ScannerError: while scanning for the next token
found character '\t' that cannot start any token
 in "./docker-compose.yml", line 3, column 1
✘ ✝  ~/Documents/github/docker_compose_django  atom docker-compose.yml
✝  ~/Documents/github/docker_compose_django  docker-compose run web django-admin.py startproject composeexample .
✝  ~/Documents/github/docker_compose_django  ls -l
total 32
-rw-r--r--  1 SELO  staff  146  7 19 23:00 Dockerfile
drwxr-xr-x  6 SELO  staff  204  7 19 23:12 composeexample
-rw-r--r--  1 SELO  staff  209  7 19 23:10 docker-compose.yml
-rwxr-xr-x  1 SELO  staff  257  7 19 23:12 manage.py
-rw-r--r--  1 SELO  staff   16  7 19 23:02 requirements.txt
✝  ~/Documents/github/docker_compose_django  cd composeexample
✝  ~/Documents/github/docker_compose_django/composeexample  ls
__init__.py settings.py urls.py     wsgi.py
✝  ~/Documents/github/docker_compose_django/composeexample  vim settings.py
✝  ~/Documents/github/docker_compose_django/composeexample  docker-compose up
```

<img src="https://blog.docker.com/media/2015/09/docker-hub-diagram.png">

[Docker Compose](https://docs.docker.com/compose/overview/) 란 멀티 컨테이너의 실행을 위한 툴입니다. 한번의 실행으로 미리 정의된 모든 서비스를 생성하고 시작시킬수 있습니다.

[클러스터](https://ko.wikipedia.org/wiki/%EC%BB%B4%ED%93%A8%ED%84%B0_%ED%81%B4%EB%9F%AC%EC%8A%A4%ED%84%B0)

[Celery](http://www.celeryproject.org/) 란 Python으로 작성된 비동기 작업 큐입니다. 작업(메시지)을 브로커를 통해 전달하면 하나 이상의 워커가 이를 처리하게 됩니다. 예를 들면 사용자에게 이메일 발송, SMS 발송, 게시물 등록 등 비동기 처리가 필요한 작업을 Celery에게 위임하고 처리할 수 있습니다.

psycopg2


## Reference
* [Quickstart: Docker Compose and Django](https://docs.docker.com/compose/django/)
* [Docker 한글 문서 / 영상 모음집](http://documents.docker.co.kr/)
* [Continuous Delivery with Docker](http://xebia.github.io/cd-with-docker/#/)
* [도커 컴포스 장고 튜토리얼 소스 - github/SELO77](https://github.com/SELO77/docker_compose_django)
* [Celery를 이용한 분산처리 프로세스 작성하기](https://medium.com/sunhyoups-story/celery-b96eb337b9cf#.2jmk71j60)
* [스포카 서버의 구조](https://spoqa.github.io/2011/12/24/about-spoqa-server-stack.html)
* [AWS Container Day SlideShare](http://www.slideshare.net/awskorea/aws-container-day)
* [도커(Docker) 튜토리얼 : 깐 김에 배포까지](http://blog.nacyot.com/articles/2014-01-27-easy-deploy-with-docker/)

잘못된 부분에 대한 지적은 언제든지 감사히 받겠습니다.
[rochan87@gmail.com](rochan87@gmail.com)

## Related Posts
{% post_link What-is-Docker %}
<br/>
