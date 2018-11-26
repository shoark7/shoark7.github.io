---
layout: post
title: '조합과 순열 알고리즘, 파이썬으로 구현하기'
date: 2018-11-26
description: 'I implement combination and permutation algorithm in Python'
img:  /algorithm/comb-perm-logo.jpg
categories: [Programming, Algorithm]
tags: [Algorithm, Combination, Permutation]
---

## 들어가며

조합과 순열은 중학생 때인가, 고등학생 때인가 배우는 수학이다. 아마 정상적으로 고등학교까지 학과 과정을 마친 사람이라면 조합과 순열의 기본적인 개념을 숙지하고 있을 것이다. 나도 마찬가지이고, 수학 중에서 확률과 경우의 수를 좋아했기 때문에 수학의 많은 분야 중에서 이 부분은 특히 더 열심히 한 기억이 있다.  

하지만 조합과 순열을 알고리즘으로 구현하는 데는 상당한 애를 먹었고, 난 '이들을 알고리즘으로 구현하고 싶다'는 욕구를 거의 2년간 품고 있었지만 실현시키지 못했다. 여러 블로그도 찾아보고, 파이썬의 내장 알고리즘 코드를 살펴보기도 했지만 그때 내가 이해할 수 있는 수준이 아니었다. 이제야 알고리즘을 제대로 공부하면서 이 둘을 구현할 수 있게 되었고 이번 포스트에서 이를 정리해보도록 한다. **당연히 내가 말한 조합, 순열은 공식으로 구해지는 가지수를 말하는 것이 아니고 조합과 순열의 모든 경우를 구하는 것을 전제로 한다. 그리고 별 생각없이 만들면 놓치기 쉬운 중복 문제를 제거하는 방법을 살펴본다.**


## 순열 만들기

**순열(Permutation)은 서로 다른 _n_ 개의 대상에서 _r_ 개를 뽑아 일렬로 배열한 것을 말하고 그 경우의 수는 $$nPr$$로 표현한다.($$n \geq r$$) 그리고 _n_ 과 _r_ 이 같을 때 순열의 경우의 수는 계승(factorial, $$n!$$)이 된다.** 그리고 순열을 구하는 다음과 같은 공식이 있다.


$$
\begin{align}  \label{x1}
	n P r = \frac{n!}{(n-r)!} (단, 0 \le r \le n) && \cdots && 1
\end{align}
$$

**우리는 코드로 리스트와 같은 어떤 순회할 수 있는 _Iterable_ 자료형과 선택할 개수 _r_ 이 들어왔을 때 각 순열을 출력하는 알고리즘을 구현하자.**


```python
def permutation(arr, r):
    # 1.
    arr = sorted(arr)
    used = [0 for _ in range(len(arr))]

    def generate(chosen, used):
        # 2.
        if len(chosen) == r:
            print(chosen)
            return
	
	# 3.
        for i in range(len(arr)):
            if not used[i]:
                chosen.append(arr[i])
                used[i] = 1
                generate(chosen, used)
                used[i] = 0
                chosen.pop()
    generate([], used)


>>> permutation('AABC', 2)
>>> combination([1, 2, 3, 4, 5], 3)

```

순열을 만드는 코드다. 그렇게 날 괴롭혔던 코드가 작성하는 데 20줄도 채 필요하지 않다는 것이 참 우습다. 

1. 먼저 사용자가 원하는 _arr_ 과 _r_ 을 받는다. 그리고 _arr_ 을 오름차순 정렬하는데 여기서는 큰 의미가 있지는 않고 단순히 출력을 이쁘게 하기 위해서이다. 그리고 **_used_ 변수를 만드는데, 이 변수는 _i_ 번째 값을 썼는지 저장하는 데 쓰인다.** 우리는 모든 순열을 하나씩 만들고 출력했는데 당연히 중복값은 저장되어서는 안 된다. 
2. 실제 순열을 만들 _generate_ 함수를 생성한다. 먼저 **_chosen_ 변수는 순열이 저장되는 변수인데 이 배열에 값을 하나씩 추가하다가 그 개수가 _r_ 이 되는 순간 하나의 순열이 만들어진 것이므로 출력 후 반환한다.**
3. 이 함수의 핵심이다. 모든 순열은 _arr_ 의 0부터 _i-1_ 번째 값으로 시작하기에 _for_ 문으로 다 만들어야 한다.  그리고 **_chosen_ 에 값 추가 후, _used_ 에 해당 변수를 사용했다고 체크한다. 그 다음 다시 _generate_ 를 반복한다. 하나가 만들어진 후에는 그 값을 uncheck해줘야 한다.**


두 예제는 모두 잘 작동한다.



## 조합 만들기

순열과 달리, 조합(Combination)은 같은 _n_ 개 중에 _r_ 를 뽑되, 순서를 고려하지 않는다. _n_ 개 중에 _r_ 를 뽑는 조합의 경우의 수는 다음과 같다.


$$
\begin{align}  \label{x2}
	\binom{n}{r} = n C r = \frac{n!}{(n-r)!r!} (단, 0 \le r \le n) && \cdots && 2
