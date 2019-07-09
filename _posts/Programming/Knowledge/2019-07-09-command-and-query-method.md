---
layout: post
title: "Command와 Query, CQS 알아보기"
date: 2019-07-09
description: "함수를 크게 범주화할 수 있는 Command, Query method에 대해 알아보고 추가로 CQS까지 살펴봅니다."
img:  /knowledge/cqs-logo.jpeg
categories: [Programming, Knowledge]
tags: [CQS]
---

## 0. Index

> 1. [들어가며](#1)
> 2. [Betrand Meyer](#2)
> 3. [개념 소개](#3)
>    - 3.1. [Query vs Command](#3a)
>    - 3.2. [Command Query Separation](#3b)
> 4. [마치며](#4)
> 5. [자료 출처](#5)


<br id="1">

## 1. 들어가며

---

아는 사람은 알지만, 나는 프로그래밍 교육 기관에서 조교, 코칭 일을 적잖이 했다. 아무래도 요즘 프로그래밍 입문을 파이썬으로 많이 하다보니 파이썬을 공부하는 내가 설 자리가 있었던 것 같다. 그래서 프로그래밍을 처음 하는 사람들에게 변수, 할당, 함수 등 초보적인 개념부터 설명할 일이 많았는데 특히 함수를 공부할 때 `list.sort()`와 `sorted()`처럼 비슷한 일을 하는데 구체적인 동작은 다른 형태에 대해 많은 코칭이 필요했다.

위 두 함수를 입문자에게는 'list를 정렬할 때 사용하는 두 가지 방법'이라고 설명한다. 근데 둘은 뚜렷이 구분되는 동작을 한다. 첫 번째 함수의 특징은 값이 반환되지 않아서 변수 할당에 사용할 수 없는데 두 번째는 그 반대다. 처음 공부하시는 분들이 이 두 가지를 혼동하는 경우가 많았고 그래서 `a = list.sort()`와 같은 실수를 많이 봤다. 이런 혼동은 비단 정렬 기능에만 해당하는 것이 아니다.

그래서 **오늘은 함수를 크게 두 가지로 구분하는 Command와 Query에 대해 공부한다.** 먼저 이 개념을 소개한 Betrand Meyer에 대해 간략히 살펴본다. 프로그래밍 분야에 큰 공헌을 한 분이라고 한다. 다음으로 Command와 Query에 대해 본격적으로 다루는데 이는 실무와는 큰 관련은 없지만 프로그래밍을 처음 공부하는 분들에게는 함수의 개념을 이해하기에 꽤나 유용하다. 경험칙으로 확인했다. 그리고 '한 함수에서 Command와 Query를 구분하는 것이 좋다'는 원칙인 CQS에 대해서도 살핀다.

이 포스트를 지난번에 맡은 구모 씨에게 바친다.


<br id="2">

## 2. Betrand Meyer

---

Command와 Query, 그리고 CQS를 알아보기 전에 먼저 이 개념들을 소개한 사람을 간략히 알아보자.


![Betrand Meyer](http://psi.iis.nsk.su/system/files/bertrand_meyer_240.jpg)

Betrand Meyer(이하 '메이어')는 프랑스 학자로 컴퓨터 언어 분야에 크게 공헌한 인물이다. OOP에 공헌했고 Design By Contract라는 개념을 소개한 인물로도 알려져 있다. 특히 Eiffel 언어를 창조했는데 언어의 이름이 이 사람이 프랑스 사람인 것과 무관하지 않아 보인다.

저서 'Object Oriented Software Construction'에서 CQS를 소개했다.


<br id="3">

## 3. 개념 소개

---

<br id="3a">

### 3.1. Query vs Command

함수는 코드 블록에 대한 추상화다. 함수는 매우 중요하고 기본적인 프로그래밍 요소로 나도 방금 쓰고 왔다. 인간은 나누는 것을 참 좋아하는데, 함수도 필요에 따라 몇몇 범주로 나눌 수 있을 것이다. 이때 Meyer는 **시스템의 상태를 바꾸는지**를 기준으로 함수를 크게 두 가지로 분류한다.

* **Query**:
  - 결과값을 반환하고, 시스템의 관찰가능한 상태를 변화시키지 않는다. 따라서 부작용에서 자유롭다.(free of side effects)
* **command**:
  - 결과를 반환하지 않고, 대신 시스템의 상태를 변화시킨다.

<br>

이 둘을 이해하는 것은 어렵지 않다.

먼저 Query. **Query는 영어로 '질의'라는 뜻을 가지기 때문에 질문에 따른 답을 반환해야 한다. 함수가 Query라면 함수는 다른 값을 바꾸지 않고 오직 질문에 대한 답을 반환한다.** 간단한 예제를 만들어볼 수 있겠다.

```python
l = [1, 2, 3, 4, 5]

print(max(l))

5
```

_max_ 함수를 사용해 배열의 원소의 최대값을 반환했는데 이 함수를 통해 값이 반환됐지만 원 배열에 변화가 발생하지는 않았다. 따라서 _max_ 내장 함수는 Query 메소드라고 할 수 있다.

<br>

Command는 '명령'이라는 뜻을 가지고 있다. 군대를 생각해보자. 상명하복이라는 말이 있듯 군대에서는 상관의 명령에 대해 말대답보다는 실제 액션이 기대된다. 이런 의미에서 **함수가 Command라면 Query와 달리 꼭 값을 반환하지 않더라도 실제 시스템의 상태를 영구적으로 변화시킨다는 의미를 갖고 있다.** 그런 의미에서 Command를 'modifier', 'mutator' 등으로 표현하기도 한단다.

```python
l = [1, 2, 3, 4, 5]
l.reverse()

print(l)

[5, 4, 3, 2, 1]
```

원 배열에 _list.reverse()_ 메소드를 사용해 배열을 뒤집었다. 이 메소드는 결과값을 반환하지 않고 다만 원 배열의 상태를 영구히 변경할 뿐이다. 따라서 _list.reverse()_ 는 Command 메소드다.

<br>

상태를 바꾸는 함수와 바꾸지 않는 함수의 구분은 꽤나 유용하다. **상태를 바꾸지 않는 함수는 안전하기 때문에 더 신뢰성을 갖고, 별다른 주의없이 원하는 대로 사용할 수 있다. 반면에 상태를 바꾸는 Command는 함수간 사용순서를 신중하게 짜야하고 부주의하게 실행하면 전혀 예상못한 결과가 나올 수 있음을 의미한다.**

이런 구분은 HTTP method와도 연결된다. HTTP method는 10여 가지가 있는데 이때 서버의 상태를 변경하지 않는 메소드를 '안전하다'(safe)고 한다. 다른 말로는 CRUD 중에 Read-only 액션만 한다고 할 수 있다.

**HTTP에서 GET은 대표적인 안전한 메소드로서 자원의 상태만을 요청하기 때문에 서버측에서 별다른 주의없이 대응해도 된다. 반면 POST 등의 안전하지 않은 메소드는 자원의 상태를 변경하기 때문에 서버 입장에서 신중하게 다루어야 한다. 이때 GET은 Query에 대응되고, POST는 Command에 대응된다.**

---

<br id="3b">

### 3.2. Command Query Separation

앞선 장에서 Command와 Query의 차이를 알아봤다. Command는 '명령'으로, 값을 반환하는 대신 상태를 변경한다. Query는 '질문'의 의미로 상태를 변화시키지 않고 값을 반환한다. **메이어는 한 함수가 Command 또는 Query 중 하나의 역할만 할 것을 강조했다. 이 프로그래밍 원칙을 Command Query Separation, CQS라고 하며 이 둘을 구분하는 것의 장점은 위에서 말한 두 개념 구분의 장점과 일맥상통하다.** 한 함수가 Command이면서 Query이기도 하다면 두 개념을 나누는 장점이 상쇄되기 때문이다.  

하지만 여기에도 예외는 있다. 쉬운 예로 스택의 pop 액션을 보자. 보통 pop 액션은 스택의 맨 위의 값을 빼서(command) 반환(query)하는 일까지 병행한다. 이 일반적인 액션은 명확히 command와 query를 겸임하고 있는 상태다. 이런 예외는 어떻게 대처해야 할까?

일단 내 생각과 다른 사람들의 일반적인 의견은 '**가능하다면 CQS를 지키되, 예외가 필요할 때는 허용하자**'다. 예외없는 법칙이 어디 있겠는가? 다만 CQS를 지키는 것이 유용하기 때문에 최대한 지키고 그럴 수 없는 경우에는 기능에 대한 문서화를 좀더 충실히 해놓는 것이 바람직하겠다.



<br id="4">

## 4. 마치며

---

이번 포스트에서는 Command와 Query, 그리고 Command Query Separation의 개념에 대해 살펴봤다. 확실히 내용이 어렵지는 않다. 함수의 `return`문을 쓸 수 있기만 하면 이해되는 수준이다. 이 포스트가 프로그래밍에서 함수를 처음 접하는 분들에게 이해의 물꼬를 터줄 수 있기를 바래본다.

이상 포스트를 마칩니다.



<br id="5">

## 5. 자료 출처

---

* [Martin Fowler: CQS](https://martinfowler.com/bliki/CommandQuerySeparation.html){:target="_blank"}
* [Wikipedia: Betrand Meyer](https://en.wikipedia.org/wiki/Bertrand_Meyer){:target="_blank"}
* [Wikipedai: CQS](https://en.wikipedia.org/wiki/Command%E2%80%93query_separation){:target="_blank"}
