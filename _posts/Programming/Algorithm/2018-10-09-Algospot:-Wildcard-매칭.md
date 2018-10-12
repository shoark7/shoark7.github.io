---
layout: post
title: '[Algospot] 와일드카드 패턴 매칭 알고리즘'
date: 2018-10-10
description: '와일드카드 패턴과 문자열이 주어질 때 둘이 매칭되는지 확인하는 알고리즘을 짜보자!'
img:  /algorithm/wildcard.png
categories: [Programming, Algorithm]
tags: [Algorithm, wildcard, Algospot]
---


#### 문제 소스 : [WILDCARD](https://algospot.com/judge/problem/read/WILDCARD){:target="_blank"}


## 0. 와일드카드란?

### 0.1. 와일드카드

프로그래밍에서 **와일드카드(wildcard)는 여러 문자열을 상징할 수 있는 '\*', '?' 등의 단일 문자를 가리킨다.** 보통 이 문자들은 '가', 'a' 처럼 단순한 문자로 취급 당하지 않고, 조건에 맞는 문자열로 해석된다.  

예를 들어보자. 맨 윗 사진은 배쉬 쉘 화면을 찍은 사진인데 'echo', 'ls' 등 기본적인 유닉스 커맨드를 활용한 예제를 보여준다.  

그 중에서 `echo *`를 주목하자. 쉘을 많이 다뤄보지 않은 사람은 _echo_ 를 인자로 받은 문자열을 그대로 화면에 출력하는 기능으로 알고 있는 경우가 많은데 **이 예제에서는 _echo_ 가 `*`를 그대로 반환하지 않고 긴 문자열을 출력했다.** 자세히 살펴 보면 밑의 _ls_ 명령과 같은 결과물을 반환했음을 알 수 있다.  

이렇게 출력된 이유는, **'\*'는 일반 문자와 다른 와일드카드 문자로서 유닉스에서는 '\\' 등으로 escape하지 않으면 0개 이상의 임의의 문자열과 매칭되는 특징을 가지고 있다.** 0개 이상의 임의의 문자열은 사실상 모든 문자열을 의미하는데 쉘 프로그램은 `echo *`을 그대로 실행하기 전에 해석해서 현재 디렉토리의 모든 파일을 문자열로 출력한 것이다.

와일드카드는 이외에도 많은데 대표적으로는 임의의 1개 문자와 매칭되는 '?' 등이 있다.  

<br>

그러면 **와일드카드가 포함된 문자열과 일반 문자열이 매칭되는지 확인할 수 있다.**  
가령 'b\*'는 b로 시작하는 모든 문자열과 매칭될 수 있다. 'b', 'bear', 'benbrode' 등등. '\*'는 0개 이상의 모든 문자열과 매칭될 수 있으니까. 그러면 '\*'는 빈 문자열 ''과도 매칭되는 것이다.  

**'?'는 임의의 1개의 문자와 매칭된다고 했다. 그러면 'be?r'는 'bear', 'beer' 등과 매칭될 수 있다.**  




### 0.2 쓰임새

이걸 뭘 어떻게 하라는건가? 와일드카드의 쓰임새는 뭘까? 와일드카드는 대표적으로 파일(폴더) 이름을 매칭하는 데 쓰인다.

**파일 이름에 와일드카드를 매칭하는 것은 내가 생각하건데 UNIX 쉘 같은 CLI(Command Line Interface) 환경을 매우 강력하게 하는 기능 중 하나**로 파일을 찾거나, 'D로 시작하는 파일만을 가져와라' 등의 명령을 내릴 때 사용될 수 있다.

바로 예를 살펴보자.

유닉스 환경에서 파일 이름이 ' . '으로 시작하는 파일은 숨김 파일의 역할을 한다. 유닉스 쉘에서 _ls_ 를 입력하면 현재 디렉토리의 모든 파일이 나오는데 그게 파일의 전부는 아니다. ' . '으로 시작하는 파일 또는 디렉토리가 숨어 있으며 보통 유저가 실제로 실행할 일이 없는 설정파일 등을 저장할 때 이런 이름을 준다.  

