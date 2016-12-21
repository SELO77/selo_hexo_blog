---
title: Python data model
categories:
  - Python
  - Language
tags:
  - Python
  - Python data model
  - magic method
thumbnail: >-
  https://selo77.github.io/2016/09/02/python-datetime-strftime-example/python-icon.png
date: 2016-12-21 22:04:31
---
## Head
하나의 언어를 완벽히 이해한다는 것은 다른 언어를 배울때 제반지식으로 도움이됩니다. 프로그래밍 언어를 사용하는 수준이 아닌 이해하는 수준은 확연히 다릅니다. 파이썬을 사용하고 코드를 작성하는데 어느정도 익숙해 젔다면, 우리는 이제 이해를 하기 위해 노력해야합니다. 파이썬 개발자라면 더욱 그러합니다.

그렇다면 파이썬을 이해하기 위해서는 부분부터 접근해야 할까요? 저는 data model로부터 시작하려 합니다.


## Body
파이썬은 기본적으로 **OOP** 를 지원합니다. Javascript 혹은 Java에서 어떤 컬렉션(예를 들면 Array)의 길이를 구할때 `customersArray.length` 와 같은 코드를 작성합니다. `customerArray` 있는 속성중 내부적으로 계산된 `length` 속성에 접근해 값을 얻습니다. 하지만 파이썬에서는 어떠한가요? `len(customerArray)` 와 같은 방식으로 길이를 얻습니다. OOP의 관점에서 이것은 옳은 방식일까요? 같이 천천히 답을 찾아봅시다.

파이썬에서 모든것은 객체입니다. 객체의 종류는 크게 두가지로 나누어집니다. **내장 자료형 객체** 와 **사용자 정의 객체** 입니다. 우리가 일반적으로 쓰는 파이썬(C파이썬)에서 `len(customerArray)`는 인터프리터에 의해 어떻게 해석되고 실행될까요? 답은 두 가지 입니다. `customerArray`가 내장 자료형이라면 `PyVarObject` C 구조체의 `ob_size` 필드의 값을 리턴 합니다. 반면 사용자 정의 객체일 경우 `customerArray.__len__()`를 실행합니다.

보기에는 분명 같은 코드로 보이지만 왜 이런 차이를 갖게 되는 걸까요?

`list`, `dict`, `tuple`, `set`과 같은 내장 자료형의 항목 수를 가져오는 연산 작업은 매우 빈번하게 일어납니다. 이러한 작업들은 매우 효율적으로 작동해야 합니다. 그래서 파이썬은 단지 내장 자료 객체 자료형에 관해서는 단지 C의 구조체 필드를 읽습니다.

사용자 정의 객체에 `__len__()` 매직 메소드가 구현되어 있다고 가정할때, 우리는 `len(customerArray)`라는 일관성을 갖는 코드로 항목수를 구하는 동일한 문제를 해결할 수 있습니다.
```java
ArrayList<String> customerList = new ArrayList<String>();
int size = customerList.size();

String[] array = new String[10];
int size = array.length;
```
위는 자바 코드에서 `ArrayList` 와 `String Array` 의 항목수를 구하는 코드입니다.
> **어떠한 케이스도 규칙을 무너트릴 만큼 충분하지 않다** - zen of python

그렇습니다. 파이썬에 **어떠한 케이스도 규칙을 무너트릴 만큼 충분하지 않다** 고 말합니다. 이러한 철학 덕분에 **일관성** 이라는 장점을 갖게되었습니다.

## Foot
파이썬에서 객체는 크게 내장객체와 사용자 정의 객체로 나누어집니다. 파이썬에서는 `__len__()`, `__getitem__()`, `__iter__()`, `__repr__()` 등과 같은 매직 메소드를 API로 제공합니다. 결국 우리는 API를 사용해 구현하면 될 뿐이고, 파이썬의 일관성 철학 덕분에 사용자 정의 객체도 내장 객체와 동일한 연산자?로 호출할수 있습니다. 결국, 파이썬 데이터 모델은 프레임워크와 같이 시퀀스, 반복자, 함수, 클래스 등 언어 자체의 구성단위에 대한 Interface를 공식적으로 정의합니다.


## PS
단순히 어떤 기술의 사용법을 설명하는 것보다 기술에 대한 이해에 관해 글쓰는 것은 정말 어려운것 같습니다.ㅠㅠㅠㅠㅠㅠㅠㅠㅠㅠㅠㅠㅠㅠㅠ

이러한 개념을 처음 접하는 분이라면 가볍게 읽고 넘기길 추천합니다. 이러한 추상적인 개념들을 한번에 이해한다면 그 사람은 다른 세계의 존재일 것이고, 저와 같은 평범한 분들은 머리에 인덱스 정도 새긴다 생각하세요. 조금 더 깊게 살펴보고 싶으신분은 [https://docs.python.org/2/reference/datamodel.html](https://docs.python.org/2/reference/datamodel.html) 를 읽어 보세요. 저는 읽다 포기했습니다...



## Reference
* [Book: Fluent 파이썬](http://book.naver.com/bookdb/book_detail.nhn?bid=8781382)
* [https://docs.python.org/2/reference/datamodel.html](https://docs.python.org/2/reference/datamodel.html)

잘못된 부분에 대한 지적은 언제든지 감사히 받겠습니다. 포스팅의 첫번째 목적은 작성자의 학습이므로 Context가 틀어지는 경우가 있을 수 있습니다.
[rochan87@gmail.com](rochan87@gmail.com)

## Related Posts
{% post_link continuous-deployment-docker %}
<br/>
