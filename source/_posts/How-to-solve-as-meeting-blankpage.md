---
title: 프로덕션 환경에서 블랭크 페이지를 만난다면?
categories:
  - Web
  - Problem
tags:
  - ELKR
  - 로그분석
  - Wireshark
  - Packet
date: 2016-07-17 13:40:31
thumbnail: https://www.wireshark.org/assets/images/wsbadge@186x57.png
---
현재 저의 역량을 벗어나는 문제를 맞닥뜨렸습니다. 다니고 싶은 회사에 지원을 했고, 파이썬 신의 기를 받아 서류합격을 했습니다. 기쁨도 잠시 인터뷰 진행 전 미션을 받았습니다. 그 중 첫 번째 미션을 정리하면서 최선의 답을 찾아보려합니다.


## 문제의 이해
>**프로덕션 환경에서 작동하는 WAS(웹 어플리케이션 서버)를 브라우저에서 접속하니 갑자기 블랭크 페이지가 뜹니다.
어떤 툴, 서비스 혹은 command를 사용하여 문제를 파악하고 해결할수 있는지 서술해주세요.**

먼저 문제를 자세히 살펴 봅시다. 프로덕션 환경? 블랭크 페이지? 프로덕션 환경이란 실제 현재 서비스 중인 환경이며, 블랭크 페이지란 아래 이미지와 같은 페이지를 의미합니다.
<img src="https://encrypted-tbn2.gstatic.com/images?q=tbn:ANd9GcRpXOqksDqlSBQaWJb9P0JtwAYskN_zfhxJWFNUX9XxQhewjGRshQ">
그렇다면 Blank Page가 뜨는 원인의 파악이 필요할 것이며 다음 단계에서 문제의 원인을 찾아보겠습니다.


## 문제 원인 파악
보통 문제에 직면했을때, 크게 두 가지 경우로 나눌 수 있습니다. 문제가 무엇인지 아는 경우와 문제가 무엇인지 모르는 경우입니다. 저는 두번째 경우에 가까웠습니다. 그래서 제가 활동하는 커뮤니티에 도움을 청했고 문제의 접근 방향을 설정 후 진행했습니다.

Blank Page의 원인은 크게 Client상의 문제와 Server상의 문제로 분류할 수 있습니다. 서버 문제의 경우 다양한 원인의 가능성이 있고, 원인을 찾기 위해서 크게 서버 상태확인, 로그 분석, 패킷 분석 등이 필요합니다.

    블랭크 페이지 원인 Case 정리
    1. Client 문제
      1.1 브라우저
      1.2 악성코드
    2. Server 문제
      2.1 WAS 문제
      2.2 네트워크(DNS, 인터넷) 문제


## 문제 해결 단계 설정
    1. Client 문제
      1.1 브라우저 설정확인
      1.2 악성코드 감염 여부 확인
    2. Server 문제
      - Server health check
      2.1 WAS 문제
        - WAS Log 분석
        - Packet 분석
      2.2 Network 문제
        - DNS 상태 확인


## 문제 원인 분석
### Client 문제
  첫번째 가정 Client가 원인인 경우 입니다. 이를 확인 하는 가장 쉬운 방법은 타 장비에서 Domain에 접속해 보는 것입니다. 타 장비에서 정상적 접근이 가능하다면 특정 장비의 문제입니다. 원인은 보통 개인 브라우저의 설정이 잘못되었거나 악성코드에 감염된 경우 입니다. 후자의 경우에는 브라우저 상에서 [DNS(Domain Name System)](https://ko.wikipedia.org/wiki/%EB%8F%84%EB%A9%94%EC%9D%B8_%EB%84%A4%EC%9E%84_%EC%8B%9C%EC%8A%A4%ED%85%9C)를 임의로 통제하는 경우가 있습니다. 도메인 네임 시스템은 전화번호부 라고 생각하면 쉬운데 악성 바이러스가 전화번호부에 등록된 이름과 번호를 임의로 변경시키게 됩니다. 정리하자면 도메인 이름을 IP 주소로 변환하는 과정에서 정상적인 주소로의 변환이 이루어지지 않습니다. 이와 같은경우는 애드웨어나 백신 프로그램을 통해서 해결할 수 있습니다.

### Server 문제
서버 문제가 원인인 경우 훨씬 복잡합니다. 여기서 부터는 제 지식의 한계와 구체적인 설명을 위하여 스펙을 정의하고 진행하겠습니다.
* AWS EC2
* Linux AMI
* WAS - Nginx
* 로그 분석 환경 - ELKR (ElasticSearch + Logstash + Kibana + Redis)

AWS Console에 접속해 Instance의 상태를 확인합니다. Instance의 상태가 정상이라면 Kibana Web에 접속에러 로그를 확인합니다. 블랭크 페이지에서 받았던 Response의  Status Code와 page byte size가 0인 Case를 검색 합니다. (검색 쿼리 예: @fields.status:502 && @fields.size:537)

케이스를 확인 했으니 Wireshark(패킷 분석툴)를 이용하여 케이스를 테스트 하고 원인을 파악합니다. 이 단계에서 네트워크 통신 과정에서 패킷유실이 있는지도 확인합니다.

## Reference
### Site
* [ELKR (ElasticSearch + Logstash + Kibana + Redis) 를 이용한 로그분석 환경 구축하기](http://brantiffy.axisj.com/archives/418)
* [Wireshark를 통한 패킷 분석](http://inverlist.postype.com/post/78617/)
### 도움을 주신분들
* Facebook Group 모여서 각장 코딩하는 모임
* 스타트업 개발자 모임 인간님
* 나는 프로그래머다의 Jaeyong_Cho 님
