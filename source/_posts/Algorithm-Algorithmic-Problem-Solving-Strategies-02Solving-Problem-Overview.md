---
title: Algorithmic Problem Solving Strategies(알고리즘 문제해결전략) - 02문제 해결 개관
categories:
  - Base
  - Algorithm
tags:
  - Algorithm
  - ProblemSolvingStrategies
date: 2016-07-10 14:10:43
thumbnail: http://book.algospot.com/static/img/cover1-small.png
---
## 2.1 도입
이번장은 추상적인 프로그래밍의 과정을 좀더 체계적으로 수련하기 위한 과정을 여러 단계로 나눠 보고 각 단계를 더 잘하기 위한 전반적인 기술들을 소개합니다. 특히 구체적인 체계없이 프로그래밍을 시작하는 저와 같은 프로그래머들에게 깨닮을 줍니다. 첫번째장에서 알고리즘의 필요성과 공부를 위한 마음을 가다듬었다면 이번장에서는 앞으로 배우게될 것들에 대한 프리뷰가 되겠습니다.

## 2.2 문제 해결 과정
알고리즘은 무엇인가? 저는 이렇게 답변했습니다. "알고리즘은 어떤 특정문제를 해결하기 위한 과정과 방법의 정의" 무언가를 공부할때 개념에 대한 본인만의 정의를 갖는것은 매우 중요합니다.

> 프로그래밍 대회를 위한 여섯 단계 문제 해결 알고리즘
>1. 문제를 읽고 이해한다.
>2. 문제를 익숙한 용어로 재정의한다.
>3. 어떻게 해결할지 계획을 세운다.
>4. 계획을 검증한다.
>5. 프로그램으로 구현한다.
>6. 어떻게 풀었는지 돌아보고, 개선할 방법이 있는지 찾아본다.

1. **문제를 읽고 이해합니다.**
2. **재정의와 추상화.** 문제를 익숙한 용어로 재정의 하며 추상화 과정을 통해 프로그래밍이 나아갈 방향을 결정합니다. 이 부분에서 추상화를 좀 더 구체적으로 정의하자면, 객체지향에서 현실세계의 존재를 클래스화 하는 과정과 비슷하다고 이해 하시면됩니다. 문제를 우리가 이해하기 쉬운 수학이나 전산 개념으로 표현하는 과정이라 생각합니다. 추상화 과정은 좋은 프로그래머가 되기 위한 필수적인 조건이며 이 단계를 넘지 못한다면 좋은 프로그래머가 되지 못할 것이라 생각됩니다.
3. **계획 세우기.** 이 단계는 문제해결의 과장 중요한 과정이며 사용할 알고리즘과 자료구조를 선택합니다.
4. **계획 검증하기.** 제가 주로 간과하는 부분입니다. 이 단계에서는 시간복잡도와 공간복잡도의 문제를 고려합니다.
5. **계획 수행하기.**
6. **회고 하기.** 이 단계는 제가 최근 가장 중요하게 여기는 부분입니다. 블로그에 굳이 공부한 내용을 포스팅 하는이유도 다른 사람에게 보여주기 보다는 회고의 과정을 통해 지식의 견고함을 갖추기 위함입니다. 문제 해결에서 효과적 회고 수행은 문제를 풀 때마다 코드와 함께 본인만의 로그를 남기는 것입니다. 물론 문제를 맞추지 못한 경우에도 해당하며 부족한 부분을 감지하고, 다른 사람의 코드를 보면서 새로운 통찰을 얻곤합니다.

>**잠시만요!!**
[코드전쟁](www.codewars.com) - 사이트 이름처럼 쉬운 문제부터 고난이도 문제까지 닥치는대로 풀어 볼 수  있는 기회를 제공하며, 무엇보다 다른 사람의 작성된 답안을 보면서 코드 작성의 수준을 향상시킬 수 있습니다.

## 2.3 문제 해결 전략
프로그래머에게 문제를 이해하는 직관의 수준은 곧 그 프로그래머의 수준이고 생각합니다. 이렇게 중요한 직관은 하루아침에 만들어 질 수 없으며, 체계적인 학습과 경험 없이는 향상시킬수 없다 생각합니다.

> ### 체계적인 접근을 위한 질문들
>* 비슷한 문제를 풀어본 적이 있던가?
>* 단순한 방법에서 시작할 수 있을까?
>* 내가 문제를 푸는 과정을 수식화할 수 있을까?
>* 문제를 단순화할 수 없을까?
>* 그림으로 그려볼 수 있을까?
>* 문제를 분해할 수 있을까?
>* 뒤에서부터 생각해서 문제를 풀 수 있을까?
>* 순서를 강제할 수 있을까?
>* 특정 형태의 답만을 고려할 수 있을까?

## 중간 정리
1장과 2장을 통해 문제 해결 능력을 정의 하고 향상시키기 위해 필요한 과정들을 집어보았습니다. 그럼 다음 포스팅에는 낮은 수준?의 알고리즘을 문제를 풀어보면서 위 에서 학습한 과정과 전략들을 적용해 보겠습니다. 문제 ==> https://algospot.com/judge/problem/read/FESTIVAL#

## Reference

* [(책) 알고리즘 문제해결전략 - 구종만](http://book.naver.com/bookdb/book_detail.nhn?bid=7058764)

<br/>
잘못된 부분에 대한 지적은 언제든지 감사히 받겠습니다.
[rochan87@gmail.com](rochan87@gmail.com)

## Related Posts
{% post_link Algorithm-Algorithmic-Problem-Solving-Strategies %}
