---
layout: post
title: "[Python] 1부터 N까지의 합을 구하는 3가지 알고리즘 살펴보기"
date: 2019-02-03
description: "파이썬으로 1부터 N까지의 자연수의 합을 구하는 알고리즘을 구현해봅시다."
img:  /algorithm/natural-number-sum-logo.jpg
categories: [Programming, Algorithm]
tags: [Algorithm, Gauss_sum]
---


### 목차

> 1. 들어가며
> 2. 문제 소개
> 3. 알고리즘 소개
>    - 3.1. 단순계산
>      * 3.1.1. _for_ 반복문 사용하기
>      * 3.1.2. Generator 사용하기
>    - 3.2. 분할정복
>    - 3.3. 가우스 공식
> 4. 마치며
> 5. 자료 출처


## 1. 들어가며

---

오늘 다룰 문제는 매우 유명한 문제로 바로 **1부터 N까지의 자연수를 더하는 알고리즘이다.** 알고리즘을 다루는 포스트는 정말 많은데 내 포스트의 가치는 다양한 복잡도를 갖는 여러 알고리즘을 제시한다는 데 있다고 생각한다. 그래서 이번에도 이 문제에 대한 3가지 정도의 해법을 준비했다. 이 중에서 **2번째 방법인 분할정복 방법은 모르고 있었을 수도 있어서 이를 눈여겨 보면 되겠다.**

그리고 첫 번째 방법은 세분화한 두 가지 방법으로 나눠 구해본다. 하나는 다른 언어 사용자들에게도 친숙한 _for_ 반복문을 통해서 구하고 두 번째는 Pythonic하게 Generator(이하 '제너레이터')를 통해 구해본다. 어떤 방법이 당신에게 더 친숙한가? 파이썬 유저라면 둘 다 '그냥' 익숙해야 한다. 당신은 과연 어떤지 테스트해보라.


## 2. 문제 소개

---

앞에서 이야기했듯이 해결해야 할 문제상황은 **1부터 N까지의 자연수를 모두 더한 값을 구하는 것이다.** 이때 **N은 1보다 큰 자연수이고 숫자간의 간격은 1이다.** 이 조건을 명시하고 시작하며 따라서 알고리즘들에서 입력에 대한 Validation은 생략한다. 실제로 알고리즘을 구현할 때는 입력을 검사해줘야 한다.

문제 자체가 너무 쉽고 유명해서 문제 소개는 여기까지 진행한다. 바로 알고리즘으로 넘어가자.



## 3. 알고리즘 소개

---

앞서 설명했듯이 첫 번째 방법은 가장 직관적으로 1부터 N까지 더하는 방식이다. 그냥 반복문으로 하면 재미없기 때문에 _for_ 반복문을 사용한 방법과 파이썬의 제너레이터를 사용해 합을 구하는 두 방법을 각각 구현한다.

**두 번째 방법은 분할정복을 사용한 방법으로 유도식을 눈여겨 보기를 바란다. 개인적으로는 이 포스트는 이 분할정복 방식을 기록하기 위한 목적성이 크다.**

세 번째 방법은 그 대단한 가우스가 만들어낸 방식이다. 이해하기도 쉽고 매우 유명하기 때문에 간단하게 살펴보자.


### 3.1. 단순계산

#### 3.1.1. _for_ 반복문 사용하기

1부터 N까지 구하는 식을 반복문으로 구현한다. 바로 함수를 구현해보자.


```python
def sum_for_loop(N):
    ret = 0
    for n in range(1, N+1):
        ret += n
    return ret


>>> print(sum_for_loop(100))
>>> print(sum_for_loop(1000))


5050
500500
```

가장 간단하고 상식적이며 어지간한 언어를 사용하는 프로그래머들이 쉽게 이해할 수 있는 코드다. 단순하게 1부터 N까지 더하고 있다. 더 이상의 설명은 생략한다.


#### 3.1.2. Generator 사용하기

다음은 Pythonic한 방법을 통해 구해볼 것이다. 먼저 우리의 문제를 다시 살펴보자. 우리의 문제는 1부터 N까지의 `합` 을 구하는 것이다. 파이썬에서 합을 구하는 함수로는 `sum` 이 있는데 이 _sum_ 에 헬핑을 해보자.