그렇다면, 현재 폴더에서 이름이 ' . '으로 시작하는 파일들을 모두 찾으려면 어떻게 해야 할까?  
조건은 분명하다. **' . '으로 시작하는 것. ' . '으로 시작하는 모든 문자열을 와일드카드로 표현하면 ' .\*'가 된다.**  

이 와일드카드 패턴을 _ls_ 에 사용하면 된다.


```sh
$ ls .*

>>> 
...

.lesshst
.mysql_history
.netrc
.node_repl_history
.pam_environment
.profile
.python-version
.sudo_as_admin_successful
.tmux.conf
.viminfo
.viminfo.tmp
.viminfw.tmp
.viminfx.tmp
.viminfy.tmp
.viminfz.tmp
.vimrc
.vimrc.bak

...
```

내 우분투 환경에서 홈 디렉토리에서 명령어를 실행했을 때의 결과 중 일부이다. ' . '으로 시작하는 파일들의 목록이 출력되었고 역시 보이는 게 다가 아니었다. **파일들의 면면을 보면 확실히 '.vimrc' 등의 설정파일이나, '.bak' 과 같은 백업 파일 등이 숨김파일로 지정되어 있음을 알 수 있다.**  


좀더 실용적인 활용을 원하는가? 그렇다면 내가 배시 쉘에서 사랑해 마지않는 프로그램을 와일드카드를 사용해서 써보도록 하자.  

`find`라는 프로그램이 있다. 말 그대로 '파일이나 폴더를 찾는' 기능으로 비슷한 역할을 하는 다양한 프로그램 중에서 좀더 복잡하고 자유도가 높다.

이 프로그램에도 아까와 같은 와일드카드 패턴을 조건으로 주고 검색할 수 있는데 추가로 소유자, 파일의 생성날짜 등등 보다 더 복잡한 조건을 줄 수 있다. 일단 'find' 소개 시간이 아니기 때문에 와일드카드 패턴으로 검색해보자.


```sh
$ find ~ -name "*.md"

>>>
...
/home/sunghwanpark/archive-directory/arduino-1.8.0/hardware/arduino/avr/bootloaders/caterina-Arduino_Robot/README.md
/home/sunghwanpark/archive-directory/arduino-1.8.0/hardware/arduino/avr/bootloaders/gemma/README.md
...
```

**이 식은 내 홈디렉토리(\~) 안에서 파일 이름이('-name') 마크다운 파일(확장자가 '.md')을 모두 찾는 식이다.** **`find`는 주어진 경로 안의 모든 디렉토리를 샅샅이 훑으면서 와일드카드 패턴에 매칭되는 폴더를 모두 콘솔에 출력한다.** 콘솔 출력이 기본 조건이며 파일을 삭제하거나 커스터마이즈된 커맨드를 _map_ 하듯이 적용할 수도 있다.

