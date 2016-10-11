---
title: Python -  == 와 is 의 차이
categories:
  - Python
  - Language
tags:
  - python
thumbnail: >-
  https://selo77.github.io/2016/09/02/python-datetime-strftime-example/python-icon.png
date: 2016-10-04 00:04:18
---
Python은 직관적이고 하이레벨 프로그래밍 언어입니다. 이에 맞게 우리가 쓰는 언어에 가까운 문법이 존재합니다. 그 중에 오늘은 is 와 == 의 차이를 공부해보겠습니다.

```python
>>> things = [1, 2, 3]
>>> things[:]
[1, 2, 3]
>>> things == things[:]
Ture
```
things와 things[:] 값을 비교하였고, True를 반환 받았습니다. 그렇다면 is를 사용하여 한번더 비교해보겠습니다.

```python
>>> things is things[:]
False
```

리턴값이 False 입니다. is 와 == 을 이해하고 사용하시는 분이라면 당연한 결과라 말씀하시겠지만 Python을 사용하여 돈을 벌고 있음에도 불구하고 저는 문제를 마딱드리기 전까지 차이를 모르고 사용했습니다. 물론 직관적으로 어느 부분에 is를 사용하고  ==을 사용해야 할지 판단했기때문에 문제(버그)에 직면하지 않았습니다. 갑자기 "똥인지 된장인지 구분못하고 쓰면안된다" 는 저의 개발 스승님 말씀이 떠오르네요...

위 결과값의 차이를 보니 확실히 is 와 == 이 뭔가는 다른것 같습니다. 그렇다면 무엇이 다를까요? 이를 확인하기 위해 어떤 방법을 동원해볼까요?

```python
>>> name = None
>>> name is None
True
>>> name == None
True
```

이번에는 둘다 같은 True를 반환했네요. 그렇다면 첫번째 주어진 조건과 두번째 조건의 차이를 알수 있다면, is 와  == 의 차이를 알수 있을것 같은 느낌이 드네요.

```python
>>> id(things)
4556601824
>>> id(things[:])
4556641344
>>> id(name)
4554182552
>>> id(None)
4554182552
```
파이썬에 내장 함수인 id()를 이용해 메모리상의 주소값을 비교해보았습니다. 결과값을 보니 is 와 == 의 차이가 뭔지 아시겠나요?

첫번째 소스의 things 와 things[:] 를 is 로 비교했을때 False를 반환했던 이유는 객체의 주소가 달랐기 때문입니다. things의 주소는  4556601824 이고, things[:] 는 4556641344 입니다. 공부를 하면서 얻은 보너스!!! [:] 처리는 Call by value 가 아니라 Call by Reference 처리라는 것도 알 수 있습니다.

정리하자면 Python에서 == 는 Value를 자체를 비교하는 연산자 이고, is 는 객체의 주소(object identity)를 비교하는 키워드 혹은 비교연산자라는 것을 알수있습니다.

오늘 공부 끝~! 부족한글 읽어주셔서 감사합니다.



## Reference
* [Python None comparison: should I use “is” or ==?](http://stackoverflow.com/questions/14247373/python-none-comparison-should-i-use-is-or)
*
*

잘못된 부분에 대한 지적은 언제든지 감사히 받겠습니다. 포스팅의 첫번째 목적은 작성자의 학습이므로 Context가 틀어지는 경우가 있을수 있씁니다.
[rochan87@gmail.com](rochan87@gmail.com)
