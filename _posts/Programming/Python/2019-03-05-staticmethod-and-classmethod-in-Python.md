---
layout: post
title: '[Python] staticmethod VS classmethod'
date: 2019-03-05
description: 'Python OOP를 제대로 활용하기 위해 꼭 필요한 staticmethod와 classmethod를 확인하고 비교, 대조해보도록 하겠습니다.'
img:  /knowledge/unix-philosophy-logo.jpg
categories: [Programming, Python]
tags: [Staticmethod, Classmethod]
---

## 0. 목차

> 1. 들어가며
> 2. 일반 메소드에 대한 이해
> 3. classmethod
>    - 3.1. 기본 이해
>    - 3.2. classmethod의 특징
>    - 3.3. 사용처
>      * 3.3.1. 싱글턴 패턴(Singleton pattern)
>      * 3.3.2. 팩토리 메소드 패턴(Factory method pattern)
> 4. staticmethod
>    - 4.1. 기본 이해
>    - 4.2. staticmethod의 특징
>    - 4.3. 사용처
> 5. 비교 & 대조
>    - 5.1. 공통점
>    - 5.2. 차이점
> 6. 마치며
> 7. 자료 출처



## 1. 들어가며

---

**Python(이하 '파이썬') 언어의 주요 특징 중 하나로 'Batteries Included'가 있다. 이는 파이썬이 개발에 도움이 될만한 다목적의 표준 라이브러리(모듈)를 풍부하게 기본 내장하고 있다는 의미로, 프로젝트 시에 필요한 패키지를 따로 다운로드하지 않아도 되는 장점(head start)이 있다.** 우리가 어지간하면 몰랐을 다양한 기본 모듈이 많은데 일례로 최근에 나는 Codewars에서 다른 사람 코드를 보면서 'calendar', 'ipaddress'와 같은 모듈이 있는지 처음 알았다. 파이썬을 3년 넘게 한 것 같은데 이런 모듈을 보면서 'ㅋ;'와 같은 감정이 드는 것을 숨길 수가 없었다. 이처럼 파이썬은 '없는 것 빼고 다 있는' 기본 라이브러리를 내장하고 있다.

