---
layout: post
title: "Python의 Closure에 대해 알아보자"
date: 2019-04-22
description: "Python에서 유용한 Closure에 대해 살펴봅니다."
img:  /python/closure-logo.jpg
categories: [Programming, Python]
tags: [Closure]
---


## 0. Index

> 1. [들어가며](#1)
> 2. [배경지식](#2)
>    - 2.1. [함수 중첩(Function nesting)](#2a)
>    - 2.2. [First Class Object](#2b)
>    - 2.3. [nonlocal](#2c)
> 3. [Closure에 대한 이해](#3)
>    - 3.1. [Closure 단어의 의미는?](#3a)
>    - 3.2. [기본 정의](#3b)
>    - 3.2. [Closure의 특징](#3c)
> 4. [Closure 사용시의 장점](#4)
> 5. [마치며](#5)
> 5. [자료 출처](#6)


<br id="1">

## 1. 들어가며

---

**오늘은 Python의 `Closure`에 대해 알아본다.** 해야지 해야지 하고 미룬 포스트인데 이제야 하게 됐다. 난 Closure가 단순히 함수 내 중첩 함수를 의미하는지 알았는데 밑에서 살펴보겠지만 그건 완전한 내 착각이었다.   

이 포스트도 앞의 두 포스트와 마찬가지로 영어로 할까 했다. 그렇게 하지 않고 한글로 한 이유는 이 _Closure_ 의 뜻에 대해 나름의 깨달음을 얻었기 때문이다. 'Closure'를 그냥 영어 단어로 해석하면 '폐쇄'란다. 그렇게 보면 답도 없다. 내가 나름 생각한 의미를 공유하기에는 독자가 영어가 모국어가 아닌 사람들이 적절하겠다 싶어서 한글로 작성한다.  

<br>

**포스트는 먼저 Closure에 대해 바로 들어가기 전에 필요한 배경지식을 살펴본다. 함수의 중첩, 일급 객체, 파이썬의 nonlocal 스코프에 대해 알고 있는 독자는 바로 3장으로 건너띄면 된다.**

그리고 **Closure에 대해 살핀다. Closure라는 단어의 의미를 먼저 음미하고, 파이썬에서의 기본 정의, 특징, 사용시의 장점에 대해 살핀다.**

들어가겠습니다. :)


<br id="2">


## 2. 배경지식

---

클로져에 대해 살펴보기 전에 3가지 개념을 짚고 넘어가야 한다. **함수 중첩과 일급 객체, 그리고 nonlocal.** 파이썬에서 이 세 가지 개념은 클로져를 구성하는 기본요소이기 때문에 먼저 살핀다. 특히 **nonlocal에 대해 잘 모른다면 이 부분만큼은 꼭 눈여겨보도록 하자.**



<br id="2a">

### 2.1. 함수 중첩(Function nesting)

Python(이하 "파이썬")에서 if 조건문 등은 중첩이 된다.

```python
n = int(input("정수를 입력하세요"))

if n % 2 == 0:
    if n % 3 == 0:
        print("6의 배수군요?")
    else:
        print("짝수로소이다 ㅎㅎ")
```

인터프리터에 '_import this_'라고 입력하면 나오면 유려한 시 **'_Zen of Python_'에서는 가급적 중첩을 피하라고 이야기하고 있다.** 하지만 중첩을 해야만 하는 경우도 있기 때문에 중첩이 틀린 건 아니다.

<br>

그리고 **파이썬에서는 함수도 중첩 선언이 된다.** 그러니까 함수 정의 안에 다른 함수를 정의할 수 있는 것이다.

```python
def greetings():
    def say_hi():
        print("Hi, everyone :)")

    say_hi()


>>> greetings()
    
Hi, everyone :)
```

인사를 건네는 _greetings_ 함수를 만들었다. 이 함수는 실제 인사를 건네는 코드를 다른 함수로 감싸서 이 내부 함수를 호출하고 있다. 이 코드는 전혀 문제가 없다.  

난 이렇게 내부 함수를 짜면 이게 다 Closure인 줄 알았다. 하지만 그건 틀린 생각이었고, 함수 중첩은 Closure이기 위한 필요조건이지 충분조건이 아니다.

---


<br id="2b">


### 2.2. First Class Object

좀 생소한 개념이 나왔다. 그런데 생각보다 어렵지는 않다.  

**프로그래밍 언어에서 First Class Object(또는 First Class Citizen, 일급 객체)는 해당 언어 내에서 일반적으로 다른 모든 개체에 통용가능한 동작(operation)이 지원되는 개체(entity)를 의미한다.**

이 동작은 주로

1. **함수의 인자로 전달되거나,**
1. **함수의 반환값이 되거나,**
1. **수정되고 할당되는 것들을 전제로 한다.**


<br>

이게 무슨 뜻일까? 어렵지 않다. 파이썬에서 가장 많이 쓰이는 자료타입이 뭐가 있을까? **_list_, _str_, _int_ 등등이 쉽게 떠오른다. 이렇게 기본적이고 유명한 자료타입들은 함수의 인자로 전달되거나, 반환값이 되거나, 수정되고 할당될 수 있다.(적어도 개념적으로는)**  

이런 자료형은 파이썬의 1급 객체다.(First Class Object) 파이썬을 오래 한 나에게는 이게 상식적이고 당연한데 그렇지 않은 언어들이 있나보다. 가령 C 언어에서는 함수의 인자로 함수의 포인터를 전달할 수는 있어도, 함수의 이름을 전달할 수는 없다. **기술적으로 포인터가 일급 객체라는 표현은 맞아도 함수가 일급 객체라는 표현은 적절하지 않은 것이다.**

<br>

반면 **파이썬에서는 함수(function)도 1급 객체다. 함수에는 위의 기본 자료타입들에 적용가능한 동작들이 똑같이 적용 가능하다.**


```python
def add(a, b):
    return a + b

def execute(func, *args):
    return func(*args) # 2.

f = add # 3.

>>> execute(f, 3, 5) # 1.

8
```

Packing과 Unpacking을 활용한 간단한 예제이다. 두 수의 합을 반환하는 함수 _add_ 를 정의했는데 이를 직접 호출하지 않고 감싸는 _execute_ 함수를 만들었다.  

이 예제에서 앞서 이야기한 1급 객체에 적용가능한 동작이 모두 적용되었다.

1. **_f_ 라는 함수가 _execute_ 의 함수의 인자로 전달되었고,**
1. **함수 내부에서 인자로 받은 함수 _func_ 를 문제없이 사용하고 있으며,**
1. **_add_ 라는 원 함수의 이름이 마음에 안 들었는지 _f_ 라는 새 이름에 할당했다.**

<br>

즉, **파이썬에서 함수는 1급 객체이다.** 이 특성이 있어야 Closure가 성립될 수 있다.

---


<br id="2c">

### 2.3. nonlocal


이 개념은 중요하다. 꼭 Closure가 아니라도 의미가 있기에 조금 길게 설명하자. 먼저 간단한 예시를 들고 가자.

```python
z = 3

def outer(x):
    y = 10
    def inner():
        x = 1000
        return x

    return inner()

print(outer(10))
```

앞서 파이썬에서 함수 중첩이 가능하다는 것을 확인했다. 그건 그런데, **위의 함수엣는 _x_ 값에 대한 코드가 두 번 제시됐다.** 처음은 함수 실행 시에 받는 임의의 _x_ 이고, 다음은 _inner_ 함수 내에서 1000으로 초기화하는 변수 _x_ 이다. 예시처럼 함수 호출 시 인자를 10으로 줬을 때 반환되는 값은 몇이어야 하는가?

<br>

위와 같은 이슈는 결국 **scope**에 대한 이야기다. **_inner_ 함수 입장에서 바라보겠다.**

* **_inner_ 함수 블록 안에 있는 영역은 _local_ 스코프라고 불린다. 로컬 영역 안의 모든 개체들은 _inner_ 의 제어 아래에 있다.**
* **_outer_ 의 안에 있되, _inner_ 의 밖에 있는 영역은 _nonlocal_ 이라고 불린다. _outer_ 의 _y_ 변수는 _inner_ 입장에서는 _nonlocal_ 영역의 변수이다.**
* **_outer_ 함수 밖의 영역은 _global_ 영역이다. _z_ 변수는 _global_ 영역에 선언된 변수로 _outer_ 함수뿐 아니라 다른 코드나 함수에서도 참조가능할 것이다.**

<br>

이런 _global_, _nonlocal_, _local_ 의 구분, 다시 말해 스코프(namespace라고 말할 수도 있을 것이다.)의 구분은 어떤 의미가 있는가? **각 스코프는 자신의 영역에 최대한의 관심을 가지며, 다른 영역의 변수나 객체에 대해서는 제한적인 제어를 가지게 된다.**  


```python
def greetings(x):
    def say_hi():
        print(x)

    say_hi()


greetings('안녕하세요?')

안녕하세요?
```

아까의 예와 비슷하다. _say\_hi_ 내부 함수는 _nonlocal_ 영역의 _x_ 의 변수를 그대로 반환하는 기능을 갖고 있다. 그리고 _greetings_ 가 받은 문자열을 문제없이 참조할 수 있었다. **그러니까 외부 스코프의 변수에 대해 '읽기'가 문제없이 가능하다고 이해하면 된다.**  

하지만 **자신의 영역이 아닌 영역에 대해 '쓰기'는 제한적이다.**



```python
def count(x):
    def increment():
        x += 1
        print(x)

    increment()


>>> count(5)

UnboundLocalError: local variable 'x' referenced before assignment
```

음 뭐가 문제지? 특이한 에러가 발생했다. **_UnboundLocalError_ 로 _local_ 변수 _x_ 가 할당되기 전에 참조됐다는 의미이다.**  하지만 우리는 _nonlocal_ 의 _x_ 에 1을 더한건데?  

여기에 트릭이 있다. **_local_ 영역에서 밖의 영역에 대한 값을 참조하는, 또는 읽는 것은 항상 문제가 없는데, 값을 수정하거나 새로 할당하는 것은, 쓰는 것(write)은 안 된다.**   

위에서는 '_x += 1_'가 '수정하는' 역할을 하고 있다. 이렇게 **수정하는, 쓰는 코드가 나오면 따로 언급이 없는 한, _increment_ 함수는 _x_ 가 자신이 제어할 수 있는 _local_ 변수라고 무조건 가정한다.** 함부로 외부의 변수를 건드리는 디버그가 어려운 오류를 막기 위해서다. 선언하지도 않는 변수에 값을 더하는건 당연히 말이 안 된다. 그래서 로컬 스코프에 변수가 할당이 되지 않았다는 에러가 출력된 것이다.  

왜 위와 같이 헷갈리게 만들어놨을까? **그것은 코드 영역의 책임과 권한을 명확히 나누는 것이 좋기 때문이다. 예제의 _count_ 함수는 하나의 내부 함수를 갖고 있지만, 어떤 경우에는 수십여개의 내부 함수를 가질 수도 있다. 이때 내부 함수마다 count의 상태값을 건드리고 수정한다면 예상하지 못한 결과를 초래할 수 있다.** 그래서 읽기는 가능하지만 쓰기는 제한하고 있는 것이다. 리눅스에서 모든 파일에 유저마다, 그룹마다 쓰기와 읽기, 실행에 대한 권한을 제어하는 것은 같은 이치다.

만약 위의 예제에서 의도적으로 _nonlocal_ 스코프의 값을 수정하고 싶으면 어떻게 할까? **이때 _nonlocal_ statement를 쓰면 된다.**


```python
def count(x):
    def increment():
        nonlocal x  # x가 로컬이 아닌 nonlocal의 변수임을 확인한다.
        x += 1
        print(x)

    increment()

count(5)

>>> 6
```

**_increment_ 함수 정의 바로 아랫줄에 '_nonlocal x_'라고 선언했다. 이 코드는 _x_ 가 _local_ 변수가 아닌, _nonlocal_, 여기서는 _count_ 스코프 내의 변수라는 것을 개발자가 명시적으로 선언하는 것으로 _nonlocal_ 영역의 상태에 대해 읽는 것뿐 아니라 쓰는 것도 가능하게 된다.** 같은 식으로 _global_ 스코프의 값을 제어하고 싶다면 '_global x_'와 같이 사용할 수도 있을 것이다.


<br>


```python
z = 3

def outer(x):
    y = 10
    def inner():
        x = 1000
        return x

    return inner()

>>> print(outer(10))
```

자, 멀리 돌아왔다. 우리의 원 질문은, 저 함수를 실행했을 때 값이 _outer_ 의 10이 나올지, _inner_ 의 1000이 나올지이다. 결과는? (두근두근)  

명심하자. **함수는 자신이 제어권을 가장 많이 확보하고 있는, 자신에게 가장 가까운 스코프부터 찾아나아간다.** _inner_ 함수는 자신의 _local_ 스코프에서 _x_ 를 찾았기 때문에 밖의 스코프를 더 이상 찾아볼 이유가 없다. 그렇기 때문에 _outer_ 의 인자로 몇을 주든지 간에 무조건 1000이 나올 것이다.

```python
outer(1)
outer(10)
outer(100)

>>> 1000
>>> 1000
>>> 1000
```

<br>

자, 생각보다 길었지만 Closure을 이해하기 위한 세 가지 선행개념을 살펴보았다. 이제 Closure로 넘어가자.



<br id="3">

## 3. Closure에 대한 이해

---

이제 기본지식을 바탕으로 closure(이하 "클로져")에 대해 알아보자. **먼저 아리송한 Closure의 단어의 뜻을 잡고 가자.** 기술용어의 뜻을 제대로 파악하지 못하고 쓰는 것은 절대 지양해야 한다. 이 단어의 개념을 이해하면 클로져의 정의를 파악하고, 특징과 사용 시의 장점에 대해 알아본다.


<br id="3a">

### 3.1. Closure 단어의 의미는?

Closure는 여기서 무슨 의미일까? 이 영어 단어의 의미가 파이썬의 클로져에 던지는 메시지는 무엇일까?  

Closure라는 단어에 집착하기 전에 관련된 단어로 **_enclose_** 로 우회해서 이해해보자.

**Enclose는 _close_ 에 대해 _en_ 접두사가 붙어 (담, 울타리 등으로) '두르다', '둘러치다'란 의미를 갖고 있다.**  이 뜻 그대로 이해해보자.

<br>

방대한 초원을 공유지로 하여 많은 사람들이 각자의 가축을 기른다고 하자. 누구는 소를 키우고 누구는 양을 키우고... 공유지에서 풀을 먹일 땐 같이 풀어놓더라도, 향후 분명 각자의 소유지에 담을 둘러(enclose) 가축들을 관리할 것이다. 아래 그림은 그 예시이다.


![Enclosure png with enclosed cage](/assets/img/python/enclosure-cage.png)


김가네와 박가네가 서로의 우리에 가축동물을 기르고 있다. 이렇게 각자의 영역을 구축하여(enclose) 동물들을 관리하면 어떤 장점이 있을까?  

당연한 얘기지만, **각자의 동물(재산)에 대한 관리와 책임을 명확히 할 수 있고, 서로 다른 재산끼리의 불필요한 충돌을 방지할 수 있으며, 각자의 입맛에 맞게 재산을 관리할 수 있다.** 박가네는 그래프에 대한 깊은 이해가 있어 양들의 배치를 2차원 행렬 그래프에 가깝게 배치했지만, 김가네 목장은 소를 단순히 우리 안에서 방목하고 있다. 각자의 필요나 기호에 맞게 관리한 것이다.  

**이렇게 어떤 재산이나 속성을 Enclose하여 자신만의 영역을 구축하는 것, 그것의 장점을 이해함으로써 클로져를 더 쉽게 이해할 수 있다.** 이게 본격적인 정의와 특징을 살펴보면서, 클로져의 장점을 다루며 위의 예시를 상기할 것이다.

---


<br id="3b">

### 3.2. 기본 정의

길고 길었는데 이제 진짜 클로져에 대해 살펴보자. **파이썬에서 클로져는 '자신을 둘러싼 스코프(네임스페이스)의 상태값을 기억하는 함수'다.** 그리고 어떤 함수가 클로져이기 위해서는 다음의 세 가지 조건을 만족해야 한다.

1. **해당 함수는 어떤 함수 내의 중첩된 함수여야 한다.**
1. **해당 함수는 자신을 둘러싼(enclose) 함수 내의 상태값을 반드시 참조해야 한다.**
1. **해당 함수를 둘러싼 함수는 이 함수를 반환해야 한다.**

<br>

이해를 위해 예시를 들자. 몇 주 전 파이썬에서 팩토리얼을 구하는 5가지 방법에 대한 [포스트](https://shoark7.github.io/programming/algorithm/several-ways-to-solve-factorial-in-python.html#4){:target="_blank"}를 작성했다. 해당 포스트의 말미에서는 효율을 높이기 위한 Memoization을 제시했는데 이 방법은 5가지 알고리즘에 모두 적용가능하다. 그러면 **Memoization 코드를 따로 분리시키고 각 알고리즘에서 그 모듈을 사용한다면 코드를 5번 하드코딩한 것보다 유지보수도 쉽고 가독성도 올라갈 것이 자명하다.**(Modularity, that's what matters.)

해당 포스트에서 캐시 히트 여부를 검사하는 분리된 모듈 코드는 다음과 같았다.

```python
def in_cache(func):
    cache = {}
    def wrapper(n):
        if n in cache:
            return cache[n]
        else:
            cache[n] = func(n)
            return cache[n]
    return wrapper
```

_in\_cache_ 함수는 _cache_ 라는 _dict_ 자료구조와 _wrapper_ 라는 내장 중첩함수를 가지고 있다. 이 중첩함수는 정수 _n_ 를 받아서 _n_ 의 key에 해당하는 value가 _cache_ 에 담겨 있으면 반환하고, 아니면 함수 _func_ 를 실행해서 값을 저장한 뒤 반환한다.  

<br>

이 함수를 실제로 적용해보기 전에, _wrapper_ 함수에 대해 살펴보자. 위에서 어떤 함수의 클로져이기 위한 특징을 살폈는데 공교롭게도 **이 함수는 클로져이기 위한 조건을 모두 충족한다.**

1. **_in\_cache_ 함수 내의 중첩된 함수이고,**
1. **Enclosing하는 _in\_cache_ 스코프의 _cache_ 라는 상태값을 참조하고 있으며,**
1. **자신을 둘러싼 함수는 자신(_wrapper_)을 반환하고 있다!**


일단 _wrapper_ 는 정의상 클로져라는 얘기이고, 이 함수를 제대로 사용해보자.  

위 포스트의 팩토리얼 함수를 하나 가져와서 _in\_cache_ 를 적용해보겠다.


```python
def factorial(n):
    ret = 1
    for i in range(1, n+1):
        ret *= i
    return ret
```

주어진 정수에 대해 팩토리얼을 구하는 초보적인 코드다. Memoization과 실제 팩토리얼을 구하는 코드가 분리된 상태로 Memoization을 기능에 추가하려면 다음과 같이 작동시킨다.


```python
factorial = in_cache(factorial)
```


<br>

그리고 이해를 위해 _wrapper_ 함수에 코드를 한 줄 추가한다.


```python
def in_cache(func):
    cache = {}
    def wrapper(n):
        print(cache) ## !!!!
        if n in cache:
            return cache[n]
        else:
            cache[n] = func(n)
            return cache[n]
    return wrapper


def factorial(n):
    ret = 1
    for i in range(1, n+1):
        ret *= i
    return ret

factorial = in_cache(factorial)
```

이제 진짜 핵심으로 들어간다. 그 클로져라는 _wrapper_ 함수 안에 _cache_ 의 상태값을 출력하는 코드를 넣었다.  

저 코드는 _wrapper_ 을 _enclosing_ 하는 스코프의 _cache_ 변수를 추적한다.


이제 함수를 몇 번 실행해보자.

```python
factorial(3)
factorial(5)
factorial(10)

{}
6

{3: 6}
120


{3: 6, 5: 120}
3628800
```

위의 \{\} 결과가 _cache_ 의 상태고, 그 아래는 _n_ 에 따른 팩토리얼 값이다. 이상한 것을 발견했는가?  

$$\text{cache는 함수가 실행됨에 따라 그 상태가 업데이트되고 있다. 이전 결과값을 저장하고 있는 것이다!}$$


이것을 그림으로 표현하면 다음과 같을 것이다.

![Enclosure boy~](/assets/img/python/enclosure-2.png)

전역 스코프에는 수많은 변수들이 저장되어 있다. 그중에는 _factorial_ 함수도 있다. **이 함수는 원래 정의한 팩토리얼 함수가 아닌, '_in\_cache(factorial)_'의 실행결과 반환된 함수로, 이게 곧 클로져다.**(클로져의 조건 3번) 이 클로져에 다시 한 번 _factorial_ 이라는 이름을 할당해서 사용하는 것뿐, _cached\_factorial_ 등의 이름을 붙여도 상관은 없다.

**이 클로져는 자체 스코프를 가지고 있어, _cache_ 라는 상태는 매번 실행할 때마다 초기화되는 것이 아니라 값이 유지되고 있다.** 마치 전역공간에 선언이라도 했듯이 말이다.

신기하게도 원래 함수 정의에서 _cache_ 는 _wrapper_ 함수 스코프의 밖에 선언되어 있었다. 그럼에도 _wrapper_(여기서는 _factorial_)는 _cache_ 에 접근이 되고, 그 상태를 자신의 스코프 내에서 저장하고 제어할 수 있다.

아까 살펴본 클로져의 정의, **'클로져는 자신을 둘러싼 스코프(네임스페이스)의 상태값을 기억하는 함수'**는 이런 뜻인 것이다. 이 예에서 _factorial_ 스코프에서는 자신을 둘러싼(enclosing) 스코프의 상태값을(_cache_) 기억하고 제어할 수 있다.  

이를 통해 **자신만의 스코프 내에서 함수 실행시마다 초기화되는 것이 아닌, 지속적으로 관리되고 유지되는 _cache_ 를 두고 소기의 목적을 달성할 수 있다.**


---


<br id="3c">

### 3.3. Closure의 특징

클로져를 사용할 때의 특징과 장점을 살펴보도록 하자.  

일단 눈에 띠는 특징으로 **클로져는 자신을 둘러싼 함수 스코프의 상태값을 참조하는데, 이 값은 함수가 메모리에서 사라져도 값이 유지가 된다.**

```python
def times_multiply(n):
    def multiply(x):
        return n * x
    return multiply


times_3 = times_multiply(3)
times_4 = times_multiply(4)

times_3(5)
times_4(5)


15
20
```

이제는 다른 예제다. _times\_multiply_ 는 _n_ 을 받아서 _multiply_ 라는 함수를 반환한다. **이 _multiply_ 내장 중첩함수는 클로져로 상위 스코프의 _n_ 을 참조하고 있다.  결과 _times\_3_, _times\_4_ 는 반환된 클로져로 들어온 숫자에 각각 3, 4를 곱해 반환한다.**

이때 _times\_multiply_ 를 메모리 상에서 삭제하자.


```python
del(times_multiply)
```

그러면 **이 함수는 더 이상 호출할 수 없는데, 이게 기존에 생성된 클로져에도 영향을 미칠까? **

```python
times_3(5)


15
```

문제없이 호출가능하다. **클로져는 원 함수에 어떤 변화(심지어는 삭제)가 발생되어도 자신의 스코프는 지킨다.**

<br>

두 번째 특징으로 **클로져에서 자신 안에 정의된 내부 변수가 아닌, Enclosing하고 있는 변수에 접근하는 것을 파이썬에서 지원하고 있다.**

```python
times_4.__closure__[0].cell_contents

4
```

**파이썬 3 기준으로, 클로져 함수는 \_\_closure\_\_ 변수를 자동으로 갖고 있다. 이 변수는 튜플 타입으로서 클로져가 _enclosing_ 스코프에서 참조하는 변수들을 담고 있다. 그리고 각 원소의 _cell\_contents_ 는 그 값 자체를 갖고 있다.**  

위에서는 4라는 값을 감싸는 함수의 인자로 주었기 때문에 저 값은 클로져가 참조하는 값으로 유지된다. 그리고 이 클로져는 값을 하나만 참조했기 때문에 \_\_closure\_\_ 는 길이가 1인 튜틀이다.

```python
times_4.__closure__[1].cell_contents


IndexError: tuple index out of range 
```

만약 enclosing 스코프에서 값을 여러 개 참조한다면 그 개수만큼 접근가능할 것이다. **클로져가 생성될 때(_times_3 = times_multiply(3)_) 이 \_\_closure\_\_ 변수가 같이 생성되고 유지되기 때문에 기존 함수가 삭제되어도 문제없이 클로져를 실행할 수 있다.**


<br>

그리고 내가 좋아하는 **decorator는 결국 클로져를 만드는 문법이다.**

```python
factorial = in_cache(factorial)
```

**_in\_cache_ 는 함수를 받아 Memoization 코드를 추가해 다시 함수를 반환하는 함수로, 위에서는 반환된 클로져를 다시 _factorial_ 이라는 이름으로 재할당했다.**

이 작업은 데코레이터가 정확히 하는 일이기도 하다.

```python
@in_cache
def factorial(n):
    ...
```


<br id="4">

## 4. Closure 사용시의 장점

---

그럼 클로져를 사용하면 대체 뭐가 좋을까? 아까의 _factorial_ 예제를 보자. **캐시를 자신의 스코프 안에 저장하는 대신 그냥 전역변수로 두고 쓰면 되잖아? 왜 귀찮게 클로져를 만들어서 해야 하는거야?** 충분히 던질 수 있는 질문이다.

![Enclosure png with enclosed cage](/assets/img/python/enclosure-cage.png)

아까 살펴 본 이미지다. 우리는 공유지에 각 개인의 소유 가축을 모두 풀어놓지 않고 울타리를 둘러쳐 자신의 영역을 구축한다. 


결과적으로 이렇게 하는 이유와 Closure 사용의 장점이 일맥상통한다. 

* 관리와 책임을 명확히 할 수 있고
* 각 변수가 섞여 불필요한 충돌을 방지할 수 있으며
* 사용환경(context)에 맞게 임의대로 내부구조를 조정할 수 있다.

<br>

이 장점을 현실적인 예로 살펴보자. 앞서 우리는 _factorial_ 함수를 정의했다. 추가로 1부터 N까지의 합을 구해 반환하는 _sum\_to\_N_ 함수를 정의해서 같이 사용해야 한다고 하자.


```python
def sum_to_N(N):
    s = 0
    for n in range(N+1):
        s += n
    return s


sum_to_N(10)

55
```

**이 함수 또한 빈번하게 호출된다면 Memoization을 통해 효율성을 높일 수 있다.** 그러면, 이런 비슷한 함수가 있을 때마다 전역공간에 cache를 두고 사용할 수 있는가? 10!은 3628800이고 1부터 10까지의 합은 55다. 전혀 다른 숫자기 때문에 같은 이름의 캐시를 쓸 수 없고, 굳이 전역공간에 캐시를 둔다면 cache_factorial, cache_sum_n과 같은 딱 보기에도 안쓰러운 이름의 변수를 써야 한다.  

하지만 스코프를 분리해주고 자신의 스코프 안에서만 관리되는 캐시를 쓴다면 두 캐시가 충돌하지 않게 되서 사용성이 훨씬 커진다.

이걸 이렇게 그림으로 표현할 수도 있을까?

![Enclosured cache](/assets/img/python/enclosure-cache.png)

각 함수가 자신만의 스코프 안에서 고유한 cache를 유지하고 이 값을 문제없이 사용한다. 저 캐시들을 전역변수에 할당하고 사용해야 한다면 정말 끔찍할 것이다.  

여기서 `Closure`라는 단어의 의미를 이렇게 정의해볼 수도 있겠다. **Closure는 폐쇄라는 뜻을 갖는데, 어떤 굳게 닫힌 문을 연상시킨다. 굳게 닫힌 문이라도 언젠가는 열리기 마련이고, 우리는 이 문을 통해 해당 스코프에 대한 간접적인 접근이 가능하다.** 클로져가 하는 일이 바로 그런 것이 아닌가? 클로져를 호출해서 그 스코프 안의 변수에 접근하고 있으니... 그 이외의 방법으로 접근하는 것은 불가능하다.



<br id="5">

## 5. 마치며

---

클로져에 대해 살펴봤다. 또 길어졌는데 묵은 통증이 싹 사라지는 느낌이다. 이제 누군가에게 파이썬 클로져에 대해 확실히 설명할 수 있을 것 같다. 다행이다. :)

근데 포스트를 잘 만들었는지는 모르겠다. 더 쉽게, 더 간결하게 쓸 수는 없었나? 이게 최선이었나? 이 정도 글에서도 헤매는 나를 보니 수백 페이지의 책을 쓰는 사람들은 정말 대단하게 느껴진다. 하지만 포기하지 않는다. 또다시 달려볼 수밖에.

이상 포스트를 마칩니다.




<br id="6">

## 6. 자료 출처

---

* [GeeksforGeeks: Python closures](https://www.geeksforgeeks.org/python-closures/){:target="_blank"}
* [Parkito's on the way: several ways to solve factorials in Python](https://shoark7.github.io/programming/algorithm/several-ways-to-solve-factorial-in-python.html){:target="_blank"}
* [Programiz: Python closures](https://www.programiz.com/python-programming/closure){:target="_blank"}
* [Stackoverflow: what exactly is contained within a obj closure](https://stackoverflow.com/questions/14413946/what-exactly-is-contained-within-a-obj-closure){:target="_blank"}
* [Wikipedia: First-class citizen](https://en.wikipedia.org/wiki/First-class_citizen){:target="_blank"}
