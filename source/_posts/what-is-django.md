---
title: The Django Beginning (MVC Vs MTV)
categories:
  - Python
  - Django
tags:
  - python
  - Django
  - MTV
  - MVC
date: 2016-08-01 20:44:09
thumbnail: https://selo77.github.io/2016/08/01/what-is-django/jango.png
---

## Django란?
장고는 Python에서 사용하는 가장 대표적인 웹 프레임웍 입니다. 자바에 스프링, 루비에 레일스가 있다면 파이썬에는 그 이름도 특이한 [장고](https://www.djangoproject.com/)!! 가 존재합니다.

장고는 기본적으로 [MVC Architecture pattern](https://ko.wikipedia.org/wiki/%EB%AA%A8%EB%8D%B8-%EB%B7%B0-%EC%BB%A8%ED%8A%B8%EB%A1%A4%EB%9F%AC)을 따릅니다. MVC 패턴은 웹 프레임웍에서 가장 많이 체택되는 디자인 패턴중 하나로서 역할에 따른 소스 코드의 분리로 많은 장점들을 갖게 됩니다. 장고는 MTV(Model Template View)는 디자인 패턴을 따르지만 이는 MVC 패턴의 일부로 생각합니다. 그럼 먼저 장고의 기본 아키텍처를 보고 넘어가겠습니다.
{% asset_img Django_mvc.png Django Basic Architecture %}
{% asset_img MVCBasic.jpg Spring MVC Architecture %}
첫번째 다이어그램은 장고의 MTV 패턴이 적용된 아키텍처이며, 아래는 Java Spring의 MVC 아키텍처 입니다. 사실 장고가 뭔지도 잘 모르는데 아키텍처를 먼저 보는 이유는 무작정 코드를 작성하는 것보다 아키텍처 다이어그램을 머리에 세기고, 코드를 작성하면 데이터 흐름을 어느 정도 이해할수 있기 때문입니다. 또한 세부적인 코드가 전체에서 어느 부분에 영향을 미치게 되는지 이해를 도와줍니다.

## MVC Vs MTV
MVC 와 Django MTV를 비교를 통해 정리해보겠습니다. 먼저 MVC부터 살펴 보면 데이터베이스와 interaction은 **Model** 에서 처리하고, Business Logic은 **Controller**, User Interface의 생성은 **View** 에서 각각 처리합니다. (위의 다이어그램과 함께) 전체적 흐름을 살펴보자면 Request에 해당하는 컨트롤러를 호출하고, 컨트롤러는 request의 응답에 필요한 데이터를 찾기 위해서 적절한 Model을 소환합니다!! 최종적으로 View를 호출 Model에서 얻은 데이터를 토대로 사용자에게 보낼 User Interface를 구성 후 Response를 보내게 됩니다.

그렇다면 장고의 MTV는 뭐가 다를까요? 뭐가 다르기에 MTV라고 부르는 것일까요? MTV는 MVC를 약간 수정한  패턴입니다. MTV의 **Model** 은 MVC Model과 같은 역할을 합니다. 데이터 베이스와 데이트 추출을 담당 합니다. Django는 기본적으로 [ORM(Object Relational Mapping)](http://debop.blogspot.kr/2012/02/orm-object-relational-mapping.html) 테크닉을 지원합니다. ORM방식의 지원으로 개발자는 SQL의 작성 작업의 대부분으로 부터 자유로워 지며, OOP 개발에 집중할 수 있게 도와줍니다.
 **View** 는 MVC의 Controller와 같은 Business Logic을 처리합니다. 마지막으로 **Template** 은 Client에게 보여질 User Interface를 구현하며, Django Template은 스크립트 언어인 Python의 장점을 극대화 시킨 강력한 templating system을 제공합니다. Middleware, URL Resolver Template Loader 부분은 당장 구현이 필요한 부분은 아니므로 넘어가셔도 상관없습니다.

{% asset_img jumpstart-django-42-728.jpg Django Basic Architecture %}

위 다이어그램의 데이터 흐름과 함께 MTV 각각의 역할을 생각하시면 전체적인 그림이 그려지실 겁니다.

## 결론
파이썬의 강력한 웹 프레임웍 장고에 대해 살펴보았습니다. 장고는 MVC 패턴의 장점을 살리면서 빠른 생산을 위한 MTV 패턴을 채택하였습니다. 또한 ORM 테크를 지원하여 객체지향적인 코드 생산에만 전념할 수 있도록 도와줍니다. 또한 위에서 설명하지는 않았지만 깊은 역사?와 함께 수많은 지원 패키지들이 존재합니다. 이러한 수많은 장점 덕분에 스타트업에서 선호하는 웹 프레임웍 중 탑 순위권 안에 들었으며, 점점 더 많은 채택을 받으며 발전하고 있습니다. 아직은 어렵게 다가올수 있지만, 장고 프레임웍 하나만 제대로 이해해도 먹고 사는데는 지장이 없으리라 생각됩니다 흐흐.

Ps. 아마도 다음 포스팅은 장고 공식 사이트의 튜토리얼을 통해 간단한 여론조사 어플리케이션을 만들어 볼 예정입니다~.

## Reference
* [Introduction to Django](https://bharatikunal.wordpress.com/2009/03/11/introduction-to-django/)
* [more abount python packages](https://docs.python.org/3/tutorial/modules.html#tut-packages)
* [PyCharm과 함께 DJango와 RestFramework를 활용한 웹 사이트 구축하기](https://devissue.wordpress.com/2015/02/01/pycharm%EA%B3%BC-%ED%95%A8%EA%BB%98-django%EC%99%80-restframework%EB%A5%BC-%ED%99%9C%EC%9A%A9%ED%95%9C-%EC%9B%B9-%EC%82%AC%EC%9D%B4%ED%8A%B8-%EA%B5%AC%EC%B6%95%ED%95%98%EA%B8%B0/)
* [virtualenv를 사용하자 - 가상 개발환경 구축하기](http://pythoninreal.blogspot.kr/2013/12/virtualenv.html)
* [Adding Existing Virtual Environment on PyCharm](https://www.jetbrains.com/help/pycharm/2016.1/adding-existing-virtual-environment.html)
* [Django Design philosophies](https://docs.djangoproject.com/en/1.10/misc/design-philosophies/#dry)
* [ORM의 기본적인 개념 및 활용방안](http://www.javajigi.net/pages/viewpage.action?pageId=6560)


잘못된 부분에 대한 지적은 언제든지 감사히 받겠습니다.
[rochan87@gmail.com](rochan87@gmail.com)

<!-- ## Related Posts
{% post_link continuous-deployment-docker %}
<br/> -->
