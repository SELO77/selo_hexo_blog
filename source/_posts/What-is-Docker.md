---
title: Docker 란?
categories:
  - DevEnv
  - Docker
tags:
  - Docker
  - CD
  - DevOps
date: 2016-07-19 07:47:23
thumbnail: http://www.jsitech.com/wp-content/uploads/2015/11/DockerLogo.png
---

<img src="https://d21ii91i3y6o6h.cloudfront.net/gallery_images/from_proof/1026/large/1396373089/docker.png">

## Docker 란?
**도커란 컨테이너(이미지)를 실행 관리하고 배포하기 위한 기술입니다.** 범위를 좁게 하면 리눅스 컨테이너를 관리하는 도구입니다. 리눅스 컨테이너? 자바에서 서블릿컨테이너, JSP컨테이너는 들어봤는데 리눅스도 컨테이너가 있네요. 제가 알고 있는 컨테이너는 자바 빈들을 실행하고 관리 하기 위해 존재 했었는데요.
>[리눅스 컨테이너(LXC)란](https://ko.wikipedia.org/wiki/LXC) 단일 컨트롤 호스타 상에서 리눅스 시스템(컨테이너)를 실행하기 위한 위한 운영 시스템 레벨 가상화 방법

리눅스 컨테이너는 [Control Group(Cgroup)](https://access.redhat.com/documentation/ko-KR/Red_Hat_Enterprise_Linux/6/html/Resource_Management_Guide/ch01.html)와 [namespace](http://bluese05.tistory.com/11) 결합하여 애플리케이션을 위한 가상 환경을 제공합니다. Docker 또한 이러한 실행 환경을 갖게 되고 독립된 드라이버로서 작동할수 있게 됩니다. **간단히 정리를 하자면 Docker는 Cgroup 기술로 Host OS 자원을 활용하고, namespace를 통해 독립된 실행 공간을 갖게 됩니다.**


## Docker 용어정리
Docker(도커)의 개념을 이해했으면 Docker 내부적으로 사용되는 용어를 정리 해봅시다. 먼저 Docker의 환경의 전체적인 흐름을 살펴보실까요~

> 도커 환경은 크게 도커 호스트와 도커 클라이언트로 생각해 볼 수 있습니다. 도커 호스트는 도커 데몬(도커 엔진?)을 기반으로 도커 컨테이너들을 실행 및 관리 합니다. 반면 도커 클라이언트는 도커 명령을 실행하는데 쉽게 이해하면 인터페이스로서 도커 이미지를 관리합니다.

빠른 이해를 위해 기본 웹 환경과 대입해 이해해보겠습니다.
* 도커 호스트는 도커 컨테이너를 실행하는 가상머신. (서버)
* 도커 클라이언트는 도커 Interface (클라이언트 프로그램)
* 도커 데몬은 도커 엔진 (서버 프로세스)
* 도커 컨테이너는 하나의 프로세스 (이미지의 인스턴스)
* 도커 이미지는 실행파일 (소스코드?)

어느 정도 개념을 정리 했으니 도커 아키텍처를 보면서 구체화 시켜봅시다.





## Docker Architecture
* **간단한 Docker Architecture**
<img src="http://southworks.com/blog/wp-content/uploads/sites/81/2015/07/docker_architecture.png">

<img src="http://nordicapis.com/wp-content/uploads/Docker-API-infographic-container-devops-nordic-apis.png">
<br/>

* **기존의 가상머신 환경과 Docker의 차이**
<img src="http://siliconangle.com/files/2014/08/Docker-vs-Virtualization.jpg">
<br/>

* **Docker Commands Diagram**
<img src="https://philipzheng.gitbooks.io/docker_practice/content/_images/cmd_logic.png">
<br/>

* **Docker Renterprise Architecture**
<img src="https://docs.opensvc.com/_images/docker.enterprise.architecture.png">


## Docker 철학
https://docs.docker.com/engine/userguide/eng-image/dockerfile_best-practices/
> Run only one process per container

위 링크를 보시면 아래 문구의 Docker의 철학이 담겨있습니다. 그 이유는 한개의 이미지에 여러개의 프로세스를 넣으면 확장성과 재사용성이 급격히 저하가 됩니다. 물론 Docker 생태계가 확장하는데도 더 어려워 질것입니다. 이렇듯 그 기술의 철학에 맞게 사용하는것도 매우 중요합니다. 차후 Docker로 이미지를 Build하고 사용하면서 이 부분은 한번 더 집고 넘어가도록 하겠습니다.


## 왜 Docker 인가?
짧지만 핫하디 핫한 Docker(도커)를 살펴보았습니다. DevOps에 무뇌한인 저에게는 개발만이 전부가 아니다 라는 큰 방향을 일깨워주었고, 이렇게 편리한 Tool을 사용하지 않는 것은 죄악이다!! 라는 조금은 단순무식한 결론을 얻었습니다. 실제 프로덕션환경에서 사용경험은 전무하지만 단지 개념만 놓고 보았을때 결론입니다. Docker는 리눅스 컨테이너라는 기존의 [하이퍼바이저](https://ko.wikipedia.org/wiki/%ED%95%98%EC%9D%B4%ED%8D%BC%EB%B0%94%EC%9D%B4%EC%A0%80)라는 조금은 무거운 과정을 훨씬 가볍게 해주었으며, DevOps의 최전선 기술로 우리의 개발환경을 한층 윤택하게 만들어줄 것이라는 결론과 함께 Docker 살펴보기를 마무리 하겠습니다. 감사합니다.





## Reference
[docker getting started: 왕초보를 위한 docker 입문](http://blog.iolo.kr/510)
[도커 무작정 따라하기](http://www.slideshare.net/pyrasis/docker-fordummies-44424016)
[Docker 한글 문서 / 영상 모음집](http://documents.docker.co.kr/)

잘못된 부분에 대한 지적은 언제든지 감사히 받겠습니다.
[rochan87@gmail.com](rochan87@gmail.com)

## Related Posts
{% post_link continuous-deployment-docker %}
<br/>
