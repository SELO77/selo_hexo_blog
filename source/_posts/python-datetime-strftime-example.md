---
title: Python datetime module(class datetime, timedelta ...)
categories:
  - Python
  - Language
tags:
  - python
  - datetime
  - strftime
  - strptime
date: 2016-09-02 11:49:32
thumbnail: https://selo77.github.io/2016/09/02/python-datetime-strftime-example/python-icon.png
---

## 들어가기전에
파이썬으로 하는 개발이 즐거운 이유중 하나는 강력한 내장 모듈입니다. 3.3부터 추가된 asyncio(제가 가장 좋아하는 모듈입니다.)!! 혹은 multiprocessing, logging, sys, os 등등등 왠만해서는 3rd Library 필요없이 구현이 가능합니다. 오늘은 이런 강력한 모듈 중 하나인 datetime에 관하여 살펴보겠습니다.

날짜와 시간 처리는 개발자에게 상당한 고민을 요구합니다. 특히 글로벌 서비스의 경우는 시간대 설정이 매우 종요합니다. 서비스 하는 국가가 섬머타임 정책까지 사용한다면 ??? 나ㅣ어ㅣ만어ㅣ만어ㅣ ㅇㅇ아ㅣ너ㅣㅏㄴ어리ㅓㅏ !!!!!! 하지만 걱정안하셔도 됩니다. 이미 똑똑한 선구자들께서는 이미 우리를 위해 길을 만들어 놓으셨답니다.

## datetime Objects
datetime 모듈은 모듈 이름 그대로 날짜와 시간의 조작에 관한 거의 모든 기능을 제공합니다. 구구절절 설명 보다는 코드를 보면서 살펴봅시다~. 아래 코드는 기록을 위해 texteditor를 사용하였습니다.

```python
import datetime


print type(datetime) # module


from datetime import datetime


print datetime(year=2016, month=10, day=23) # 2016-10-23 00:00:00

# def __init__(self, year, month, day, hour=None, minute=None, second=None, microsecond=None, tzinfo=None): # real signature unknown; restored from __doc__

```


먼저 말씀드렸다 싶이 datetime 자체는 모듈 패키지로서, 다양한 Class를 갖고 있습니다. 그 중 핵심이 되는 class datetime를 기반으로 다양한 연산과 활용이 가능하답니다.( module datetime 과 class datetime이 이름이 똑같은 이유는 아마도 이러한 이유가 아닐까 생각합니다. ) datetime의 생성자를 살펴보면 기본적으로 년, 월, 일 3가지 인자를 initial value를 인자로 받아 상태값을 셋팅합니다. 여기서 중요한 부분은 tzinfo=none 입니다. 제가 현재 일하는 회사에서는 30개국을 대상으로 서비스를 진행하는데, 국가에 따라 tzinfo를 설정 따로 GMT +A 를 계산할 필요가 없습니다.(서머타임 예외) **Key point: datetime모듈의 핵심 클래스는 class datetime이다. Why? datetime모듈을 사용은 단순히 날짜와 시간을 확인하기 보다는 날짜와 시간 연산을 위해 사용하는 경우가 대부분입니다. 그렇기에 datetime 객체는 연산을 위한 핵심 type 입니다. type이 정확하지 않은 경우 TypeError를 맞이하겠죠!**

아래에서는 제가 주로 사용하는 datetime의 메소드를 살펴보겠습니다.

### strptime() 과 strftime()

```python
mybirthday_str = datetime.strftime(mybirthday_datetime, "%Y/%m/%d %H:%M:%S")
print mybirthday_str # 1987/04/13 00:00:00
print type(mybirthday_str) # <type 'str'>
```
strftime() 은 datetime object와 format(날짜형식)을 입력 받아, 입력받은 format에 맞는 string object로 반환해줍니다. 이와 반대로 strptime()은 string object와 format을 입력 받아 datetime object로 캐스팅 해줍니다.

```python
now_str = "2016-09-02 21:31:30"
now_datetime = datetime.strptime(now_str, "%Y-%m-%d %H:%M:%S")
print type(now_datetime) # <type 'datetime.datetime'>
```
하지만 여기서 끝난다면 파이썬 내장모듈이라기에 약한 느낌이죠?

```python
print datetime.strftime(now_datetime, "%y %B %A %p %I/ week number of the year: %W")
# 16 September Friday PM 09/ week number of the year: 35
```

위와 같이 다양한 Directive로 데이터를 표현할 수도 있답니다. 결론, 캐스팅 헬퍼 메소드의 구현 과정없이 내장 모듈을 사용하시면 되겠습니다!!
아 참고로 strftime()는 datetime 뿐만 아니라 date, time objects 모두 지원합니다.


[Python API: strftime & strptime ](https://docs.python.org/2/library/datetime.html#strftime-strptime-behavior)

## timedelta Objects
```python
from datetime import datetime, timedelta


today_datetime = datetime.today()
print today_datetime # 2016-09-02 22:38:09.543477
one_weeks = timedelta(weeks=1)
# days=None, seconds=None, microseconds=None, milliseconds=None, minutes=None, hours=None, weeks=None
one_weeks_ago = today_datetime - one_weeks
print one_weeks_ago # 2016-08-26 22:38:09.543477
```

위의 예제처럼 timedelta Object를 사용하면 날짜 시간 연산을 직관적으로 해결할 수 있도록 도와줍니다.


## tzinfo Objects


## date, time Objects
위 Objects 이외에도 date, time Objects가 존재하지만 저같은 경우는 datetime Objects로 대부분 처리 함으로 이 Objects에 대한 설명은 생략하도록 하겠습니다. 원하시는 분은 아래 Reference의 datetime module API를 살펴보시기 바랍니다.




## Reference
* [overapi/python](http://overapi.com/python)
* [python module datetime api](https://docs.python.org/2/library/datetime.html)


잘못된 부분에 대한 지적은 언제든지 감사히 받겠습니다. 포스팅의 첫번째 목적은 작성자의 학습이므로 Context가 틀어지는 경우가 있을수 있씁니다.
[rochan87@gmail.com](rochan87@gmail.com)

## Related Posts
{% post_link Python-definition %}
<br/>