그러한 정신에서인지, 파이썬에서는 표준 라이브러리가 풍부할 뿐만 아니라 **기본 로드('built-in', 이하 '빌트인')된 함수와 자료구조도 많은 편이다.** 항상 사용되는 _list_, _dict_ 와 같은 자료구조에서부터 _sum_, _round_ 와 같은 함수가 바로 그것이다. 언급한 정도는 누구나 알 것이다. 근데 파이썬에는 이외에도 다양한 빌트인 함수가 많다. 그 목록은 [여기](https://docs.python.org/3/library/functions.html){:target="_blank"}에서 확인할 수 있는데, 나는 아직도 여기에서 이해하지 못한 것들이 많다. 부담감을 가지고 다 공부할 필요는 없어보이고 필요할 때마다 공부해나가면 되지 않을까 싶다.

그 테이블에서 **'classmethod'와 'staticmethod'**가 보이는지? 오늘 포스트는 이 둘을 비교하는 것을 다루려고 한다. 둘 다 **파이썬에서 OOP를 제대로 활용하기 위해 꼭 필요한 요소들이다.** 또 **다양한 디자인 패턴을 구현하는 데 중요한 역할을 맡고 있다.** 'classmethod'에 대해서만 얼핏 알고 있었고, 둘의 차이는 거의 모르다시피 했는데 이번 기회에 제대로 짚고 넘어가도록 하자.

<br>

**둘에 대해 알아보기 전에 먼저 클래스의 일반 메소드에 대해 살펴보자.** classmethod와 staticmethod의 차이보다는 이 둘과 일반 메소드의 차이가 훨씬 크기에 꼭 짚고 넘어가야 한다. **그다음 classmethod와 staticmethod를 살펴본다. 각각의 특징과 자주 쓰이는 사용처에 대해 살펴보려고 한다. 그 다음 둘의 공통점과 차이점을 비교, 대조 후 포스트를 마무리한다.**


## 2. 일반 메소드에 대한 이해

---

**classmethod와 staticmethod는 OOP와 깊은 관련이 있고 실제로 클래스 내의 메소드에만 적용가능하다.** 그리고 둘은 우리가 클래스에 대해 처음 배우고 사용하는 일반 메소드와는 차이가 있다. **따라서 classmethod와 staticmethod에 대해 탐구하기 전에 먼저 일반 메소드에 대해 짚고 넘어가자.**

클래스와 메소드를 모르는 사람은 없다. **클래스는 어떤 특징에 기반한 한 집단을 프로그래밍적으로 정의한 것에 지나지 않고 메소드는 그 집단의 개체들이 행할 수 있는 어떤 동작이나 행동을 의미한다.** 여기서 개체는 Instance(이하 '인스턴스')로서 클래스와 인스턴스는 흔히들 붕어빵틀과 붕어빵과의 관계로 이해하고는 한다. 꼭 맞지는 않겠지만 당장 이해하기에 나쁜 설명은 아닌 듯 하다. 

간단하게 클래스와 메소드를 만들어보자. 우리를 둘러싼 '인간'에 대한 클래스와 그들이 행할 수 있는 메소드를 만들 수 있다.

```python
class Human:

    def __init__(self, name, age):
        self.name = name
        self.age = age
        self.use_glasses = False

    def introduce_myself(self):
        return f"My name is {self.name} and I'm {self.age} years old."


A = Human('성환', '28')
B = Human('Gosari Muchim', '27')

>>> print(A.introduce_myself())
>>> print(B.introduce_myself())


My name is 성환 and I'm 28 years old.
My name is Gosari Muchim and I'm 27 years old.
```

'Human' 클래스를 정의하고 생성자 메소드(\_\_init\_\_)와 자기 소개하는 메소드(introduce\_myself)를 만들었다. 간단한 OOP이다.

이때 꼭 짚고 넘어갈 것이 있다. 파이썬에서 일반 메소드들에는 첫 인자로 'self'를 꼭 넣어준다. **'self'를 암시적으로(implicitly) 넣어줌으로써 일반 메소드가 인스턴스의 변수에 접근할 수 있다.** 인스턴스를 지칭하는 단어는 꼭 'self'이여야 할 필요는 없지만 **첫 인자로 인스턴스 자신을 의미하는 인자는 어떤 식으로든 꼭 넣어줘야 한다.** 그리고 'self'가 다른 개발자 모두에게 이해하기도 좋다.   

생성자 메소드에서는 인스턴스마다의 이름, 나이, 안경 착용 유무를 변수로 할당한다. 인스턴스마다의 변수는 인스턴스마다 값이 제각각이라서 A와 B의 자기소개 메소드에서 보듯이 이름, 나이 등이 다 다르다. **이처럼 인스턴스 변수는 인스턴스마다 다르고, 이를 사용하는 일반 메소드는 인스턴스마다 서로 다른 값을 출력하게 된다.** 다시 말해 **일반 메소드는 인스턴스에 종속적이다.(dependent or bound to)** 이런 의미에서 일반 메소드는 인스턴스 메소드라고 부를 수도 있을 것이다.

<br>

이렇듯 **일반 메소드는 인스턴스에 종속적인 결과를 출력한다.** 하지만 때에 따라서는 각각의 인스턴스와 상관 없는, 다시 말해 인스턴스마다 값이 항상 동일한, 또는 클래스 단위로 관리해야 할 변수나 메소드가 있지 않을까?

아까의 Human 클래스를 다시 보자. 현생 인류종의 학명은 그 유명한 'Homo sapiens'로 '지혜로운 사람'이라는 뜻이라고 한다. 내가 아는 한 현생 인류종은 모두 이 호모 사피엔스이고 개체마다, 다시 말해 인스턴스마다 값이 달리지지 않는다.  

이 값을 클래스에 변수로 할당하고자 할 때, 생성자 메소드에 '*self.species = "homo\_sapiens"*' 라고 쓸 수는 있지만 바람직하지 않다. 저 할당 자체에서 '인류의 종은 개체마다 달라질 수 있다'는 뉘앙스를 풍기기 때문이다. 향후 유전공학이 발달하고 생명윤리에 큰 변화가 있지 않는 이상 현실적으로는 이는 틀렸다. **이런 경우에는 인류의 학명은 인스턴스 변수가 아니라 클래스 변수로 할당하면 된다.**


```python
class Human:
    # 인류의 학명은 모든 인스턴스마다 동일하다!
    # 따라서 클래스 변수로 'species' 할당
    species = 'Homo Sapiens'

    def __init__(self, name, age):
        ...

C = Human('Charles Darwin', 30)

>>> print(Human.species)
>>> print(C.species)


Homo Sapiens
Homo Sapiens
```

**_species_ 변수는 클래스 변수로, 클래스 단위로 접근, 관리되는 변수이다. 그래서 _Human.species_ 처럼 인스턴스가 아닌 클래스에서 접근해도 인간의 종을 바르게 확인할 수 있다.** 이때 눈여겨 볼 점은 _C_ 라는 이름의 인스턴스에서도 클래스 변수에 접근 가능하다는 것이다. 

일반 메소드는 확인한 것처럼 인스턴스 단위의 변수를 다루고 관리한다. 반대로 **클래스 변수는 '클래스 단위'로 설정되고 할당되는 변수이다.** 여기서 classmethod가 무엇일지에 대해 눈치껏 파악할 수도 있을 것이다. 이제 본격적으로 classmethod와 staticmethod에 대해 알아보도록 하자.



## 3. classmethod

---

### 3.1. 기본 이해

classmethod는 앞서 확인한 일반 메소드의 반대로 확인하면 된다. 일반 메소드가 인스턴스 변수의 값을 다루고 인스턴스마다에서 서로 다른 결과를 출력할 것이라면, **classmethod는 클래스 단위로 관리되는 클래스 변수에 접근하기 때문에 그리고 클래스의 모든 인스턴스마다에서 같은 값을 다루고 출력한다.**

classmethod는 내장 함수이다. 맨 위에서 확인했다. 항상 처음 보는 모르는 대상에 대해서는 헬핑을 하자. 그 결과는 다음과 같다.


```python
>>> help(classmethod)


classmethod(function) -> method

Convert a function to be a class method.

A class method receives the class as implicit first argument,
just like an instance method receives the instance.
To declare a class method, use this idiom:

  class C:
      @classmethod
      def f(cls, arg1, arg2, ...):
          ...

It can be called either on the class (e.g. C.f()) or on an instance
(e.g. C().f()).  The instance is ignored except for its class.
If a class method is called for a derived class, the derived class
object is passed as the implied first argument.

Class methods are different than C++ or Java static methods.
If you want those, see the staticmethod builtin.
```

헬핑은 파이썬의 기본이고 큰 장점이다! 잊지 말자.

**기본 사용법은 함수를 받아 메소드를 반환한다.**(반환된 메소드를 '클래스메소드'라고 표현하겠다. 이는 _classmethod_ 함수로 반환된 class method를 지칭한다.) 그리고 이 클래스메소드는 **첫 인자로 클래스를 뜻하는 'cls'라는 변수를 암묵적으로 받는다.** 'cls'를 통해 클래스 변수에 접근할 수 있는데 일반 메소드에서 'self'를 통해 인스턴스 변수에 접근할 수 있었던 것과 같은 의미다.

기본적인 사용법은 다음과 같다. 이번에는 고양이 클래스를 정의해보자.

```python
class Cat:
    species = 'Felis Catus'

    def get_species(cls):
        print(f'Scientific name for cat is {cls.species}!')

Cat.get_species = classmethod(Cat.get_species)

>>> print(Cat.get_species())


Scientific name for cat is Felis Catus!
```

고양이의 학명은 'Felis Catus'란다. 오늘 처음 알았다. 고양이 학명을 Cat의 클래스 변수로 설정했다. 그리고 고양이의 학명을 반환하는 _get\_species_ 메소드를 만들었다. 근데 이 메소드는 인스턴스 변수에 접근하는 일반 메소드가 아니라 클래스 변수를 조작하는 클래스메소드이다. 따라서 그대로 사용하면 안 되고 **_Cat.get\_species = classmethod(Cat.get\_species)_ 처럼 *classmethod* 내장 함수를 써서 일반 메소드를 클래스메소드로 변환해줘야 한다.**

잘 작동한다. 하지만 클래스메소드를 정의할 때마다 귀찮게 _classmethod_ 함수를 따로 쓰기 귀찮기 때문에 **헬핑에서처럼 데코레이터로 클래스메소드를 정의한다.**


```python
class Cat:
    species = 'Felis Catus'

    @classmethod
    def get_species(cls):
        ...

>>> print(Cat.get_species())


Scientific name for cat is Felis Catus!
```

이게 다다! 이제 우리는 인스턴스 변수를 조작하는 일반 메소드와 함께 클래스 변수를 조작하는 클래스메소드도 정의할 수 있게 되었다. 


### 3.2. classmethod의 특징

_classmethod_ 데코레이터를 통해 생성된 클래스메소드의 특징을 다음과 같이 정리해볼 수 있다.

* **클래스메소드는 인스턴스에 독립적이다.(independent)**
  - 클래스메소드는 인스턴스에서도 실행할 수 있지만 클래스 자체에서도 문제없이 실행할 수 있다.
  - 그리고 인스턴스마다에서 반환값이 변하지 않는다.
* **클래스에 종속적이다.(dependent)**
  - 클래스메소드는 클래스를 통해 호출할 수 있다. 따라서 클래스에 종속적이다.
* **클래스메소드는 클래스 변수를 조작할 수 있다.**
  - classmethod로 반환된 클래스메소드는 첫 인자로 'cls'를 받는다. 이 'cls'를 통해 클래스를 지칭할 수 있고 따라서 클래스 변수에 접근, 관리할 수 있다. 우리가 할당한 _species_ 변수는 클래스 변수다.

---



### 3.3. 사용처

_classmethod_ 함수를 통해 정의하는 클래스메소드는 어디에 쓸 수 있을까? 앞서 **classmethod와 staticmethod는 디자인 패턴을 구현하는 데 요긴하게 사용된다고 짧게 언급했다.** classmethod를 통해 두 가지의 유명한 패턴을 구현해보도록 하자.


#### 3.3.1. 싱글턴 패턴(Singleton pattern)

디자인 패턴 중에서 가장 유명한 패턴은 아마 싱글턴 패턴이 아닐까 한다. 싱글턴 패턴은 내가 예전에 인강으로 자바 OOP에 대해 들을 때 재능기부하시는 강사분이 처음으로 소개해줘서 꽤 오랫동안 알고 있었다. 개념 또한 쉽다. **싱글턴 패턴은 클래스마다에서 단 하나의 인스턴스만 허용하는 디자인 패턴이다.** 최근에 『코스모스』를 읽어서 그 감성에서 가정하자면 언젠가 탄생할 우주 정부에서 전 우주를 호령할 대통령은 아마 한 명이지 않을까? 그러면 대통령 클래스의 인스턴스는 단 하나만 있어야 한다.

싱글턴 패턴은 클래스메소드를 사용하면 매우 쉽게 구현할 수 있다.

```python
class Singleton:
    __instance = None

    @classmethod
    def instance(cls, *args, **kwargs):
        if cls.__instance:
            return cls.__instance
        else:
            cls.__instance = cls(*args, **kwargs)
            return cls.__instance


class MyClass(Singleton):
    pass


>>> a = MyClass.instance()
>>> b = MyClass.instance()
>>> print(a is b)


True
```

* _Singleton_ 클래스를 구현하고 *\_\_instance* 라는 클래스 변수를 정의했다. 이 변수에 허용되는 단 하나의 싱글턴 인스턴스를 담을 생각이다. 싱글턴에서는 인스턴스가 단 하나이기 때문에 클래스 변수에 이 단 하나의 인스턴스를 할당해도 이치에 맞는다. 이를 활용해서 싱글턴 인스턴스를 만들거나 있는 인스턴스를 반환하는 _instance_ 클래스메소드를 정의했다. 이 메소드는 인스턴스가 정의되어 있으면 이를 반환하고 없으면 하나 만들어 내놓는다.

이 코드는 이전에 [디자인 패턴에 대해 공부한 포스트](https://shoark7.github.io/programming/knowledge/what-is-design-pattern.html){:target="_blank"}에서 가져왔다.

<br>


#### 3.3.2. 팩토리 메소드 패턴(Factory method pattern)

팩토리 메소드 패턴은 디자인 패턴의 하나로서 C++의 함수 오버로딩(function overloading)과 유사하다. 팩토리 메소드 패턴을 통해 클래스의 인스턴스를 생성하는 다양한 방법을 한 클래스 내에서 정의할 수 있다. 

아까 사용했던 Human 클래스를 다시 가져와보자.

```python
class Human:

    def __init__(self, name, age):
        self.name = name
        self.age = age
        self.use_glasses = False

    def introduce_myself(self):
        return f"My name is {self.name} and I'm {self.age} years old."
```

이 클래스는 이름과 나이를 입력 받아 인스턴스에 할당하는데 인스턴스를 조금 다르게 할당하고 싶을 수도 있다. 예를 들어 나이를 할당할 때 나이가 아니라 그 사람이 출생한 연도를 대신 입력 받아도 문제없이 나이가 결정되도록 만들고 싶을 수 있다.  

이럴 때 팩토리 메소드 패턴을 사용하면 좋다

```python
class Human:
    species = 'Homo Sapiens'

    def __init__(self, name, age):
        self.name = name
        self.age = age
        self.use_glasses = False

    @classmethod
    def from_year(cls, name, year):
        import datetime
        return cls(name, datetime.datetime.now().year - year)
```

나이 대신 태어난 연도와 이름을 받아 인간을 창조하는 *from\_year* 클래스메소드를 정의했다. 이 메소드는 올해의 연도에서 태어난 연도를 빼서 나이를 알아낸다. 기존의 나이를 직접 받는 방식도 좋지만, 이와 같이 태어난 연도를 직접 받는 인터페이스도 충분히 의미 있을 수 있다.

_classmethod_ 를 통해 인스턴스를 생성하는 다양한 인터페이스를 생성하는 팩토리 메소드 패턴을 구현했다.



---

## 4. staticmethod

---

아까 _help(classmethod)_ 를 한 것을 기억하는지? 그중 한 문장을 가져와보자.

```
Class methods are different than C++ or Java static methods.
If you want those, see the staticmethod builtin.
```

헬핑 문서의 맨 마지막 두 문장이다. 여기서는 _classmethod_ 함수를 통해 반환된 클래스메소드는 C++, 자바의 static method와는 다르다고 이야기하고 있다. 그리고 그것을 구현하려면 _staticmethod_ 를 살펴보라고 한다.  

이제 우리의 방향은 정해졌다. 근데 staticmethod는 classmethod를 어느 정도 이해했다면 문제가 없다. 거의 비슷하기 때문이다. 그래서 4장은 3장보다 짧아질 것 같다.



### 4.1. 기본 이해

_staticmethod_ 내장 함수에 헬핑을 해보자

```python
>>> help(staticmethod)

Convert a function to be a static method.

A static method does not receive an implicit first argument.
To declare a static method, use this idiom:

     class C:
         @staticmethod
         def f(arg1, arg2, ...):
             ...

It can be called either on the class (e.g. C.f()) or on an instance
(e.g. C().f()).  The instance is ignored except for its class.

Static methods in Python are similar to those found in Java or C++.
For a more advanced concept, see the classmethod builtin.
```

**이 함수는 다른 함수를 인자로 받아서 static method로 변환해 반환한다.**(이때 반환된 staticmethod를 '스태틱메소드'라고 언급하겠다.)

근데, 그 다음 문장이 _classmethod_ 와의 확연한 차이를 드러낸다.

<br>

> static method(스태틱메소드)는 암시적인 첫 인자를 받지 않는다.

<br>


이것이 staticmethod와 classmethod의 중요한 차이이다. 

**클래스메소드는 암시적인 첫 인자, 클래스 자체를 받아서 클래스 변수에 접근했다. 그리고 그 첫 인자는 관습적으로 'cls'로 지칭한다.** 이와는 대조적으로 **_staticmethod_ 함수로 생성된 스태틱메소드는 클래스 자신을 지칭하는 첫 인자를 받지 않기에 인스턴스의 상태는 물론 클래스의 상태와도 상관 없는 메소드가 된다.**

간단한 예제를 살펴보자. 우리는 '수학적 연산'이라는 클래스를 정의하고자 한다.

```python
class MathCalculation:
    @staticmethod
    def factorial(n):
        ret = 1
        for i in range(2, n+1):
            ret *= i
        return ret

>>> MathCalculation.factorial(10)

3628800
```

이 클래스는 기본적인 사칙연산부터 삼각함수 계산까지의 다양한 수학적 연산을 정의한다. 근데 상식적으로 우리가 정의한 클래스는 뭔가 인스턴스가 딱히 필요하지 않는 추상적인 연산들의 집합이다. 인간 클래스의 인간 인스턴스들은 매우 그럴 듯 하지만(현실에서 많이들 뛰어다니기 때문이다), 수학적 연산 클래스의 수학 연산 인스턴스는 현실의 필요로서 다가오지 않고, 실제로 필요하지 않다.(현실에서는 수학적 연산이 개체로서 뛰어다니지 않는다) 이 클래스는 수학 계산만 잘하면 되지, 인스턴스의 다양성이나 인스턴스간 상호작용이 딱히 필요하지 않아 보인다.  

또 의도한 _factorial_ 메소드에서는 클래스 변수에 대한 접근이 필요없다. 단순히 자연수 _n_ 을 받아 그 팩토리얼을 반환하면 된다. 이럴 때 스태틱메소드를 쓰면 좋다.


---

### 4.2. staticmethod의 특징

_classmethod_ 데코레이터를 통해 생성된 클래스메소드의 특징을 다음과 같이 정리해볼 수 있다.

* **스태틱메소드는 인스턴스에 독립적이다.(independent)**
  - 클래스메소드와 같다. 스태틱메소드를 실행하기 위해서는 인스턴스를 생성하지 않아도 된다.
* **클래스의 상태에 독립적이다.**
  - 스태틱메소드는 첫 인자로 'cls'를 받지 않는다. 따라서 클래스 변수(상태)도 사용하지 않고 따라서 클래스의 상태에 독립적이다.
* **클래스에 종속적이다.**
  - 위의 특징과 구분되어야 한다. 스태틱메소드도 결국 클래스의 속성(attribute)이다. 따라서 클래스에 Bound 되어 있다.

---



### 4.3. 사용처

스태틱메소드는 클래스메소드와 달리 사용처가 제한된다. **보통은 어떤 클래스의 유틸리티 메소드로 많이 쓰인다.** 다음과 같은 예를 만들어보자.

아까 우리는 Human 클래스를 정의했다. 이 클래스는 당신과 같은 인간을 정의하는데 추가 메소드들을 정의하려고 한다. 그중 임의의 숫자를 입력 받아 인간이 읽기 쉽게 천 단위로 `,`를 넣어 반환하는 'humanify\_number'이라는 메소드를 만들고 싶다고 하자.  

이 메소드를 일반 메소드로 만들 수는 있지만, 인스턴스의 상태에 종속적일 이유도 없고 또 클래스의 상태에 종속적일 이유도 굳이 없다. 그냥 숫자를 하나 입력 받아 처리하면 되기 때문이다. 따라서 이 메소드를 스태틱메소드로 만들자.


```python
class Human:
    species = 'Homo Sapiens'

    def __init__(self, name, age):
        ...

    @staticmethod
    def humanify_number(n):
        return f'{n:,}'
	# {} 안의 내용이 이해가 안 가면 문의주세요.


>>> Human.humanify_number(1000)
>>> Human.humanify_number(10*9*8*7*6*5*4*3*2*1)

'1,000'
'3,628,800'
```

지금까지 classmethod와 staticmethod에 대해 알아보았다.

---



## 5. 비교 & 대조

---

3장과 4장에서  _classmethod_ 로 생성된 클래스메소드와 _staticmethod_ 로 생성된 스태틱메소드에 대해 각각 알아봤다. 이번 5장에서는 이 둘의 공통점과 차이점을 정리해보자. 언제나 비교와 대조는 서로에 대한 이해를 높이는 데 도움이 된다.


### 5.1. 공통점

클래스메소드와 스태틱메소드의 공통점은 다음과 같다.

1. **인스턴스에 대해 독립적이다.**
  - 둘 모두 실행하기 위해 인스턴스를 생성할 필요가 없고 클래스에서 직접 호출할 수 있다. 따라서 인스턴스의 상태에 대해 독립적이다.
1. **인스턴스에서 실행가능하다.**
  - 이 둘은 인스턴스에 대해 독립적인데 특이하게도 인스턴스에서 실행은 할 수 있다.
1. **클래스에 종속적이다.(bound or dependent)**
  - 둘 모두 클래스에 속한 속성이다. 클래스를 통하지 않고는 실행할 방법이 없다. 따라서 클래스에 대해 종속적이다. 


---



### 5.2. 차이점

1. **클래스메소드는 클래스 변수에 접근가능한 데 반해 스태틱메소드는 그렇지 않다.**
  - 클래스메소드에서는 'cls'라는 클래스를 지칭하는 인자를 암시적으로 받아 이 변수를 통해 클래스 변수에 접근할 수 있다.
  - 스태틱메소드는 첫 인자로 이 변수를 받지 않는다. 따라서 함수 블록 내에서 하드코딩하지 않는 이상 클래스 변수에 접근할 수 없다.
1. **클래스메소드는 클래스 변수(상태)에 종속적이고 스태틱메소드는 클래스 변수(상태)에 독립적이다.**
  - 클래스메소드는 클래스 변수 값에 따라 결과가 달라질 수 있지만 스태틱메소드는 그렇지 않다.
1. **클래스가 상속될 때 클래스메소드는 상속을 제대로 반영하지만 스태틱메소드는 그렇지 않다.**
  - 이는 예제를 통해 확인해야 한다.
  - 우리는 클래스 상속관계를 만들되 'name'이라는 클래스 변수를 통해 클래스의 이름을 관리하고 클래스의 이름을 반환하는 'get\_class\_name'이라는 메소드로 클래스의 이름을 확인하고 싶다. 이때 이름을 구하는 하나의 메소드를 클래스메소드, 스태틱메소드로 각각 정의하고 상속관계에서 차이를 보자.


```python
# 먼저 클래스메소드로 정의
class BaseClass:
    name = "I'm BaseClass to be inherited"

    @classmethod
    def get_class_name(cls):
        print(cls.name)

class RealClass(BaseClass):
    name = "Succeeding you, father"

>>> RealClass.get_class_name()

Succeeding you, father
```


_BaseClass_ 는 클래스 이름을 반환하는 '*get\_class\_name*' 메소드를 정의한다. 그리고 _RealClass_ 는 _BaseClass_ 를 상속하되, 클래스 이름(_name_)은 그에 맞게 당연히 바꼈다.  

먼저 클래스 이름을 반환하는 메소드를 클래스메소드로 만들었다. 

이때, **메소드는 상속된 클래스의 이름을 올바르게 표현한다.** 클래스가 바꼈으니 바뀐 클래스의 이름을 출력하는 것이 이 예제에서는 이치에 맞다.

<br>

이번엔 같은 함수를 스태틱메소드로 만들어보자.

```python
# 스태틱메소드로 정의
class BaseClass:
    name = "I'm BaseClass to be inherited"

    @staticmethod
    def get_class_name():
        print(BaseClass.name)

class RealClass(BaseClass):
    name = "Succeeding you, father"

>>> RealClass.get_class_name()

I'm BaseClass to be inherited
```

스태틱메소드에서는 인자를 받지 않았다.  

**또, 스태틱메소드로 정의했을 때는 클래스의 변수에  _BaseClass.name_ 처럼 하드코딩해서 접근했다.**  
하드코딩을 할 수밖에 없었던 이유는 **스태틱메소드는 첫 인자로 'cls' 인자를 받지 않기 때문에 클래스 변수에 직접 접근할 방법이 없기 때문이다.** 

그래서 상속을 했을 때도 메소드의 코드는 부모 클래스를 그대로 지칭하고 따라서 자식 클래스의 메소드가 부모의 이름을 출력하고 있다.  

이처럼 **클래스메소드는 상속관계를 잘 반영하고, 스태틱메소드는 그렇지 않다.**

---



## 6. 마치며

---

이상으로 classmethod와 staticmethod 각각을 알아보고 서로를 비교, 대조해보았다. 이 둘은 인스턴스의 상태에 영향을 받는 일반 메소드와 달리, 인스턴스에 독립적이고 클래스에 종속적인 메소드를 만드는 내장 함수로서 OOP의 여러 디자인 패턴을 구현하는 데 요긴하게 사용된다. 이때 _classmethod_ 를 통해 반환된 클래스메소드는 'cls'라는 첫 인자를 암시적으로 받아 클래스의 상태에 종속적인 데 반해, _staticmethod_ 를 통해 반환된 스태틱메소드는 클래스 상태에도 독립적인 특징을 보였다.  

생각보다 너무 길어졌다. 전혀 예상하지 못했는데 실제 난이도에 비해 분량이 방대해진 느낌을 지울 수 없기는 하다. 이 포스트는 OOP에 익숙하신 분들보다는 OOP에 익숙하지 않고 classmethod, staticmethod에 대해 정말 아무것도 모르는 분들을 위한 가이드가 될 것으로 판단된다. 그래도 나도 이번에 준비하면서 이 둘은 확실하게 구분할 수 있게 되었다.  

이상 포스트를 마칩니다.



## 7. 자료 출처

---

* [GeeksforGeeks: Static functions in C](https://www.geeksforgeeks.org/what-are-static-functions-in-c/){:target="_blank"}
* [PEP 206: Python Advanced Library](https://www.python.org/dev/peps/pep-0206/){:target="_blank"}
* [Wikipedia: Factory method pattern](https://en.wikipedia.org/wiki/Factory_method_pattern){:target="_blank"}
* [Programiz: classmethod](https://www.programiz.com/python-programming/methods/built-in/classmethod){:target="_blank"}
* [Programiz: staticmethod](https://www.programiz.com/python-programming/methods/built-in/staticmethod){:target="_blank"}
