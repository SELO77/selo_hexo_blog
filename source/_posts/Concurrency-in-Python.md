---
title: Concurrency in Python
categories:
  - Python
  - Language
tags:
  - Concurrency
  - python
  - asyncio
  - thread
  - multiprocess
thumbnail: >-
  https://selo77.github.io/2016/09/02/python-datetime-strftime-example/python-icon.png
date: 2016-12-11 00:14:24
---
안녕하세요. SELO 입니다. 저희 회사에서는 격주 단위로 개발세미나를 진행하는데요. 개발자가 자유롭게 주제를 선택하여 세미나를 진행한답니다. 최근에 개인적으로 관심을 두고 있던 Concurrency에 관하여 세미나를 진행하게 되었고, 그 내용을 정리해보려 합니다.

전반적인 내용은 다음과 같습니다. Concurrency의 개념을 정리하고, Python에서의 Concurrency 구현에 대하여 살펴보겠습니다.

## Concurrency and Parallelism
동시성은 무엇이고, 병렬성은 무엇일까요? 잠시 생각해보고, 스스로 답변해보세요. 명확하게 정리가 되신다면 이 파트는 뛰어넘으셔도 됩니다. 그렇지 않으시다면 저와 같이 정리를 한번 해봅시다.

> 컴퓨터 과학에서 동시성이란 프로그램, 알고리즘 또는 문제가 분리될수 있는 속성을 말합니다. 즉, 프로그램 또는 알고리즘들이 무작위나 부분적 순서를 갖고 실행 되더라도 동일한 최종결과를 얻습니다.
[ Concurrency (Computer Science) - wikipedia](https://en.wikipedia.org/wiki/Concurrency_(computer_science))

위키피디아에 정의된 동시성 정의는 위와 같습니다. 개념자체가 추상적이기 때문에 한 번에 이해하기가 조금 어렵습니다. 조금 더 구체적으로 정의하자면 동시에 두 개 이상의 작업을 다루는 구조를 동시성이라 합니다. 그렇다면 병렬성은 무엇일까요? 우리가 알고 있는 병렬성도 분명히 두개 이상의 작업이 함께 다루어지는 것 아닌가요?

> 컴퓨터 과학에서 병렬처리란 많은 계산이나 프로세스 실행이 동시에 수행되는 일종의 실행 방식입니다.
[Parallel computing - wikipedia](https://en.wikipedia.org/wiki/Parallel_computing)

한마디로 병렬성은 두 개 이상의 연산이 동시에 처리되는 실행 방식입니다. 동시성 보다는 개념이 더 뚜렷해보이지 않나요? 그 이유는 차차 알게되겠지만 **병렬성은 일종의 실행방식에 대한 개념이고, 동시성은 구조에 관한 개념이기 때문에 훨씬 더 추상적입니다. 그리고 비동기, 병렬처리 등과 같은 동시성 구현을 위한 처리나 실행 방식의 개념을 포괄합니다.**


아래 그림은 동시성과 병렬성의 이해를 위한 극단적인 예시입니다. 하지만 혼동되는 개념을 정리하는데 도움이 됩니다. 그림을 보아도 혼동이 된다면 아래 정리만 기억해주세요.

{% asset_img Concurrency_vs_Parallelism.png Concurrency Vs Parallelism %}

**동시성은 동시에 많은 것을 다루는 구조**
**병렬성은 동시에 많은 것을 실행하는 처리방식**


## Implement Concurrency in Python
이번 부분에서는 파이썬에서 동시성 구현해보고, 각 방법의 차이를 이해하는 시간을 갖겠습니다.

### threading
동시성 구현에서 개발자에게 가장 익숙한 것은 스레드가 아닐까 생각됩니다. 스레드는 기본적으로 독립적인 실행 흐름을 갖고, 프로그램의 메모리를 공유합니다. 스레드의 개념을 짚고 넘어가는 이유는 차후 얘기하게 될 파이썬에서의 스레드가 갖게 되는 제약을 명확히 이해하기 위해서입니다.


* **cpu/0basic.py**
```python
# cpu/0basic.py
import time


def do_work(start, end, result):
    sum = 0
    for i in range(start, end):
        sum += i
    result['sum'] = sum


if __name__ == '__main__':
    START, END = 0, 100000000
    result = {}
    st = time.time()
    do_work(START, END, result)
    print('== sum:{} running time {:.4f}s'.format(result['sum'],time.time() - st))
    # == sum:4999999950000000 running time 8.6880s
```
위 코드는 단순히 0 부터 100000000(일만)까지 순차적으로 더한 후 실행시간을 출력하는 프로그램입니다. 동시성이 구현되지 않은 절차식 코드입니다. 제 컴퓨터 기준 8.6s의 실행시간이 출력되었습니다.

반면 아래 코드는 파이썬 `threading` 모듈을 사용해서 두개의 스레드를 생성한 후 더하기 작업을 반씩 나누어 처리하는 코드입니다. 예측되는 실행시간은 절차식 코드의 실행시간의 절반인 4~5초 언저리가 될것입니다.


* **cpu/1thread.py**
``` python
# cpu/1thread.py
import os
import time
from threading import Thread

def do_work(start, end, result):
    # print(os.getpid())
    sum = 0
    for i in range(start, end):
        sum += i
    result.append(sum)


if __name__ == "__main__":
    START, END = 0, 100000000
    result = list()
    st = time.time()
    th1 = Thread(target=do_work, args=(START, int(END/2), result))
    th2 = Thread(target=do_work, args=(int(END/2), END, result))
    th1.start()
    th2.start()
    th1.join()
    th2.join()
    print('==sum:{}, running time {:.4f}s'.format(sum(result),time.time() - st))
    # ==sum:4999999950000000, running time 8.9179s
```

실행 결과는 우리가 예상했던 바와는 너무도 다릅니다. 출력된 실행시간을 보면 8.9s로 스레드를 구현하지 않은 코드보다 조금 더 느립니다. 스레드가 정상적으로 작동하였다면 이런 결과는 나올수가 없겠죠.
이유는 바로 GIL(Global Interpreter Lock) 이라는 놈때문 입니다.

> Global interpreter lock (GIL) is a mechanism used in computer language interpreters to synchronize the execution of threads so that only one native thread can execute at a time.
[Global interpreter lock - Wikipedia](https://en.wikipedia.org/wiki/Global_interpreter_lock)

GIL에 대해서 다루는 포스팅은 아니기에 짧게 설명하고 넘어가도록하겠습니다. GIL은 한번에 한 스레드만 파이썬 바이트 코드를 실행하도록 강제합니다. 그렇기 때문에 단일 파이썬 프로세스가 동시에 다중 CPU 코어를 사용할 수 없습니다. 그렇다면 제대로 쓰지도 못하는 스레드 모듈을 왜 만들었을까요?

GIL에 대한 자세한 내용은 아래 문서를 참고하세요.
[UnderstandingGIL](http://www.dabeaz.com/python/UnderstandingGIL.pdf)

* **io/0basic.py**
```python
# io/0basic.py
import time
from urllib.request import urlopen

urls = ['http://www.naver.com',
       'https://www.google.com',
       'https://www.apple.com',
       'http://www.bing.com/'] * 10


def fetch(url):
    print('Start with', url)
    urlopen(url)
    print('End', url)


st = time.time()
for url in urls:
    fetch(url)


print("duration(s):{:.4f}".format(time.time() - st))
# duration(s):6.0583
```

이번 코드에서는 40개의 url에 해당하는 http network 작업을 절차적으로 실행합니다. 대략 6.0s 실행시간이 걸렸습니다. 아래코드는 같은 문제를 4개의 thread를 생성 작업하는 방식입니다.


* **io/1thread.py**
```python
import time
from concurrent.futures import ThreadPoolExecutor
from urllib.request import urlopen

urls = ['http://www.naver.com',
       'https://www.google.com',
       'https://www.apple.com',
       'http://www.bing.com/'] * 10
NUM_WORKERS = 4

def fetch(url):
    print('Start with', url)
    urlopen(url)
    print('End', url)


st = time.time()

with ThreadPoolExecutor(max_workers=NUM_WORKERS) as th:
    for url in urls:
        th.submit(fetch, url)


print("duration(s):{:.4f}, NUM_WORKERS:{}".format((time.time() - st), NUM_WORKERS))
# duration(s):1.6696, NUM_WORKERS:4
```

첫번째 `cpu/1thread.py`는 스레드가 정삭적을 작동하는것 같아 보이지 않습니다. 스레드를 사용했음에도 불구하고 절차코드보다 느린 실행시간이 걸렸습니다. 그렇다면 이번 `io/1thread.py` 코드도 스레드가 정상적으로 작동하지 않았을까요? 아닙니다. 출력된 내용을 보면 1.6s의 실행시간이 걸렸습니다. 절차형 코드 6.0s 비해 1/4 실행시간이 걸렸습니다. 왜 이런 차이가 생기는 걸까요?

코드가 해결하려하는 핵심 작업의 종류가 다르기 때문입니다. 첫번째 스레드 코드는 CPU-Bound 작업이 중심이였고, 두번째 스레드 코드는 IO-Handling이 주된 작업이었습니다. 각 작업의 특성을 생각해본다면 원인을 유추해낼수 있습니다. CPU-Bound 작업은 연산이 지속적으로 이루어지깄때문에 싱글 스레드 기반에서는 Context-switching 할 여유가 없습니다. 하지만 IO-Bound 작업은 대부분의 시간을 대기시간으로 보내게 되고 이때 GIL은 해제됩니다. 해제됨과 동시에 다른 스레드가 실행됩니다.

그렇다면 파이썬에서 CPU-Bound 작업을 동시 처리할 수 있는 무언가는 없을까요?

### multiprocessing

* **cpu/2process.py**
```python
import time
import os
from multiprocessing import Process, Queue


def do_work(start, end, result):
    sum = 0
    for i in range(int(start), int(end)):
        sum += i
    result.put(sum)
    return


if __name__ == '__main__':
    START, END = 0, 100000000
    result = Queue()
    st = time.time()
    pr1 = Process(target=do_work, args=(START, END / 2, result))
    pr2 = Process(target=do_work, args=(END / 2, END, result))
    pr1.start()
    pr2.start()
    pr1.join()
    pr2.join()
    result.put('STOP')
    sum = 0
    while True:
        tmp = result.get()
        if tmp == 'STOP': break
        else: sum += tmp

    print('==sum:{}, running time {:.4f}s'.format(sum, time.time() - st)) #  3.9502s
```
`cpu/1thread.py`의 실행시간 8.9s에 비해 3.9s라는 1/2 정도의 실행시간이 걸렸습니다. 실행시간 단축이 주는 의미를 풀어보자면 동시에 두 가지 작업이 함께 진행되었을 것입니다. 위 코드가 CPU-Bound 중심의 작업을 처리하기때문에 특별히 wating time을 갖지 않습니다. 결국 두개의 프로세스가 계속적으로 연산을 처리하지 않았다면 `cpu/1thread.py`와 비슷한 실행시간이 걸렸을 것입니다.

`multiprocessing` 은 스레드 대신 하위 프로세스를 사용하여 GIL 효율적으로 회피합니다. 결론부터 말하자면 우리가 원하던 병렬처리가 가능해집니다. 각 프로세스는 독립된 메모리공간을 갖고 동시에 진행되며, 결국 프로그래머는 컴퓨터 상의 다중 프로세스를 완벽하게 활용할 수 있게됩니다. (물론 완벽한 병렬처리가 진행되려면 컴퓨터가 다중코어여야 합니다.)



### asyncio

asyncio 는 파이썬 3.4 에서 새롭게 추가된 비동기 I/O 패키지입니다. asyncio 패키지는 이벤트루프에 운용되는 코루틴을 이용해서 동시성을 구현합니다. 이번 포스팅에 담기에는 방대한 내용이기에 구현 방법만 살펴보겠습니다. 자세한 내용은 아래 링크를 살펴보시면 도움이 될것입니다.

[PYTHON: GENERATORS, COROUTINES, NATIVE COROUTINES AND ASYNC/AWAIT
](http://masnun.com/2015/11/13/python-generators-coroutines-native-coroutines-and-async-await.html)
[Python3, asyncio와 놀아보기](http://b.ssut.me/58)

* **io/2asyncio.py**
```python
import asyncio
import time
from urllib.request import urlopen


import aiohttp


urls = ['http://www.naver.com',
       'https://www.google.com',
       'https://www.apple.com',
       'http://www.bing.com/'] * 10


@asyncio.coroutine
def fetch(url):
    print('Start with', url)
    res = yield from aiohttp.request('GET', url)
    res.close()
    print('End', url)


st = time.time()
def fetch_all(urls):
    loop = asyncio.get_event_loop()
    fetchs = [fetch(url) for url in urls]
    wait_coro = asyncio.wait(fetchs)
    loop.run_until_complete(wait_coro)
    loop.close()


fetch_all(urls)
print("duration(s):{:.4f}".format(time.time() - st))
# duration(s):0.8603
```

(참고: `asyncio`는 TCP와 UDP 프로토콜만 지원합니다. HTTP 등의 프로토콜을 지원하려면 `aiohttp`와 같은 서드파티 패키지가 필요합니다.)

`asycnio`는 아래 그림과 같은 방식의 이벤트 루프를 중심으로 운용되며 이벤트 루프가 큐에 있는 코루틴을 하나씩 활성화하는 단일 스레드 프로그램입니다. 이러한 개념을 기억해주시고 코드를 살펴보면 이해하는데 도움이 될것입니다.

{% asset_img eventloop.png EventLoop %}


각 url을 파라미터로 받는 `fetch()` coroutine 을 list에 담아 `asyncio.wait(fetchs)` 함수에 넘겨줍니다. `asyncio.wait()`은 넘겨준 리스트의 coroutine을 이벤트루프가 스케줄링 가능한 Task Object로 warapping합니다. 이벤트 루프가 테스크를 모두 완료하고 프로그램은 종료됩니다. 실행시간은 0.9s가 걸렸습니다. 절차식 코드나 스레드 코드에 비하면 엄청난 속도 개선입니다. 물론 스레드 워커수를 가용가능한 최대치로 설정 후 실행한다면 속도는 비슷하게 나오리라 예상됩니다. 하지만 스레드로 복잡한 프로그램을  구현해 보셨다면 스레드의 스케줄링이 얼마나 어려운 작업인지 잘 아실 것입니다. 락을 잠고, 블락당하지 않게 해야 합니다. 하지만 코루틴기반의 `asyncio`의 사용은 개발자가 `yield` 명시만으로도 스케줄링이 가능하고 방해받지 않습니다.


실제로 `asyncio`는 내부적으로는 커널 수준까지 내려가는 저수준 스레드에 의존하지만, 패키지 사용자 즉 개발자는 스레드를 생성하거나 내부적으로 스레드가 사용되고 있다는 사실을 알 필요가 없습니다. 어플리케이션 수준에서 단지 우리가 작성한 코드가 블로킹되지 않게 보장하면 되며, 이벤트 루프가 동시성에 대한 나머지 모든 작업을 처리해줍니다. 결국 개발자가 스레드를 관리할 필요성을 제거함으로써 멀티스레드 시스템보다 더 많은 동시성 연결을 쉽게 관리할 수 있습니다.

## Conclusion
파이썬에서의 동시성 구현 방법들에 관하여 살펴보았습니다. 동시성 관련 개념들은 점점 더 중요해지고 있습니다. 그 이유는 다들 아시겠지만 과거 개발환경은 대부분 멀티쓰레딩 환경에서 하나의 CPU를 효율적으로 공유하도록 만드는데 초점이 있었습니다. 하지만 현재 멀티코어 시대에는 기존 방식으로는 성능향상의 한계가 있습니다. 그렇기에 병렬, 비동기 프로그래밍, 분산 컴퓨팅, 함수형 프로그래밍, 빅테이터, 인공지능 등 다양한 기술들이 동시성 패러다임과 함께 발달하고 있습니다.

Concurrent in Python 한정적인 주제로 진행했지만, 제가 전달하고 싶은 내용은 단순히 구현하는 방법이 아닌 **동시성 관점과 사고를 갖고 개발할 수 있는 개발자가 되자!** 입니다.


PS. 이렇게 인생의 첫 세미나가 이렇게 끝났네요. 느낀 점은 사용하는 것과 아는 것은 다르고, 가르침은 또 다른 범위의 문제라는 것을 깨달았습니다. 분량조절과 범위선정은 정말 어려웠습니다. 관련된 개념은 너무 많은데 주어진 시간에 정확한 내용을 전달하려면 무엇을 간략히 하고 정리해야할지... 미숙함이 많은 세미나였고, 내용이었지만 개인적으로는 정말 좋은 경험이 되었습니다. 40km 유격 행군보다 몇배는 힘든 세미나 준비였지만 이 문장을 끝으로 마무리하겠습니다. 감사합니다.







## Reference
* [An Introduction to Python Concurrency](http://www.slideshare.net/dabeaz/an-introduction-to-python-concurrency)
* [Async python](http://masnun.rocks/2016/10/06/async-python-the-different-forms-of-concurrency/)
* [책: Fluent Python](http://book.naver.com/bookdb/book_detail.nhn?bid=8781382)

잘못된 부분에 대한 지적은 언제든지 감사히 받겠습니다. 포스팅의 첫번째 목적은 작성자의 학습이므로 Context가 틀어지는 경우가 있을 수 있습니다.
[rochan87@gmail.com](rochan87@gmail.com)

## Related Posts
* {% post_link python-asyncio-Tasks %}
* {% post_link Python-Asyncio %}
<br/>
