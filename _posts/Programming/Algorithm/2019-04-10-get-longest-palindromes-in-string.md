---
layout: post
title: "[Python] Get longest palindromes in string"
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

---

This is my second post written totally in English. Well, this post was one of my must-do items but I couldn't make it because I was too lazy. If you're intested in algorithm, this subject would be attractive, and maybe a piece of cake to you. Today's post is about `palindrome`. Palindrome is the very famous, easy-to-introduce algorithm for newbies in computer science or any computer languages. But often, it just focuses on telling whether the given string is a palindrome or not. It's also interesting but we want more, right? So, **today's post is about 'getting a list of longest palindromes in a string'. A string can be any sizes long and we have to find all longest palindromes.**

I think you wouldn't know my focus on posts on algorithms because they're all written in Korean. I try to introduce various algorithms on a single problem and try to divide the original problem into subproblems and assemble them to solve the original one. This kind of behavior is really important for other cases and this kind of view is my pride on my posts on algorithms.  

So, I'll solve the problem in 2 ways today: One way is really simple, codes are short and I didn't put my attention too much because question itself is not that difficult actually. But, codes only written in hands are always not good. We'll see what's and why's wrong in first solution. And in 2nd solution, we'll divide it and solve it continously and assemble them. While doing so, we'll use dynamic programming and improve time complexity of the algorithm. Also, you'll get to know this way is much more beautiful and healthy for maintenance, reusabilly and for your mental health.

OK, I was too talkative. Let's move on and dive into algorithm.


## Problem introduction

---

**Today's post is about 'getting a list of longest palindromes in a string'. Palindrome is a sequence of characters which reads the same backward as forward, such as '_hannah_', '_racecar_', '_기러기_'.** If you've studied programming anyhow, I think you might have come across this word or problem related to this. Even if not, it's okay cause problem is easy and intuitive. We feel comfortable within 2-dimensional areas.  

And we're given a string. It can be any string and you have to return a list. Here's an example.

![Example of a get longest palindrome](/assets/img/algorithm/longest-palindromes.png)

Somebody emphasizes importance of levelness of the ground for multi-pulpose radars. His words are given as a string. And **we have a function named '_get\_longest\_palindromes_' and this function returns longest palindromes.** This sentence have two longest palindromes and they're 'level' and 'radar'. They're both 5 words long. So the returned list has two items inside.  

And **if a string has no palindromes(like 'abc'), it returns a list of all characters(['a', 'b', 'c']) cause a character of one length is a palindrome technically. If an empty string('') is given, we return a list of an empty string([\'\']).**


## Way 1. Implement it simple way

---

Actually, palindrome is an one of easy examples of many brain-\*ucking problems related to string and we can solve it without any sort of deep thinking or taking notes. With definition, we can know that length of longest palindromes is between 0(inclusive) and length of the original string(inclusive). If so, **how about iterating N to 0(not 0 to N) and test all substrings in a string if they're palindromes. If any substring matches, we can iterate until that candidate length and finish the loop cause we don't need short palindromes in this problem.**  

I just created the simple version of '_get\_longest\_palindromes_' function. It's only 2 _for_ loop deep and codes are short too.

```python
def get_longest_palindromes(strng):
    N = len(strng)
    ans = []

    for l in range(N, 0, -1):	# 1.
        found = False
        for s in range(N-l+1):	# 2.
            target = strng[s:s+l]
	    if target == target[::-1]:	# 3.
                ans.append(strng[s:s+l])
                found = True
        if found:
            break

    return ans if strng else ['']	# 4.
```

Here're some comments on codes section 1, 2, 3.

1. **We first iterate on possible longest length in [N, 1]** 
  - We don't need to check 0 because shortest palindromes are one length long if not string is empty.
  - And we define _found_ variable to check if we found palindromes in that candidate length. At every end of first loop, we'll check if _found_ is changed and end the loop if longest palindromes are found and saved.
2. **Check every substring of length _l_ if it is a palindrome**
  - Look at the length of iteration of 2nd loop. It's $$N-l+1$$, not $$N-l$$. It may seem confusing but simple. If $$l == N$$, we have to iterate only once. But if we don't add 1 in iteration count, no iteration is executed.(_N-N_ is 0 and _range(0)_ is not executed) So we have to add 1. To be honest, I was really confused at first.
3. **Direct codes of checking a substring is a palindrome**
  - With length variable(_l_) and start location of a substring(_s_) we can retrieve a target substring. And now what's left is checking it. There can be a lot of ways to know but we use a very easy and intuitive way. **_Just compare the substring to backwards string._**  We used a Python trick to reverse a Sequence backwards. **_Using -1 stride_**
  - **If we found palindromes, we add in the _ans_ variable and toggle _found_ variable to _True_**
4. After all iterations, we return the _ans_. But We didn't consider a case of an empty string. If so return [\'\'] or return _ans_ otherwise.


<br>

How do you think of this codes? Well, **I can solve it in this way but I won't recommend this kind of algorithms and approach to the original problem.** I train myself to be negative on this kind of approach actually. This codes don't imply any philosophy. 

Next algorithm is way more appropriate for this purpose. It needs more time and energy, insight on the question but I assure you that you will be more satisfied with algorithm.












## Way 2. A more elegant way

### Open your eyes: 'Way 1' is not our role model

#### Easy one first: define subproblem

#### Need for more efficient program


### Code review

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

        ans = False if strng[lo] != strng[hi] else is_palindrome(lo+1, hi-1)
        cache[lo][hi] = ans
        return ans

    def generate_palindromes():
        ret = []
        longest = N
        found = False

        if not strng:
            return ['']

        for l in range(N, 0, -1):
            found = False
            for s in range(N-l+1):
                if is_palindrome(s, s+l-1):
                    found = True
                    ret.append(strng[s:s+l])
            if found:
                break
        return ret

    return generate_palindromes()


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

---



## Data source

---

* [Wikipedia: Palindrome](https://en.wikipedia.org/wiki/Palindrome)
