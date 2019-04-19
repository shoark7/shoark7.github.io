---
layout: post
title: "Python의 Closure에 대해 알아보자"
date: 2019-04-20
description: "Python에서 유용한 Closure에 대해 살펴봅니다."
img:  /python/closure-logo.jpg
categories: [Programming, Python]
tags: [Closure]
---


## 0. Index

> 1. [Prologue](#1)
> 2. [Way of loading and using other modules: _import_](#2)
> 3. [Some hidden features of 'import'](#3)
>    - 3.1. [Using other characters besides english for modules](#3a)
>    - 3.2. [Do all Python module names have to end with '.py'?](#3b)
> 4. [Registering our modules and module import order](#4)
>    - 4.1. [Make our modules system-wide!](#4a)
>      * 4.1.1. [Test case definition](#4a!)
>      * 4.1.2. [Dynamically add it!](#4a@)
>      * 4.1.3. [Use environment variable](#4a#)
>    - 4.2. [Modules with same names](#4b)
> 5. [Epilogue](#5)



## 1. 들어가며

---

**오늘은 Python의 `Closure`에 대해 알아본다.** 해야지 해야지 하고 미룬 포스트인데 이제야 하게 됐다. 난 Closure가 단순히 함수 내 함수를 의미하는지 알았는데 밑에서 살펴보겠지만 그건 완전한 내 착각이었다.   

이 포스트도 앞의 두 포스트와 마찬가지로 영어로 할까 했다. 그렇게 하지 않고 한글로 한 이유는 이 Closure의 뜻에 대해 나름의 깨달음을 얻었기 때문이다. 'Closure'를 그냥 영어 단어로 해석하면 '폐쇄'란다. 그렇게 보면 안 된다. 내가 나름 생각한 의미를 공유하기에는 영어가 모국어가 아닌 사람들이 적절하겠다 싶어서 한글로 작성한다.  

아마 이번 포스트는 매우 길어질 것 같지는 않다. 포스트 하나 쓸 때마다 지치는데 보다 더 정수만 담아, 잉여 데이터 출력 없이 의미가 전달될 수 있도록 노력해야겠다. 아직 부족하다.  

<br>

**포스트는 먼저 Closure에 대해 바로 들어가기 전에 필요한 사전지식을 살펴본다. 그리고 Closure에 대해 살핀다. 기본 정의부터 특징, 사용시의 장점에 대해 살핀다. 특히 장점이 매우 중요하기 때문에 집중해서 봐주면 좋겠다. 마지막으로는 Closure의 대표적인 사용 사례인 decorator에 대해 살핀 뒤 포스트를 마무리한다.**  

들어가겠습니다. :)


## 2. 배경지식

---

### 함수 중첩(Function nesting)

아시다시피 Python(이하 "파이썬")에서 if 조건문은 중첩이 된다.

```python
n = int(input("정수를 입력하세요"))

if n % 2 == 0:
    if n % 3 == 0:
        print("6의 배수군요?")
    else:
        print("짝수로소이다 ㅎㅎ")
```

인터프리터에 '_import this_'라고 입력하면 나오면 유려한 시 **'_Zen of Python_'에서는 가급적 중첩을 피하라고 이야기하고 있다.** 꼭 필요한 경우는 어쩔 수 없지만 아닌 경우에는 가급적 펼치는 게(flatten) 나을 것 같다.

<br>

**파이썬에서는 조건문뿐만 아니라 함수도 중첩이 된다.** 그러니까 함수 정의 안에 다른 함수를 정의할 수 있는 것이다.

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


### First Class Object

좀 생소한 개념이 나왔다. 그런데 생각보다 어렵지는 않다.  

**프로그래밍 언어에서 First Class Object(또는 First Class Citizen)는 해당 언어 내에서 일반적으로 다른 모든 개체에 통용가능한 동작(operation)이 지원되는 개체(entity)를 의미한다.**

이 동작은 주로

1. **함수의 인자로 전달되거나,**
1. **함수의 반환값이 되거나,**
1. **수정되고 할당되는 것들을 전제로 한다.**


<br>

이게 무슨 뜻일까? 어렵지 않다. 파이썬에서 가장 많이 쓰이는 자료타입이 뭐가 있을까? **_list_, _str_, _int_ 등등이 쉽게 떠오른다. 이렇게 기본적이고 유명한 자료타입들은 함수의 인자로 전달되거나, 반환값이 되거나, 수정되고 할당될 수 있다.(적어도 개념적으로는)**  

이런 자료형은 파이썬의 1급 객체다.(First Class Object) 파이썬을 오래 한 나에게는 이게 상식적이고 당연한데 그렇지 않은 언어들이 있나보다.  [][][][] 추가적인 언급 필요 [][][][]

<br>

그리고 **파이썬에서는 함수(function)도 1급 객체다. 함수에는 위의 기본 자료타입들에 적용가능한 동작들이 똑같이 적용 가능하다.**


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

1. _f_ 라는 함수가 _execute_ 의 함수의 인자로 전달되었고,
1. 함수 내부에서 받은 함수 _func_ 를 반환하고 있으며
1. _add_ 라는 원 함수의 이름이 마음에 안 들었는지 _f_ 라는 새 이름에 할당했다.

<br>

즉, 파이썬에서 함수는 1급 객체이다. 이 특성이 있어야 Closure가 성립될 수 있다.



### _nonlocal_


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

앞서 파이썬에서 함수 중첩이 가능하다는 것을 확인했다. 그건 그런데, _x_ 값에 대한 코드가 두 번 제시됐다. 처음은 함수 실행 시에 받는 임의의 _x_ 이고, 다음은 _inner_ 함수 내에서 1000으로 초기화하는 변수 _x_ 이다. 예시처럼 함수 호출 시 인자를 10으로 줬을 때 반환되는 값은 몇이어야 하는가?

위와 같은 이슈는 **Scope**에 대한 이야기다. **_inner_ 함수 입장에서 바라보겠다.**

* **_inner_ 함수 블록 안에 있는 영역은 _local_ 스코프라고 불린다. 로컬 영역 안의 모든 개체들은 _inner_ 의 제어 아래에 있다.**
* **_outer_ 의 안에 있되, _inner_ 의 밖에 있는 영역은 _nonlocal_ 이라고 불린다. _outer_ 의 _y_ 변수는 _inner_ 입장에서는 _nonlocal_ 영역의 변수이다.**
* **_outer_ 함수 밖의 영역은 _global_ 영역이다. _z_ 변수는 _global_ 영역에 선언된 변수로 _outer_ 뿐만 아니라 다른 코드나 함수에서도 참조가능할 것이다.**

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

아까의 예와 비슷하다. _say\_hi_ 내부 함수는 _nonlocal_ 영역의 _x_ 의 변수를 그대로 반환하는 기능을 갖고 있다. 그리고 _greetings_ 가 받은 문자열을 문제없이 참조할 수 있었다. **그러니까 '읽기'가 가능하다고 이해하면 된다.**  

하지만 **자신의 영역이 아닌 영역에 대해 '쓰기'는 제한적이다.**



```python
def count(x):
    def increment():
        print(x)
        x += 1

    increment()


>>> count(5)

UnboundLocalError: local variable 'x' referenced before assignment
```

음 뭐가 문제지? 특이한 에러가 발생했다. **_UnboundLocalError_ 로 _local_ 변수 _x_ 가 할당되기 전에 참조됐다는 의미이다.**  하지만 우리는 _nonlocal_ 영역에서 받은 _x_ 에 값을 1 추가한건데?  

여기에 트릭이 있다. **_local_ 영역에서(여기서는 _increment_) 밖의 영역에 대한 값을 참조하는, 또는 읽는 것은 항상 문제가 없는데, 값을 수정하거나 새로 할당하는 것은, 쓰는 것은 안 된다.**   

위에서는 '_x += 1_'가 '수정하는' 역할을 하고 있다. 이렇게 수정하는, 쓰는 코드가 나오면 따로 언급이 없는 한, _increment_ 함수는 _x_ 가 자신이 제어할 수 있는 _local_ 변수라고 무조건 가정한다. 선언하지도 않는 변수에 값을 더하는건 당연히 말이 안 된다. 그래서 위와 같은 에러가 출력되는 것이다.  

왜 위와 같이 헷갈리게 만들어놨을까? **그것은 코드 영역의 책임과 권한을 명확히 나누는 것이 좋기 때문이다. 예제의 _count_ 함수는 하나의 내부 함수를 갖고 있지만, 어떤 경우에는 수십여개의 내부 함수를 가질 수도 있다. 이때 내부 함수마다 자신의 상태값을 건드리고 수정한다면 예상하지 못한 결과를 초래할 수 있다.** 그래서 읽기는 가능하지만 쓰기는 제한하고 있는 것이다. 리눅스에서 유저마다, 그룹마다 쓰기와 읽기, 실행에 대한 권한을 제어하는 것은 같은 이치다.

만약 위의 예제에서 _nonlocal_ 의 값을 수정하고 싶으면 어떻게 할까? 이때 _nonlocal_ statement를 쓰면 된다.


```python
def count(x):
    def increment():
        nonlocal x  # x가 로컬이 아닌 nonlocal의 변수임을 확인한다.
        print(x)
        x += 1

    increment()

count(5)

>>> 5
```

**_increment_ 함수 정의 바로 아랫줄에 '_nonlocal x_'라고 선언했다. 저 코드는 _x_ 가 _local_ 변수가 아닌, _nonlocal_, 여기서는 _count_ 스코프 내의 변수라는 것을 개발자가 명시적으로 선언하는 것으로 _nonlocal_ 영역의 상태에 대해 읽는 것뿐 아니라 쓰는 것도 가능하게 된다.** 같은 식으로 _global_ 스코프의 값을 제어하고 싶다면 '_global x_'와 같이 사용할 수도 있을 것이다.





## 2. Closure에 대한 이해

---


### Closure의 의미는?

### 기본 정의


### Closure의 특징

### Closure의 장점









## 3. Closure의 대표적 사용 사례: decorator(\@)


## 4. 마치며

---



## 5. 자료 출처

---

* [GeeksforGeeks: Python closures](https://www.geeksforgeeks.org/python-closures/)
* [Programiz: Python closures](https://www.programiz.com/python-programming/closure)
* [Stackoverflow: what exactly is contained within a obj closure](https://stackoverflow.com/questions/14413946/what-exactly-is-contained-within-a-obj-closure)
* [Wikipedia: First-class citizen](https://en.wikipedia.org/wiki/First-class_citizen)
* []()
* []()
* []()
* []()
* []()
* []()
* []()
