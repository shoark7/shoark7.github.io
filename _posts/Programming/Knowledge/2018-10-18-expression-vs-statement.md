---
layout: post
title: 코드 단위인 Expression과 Statement의 차이를 알아보자
date: 2018-10-18
description: What is the difference between expression and statement?
img:  /knowledge/logo-expression-statement.jpg
categories: [Programming, Knowledge]
tags: [Expression, Statement, expression-vs-statement]
---

## 들어가며

---

프로그래밍을 공부하며 알게 모르게 expression과 statement라는 표현을 보게 된다. 일례로 우리가 처음 책에서 배우는 프로그래밍에서 'if 문'이라고 배우는 것은 영어로 `if statement`다. expression은 수학과 관련된 알고리즘을 찾다보면 조금씩 보이는 것 같다. 하지만 난 이 둘의 차이를 몰랐는데, '그냥 둘 다 코드 한 줄을 의미한다'고 생각하고 넘어갔던 것 같다.  

그러다 이 둘을 구분해야 할 시기를 마주쳤는데 바로 파이썬의 `eval`, `exec` 내장 함수를 만나서이다. 둘은 메타프로그래밍을 가능케 하는 함수로 비슷하지만 애매하게 달랐다. 그리고 그 중심에는 expression과 statement의 구분이 자리잡고 있었다.  

그래서 **이번 포스트에서는 expression과 statement를 각각 알아보고 그 둘의 집합 관계를 살펴보고자 한다.** 꼭 파이썬이 아니더라도 컴퓨터 공학적으로 알아두면 의미 있을 것이라 생각한다.


## Expression

---

**Expression은 '수식'이라는 뜻으로 하나 이상의 값으로 표현(reduce)될 수 있는 코드를 말한다.** 수식이라는 뜻에 맞게 우리가 일상생활에서 하는 사칙연산식이 곧 expression이다. 가령 '1+1', '2+5' 등등.  

**일상생활에서의 수식은 숫자와 연산자만으로 이루어지는 것과 달리 컴퓨터 과학에서 수식은 함수 콜(), 변수 이름 등의 식별자, 배열 등의 할당 연산자([]) 등까지도 포함한 식을 의미한다. 핵심은, expression들은 평가(evaluate)가 가능해서 하나의 '값'으로 환원된다는 것이다.**

```python
def get(n):
    return n

a, b, c = 1, 2, 3
arr = [1, 2, 3]


1 + 2 + 3	-> 6		# 1
a + b	-> 3		# 2
arr[2]	-> 3		# 3
get(5)	-> 5		# 4
10		-> 10	# 5
```
\# 1, 2, 3, 4, 5는 서로 다른 형태의 expression들이다. **이 expression들은 그 모양과 형태는 다 다를지언정 하나의 단일 값으로 평가될 수 있다.** 각각 6, 3, 3, 5, 10으로 평가되었다. **여기서 평가(evaluate)라는 말이 참 중요하고 의미가 있다.** '5'라는 숫자는 우리는 바로 알아보지만 컴퓨터는 바로 알 수 없다. '5'라는 글자는 컴퓨터에게는 상징에 지나지 않는 것이다. 컴퓨터는 이 '5'라는 상징을 자신이 이해할 수 있는 기계 이진코드로 평가해서 이해해야 한다.  

**\# 5를 보자. '10'의 평가값은 숫자 10이다. 이때 16진수 '0xA', 2진수 '1010' 모두 평가값이 10이다. 이 셋은 평가값이 같은 서로 다른 숫자 리터럴인 것이다.** 리터럴의 형태가 달라도 평가값은 같을 수 있다는 것을 알 수 있다. 그것의 또 다른 예로 \#1, 2, 3은 형태가 다 다르지만 그 평가값은 값다.  

<br>

expression의 개념을 파이썬에서 사용해보자. 앞서 말한 **파이썬의 `eval` 함수는 _str_ 형태의 expression을 인자로 받아 평가해 그 값을 반환하는 함수이다.**

```python
a, b = 4, 5
eval('1 + 2 + 3')
eval('a + b')

6
9
```

