---
title: Python- yield, generator, coroutine
categories:
  - Python
  - Language
tags:
  - python
  - yield
  - generator
  - coroutine
  - asyncio
date: 2016-07-05 20:16:31
thumbnail: https://encrypted-tbn1.gstatic.com/images?q=tbn:ANd9GcQ-llODQKuO5a5mGb3WdoVKmGSWnTx_KgSLzuW0rjYpdN4ptIfBTw
---

## AsyncIO ?
아래 그림은 Python3.4 부터 적용된 asyncIO 라는 강력한 비동기 모듈의 프로세스를 간략하게 설명한 그림입니다. 보자마자 머리가 지끈 지끈 아파오기 시작하시져?

<img src="https://docs.python.org/3/_images/tulip_coro.png">

비동기, 병령처리, 동시성 너무나 자주 듣는 용어들이지만 깔끔하게 머릿속에 정리가 되지않습니다. 매일 같이 아래와 같은 코딩을 비동기 기반 개발을 함에도 불구하고 반에 반 밖에 이해를 못하고 코딩을 하는것 같습니다.ㅠㅠ 그래서 이번 기회에 포스팅을 통해 AsyncIO 비동기 모듈을 완벽 정복해보려 합니다.
```python
import asyncio

from module import module_dao, module_email

@asyncio.coroutine
def an_asyn_fnc():
  item = yield from another_asynfnc()
  asyncio.async(module_email(item.email))
  return item

@asyncio.coroutine
def another_asynfnc()
  query = """
  SELECT * FROM users WHERE userID = 'SELO'
  """
  dt_user = yield from module_dao(query)
  if dt_user.get('succeed', None):
    return dt_user['item']
  else:
    raise Exception
```
(위 코딩은 너무 깊게 생각할 가치가 없습니다....... 하지만 한번 눈으로 보시면 아래 개념들을 이해하는데 조금은 도움이 될듯합니다.)

## yield, generator, coroutine
AsyncIO 를 이해하기 위해서 사전에 알고가야 할 개념들이 존재합니다. 바로 오늘 같이 공부해볼 yield 키워드, generator 객체, coroutine 개념입니다. 먼저 yield 키워드와 generator 부터 살펴보겠습니다.

**return 처럼 yield는 값을 반환한다. 하지만 yield는 리턴 값을 비롯한 Context(환경) 포함한 제너레이터라는 객체를 반환하는데 이 제네레이터 객체는 iterable(순환가능) 합니다.** 말이 상당히 야리꾸리 합니다. 처음에는 이해가 안되는게 당연합니다.

```python
for i in range(5):
  print(i, end= ",") # 0,1,2,3,4,

def custom_range(end):
  i = 0
  while i < end:
    yield i
    i += 1

print()
result = custom_range(5)
print(result) # <generator object custom_range at 0x1017c5a98>
```

위 custom_range() 함수는 내장함수인 range() 함수를 제너레이터를 이용해 구현한 예입니다.
위와 같이 구현된 함수를 코루틴 함수라 합니다. 코루틴? 제너레이터? 여기서는 하나만 기억하고 넘어갑시다. yield가 선언된 함수는 yield를 만나는 순간 제너레이터라는 객체를 반환한다!! 그러면 왜 제너레이터는 순환가능한 것인가? 왜 순환 가능하여야만 하는가? 아래 코드를 보면서 궁금증을 풀어봅시다.

### generator는 순환 가능!! 왜?
```python
for i in result:
  print(i, end=',') # 0,1,2,3,4,
print()
print(list(custom_range(5))) # [0, 1, 2, 3, 4]
print([i for i in custom_range(5)]) # [0, 1, 2, 3, 4]

generator = custom_range(2)
print(next(generator)) # 0
print(next(generator)) # 1

# 아래코드는 리스트의 아웃오브인덱스 예외와 유사하다. 더이상 진입점이 없으므로 예외를 발생시킨다.
# print(next(generator)) # raise Exception StopIteration
```

위 generator 변수에 대입된 custom_range(2) 함수는 yield 키워드에서 값을 반환하고, 다음 next()에 의해 호출될 때까지 해당 라인을 진입점으로 기억해둡니다. 이러한 진입점이 여러 개 인 함수를 코루틴(coroutine) 이라하며, 기존에 우리가 주로 사용하는 코드를 순서대로 실행하다가 return 코드를 만나고 최종 값을 리턴하면서 context를 잃는 방식을 서브루틴(subroutine)이라고 합니다. 결론은 이미 첫째줄에 말씀드렸는데요. ***"yield를 만나는 순간 Context(환경)를 포함한 제너레이터라는 객체를 반환." 결국 제너레이터라는 객체는 코루틴이라는 함수가 진입점을 여러 곳 갖고 있기때문에 호출되는 순서에 따라 Context(환경)이 달라지게 됩니다. 이로 인하여 iterable(순환가능) 할 수 밖에 없는 숙명을 띠게 됩니다.***

## Reference
[Python 3, asyncio와 놀아보기](http://b.ssut.me/58)
rochan87@gmail.com 필자의 머릿속.

<!-- ### Related Posts -->
