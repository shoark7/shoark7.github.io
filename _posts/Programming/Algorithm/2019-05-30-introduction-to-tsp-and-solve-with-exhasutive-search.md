---
layout: post
title: "TSP 알고리즘 1: 문제 소개 및 완전탐색 구현"
date: 2019-05-30
description: "유명한 TSP, '여행하는 외판원 문제'를 소개하고, 완전탐색으로 구현합니다."
img:  /algorithm/tsp-dynamic-programming-logo.jpg
categories: [Programming, Algorithm]
tags: [TSP, exhaustive_search]
---

## 0. Index

> 1. [들어가며](#1)
> 2. [문제 소개](#2)
> 3. [완전탐색으로 풀기](#3)
>    - 3.1. [문제 정의](#3a)
>    - 3.2. [완전탐색 코드](#3b)
> 4. [마치며](#4)
> 5. [자료 출처](#5)


<br id="1">


## 1. 들어가며

---

간만에 알고리즘 포스트다. 마지막 알고리즘 포스트가 4월 16일에 쓴 문자열에서 가장 긴 팰린드롬을 찾는 [포스트](https://shoark7.github.io/programming/algorithm/get-longest-palindromes-in-string){:target="_blank"}였는데 이 포스트는 영어로 썼기 때문에 한글로 쓰는 알고리즘 포스트가 더 반갑게 느껴지는 것 같기도 하다.

오늘 포스트는 백준 사이트의 [2098](https://www.acmicpc.net/problem/2098){:target="_blank"}번 문제에 대한 해답이다. 바로 그 유명한 TSP, '여행하는 외판원 문제'로서 이 분야는 너무 유명하고 연구도 많이 진행돼 다양한 변형된 형태와 해결기법들이 존재하는 것으로 알고 있는데, 솔직히 현재 내 앎의 수준을 아득히 넘어선다. 그래서 오늘은 **가장 정석적인 TSP의 문제소개와 함께 완전탐색으로 문제를 해결한다.**

**TSP는 이번 포스트를 포함해 최소 두 번 이상의 연속 포스트가 될 것이다.** 두 번째 포스트는 문제를 좀더 고찰하고, 개선점을 찾은 뒤 부분문제를 정의해 동적 계획법으로 풀어본다. 추가로 경로가 아닌 최소의 길이를 구하는 원 문제의 요구 사항에 그치지 않고 실제 경로를 구하는 연구까지 해볼 생각이다. 원래는 평소 하던대로 문제 소개, 완전탐색, 동적 계획법 풀이를 모두 한 포스트에 적으려고 했는데 시리즈로 작성하는 이유는 완전탐색 코드까지 작성한 결과 포스트가 너무 길어 동적 계획법까지 다 다루기에는 양이 넘쳤기 때문이다. 그래서 나눌 수밖에 없었다. 덕분에 내 블로그 역사상 첫 '시리즈'가 되었다. 

[직전 포스트](https://shoark7.github.io/programming/knowledge/some-useful-bit-tricks-and-usages){:target="_blank"}에서 유용하고 재미있는 비트 연산을 소개했다. **이번 TSP 시리즈의 특징은 소개한 비트 연산을 활용해서 이 문제를 풀어볼 것이다.** 사실 이번 시리즈는 직전 포스트의 내용의 강력함을 어필하기 위해 준비하기도 했다 :) 혹시나 실제 알고리즘에서 비트 연산이 헷갈리시는 분들은 저 포스트를 참고하시면 좋을 듯 하다.


<br id="2">

## 2. 문제 소개

---

**TSP(Travelling Salesman Problem, 일명 '여행하는 외판원 문제')는 조합 최적화(Combinatorial Optimization) 문제로 전산학에서 연구된 가장 유명한 문제 중 하나다.** 이 문제의 요구사항은 간단하다.

![Example of simple TSP](/assets/img/algorithm/tsp-dynamic-programming-example.jpg)

<p class="function-definition">
  도시의 개수와 각 도시 쌍 간의 거리들이 주어질 때, 모든 도시를 한 번씩 방문하고 여행을 시작한 원래 도시로 돌아올 수 있는 최단거리 경로(Shortest distance path)를 구하라 
</p>


**이 포스트에서는 각 도시를 단 한 번씩만 방문할 수 있다고 가정한다.** 이는 백준 문제의 요구사항과 일치한다. 하지만 다른 변형에서는 거리를 최소로 만들기만 한다면 한 도시를 두 번 이상 방문하게 할 수도 있다. 또 **원 문제는 실제 경로가 아닌 경로의 길의의 최소값만을 구하기 때문에 완전탐색 코드에서는 실제 경로를 구하지는 않는다.**

그나저나 왜 문제 이름이 '여행하는 외판원 문제'인지 이제 이해가 간다. 실제 영업하는 외판원이 여러 도시로 영업 출장을 다녀온 뒤 집으로 돌아오는 것이 쉽게 연상되지 않는가? 최근에 보고 있는 드라마 '미생'이 생각나기도 한다.

<br>

문제 설명은 쉽지만 바로 풀기는 마냥 쉽지 않다. 문제 자체도 NP-난해 문제로 적어도 아직까진 효율적이라고 판단되는, 다항 이하의 시간복잡도를 갖는 풀이가 나오지 않았다. 이 문제는 현실에 충분히 적용해볼 수 있는 문제로 가령 '해외 여행을 가는데 경로를 어떻게 짜지?' 등의 일상적인 고민에 적용해볼 수 있고, 실제로 생물학, 천문학 등의 분야에서 응용되고 있다고 한다. 그 중요성으로 말미암아 효율적인 알고리즘을 위한 정말 다양한 노력과 연구들이 있었고, 조금이라도 성능을 개선하는 기상천외한 방법들이 많이 연구되었다.

그 노력들은 결실을 맺었는데, 다음 포스트에서 소개할 동적 계획법을 통한 개선은 물론이고, 가지치기(pruning), 탐색 순서 바꾸기 등의 방법들이 개발되었다. 또 꼭 정확한 답을 찾지 않더라도 1% 이내의 작은 오차를 갖는 효율적인 휴리스틱 알고리즘들도 많이 연구되었다.(물론 여기서는 다루지 않는다.) 대개 외판원 순회 알고리즘을 구현할 때는 도시의 수를 어지간하면 20개를 넘기지 않게 잡는다. 하지만 어떤 효율적인 알고리즘 논문에서는 무려 49개의 도시를 예로 들며 최적화한 알고리즘으로 멋지게 테스트를 성공하기도 했다. 이 정도의 도시 수는 이 포스트 내용처럼 단순하게 짜면 아마 내가 죽기 전에는 답이 나오지 않을 것이다.(이것도 낙관적인 전망이다.)

이렇게 유명하고 중요한 문제기 때문에 백준, 알고스팟 등 다양한 알고리즘 사이트에서 이 문제를 접할 수 있다. 충분히 공부할 가치가 있으며 지금 이 포스트를 읽는 것이 옳은 판단이라고 미소지을 수 있도록 잘 작성해보도록 하겠다.


<br id="3">

## 3. 완전탐색으로 풀기

---

<br id="3a">

### 3.1. 문제 정의

첫 번째 풀이로는 완전탐색(exhaustive search)을 사용해서 코드를 작성한다. 완전탐색의 장점은 문제를 비교적 직관적으로 바라보고 풀어도 답이 나온다는 것이다. TSP를 직관적으로 바라보고 답을 찾으려면 문제 정의를 다음과 같이 하자.

<p class="function-definition">각 도시에서 출발해서 다른 모든 도시를 차례로 방문하고 모든 도시를 방문했으면 해당 경로의 길이와 지금까지 찾은 중간해의 최소값을 택해 나가자.</p>


'_각 도시를 잇는 모든 경로를 만들어 그중 길의의 최소값을 택하자_'. 상당히 직관적이고 누구나 일단 머리는 끄덕여지는 문제 정의다. 그러면 이제 이를 함수식으로 옮기자. 한 도시에서 시작해 각 도시를 한 번씩 모두 거치는데 이때 각 방문을 재귀함수로 정의할 수 있을 것 같다.


> find\_path(start, last, V, tmp\_dist):
> 
> * 여행을 start에서 시작했고,
> * 현재까지 방문한 중간 경로의 마지막 도시는 last이고,
> * 방문한 도시의 집합은 V,
> * 중간경로의 길이는 tmp\_dist일 때
> 
> 해당 중간경로를 사용해서 여행을 마쳤을 때의 완성된 모든 경로의 길의의 최소값을 구하라.



미안하다. 좀 길다. 그리고 함수에서 관리하는 상태 개수 또한 4개로 적지 않다. 사실 각 상태를 어떤 자료형을 쓰느냐에 따라 상태의 수를 조금 줄일 수도 있다. 하지만 이후 동적 계획법 포스트를 생각했을 때 이런 상태관리가 적절하다고 일단 판단했다.

_find\_path_ 함수에 대한 유사코드(pseudo code)를 살펴보자.

\\[
	\text{전체 도시 수가 N, 각 도시 간 거리를 담은 행렬이 D,}
	\text{최종적으로 반환할 최소 거리가 ans일 때,}
\\]

```
	[01] ans = infinite
	[02] 
	[03] find_path(start, last, V, tmp_dist):
	[04]    if 모든 도시를 방문했다면:
	[05]       return_home_dist = D[last][start] or infinite
	[06]       ans = min(ans, tmp_dist + return_home_dist)
	[07]       return
	[08]
	[09]    for left_city in V의 여집합:
	[10]      if last와 left_city가 연결되어 있다면:
	[11]         left_city를 방문 및 V에 추가.
	[12]         find_path(start, left_city, V, tmp_dist + D[last][left_city])
	[13]         V에서 left_city를 제거.

	...
	[14] 이제 'ans'가 모든 경로의 최소값
```

4가지의 상태를 유지하며 최종 정답을 경신해나가는 _find\_path_ 함수의 유사코드를 작성했다. 도시 수와 도시 간 거리를 담은 행렬을 각각 N과 D라고 한다.(이는 문제 정의에서 주어진다.) 그리고 1번 줄처럼 반환할 최종값을 무한으로 설정하고 점점 줄여나갈 것이다.

이 함수는 기본적으로 재귀함수다. 함수의 탈출조건은 4번처럼 모든 도시를 방문했을 때다. 모든 도시를 방문했으면 6번 줄에서 _ans_ 와 지금까지 만든 경로의 길이를 비교해 더 작은 값으로 _ans_ 를 경신한다. 이때 5번 줄을 주목하자. **모든 도시를 방문했을 때 외판원은 아직 집에 돌아오지 않았다. 경로의 마지막 도시에서 첫 도시로 돌아와야 하는데 두 도시가 이어져 있는지 확인해야 한다. 이어져 있으면 그 값을 길이에 추가하면 되지만 이어져 있지 않으면 모든 도시를 방문했어도 결국 돌아와야 한다는 문제 요구를 충족하지 못하기 때문에 무한값을 대신 내보내 이 경로가 답이 될 수 없게 한다.** 파이썬에서 `or` 연산자는 두 값 중 하나를 선택하도록 할 수도 있다. 

함수에서 여행을 시작한 _start_ 도시를 기억해야 했던 이유가 이것이다. 결국 돌아와야 하기 때문에 긴 여행 후에도 출발 도시를 기억하고 있어야 함수를 마무리할 수 있다.

다음은 나머지 도시를 방문하는 for 문을 살펴보자. 9번 줄에서 $$V^\complement$$는 방문한 도시의 여집합, 즉 아직 방문하지 않은 도시의 집합이다. 이를 실제 코드에서는 비트마스킹으로 구현할 것이다. 10번 줄에서 이 도시를 방문할지에 대한 검증을 한다. 원 백준 문제에서는 도시 간 연결이 안 되어 있는 경우도 있기 때문에 현재 중간경로의 마지막 도시에서 후보 도시로 연결되는 길이 있는지 확인해야 한다. 11번 줄에서 연결되어 있으면 방문하고, 해당 도시를 V에 포함시켜야 한다. 12번째 줄이 다음 탐색을 해나가는 재귀호출이다. _last_ 를 방금 방문한 _left\_city_ 로 교체한다. 중간 경로의 길이 또한 경신한다. 마지막으로 13번 줄에서 _left\_city_ 를 V에서 제거한다. 이는 전에 조합과 순열을 구현했던 [포스트](https://shoark7.github.io/programming/algorithm/Permutations-and-Combinations){:target="_blank"}에서와 같은 원리다.

<br>

유사코드에서 모든 변수가 적절히 사용되었다. 이 변수들이 없으면 함수가 동작하지 않는다.

<br id="3b">

### 3.2. 완전탐색 코드

유사코드를 실제 파이썬 코드로 옮기자. 설명은 이후에 하겠다.


```python
def tsp(D):
    N = len(D)
    inf = float('inf')
    ans = inf
    VISITED_ALL = (1 << N) - 1

    def find_path(start, last, visited, tmp_dist):
        nonlocal ans
        if visited == VISITED_ALL:
	    return_home_dist = D[last][start] or inf
            ans = min(ans, tmp_dist + return_home_dist)
            return

        for city in range(N):
            if visited & (1 << city) == 0 and D[last][city] != 0:
                find_path(start, city, visited | (1 << city), tmp_dist + D[last][city])

    for c in range(N):
        find_path(c, c, 1 << c, 0)

    return ans
```

유사코드를 실제 코드로 옮겼다. 이 코드에서 눈여겨봐야 할 점은 바로 비트마스킹을 썼다는 것이다. 앞서 말했듯이 이 포스트는 직전에 작성한 비트 연산을 실제 코드에서 쓸 수 있다는 것을 증명하기 위한 포스트이기도 하다.  

이 함수에서 집중한 것은 '구현할 때 V를 어떤 자료구조를 사용할 것이냐'하는 것이었다. 익숙하고 쉬운 리스트형 비트맵을 쓸 수도 있었고 말 그대로 _set_ 자료구조를 쓸 수도 있었다. 우리는 비트를 쓴다. 이진수로 어떻게 방문한 도시 집합을 표현하는가? 간단하다. 모든 도시는 방문한 도시와 방문하지 않은 도시로 나눌 수 있다. 각 경우는 1과 0에 대응할 수 있다. 비트 사용의 여지가 확실하다.  

즉, n번째 비트의 on/off 여부로 n번째 도시를 방문했는지의 여부를 표현하자. **도시의 수 N이 8일 때, $$11110000_{(2)}$$는 0, 1, 2, 3번 도시는 방문하지 않았고, 4, 5, 6, 7번 도시는 방문한 집합을 표현한다.**

<br>

이에 대한 이해를 바탕으로 각 코드를 해석하면 다음과 같다:

```python
inf = float('inf')
ans = inf
```
파이썬에서 '무한'은 math.inf 변수를 쓰면 되는데 _math_ 모듈을 import하지 않고도 위와 같이 불러올 수 있어 신기해서 가져왔다. 정답(_ans_) 변수를 무한으로 초기화하고 경로를 찾을 때마다 더 작은 값으로 경신해서 최종답을 구할 것이다.

```python
VISITED_ALL = (1 << N) - 1
```

모든 도시를 방문했음을 의미하는 상수다. **직전 포스트에서 `(1 << N) - 1`은 'N개의 비트를 모두 켠다'와 같다고 했다.** 여기서는 'N개의 도시를 모두 방문했다'와 같다.

```python
def find_path(start, last, visited, tmp_dist):
```

각 도시를 방문하는 재귀함수를 정의한다. 방문 도시 집합 V를 _visited_ 로 이름을 바꿨다. 실제 코딩에서 (적어도 개념적으로는) 수시로 변하는 _visited_ 를 상수로 취급할 수 없기 때문이다. 일반적으로 파이썬에서는 변수는 소문자로, 상수는 대문자로 표현한다.

```python
    if visited == VISITED_ALL:
        return_home_dist = D[last][start] or inf
        ans = min(ans, tmp_dist + return_home_dist)
        return
```

각 방문에서 방문 도시 집합 _visited_ 가 모든 도시를 방문했음을 의미하는 상수 _VISITED\_ALL_ 이면 모든 도시를 방문했기 때문에 최소값을 경신하고 종료한다. 코드 블락의 내용은 유사코드와 정확히 일치한다.


```python
   for city in range(N):
       if visited & (1 << city) == 0 and D[last][city] != 0:
           find_path(start, city, visited | (1 << city), tmp_dist + D[last][city])
```

아직 여행 중이면 방문하지 않은 각 도시를 방문한다. 모든 도시를 다 방문하는 것이 아니라 다음 조건을 만족하는 도시를 선택해야 하는데:

1. **아직 방문하지 않은 도시이며(유사코드의 $$V^\complement$$ 구현),**
1. **마지막 방문 도시와 후보 도시가 이어져 있어야 한다.**

if 문은 두 개의 조건식으로 이를 검증한다. 첫 번째 조건 **`A & (1 << n) != 0`은 A의 n번째 비트가 켜져 있는지 검증하는 식이라고 했다.** 이를 통해 방문 여부를 판단할 수 있다. 두 번째 조건은 원 백준 문제에서 두 도시가 이어져 있지 않으면 거리가 0이라고 명시했기 때문에 그대로 따른다.

주목할 점은 **재귀호출에서 `visited | (1 << city)`로 _visited_ 를 경신하고 있다는 점이다. 이는 OR(`|`) 비트연산자를 이용한 합집합이다.** 직전 포스트에서는 차집합만 구현했는데 비트 합집합은 이렇게 쉽게 만들 수 있다.

```python
    for c in range(N):
        find_path(c, c, 1 << c, 0)
```

마지막으로 각 재귀호출은 시작하는 점화식에 불을 붙인다. 무(無)에서 각 도시를 처음으로 방문해 나간다. 모든 도시가 시작점이 될 수 있기 때문에 다 테스트한다. visited를 `1 << c`로, tmp\_dist를 0으로 설정하는 것만 확인하자.

<br>

완전탐색의 시간복잡도는 어떻게 될까? 이 문제는 N개의 도시를 줄세우고 이때의 길이의 최소값을 찾는 것과 동일하기 때문에 $$O(N!)$$이 된다. 


<br id="4">

## 4. 마치며

---

TSP에 대한 소개와 완전탐색 코드를 살펴봤다. 이 코드는 현실에서는 쓰면 안 된다. $$O(N!)$$ 시간복잡도는 N에 따라 지나치게 크게 증가하기 때문에 완전탐색으로 TSP를 풀면 어지간히 N이 작지 않은 이상 바로 낙방이다. 원 백준 문제에서도 N의 상한이 16밖에 되지 않음에도 완전탐색 풀이는 통과하지 못한다.($$16!$$은 14자리의 수다. 1조 X 10)

**이 완전탐색 풀이는 동적 계획법으로 나아가기 위한 발판 역할이다. 그래서 구현한 풀이는 '만들 수 있는 최고의 완전탐색 풀이'는 아니며, 개선할 수 있는 여지를 남겨놓았다.**

뭘 했다고 이렇게 길어지는지 모르겠다. 수고했다. 나.

이상 포스트를 마칩니다.


<br id="5">

## 5. 자료 출처

---

* [eklitzke: The Traveling Salesman Problem Is Not NP-complete](https://eklitzke.org/the-traveling-salesman-problem-is-not-np-complete){:target="_blank"}
* [Wikipedia: Travelling salesman problem](https://en.wikipedia.org/wiki/Travelling_salesman_problem){:target="_blank"}
* 『알고리즘 문제 해결 전략』11장 조합 탐색, 구종만, 인사이트(insight)