문자열 형태의 expression을 받아 각각 6과 9라는 평가값을 반환했다. 이것만 보면 굳이 함수를 쓴 이유가 무엇인지, 그냥  '1+2+3', 'a+b'이라고 하면 되는 것 같기도 하다. 좀더 그럴듯한 활용사례는 [여기](https://shoark7.github.io/programming/algorithm/3ways-to-get-multiplication-in-a-list-in-python.html){:target="\_blank"}의 3번 절을 보도록 하자.



## Statement

---

다음은 statement. **statement는 '진술', '서술'의 의미로 프로그래밍에서는 실행가능한(executable) 최소의 독립적인 코드 조각을 일컫는다.** 우리가 프로그래밍을 하면서 컴파일러가 이해하고 실행할 수 있는 모든 구문은 statement다. 문법적으로 해당 언어에 적합한 모든 코드 한 줄이나 블록은 statement라고 할 수 있다. **statement는 흔히 한 개 이상의 expression과 프로그래밍 키워드를 포함하는 경우가 많다.**

```python
a = 3		# 1
a, b = 2, 3	# 2
if is_valid:		# 3
    return 4	# 4
```

위는 statement의 몇 가지 사례를 보여준다. 먼저 \# 1. 숫자 3을 a라는 변수에 할당한다. **변수에 할당하는 할당문은 expression처럼 평가되어 하나의 값을 반환하지 않는다.(적어도 파이썬에서는)** 단순히 파이썬 인터프리터가 실행가능해서 a라는 변수가 생길 뿐이다. **이 statement에는 '3'이라는 expression이 쓰이고 있다. 이렇게 statement는 하나 이상의 expression을 포함할 수 있다.** \# 2 도 마찬가지이다.  
\# 3은 _if_ 문으로 컴퓨터가 실행가능한 구문이다. _if_ 라는 파이썬 키워드가 사용되었다. \# 4는 _return_ 문으로 이 또한 컴퓨터가 실행 가능하므로 statement이다. 여기서 _return_ 은 키워드, '4'는 expression이다.


<br>

statement를 파이썬에서 활용해보자. 앞서 _eval_ 이 expression을 실행해서 값을 반환하는 함수인 것과 달리 **`exec`은 문자열 형태의 statement를 실행하는 내장 함수이다.**  

이런 예제를 생각해보자. 내가 실제로 고민했던 문제인데, 내가 'r1', 'r2', ..., 'r20' 이라는 변수를 만들고 값을 각각 1부터 20까지 할당하고 싶다고 하자. 'r1 = 1', 'r2 = 2', ..., 'r20 = 20'과 같이 말이다. 이걸 어떻게 해야 할까? 손으로?? 그러면 실격이다.  

statement 예제의 \# 1번이 할당문이었던 것을 참조해서 할 순 없을까? `exec`을 쓰면 가능하다.


```python
for i in range(1, 20+1):
    exec('r' + str(i) + ' = ' + str(i))


r1
r2
r3
...

1
2
3
...
```

_for_ statement를 돌면서 각 문장은 'r1 = 1', 'r2 = 2', ..., 'r20 = 20'와 같이 나오기 때문에 그 문장을 `exec`하면 변수가  각각 할당된다.



## 둘의 관계

---

그러면 이 둘의 관계는 어떻게 표현할 수 있을까? 어떤 추상적인 집합의 관계를 표현할 때 가시적인 집합관계로 표현하면 이해하기 쉬울 때가 많다. 아마 예상했듯이 **expression은 statement의 부분집합이다.**

![expression-vs-statement-diagram](/assets/img/knowledge/expression_statement.png)

개념적으로 생각하면 쉽다. '3+2'는 평가가 가능한 expression이지만 동시에 실행가능한 구문이기도 하다. 파이썬 인터프리터에 '3 + 2'를 입력하면 정상적으로 실행한다. **즉, 모든 expression은 statement다.**  

반면에 **어떤 statement는 expression이지 않다.** `return 3` 이런 구문은 '함수에서 3을 반환한다'는 의미일 뿐이지 평가해서 3이라는 값이 나오지 않는다. 'a = 3' 같은 표현도 마찬가지이다. '3'을 _a_ 라는 변수에 할당할 뿐, 평가 후 어떤 값으로 환원되지 않는다. 이 관계를 집합으로 표현하면 위와 같이 표현할 수 있다.  

expression이 statement의 부분집합이라는 증거를 살펴볼 수도 있다. 아까 `eval`과 `exec`의 예에서 `eval`은 `exec`로, `exec`은 `eval`로 바꿔서 실행해보자. `exec('1+2')`는 실행되지만, `eval('a = 3')`은 실행되지 않는다.



## 마치며

---

statement와 expression에 대해, 그리고 이 둘의 관계에 대해 살펴보았다. 다만 포스트를 위해 많이 찾아보면서 느낀 것이지만 statement과 expression에 대해 '딱 이거다'하는 정의가 없어서 사람마다 조금씩 정의하는 것이 다르기도 했다는 것을 기억해주었으면 한다. 그래서 나와 의견이 다른 사람이 있을 수도 있다. 하지만 적어도 파이썬 언어에서는 위와 같이 이해하는 것이 언어 사용에 도움이 된다. `eval`과 `exec`의 예에서만 봐도 알 수 있었다.  

이상 포스트를 마친다.