\end{align}
$$


이제 이를 코드로 구현해보자.


```python
def combination(arr, r):
    # 1.
    arr = sorted(arr)

    # 2.
    def generate(chosen):
        if len(chosen) == r:
            print(chosen)
            return

    	# 3.
        start = arr.index(chosen[-1]) + 1 if chosen else 0
        for nxt in range(start, len(arr)):
            chosen.append(arr[nxt])
            generate(chosen)
            chosen.pop()
    generate([])


>>> combination('ABCDE', 2)
>>> combination([1, 2, 3, 4, 5], 3)
```

1. 입력은 순열 때와 같다. 배열도 마찬가지로 정렬한다.
2. 조합을 만드는 _generate_ 함수를 만든다. 순열과 마찬가지로 _chosen_ 에 저장된 아이템 개수가 _r_ 개이면 조합이 하나 완성된 것이기 때문에 값을 출력하고 함수를 종료시킨다.
3. _for_ 문을 돌리되, 시작을 _chosen_ 에 저장된 마지막 값 다음으로 정한다. 이는 아까 순열함수와 대비되는 부분으로, 조합은 순열과 달리 순서를 고려하지 않고 뽑기 때문에, 가짓수를 제한해줘야 한다. _start_ 가 _chosen_ 이 비어있을 경우 0이 되는 것도 참고한다. 빈값일 때는 그냥 0을 넣어야 한다.

이것도 잘 작동한다.


## 놓치기 쉬운 중복 문제

우리가 만든 순열, 조합함수는 일단 잘 작동한다. 근데 아직 한 가지 문제가 있으니, 순열 함수에서 입력을 다음과 같이 줘보자.

```python
>>> permutation('AABC', 2)


['A', 'A']
['A', 'B']
['A', 'C']
['A', 'A']
['A', 'B']
['A', 'C']
['B', 'A']
['B', 'A']
['B', 'C']
['C', 'A']
['C', 'A']
['C', 'B']
...
```

뭔가 이상한 점을 느낄 수 있겠는가? 그렇다. 값이 중복되고 있다. 그 이유는 입력의 원소들이 중복되기 때문이다. 이 예제에서는 'A'가 2개로 중복되고 있다.

이때는 어떻게 해야 할까? **중복되는 원소에 등장하는 순서를 정하는 것이 답이다.** 예제에서 'A'가 두 개면, 'A'에 보이지 않는 0, 1의 인덱스를 줘서 순서를 지켜서 등장하게 하면 중복이 나오지 않는다. 순열 함수에 이를 적용해보면 다음과 같다.

```python
def permutation(arr, r):
    # 1.
    arr = sorted(arr)
    used = [0 for _ in range(len(arr))]

    def generate(chosen, used):
        # 2.
        if len(chosen) == r:
            print(chosen)
            return
	
        for i in range(len(arr)):
	    # 3.
            if not used[i] and (i == 0 or arr[i-1] != arr[i] or used[i-1]):
                chosen.append(arr[i])
                used[i] = 1
                generate(chosen, used)
                used[i] = 0
                chosen.pop()
    generate([], used)


>>> permutation('AABC', 2)


['A', 'B']
['A', 'C']
['B', 'A']
['B', 'C']
['C', 'A']
['C', 'B']
```

3번은 살펴보자. 어떤 원소에 대해 그 원소가 등장할 순서일 때는 다음과 같은 조건을 만족하면 된다.

1. _i_ 가 0일 때:
  _i_ 가 0이면 맨 처음이기 때문에 그냥 바로 쓰면 된다.
2. _arr[i-1] != arr[i]_ 일 때:
  **지금은 _arr_ 이 정렬되어 있다.** 이때 _i_ 번째 원소가 _i-1_ 번째와 다르면 그냥 'B', 'C' 처럼 서로 다른 원소이기 때문에 바로 쓴다.
3. _used[i-1]_ 일 때:
  가령 두 번째 'A'이면, 첫 번째 'A'가 사용된 상태여야만 쓸 수 있다. 그래서 전 단계가 쓰인 상태인지 확인한다.

이렇게 하면 순열일 때 중복을 피할 수 있다.

<br>

조합일 때도 같은 코드를 만들어준다.

```python
def combination(arr, r):
    # 1.
    arr = sorted(arr)
    used = [0 for _ in range(len(arr))]

    # 2.
    def generate(chosen):
        if len(chosen) == r:
            print(chosen)
            return

    	# 3.
        start = arr.index(chosen[-1]) + 1 if chosen else 0
        for nxt in range(start, len(arr)):
            if used[nxt] == 0 and (nxt == 0 or arr[nxt-1] != arr[nxt] or used[nxt-1]):
                chosen.append(arr[nxt])
                used[nxt] = 1
                generate(chosen)
                chosen.pop()
                used[nxt] = 0
    generate([])


>>> combination('ABCDE', 2)
>>> combination([1, 2, 3, 4, 5], 3)
```


이상 조합, 순열 알고리즘 포스트를 마친다.
