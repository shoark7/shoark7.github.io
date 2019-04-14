---
layout: post
title: "Get longest palindromes in a string"
date: 2019-04-04
description: "We get longest palindromes with a bad and a good algorithm solution in Python"
img:  /algorithm/longest-palindromes-logo.png
categories: [Programming, Algorithm]
tags: [Palindrome, Dynamic_programming]
---


## 0. Index

> 1. [들어가며](#1)
> 2. [문제 소개](#2)
> 3. [여러 방법들 살펴보기](#3)
>    - 3.1. [Don't reinvent the wheel by yourself](#3a)
>    - 3.2. [단순 반복문](#3b)
>    - 3.3. [재귀함수 사용](#3c)
>    - 3.4. [reduce 함수 사용](#3d)
>    - 3.5. [Meta!! programming](#3e)
> 4. [효율성 극대화: Cache 사용](#4)
> 5. [마치며](#5)
> 6. [자료 출처](#6)


## Prologue

## Problem introduction


## 


```python
def get_longest_palindromes(strng):
    N = len(strng)
    cache = [[None] * N for _ in range(N)]

    def is_palindrome(lo, hi):
        if cache[lo][hi] is not None:
            return cache[lo][hi]

        if lo == hi:
            return True
        elif lo + 1 == hi:
            return strng[lo] == strng[hi]

        ret = False if strng[lo] != strng[hi] else is_palindrome(lo+1, hi-1)
        cache[lo][hi] = ret
        return ret

    def generate_palindromes():
        ret = []
        longest = N
        found = False

        while not found:
            for s in range(N-longest+1):
                if is_palindrome(s, s+longest-1):
                    found = True
                    break

            if not found:
                longest -= 1

        for s in range(N-longest+1):
            if is_palindrome(s, s+longest-1):
                ret.append(strng[s:s+longest])
        return ret

    return [''] if not strng else generate_palindromes()


print(get_longest_palindromes('hannah'))
print(get_longest_palindromes('racecar'))
print(get_longest_palindromes('foobarisreadytogo'))
print(get_longest_palindromes('abcdef'))
print(get_longest_palindromes(''))


['hannah']
['racecar']
['a', 'b', 'c', 'd', 'e', 'f']
['']
```


## Epilogue