```
>>> help(sum)


Signature: sum(iterable, start=0, /)
Docstring:
Return the sum of a 'start' value (default: 0) plus an iterable of numbers

When the iterable is empty, return the start value.
This function is intended specifically for use with numeric values and may
reject non-numeric types.
```

뭐 다 좋은데 **_sum_ 함수의 첫 인자로 _iterable_ 이 눈에 띈다.** 이게 뭐지? 일반적으로 _sum([1,2,3,4,5])_ 와 같이 _sum_ 의 인자로 리스트를 많이 써봤을텐데 저 인자는 처음 보는 분들도 있을 것이다.  

**파이썬에서 접하는 많은 자료구조(_list_, _dict_, _tuple_ 등을 포함)은 내부적으로 많은 원시 자료구조를 상속 받는데 이 원시 자료구조는 _collections.abc_ 라는 모듈에 정의되어 있다.** 저 문서에서 **_iterable_ 은 원시 자료구조 중 하나로, 이 클래스를 상속 받으면 해당 자료구조는 반복문(_for_ 등)으로 순회할 수 있다.** 리스트나 튜플 등을 순회할 수 있는 것은(iterate) 이들이 _Iterable_ 부모 클래스를 상속 받기 때문이다. 이 상속 구조는 내장 함수인 _issubclass_ 를 통해 확인할 수 있다. 이 함수는 두 인자를 받아서 첫 번째 인자가 두 번째 인자의 자식 클래스이면 True, 아니면 False를 반환한다.


```python
from collections.abc import Iterable, Iterator, Generator

>>> print(issubclass(list, Iterable))
>>> print(issubclass(tuple, Iterable))


True
True
```

