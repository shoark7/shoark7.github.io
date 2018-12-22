---
layout: post
title: "최대 연속 부분수열 합을 구하는 4가지 알고리즘"
date: 2018-12-22
description: "I introduce 4 algorithms to get consecutive sum of subarrays in an array"
img:  /algorithm/rotate-array-logo.png
categories: [Programming, Algorithm]
tags: [Algorithm, Max_slice_sum, Max_consecutive_sum]
---

## 1. 들어가며

---

## 2. 문제 소개

---

## 3. 알고리즘 소개

---


### 3.1. 완전탐색

```python
MIN = -2 ** 32 - 1


def max_consecutive_sum(arr):
    N = len(arr)

    def find(now, until_now):
        if now == N:
            return MIN

        ans = max(arr[now],
                  until_now + arr[now],
                  find(now + 1, arr[now]),
                  find(now + 1, until_now + arr[now]))
        return ans

    return find(0, 0)
```



---

### 3.2. 누적합 수열

```
def cumulative(arr):
    arr = [0] + arr
    N = len(arr)
    p_sum = [0] * N
    ans = MIN

    for i in range(1, N):
        p_sum[i] = p_sum[i-1] + arr[i]

    for hi in range(1, N):
        for lo in range(1, hi+1):
            ans = max(ans, p_sum[hi] - p_sum[lo-1])

    return ans
```


---

### 3.3. 분할정복


---

### 3.4. 동적 계획법




## 마치며

---