어떤가, CLI의 강력함에 매료되지 않는가? 더 많은 와일드카드 종류는 [여기](https://support.office.com/en-us/article/examples-of-wildcard-characters-939e153f-bd30-47e4-a763-61897c87b3f4)서 확인할 수 있다.


와일드카드에 대한 설명에 시간이 많이 소요됐다. 이제 문제를 풀어보자.



## 1. 문제 분석

### 1.1 문제 개괄

맨 위의 'WILDCARD' 링크를 클릭해 문제를 확인해보면 이 문제는 **와일드카드 패턴과 test할 문자열이 주어질 때 이 둘이 매칭되는지 여부를 반환하는 문제이다.** 우리가 앞서 살펴보았던 와일드카드 활용 예제에서 컴퓨터가 직접 하던 매칭 알고리즘을 대신 우리가 직접 짜보는 것이다.  다만 이 문제에서는 주어지는 와일드카드를 '?'와 '\*'로 한정한다. '?'는 단 한 개의 임의의 문자와 매칭되고, '\*'는 0개 이상의 모든 문자열과 매칭된다.  

이 문제를 직관적으로 살펴보면 패턴과 문자열을 처음부터 한 글자씩 맞춰보면서 다르다면 거짓을 반환하면 되지 않을까 싶다. 가령 'abc'와 'abe'가 주어지면 'a'와 'b'까지는 같기 때문에 **반복하며** 'c'와 'e'가 되는 지점에서 같지 않기 때문에 거짓이 반환된다.

만약 패턴의 문자가 와일드카드가 되면 어떻게 될까? '?'일 때는 어렵지 않다. '?'는 임의의 문자이기 때문에 test 문자열이 끝나지 않았다면 그냥 넘어가면 된다.  

**진짜 문제는 '\*'로, '\*'는 최소 0개에서 최대 무한개의 문자열을 포함할 수 있기 때문에 골치 아파진다. 그렇지만 주어지는 문자열의 길이가 무한일리는 없기 때문에 우리는 '\*'가 포함하는 문자열을 0개부터 시작해서 문자열이 끝날 때까지 하나씩 늘리면서 테스트하면 될 것이다. 매칭되는 순간 참을 반환하며, test 문자열이 끝났는데도 매칭이 안 되면 거짓을 반환하면 된다.**


### 1.2. 문제 명세

우리는 '\*'가 문자를 하나도 안 포함할 때와 text 문자열의 나머지를 전부 매칭되는 경우까지 모두를 살펴야 한다. 이때 적절한 방법인 완전탐색과 만약 부분문제가 중복된다면 동적계획법을 사용해 문제를 해결하고자 한다.  

그전에, 문제를 명세하자. 문제 정의 없이 문제 해결할 수 없지.

```sh

문제 : 주어진 와일드카드 패턴과 임의의 문자열이 매칭되는지의 참/거짓 여부를 반환하라.

:입력:
	pattern | str : 와일드카드 패턴
	word    | str : 테스트할 문자열
:출력:
	매칭 여부 | bool : 패턴과 문자열이 매칭되는지 여부	


# 출력이 반환되는 기저 사례 또는 조건

	1. pattern의 n번째 글자가 '?' 또는 '*'가 아닌데 pattern과 word의 n번째 글자가 다르다. -> 거짓
	2. pattern이 끝났는데 word가 남았다. -> 무조건 거짓
	3. word가 끝났는데 pattern이 남았다. -> pattern의 나머지가 '*'의 연속이면 참, 아니면 거짓
	4. pattern의 n번째 글자가 '*'이다. -> 복잡해진다. '*'이 포함하는 글자를 0개부터 하나씩 추가해 하나라도 매칭되면 참을 반환한다. 다 실패하면 거짓 반환
	5. 위 조건에 매칭이 안 된다. -> 무조건 거짓
```

이를 바탕으로 문제를 해결해보자.


## 2. 완전탐색

```python
def wildcard_exhaustive(pattern, word):
    len_p, len_w = len(pattern), len(word) # 각 문자열의 길이를 구한다.
    nth = 0  			           # 확인할 문자의 위치 변수. 0으로 초기화한다.

    # 첫 번째 조건
    while nth < len_p and nth < len_w and (pattern[nth] == '?' or pattern[nth] == word[nth]): 
        nth += 1

    # 두 번째 조건
    if len_p == nth:
        return nth == len_w

    # 네 번째 조건
    if pattern[nth] == '*':
        skip = 0
	while skip + nth <= len_w:
	    if wildcard_exhaustive(pattern[nth+1:], word[skip+nth:]):
                return True
	    skip += 1

    # 다섯 번째 조건
    return False


wildcard_exhaustive('abc?', 'abcd')
wildcard_exhaustive('*', 'asdf')
wildcard_exhaustive('*', '')


>>> True
>>> True
>>> True
```

각 코드를 뜯어보자.

```python
    len_p, len_w = len(pattern), len(word) # 각 문자열의 길이를 구한다.
    nth = 0  			           # 확인할 문자의 위치 변수. 0으로 초기화한다.
```

len\_p, len\_w로 패턴과 문자열의 길이를 담은 변수를 만든다.  
문자열의 위치를 비교할 _nth_ 라는 변수를 만든다. _nth_ 라는 이름은 '6th', '9th' 처럼 서수를 만들 때 'th'를 붙인다는 데서 착안했다.  

---

```python
    # 첫 번째 조건
    while nth < len_p and nth < len_w and (pattern[nth] == '?' or pattern[nth] == word[nth]): 
        nth += 1
```

본격적인 조건 검사식이다. 앞서 정의한 첫 번째 조건은 _nth_ 번째 글자가 다를 때이다. 이를 뒤집으면 _nth_ 번째 글자가 같다면 그냥 넘어가면 된다. while로 글자가 달라지거나 패턴이나 문자열이 끝날 때까지 _nth_ 를 하나씩 올린다.  
이 while문을 빠져 나왔다면 나머지 조건을 확인하면 된다.

---

```python
    # 두 번째 조건
    if len_p == nth:
        return nth == len_w
```

두 번째 조건이다. 패턴이 끝났다면 문자열도 끝났는지 확인한다. _nth_ 가 _len\_w_ 와 같다면 패턴과 문자열의 길이가 같다는 것이 된다.

---

```python
    # 네 번째 조건
    if pattern[nth] == '*':
        skip = 0
	while skip + nth <= len_w:
	    if wildcard_exhaustive(pattern[nth+1:], word[skip+nth:]):
                return True
	    skip += 1

    # 다섯 번째 조건
    return False
```

마지막으로 가장 중요한 패턴의 글자가 '\*'일 때이다.

'\*'가 포함할 글자 수를 담을 변수를 _skip_ 로 저장하고 그 개수를 0개부터 시작한다. 여기서 1개씩 글자를 더 포함하면서 문자열이 매칭되는지 확인할 것이다.

**지금 네 번째 조건까지 왔다는 것은 상황이 1, 2, 3번째 조건들에 맞지 않았다는 것이고 따라서 현재 문자열은 패턴과 테스트 문자열이 끝나지도 않았고, _pattern[nth]_ 는 현재 '\*'인 상황이다.**  

<br>

그렇다면 **test 문자열이 끝나지 않을 때까지(while _skip_ + _nth_ <= _len\_w_:),**  
**'\*' 다음의 패턴의 남은 문자열(_pattern[nth+1:]_)과**  
**test 문자열의 나머지 부분(_word[skip+nth:]_)이 매칭되는지 점진적으로 확인한다.**  

당연히 _skip_ 은 문자열의 끝까지 확인해야 하기 때문에 1씩 키운다.  

그리고 네 번째까지 확인이 안 됐으면 무조건 틀리게 한다.

<br>


여기서 짚고 넘어갈 것. **`while skip + nth <= len_w:`에서 왜 `<`가 아닌 `<=`가 쓰였을까??**  
이건 '*'과 빈 문자열 ''을 매칭한다면 쉽게 이해할 수 있다. 매칭 결과는 참이 된다. 
_skip_ 도 0, _nth_ 도 0, _len\_w_ 도 0이 되는데 여기서 '<='를 주지 않으면 반복문 자체를 들어갈 수 없다.   
그래서 참도 반환되지 않겠지.  

또 이것이 위에서 세 번째 조건을 살피지 않은 이유와 같다. 세 번째 조건은
`test 문자열이 끝났는데 pattern이 끝나지 않았을 때`인데 이게 네 번째에서 걸러진다.  

이것이 완전탐색을 활용한 방법이다.




## 3. 동적계획법


### 3.1. 부분문제의 존재

위의 완전탐색 방법은 훌륭하지만, 부분문제를 중복해서 계산한다는 문제가 있다.  
가령 다음과 같은 패턴이 있다고 하자. `123*abc*def*ghi`
**이 패턴에는 '\*'가 세 개 있는데 이때 `def*ghi` 부분이 `123*...`과 `abc*...`를 해결할 때 중복된다.**  

그렇다면 우리는 동적계획법을 적용해볼 수 있다. 



### 3.2. 구현 아이디어

행에는 패턴의 길이만큼 열에는 test 문자열의 길이만큼의 크기의 2차원 배열을 만들자.  

가령 **_cache[p][w]_ 는 패턴의 p번째에서 끝까지의 부분 문자열부터, 문자열의 w번째에서 끝까지의 부분 문자열이 매칭되는지의 여부를 담는다.**

<br>

그런데 **cache의 크기를 잡을 때 패턴의 길이와 문자열의 길이에 1을 더해서 해야 한다.** 이걸 또 이해하는 게 중요한데 이것도 빈 문자열 때문이다.

가령 **패턴이 길이가 3인 `abc`로 주어진다고 하자. 그러면 `abc`의 부분 문자열은 `'abc'`, `'bc'`, `'c'`, `''` 이렇게 4가지가 나온다. 즉, 길이에 +1을 해야 문자열의 모든 문자열에 대한 커버를 할 수 있다.**  

이제 실제 구현을 해보자.



### 3.3 구현


```python
def wildcard(pattern, word):
    len_p, len_w = len(pattern), len(word)
    cache = [[-1 for _ in range(len_w+1)] for _ in range(len_p+1)]

    def match(nth_p, nth_w):
        if cache[nth_p][nth_w] != -1:
            return cache[nth_p][nth_w]

        if nth_p < len_p and nth_w < len_w and (pattern[nth_p] == '?' or pattern[nth_p] ==
                                                word[nth_w]):
            cache[nth_p][nth_w] = match(nth_p+1, nth_w+1)
            return cache[nth_p][nth_w]

        if nth_p == len_p:
            return nth_w == len_w

        if pattern[nth_p] == '*':
            if match(nth_p+1, nth_w) or (nth_w < len_w and match(nth_p, nth_w+1)):
                cache[nth_p][nth_w] = True
                return True

        cache[nth_p][nth_w] = False
        return False

    return match(0, 0)
```

위 코드는 앞서 살펴 본 완전탐색 방법과 조금 다르지만 조건만은 거의 동일하다.  


```python
len_p, len_w = len(pattern), len(word)
cache = [[-1 for _ in range(len_w+1)] for _ in range(len_p+1)]
```

길이를 담은 변수를 설정하고 캐쉬를 만든다. 이때 캐쉬의 크기를 문자열의 크기보다 1 크게 해준다.  
-1로 초기화하는 것은 값이 -1일 때 아직 계산이 안 됐다는 것을 알게 하기 위해 임의의 숫자를 선택했다.

---


```python
if cache[nth_p][nth_w] != -1:
    return cache[nth_p][nth_w]
```

캐시 값이 -1이 아니면 계산을 이미 했다는 것이기 때문에 그 값을 그대로 반환한다.  
우리가 동적계획법을 쓰는 이유이다.

---

```python
if nth_p < len_p and nth_w < len_w and (pattern[nth_p] == '?' or pattern[nth_p] ==
                                        word[nth_w]):
    cache[nth_p][nth_w] = match(nth_p+1, nth_w+1)
    return cache[nth_p][nth_w]
```
아까 _nth_ 를 증가시키던 식과 원칙적으로 똑같다. 다만, 값이 같을 때 _match_ 함수를 반복 실행함으로써 캐쉬에 값을 꾸준히 채운다. 그리고 값을 반환한다.

---


```python
if nth_p == len_p:
    return nth_w == len_w
```

두 번째 조건이다. 패턴이 끝났을 때 문자열도 끝났는지 판단해 값을 반환한다.


```python
if pattern[nth_p] == '*':
    if match(nth_p+1, nth_w) or (nth_w < len_w and match(nth_p, nth_w+1)):
        cache[nth_p][nth_w] = True
        return True

cache[nth_p][nth_w] = False
return False
```

패턴의 _nth\_p_ 번째 글자가 '\*'일 때를 확인한다.  

재밌는 if 문 중첩이 나오는데 이것이 핵심인 것 같다.  
**'\*'가 글자를 하나씩 흡수해나가는 것은 결국 '\*'가 글자를 흡수하지 않을 때와 하나 흡수할 때를 반복실행해 'or' 연산해 참이 되면 값이 참이 되는 것이다.**  

이때 `nth_w < len_w` 일 때까지 조건을 주고 계속 키워나가 하나라도 매칭이 되면 참을 반환하게 하면 된다.  

이 식은 여러 번 쳐다보자.

<br>

조건을 하나도 만족시키지 못했다면 거짓을 반환한다.


---

<br>

이렇게 와일드카드 문제를 완전탐색과 동적 계획법을 통해 해결해보았다.