우리가 별 생각없이 배운 기본적인 자료구조의 이면에는 이런 마법이 숨겨져 있다. 이들의 구체적인 목록은 [이 페이지](https://docs.python.org/3/library/collections.abc.html){:target="_blank"}에서 확인할 수 있다. 'abc'는 'Abstract Base Class'의 약자로 이 모듈은 _list_ 같은 내장 자료구조를 포함해서 파이썬에서 자주 쓰이는 여러 자료구조의 원형 자료구조들을 담고 있다.

이 포스트의 목적은 이터레이터(Iterator), 제너레이터를 구체적으로 살피는 것이 아니기 때문에 더 깊이 들어가지는 않는다. 이번에 소개할 **Pythonic한 방법은 'Generator Expression'을 사용한 방법인데 쉽게 말해 순회가능하고, 일정 규칙 내의 숫자들을 반환하는 자료구조를 사용하는 것이다.**

바로 함수를 만들어서 보자.


```python
def sum_generator(N):
    return sum(n for n in range(1, N+1))

>>> print(sum_generator(100))
>>> print(sum_generator(1000))


5050
500500
```

아까보다 코드가 짧아져서 단 한 줄이 됐다. 띠용; 이때 _sum_ 함수 안의 'n for n in range(1, N+1)'을 보자. _sum_ 함수의 첫 인자는 'iterable'이라고 했다. 그러니까 이 식은 'iterable'이다. 실제로 그렇다. **이 식(expression)은 generator라고 하며 generator는 iterable의 서브클래스이며 이름에 걸맞게 규칙에 맞는 숫자들을 차례로 생성한다(generate). 저 식(expression)은 _for_ 문 안에서 1부터 N까지 차례로 반환하는 식(expression)이며 _sum_ 함수는 저 식을 받아 하나씩 반환되는 인자를 모두 더해 반환한다.**   

**두 방법의 시간복잡도는 어떨까? 단순하게 $$O(n)$$이다. 1부터 N까지 모두 더하기 때문이다.** 그렇기에 두 방법을 하나의 카테고리로 묶을 수밖에 없었다.

파이썬 초급과 중급을 나누는 기준이 있다고 했을 때 개인적으로 난 Iterator와 Generator를 알고 사용할 수 있는지로 판단한다. 포스트와 무관한 주제이기 때문에 여기까지 하고 넘어가는데 혹시나 관련 정보가 필요하신 분이 있다면 언제든지 연락바란다. 상세히 정리해서 포스팅할 수 있도록 하겠습니다.

일단 코드는 두 번째 방법이 압도적으로 짧은데 두 방법간의 성능 차이는 어떨까? 같은 시간복잡도인데. 일단 넘어가겠습니다.

---

### 3.2. 분할정복

두 번째는 분할정복 방법이다. 이 방법은 유도식만 이해할 수 있으면 바로 재귀함수로 구현할 수 있다. 바로 유도식을 이해해보자.

**1부터 N까지 더하는 문제에서 일단 N이 짝수라고 가정하자.**

<br>

\\[
	\displaylines{
		f(n) = 1 + 2 + \cdots + (n - 1) + n \\\\ \text{이 식을 절반을 나눠보자.} \\\\ f(n) = \left(1 + 2 + \cdots + \frac{n}{2}\right) + \left((\frac{n}{2} + 1) + (\frac{n}{2} + 2) + \cdots +  (\frac{n}{2} + \frac{n}{2})\right)
	}
\\]

<br>

\\[
\text{이때 오른쪽 절반에서 } \frac{n}{2} \text{이 } \frac{n}{2} \text{개만큼 있어서 다음과 같이 정리할 수 있다.}
\\]


\\[
  \begin{align}
	f(n) & = \left(1 + 2 + \cdots + \frac{n}{2}\right) + \left((\frac{n}{2} + 1) + (\frac{n}{2} + 2) + \cdots +  (\frac{n}{2} + \frac{n}{2})\right) \\\\ & = \left(1 + 2 + \cdots + \frac{n}{2}\right) \times 2 +  \frac{n}{2} \times \frac{n}{2}  \\\\ & = f(n / 2) \times 2 + \frac{n^2}{4}
  \end{align}	
\\]

<br>

우리의 원식을 입력이 절반으로 감소한 점화식으로 표현할 수 있게 되었다! 이제 이를 함수로 구현하면 되는데 그전에 고려해야 할 것이 남아있다.

1. **처음에 입력 $$n$$이 짝수라고 정의했다. 홀수일 때는 어떻게 할까?**
1. **재귀함수에서 꼭 필요한 바로 그것. 탈출조건(base case)은 어떻게 되는가?**

* 먼저 입력이 홀수일 때. 이는 매우 간단하다. 그냥 입력을 $$n-1$$로 주고 따로 $$n$$을 더해주면 된다.
* 두 번째. 탈출조건. 모든 짝수를 계속 줄이다 보면 그들의 최후의 보루 1이 마지막 입력이 된다. 입력이 1일 때 1을 반환하도록 하면 된다.  

이제 최종적으로 식으로 정리해보자.

<br>

\\[
	f(n) =
	  \begin{cases}
	    1 & \quad \text{if } n == 1, \\\\ n + f(n - 1) & \quad \text{elif } n \text{ is odd}, \\\\ f(n / 2) \times 2 + \frac{n^2}{4} & \quad \text{elif } n \text{ is even}
	  \end{cases}
\\]

<br>

좋다! 이 최종적인 점화식을 함수로 구현해보자.


```python
def sum_for_divide_conquer(N):
    def generate(n):
        if n == 1:
            return 1
        elif n % 2 == 1:
            return n + generate(n-1)
        else:
            return generate(n // 2) * 2 + (n ** 2) // 4
    return generate(N)


>>> print(sum_for_divide_conquer(100))
>>> print(sum_for_divide_conquer(1000))

5050
500500
```

함수 안에 재귀함수 _generate_ 을 따로 만들었다. 이 함수는 입력을 받아서 점화식의 세 가지 조건을 그대로 구현하고 있다. 식이 세워지고 나서 이 함수를 만드는 데는 3분도 안 걸렸는데 함수를 작성하기 전에 식의 뼈대를 잡는 것은 이래서 중요하다고 하겠다.

**시간복잡도는 입력을 절반으로 줄여나가면서 1까지 만들기 때문에 $$O(log_2n)$$이 된다.**

---

### 3.3. 가우스 공식 사용하기

이 식은 그 유명한 가우스 공식이다. 사실 너무 유명해서 많은 설명이 필요하지는 않다고 생각되는데, 그래도 포스트 목적상 살펴는 보고 가도록 하자.

![Portrait of Gauss](/assets/img/algorithm/natural-number-sum-gauss.jpg)

가우스(Carl Friedrich Gauss)는 19세기에 활동한 천재 수학자로 어릴 때부터 그 천재성으로 이름이 드높았다고 한다. 그것을 증명하는 일화가 몇 있는데 그중 대표적으로 초등학생 때 선생님이 낸 1부터 100까지 더하라는 문제를 고작 수 초 안에 풀어서 선생님을 깜짝 놀라게 했다는 일화가 있다. 이 유명한 일화는 부정확할 수 있고 심지어 혹자는 사실이 아닐 것이라고까지 생각한다는데, 어쨌든 이번에 사용할 가우스 공식은 이 일화에서 '수 초 안에' 풀었다는 방법을 그대로 사용한다. 

<br>

1부터 $$n$$까지 더해나갈 때 $$n$$이 100이라고 하자. 그리고 그 합을 $$S$$라고 해보면 다음과 같이 쓸 수 있다.

\\[
\begin{align}
	S & =   1 +  2 +  3 + \cdots + 98 + 99 + 100 \\\\ & = 100 + 99 + 98 + \cdots +  3 +  2 +   1
\end{align}
\\]

두 표현식은 그냥 순서만 뒤집었다. 근데 이를 위아래로 더해보면 다음과 같이 정리된다.

<br>
\\[
	2S = 101 + 101 + 101 + \cdots + 101 + 101 + 101
\\]

<br>
신기하게도 각 항이 모두 101($$n + 1$$)이 된다. 그리고 항의 총 개수는 $$n$$개가 된다. 

<br>

\\[
	2S = 101 * 100
\\]

이 값은 원래 값 $$S$$의 두 배이기 때문에 절반으로 나누어 주면...

<br>
\\[
\begin{align}
	S = 101 * 100 / 2 \\\\ = 5050
\end{align}
\\]

<br>
이 식을 자연수 $$n$$으로 일반화하면 다음 식이 나온다.

<br>
\\[
	1 + 2 + \cdots + (n-1) + n = \frac{(n + 1) \times n}{2}
\\]

<br>

**시간복잡도가 $$O(1)$$로** 미쳤다고 밖에 할 수 없다. 실제로 컴퓨터가 아닌 사람이 계산해도 '수 초만에' 답이 나오는 식이고 가우스가 정말로 이 식을 초등학생 때 만들었다면 놀라지 않을 수 없다.

---

## 4. 마치며

---

오늘은 1부터 N까지 더하는 알고리즘을 살펴봤다. 알고리즘을 조금이라도 공부하는 분들은 첫 번째와 세 번째는 어지간하면 알 것이라고 생각한다. 하지만 두 번째는 모를 수도 있고 그 유도식도 퍽 재밌다. 그래서 정리해야겠다고 생각했다.  

사실 이 포스트는 알고리즘 소개와 함께 4가지 알고리즘(시간복잡도는 3개)의 입력의 크기에 따른 성능 비교를 하려고 했다. n을 1000부터 1억 정도까지 키우면서 실행시간이 어떻게 증가하는지를 파이썬의 그래프 라이브러리를 통해 그려보려고 했는데 알고리즘 소개만 해도 생각보다 커져서 한 포스트에 다 적으면 안 되겠다고 생각했다. 관련 라이브러리를 공부해서 차후 성능 비교를 해보도록 하자. 

이상 포스트를 마칩니다.



## 5. 자료 출처

---

* [Python 3. Collections.abc](https://docs.python.org/3/library/collections.abc.html){:target="_blank"}
* [Wikipedia: Carl Friedrich Gauss](https://en.wikipedia.org/wiki/Carl_Friedrich_Gauss){:target="_blank"}
* 『알고리즘 문제 해결 전략』7장 분할정복, 구종만, 인사이트(insight)
