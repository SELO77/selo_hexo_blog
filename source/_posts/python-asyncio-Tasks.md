---
title: python-asyncio-Tasks
categories:
  - Python
  - Language
tags:
  - python
  - asyncio
date: 2016-07-24 18:04:17
thumbnail: https://encrypted-tbn1.gstatic.com/images?q=tbn:ANd9GcQ-llODQKuO5a5mGb3WdoVKmGSWnTx_KgSLzuW0rjYpdN4ptIfBTw
---

```python
# asyncio Sample for MyMusicTaste
# SELO77
# 2016-07-24
import asyncio
import traceback


class SpwanClass():

  def __init__(self):
    pass

  @asyncio.coroutine
  def execute(self, request_class_list):
    response = []
    if request_class_list:
      @asyncio.coroutine
      def run(request_class):
        try:
          result = yield from request_class.execute()
          response.append(result)
        except:
          print(traceback.format_exc())
      try:
        tasks_list = []
        for each_class in request_class_list:
          tasks_list.append(
            asyncio.Task(run(each_class))
          )
        yield from asyncio.gather(*tasks_list)
      except:
        print(traceback.format_exc())
    return response


class RequestClass1():

  def __init__(self):
    print('RequestClass1.__init()__')

  @asyncio.coroutine
  def execute(self):
    return "class1_response"


class RequestClass2():

  def __init__(self):
    print('RequestClass2.__init()__')

  @asyncio.coroutine
  def execute(self):
    return "class2_response"


@asyncio.coroutine
def main():
  try:
    request_class_list = [RequestClass1(), RequestClass2()]
    spwanClass = SpwanClass()
    final_result = yield from spwanClass.execute(request_class_list)
    print("final_result:%s"%final_result)
  except:
    print(traceback.format_exc())


loop = asyncio.get_event_loop()
loop.run_until_complete(main())


```


## Reference
* 필자 머릿속


잘못된 부분에 대한 지적은 언제든지 감사히 받겠습니다.
[rochan87@gmail.com](rochan87@gmail.com)

## Related Posts
{% post_link Python-Asyncio %}
{% post_link Python-definition %}
<br/>
