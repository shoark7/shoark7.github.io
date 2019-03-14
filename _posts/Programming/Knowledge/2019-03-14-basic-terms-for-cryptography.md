---
layout: post
title: '[암호학] 암호학의 기본 용어 정리'
date: 2019-03-14
description: 'Hash, Message digest 등 암호학을 배울 때 마주치는 필수적인 단어들에 대해 공부하고 익숙해집시다.'
img:  /knowledge/cryptography-algorithms-logo.jpg
categories: [Programming, Knowledge]
tags: [Cryptography]
---

### 0. 목차

> 1. [들어가며](#1)
> 2. [용어 정리](#2)
>    - 2.1. [Cryptography, Cryptology](#2a)
>    - 2.2. [Encryption과 Decryption](#2b)
>    - 2.3. [Message Digest](#2c)
>    - 2.4. [Hash funcion](#2d)
>    - 2.5. [Break](#2e)
>    - 2.6. [Collision attack](#2f)
> 3. [마치며](#3)
> 4. [자료 출처](#4)


<br id="1">

## 1. 들어가며

---

옛날에 청산학원을 다닐 때 '\*용규'라는 성함의 수학 선생님이 있었는데 수업도 재미있고 아이들에게 살갑게 대하셔서인지 인기가 많았다. 나도 엄청 친하게 지내지는 않았지만 호감은 가지고 있었는데 정겨운 욕을 참 잘하셨던 걸로 기억한다.  

10년도 더 전에 본 사람이라 잘 기억은 안 나는데 그분이 수업 중 하신 이 말씀을 나는 기억하고 있다. '암호학 나중에 공부해봐. 재밌어.' 어떤 맥락에서 하신 말씀이신지는 모르겠는데 자신이 대학생 때 암호학 수업을 들었고 재밌었다는 말씀을 하신 것은 분명하다.  

오늘은 원래 주요 암호화 방식인 MD5, AES256, SHA256의 알고리즘을 공부하고 비교해보려고 했다. 하지만 냉정하게 말해서 이 암호화 방식들의 알고리즘들이 잘 이해가 안 가고, 당장 내일 발표하기에 양질의 컨텐츠가 나올 것 같지 않았다. 그 알고리즘의 역사, 사용처 등도 정리할 수 있지만 그 알맹이인 알고리즘이 빠지면 그게 무슨 의미인가 싶어 자괴감이 든다. 무엇보다도, 애초에 난 hash, digest 등이 뭔지도 모른다는 사실도 알게 됐다.  

따라서 **오늘은 암호화 방식에 대한 문서를 읽으면 숨쉬듯 출현하는 기본 용어들에 대해 정리를 하자.** 카이사르 암호화의 수준을 넘어가는 암호화 방식은 추후 단계적으로 공부해야 할 것 같다.


<br id="2">


## 2. 용어 정리

---

정리할 기본 용어는 내가 관련 문서에서 많이 봤거나, 중요하다고 생각하거나, 개인적으로 흥미가 가는 용어들을 정리하도록 하겠다.

<br id="2a">

### 2.1. Cryptography, Cryptology

**`Cryptography`는 '암호화 방식', '암호화 기법'을 의미하고, `Cryptology`는 Cryptography를 연구하는 학문, 다시 말해 '암호학'을 의미한다.**

예를 들어, SHA256은 유명한 Cryptography이고, 용규 샘이 수업을 들으셨던 과목은 Cryptology가 된다.

참고로, 두 용어가 공유하는 'Crypt'의 어원은 라틴어 'Crypta'라고 하며 무언가를 숨기는 '금고', 겉으로 드러나지 않는 '지하 납골당'(vault)을 의미한다고 한다.

---


<br id="2b">

### 2.2. Encryption과 Decryption

**`Encryption`은 '암호화'라고 하며 암호화의 대상이 되는 평문(plain text)을 추가적인 정보(예를 들어 해독 방법, _key_ 라고도 한다)이 없으면 사람이 이해할 수 없는 '암호'로 변환하는 작업을 의미한다.** 생성된 암호는 영어로 '**cipher**'라고 한다.

**`Decryption`은 그 반대의 작업으로 '암호 해독', '복호화'로 해석되며 주어진 암호를 _key_ 를 이용해 원래의 메시지로 변환하는 작업을 의미한다.** 

<br>

이때 질문. **Cryptography와 Encryption의 차이는 무엇일까?** 그냥 서로가 비슷해보인다.  

**Cryptography는 암호화 방식으로 암호화, 복호화를 포함하는 개별적인 암호화 원리를 구분한다.** 예를 들어 카이사르 암호화, SHA256, MD5 등은 서로 개별적인 Cryptography가 된다.  반면, **Encryption은 원래의 평문을 암호화하는 작업 자체를 의미한다.** 우리는 어떤 텍스트를 특정 Cryptography(가령 MD5)로 encrypt할 수 있고 다른 암호를 특정 Cryptography(가령 SHA256)으로 decrypt할 수 있다.

---


<br id="2c">

### 2.3. Message Digest

위의 두 절에서 다루는 용어들은 단순히 영어사전에서 찾아보면 알 수 있는 내용들이다. 그러니까 단순히 상식적인 가치를 갖는 용어라면 **이제부터는 '암호학'에서만 통용될 수 있는 용어들을 다룬다.** 뭐랄까, 암호학자들의 은어같은 느낌이 든다. 그래서 정말로 그 의미를 몰랐다.

<br>

`Message digest`, 해석하면 '메시지 소화'. 이 용어는 직역하면 이해가 잘 가지 않기 때문에 각 용어를 분리해서 이해하자.

* Message: **암호학에서 'Message'는 암호화할 원래의 평문을 의미한다.**
  - 메시지는 그 길이가 다양(variable)할 수 있다. 로이 필딩의 REST에 대한 논문과 내 'a'라는 심오한 한 글자는 길이가 달라도 모두 암호화될 수 있는 message이다.
* Digest: **'Digest'는 암호화나, 암호화된 메시지 자체를 의미한다.**
  - 왜 이 의미를 'digest', 즉 '소화하다'라는 뜻의 용어를 써서 표현했을까? 그것에 해당하는 내 뇌피셜은 다음 절인 'hash'에서 살펴본다.


<br>

그러면 이 둘을 합친 'Message digest'는 무슨 의미일까? 이 단어를 뜻하는 단 하나의 명확한 정의는 없고 다음과 같은 의미로 일반적으로 쓰인다고 한다.

1. 메시지의 내용을 hash 함수로 암호화한 고정된 길이의 표현(hash, 또는 암호) 자체.
1. 또는 그 암호를 만들어내는 **암호화 hash 함수(cryptographic hash function)**
  - 이때 'message digest'는 cryptography와 비슷한 의미로 쓰인다.


---


<br id="2d">

### 2.4. Hash funcion


Hash(이하 '해시')는 프로그래밍을 하면서 알게 모르게 많이 들어왔다. 하지만 '무슨 값을 암호로 바꾸는 것' 정도로만 이해하고 있었는데 이번에 제대로 고민해보게 됐다.  

**해시는 임의의 길이의 데이터를 고정된 길이의 다른 데이터로 매핑해주는 함수나, 그 결과 반환된 값을 의미한다.** 해시 함수는 암호화 이외에도 랜덤화, 네트워크로 전송된 파일의 완결성 유무를 검사하는 체크섬(checksum) 등의 다양한 분야에서 활용된다.  

그 유용성 때문인지 파이썬에서는 _hash_ 라는 간단한 해시 함수를 기본 내장하고 있다.

```python
# Version info: 3.6.3

>>> hash('a')

-1100551441063333505
```

이 함수는 나도 이 포스트를 준비하면서 처음 알았는데 기본적 작업보다는 고급 프로그래밍에서 사용될 것 같다.  

<br>

이제 암호학에 한정해서 해시를 설명하자. **_암호학에서 사용되는 해시 함수_** 는 다음과 같은 조건들을 만족해야 한다.

* **해시 함수는 반드시 단방향이어야 한다.**
  - 암호는 인간에게 중요한 정보를 숨기기 위해 사용한다. 원 메시지는 공개되면 안 되지만 향후 키를 알고 있는 내집단은 복호화할 수 있어야 하기 때문에 암호는 공개되는 경우가 많다. 이때 해시 함수가 양방향이라면 암호를 통해서도 원 메시지를 해독할 수 있다는 의미가 되기 때문에 암호로서 의미가 없다. 따라서 **해시 함수는 비대칭적(asymmetric)이어야 한다.**
* **같은 암호(digest)를 갖는 서로 다른 메시지를 찾는 것이 전산학적으로 실행불가능해야 한다.(computationally infeasible)**
  - 만약 두 가지 이상의 서로 다른 메시지가 같은 암호를 갖는다면 이는 암호를 해독했을 때 두 가지 이상의 서로 다른 의미로 해석될 수 있다는 뜻이 된다. 당연히 이는 바람직하지 않다.
  - 이때 왜 `전산학적으로 실행불가능`이라는 단서가 붙었을까? 뒤집어서, 같은 암호값을 갖는 서로 다른 메시지를 찾는 방법이 뭐가 있을까? 가장 무식하고 확실한 방법은 **가능한 모든 메시지를 해시로 만들어서 이중 해시가 일치하는 메시지들을 찾는 것이다.(Bruce force)** 어떤 암호화 알고리즘이든 이는 시도할 수는 있다. 하지만 전산학적으로 불가능하다. 유명한 암호화 방식은 SHA256은 256 비트의 길이를 갖는 digest를 반환하는데 이때 이 digest가 가질 수 있는 상태의 경우의 수는 $$2^{256}$$, 무려 78자리의 수다. 단순히 확률론적으로도 서로 다른 메시지가 같은 digest를 가지기는 매우 어렵고 컴퓨터로 계산하기도 어렵다.

이 두 조건을 만족하는 해시만이 **_암호학에서_** 말하는 해시 함수나 해시값을 의미한다.


<br>

근데 해시에 대해 나를 괴롭혔던 문제는 이게 아니다. **왜 단어를 요리의 한 종류인 'hash'라고 이름 붙였을까?** 해시는 영국 음식으로 우리나라에서 많이 먹는 음식은 아니지만 롯데리아의 '해시 브라운'을 먹어본 사람들은 이 고민에 공감할 것이다. 그에 대한 나의 추측은 다음과 같다.

![hash brown](/assets/img/knowledge/cryptography-algorithms-hash-brown.jpeg)

사전적으로 해시는 '요리'다. 해시는 '**잘게 썬** 고기, 다진 고기, 감자와 향신료를 **섞은 후** 단독으로 또는 양파와 같은 다른 재료를 섞어 **열에 익힌** 요리'라고 한다. 내가 하이라이트한 부분에 주목하기 바란다.

**요리의 Recipe의 특징은 보통 Recipe 대로 만든 요리는 이전의 재료 상태로 돌아갈 수 없다.(즉, 비가역적, 단방향적이다)** 이는 왠만한 요리에 해당하는 특징이다. 어제 케이크를 먹었는데 그 케이크를 원재료로 되돌릴 수 있을까? 당연히 아니다.  

**해시 요리 또한 재료를  '잘게 썰고', '섞어' 물리적으로 변형을 가해 재료로 돌아가기 어렵게 했으며, 이를 열에 익힘으로써 화학적 변형을 가해서 물리적 변형에 잠시나마 남아 있던 가역성의 여지를 완전히 없애버렸다.** 이것이 암호학에서 말하는 해시 함수의 특성과 일치한다. **해시를 통해 메시지(원재료. 소고기, 감자, 향신료 등)를 digest(요리, 여기서는 해시)로 변형시킬 수 있지만 그 반대는 안 된다.**  

해시라는 작명을 이렇게 이해한다면 encrypt된 암호를 'Digest'라고 부르는 것도 이해는 할 수 있다. 인간이 먹은 음식을 소화된 이후에 대소변으로 변형은 할 수 있어도(우리는 지금도 하고 있다), 이 대소변을 다시 먹고 싶은 요리로 변환할 수는 없으니까.  

이상이 내가 생각한 해시라는 작명의 이유이다.

---


<br id="2e">

### 2.5. Break

'Break'은 암호를 깨는 것을 말한다. Cryptography에 대한 추가 정보 없이(즉, _key_ 없이) 암호(cipher)를 통해 원문(message)를 빼내는 것이다. 

**이때 암호학적인 의미에서의 'Break'은 Brute force 공격보다 빠른 것만을 대상으로 한다.** 앞서 살펴봤듯이 모든 암호화 방식에 대해 brute force 공격은 시도는 해볼 수 있다. 하지만 Brute force 공격은 전산학적으로 실행불가능한 해시 함수를 사용하는 암호화 방식에는 의미가 없다. **만약 Brute force보다 더 나은 시간복잡도를 갖는 decrypt 방법을 찾는다면 이는 암호를 깬 것이 된다.(break)**

---


<br id="2f">

### 2.6. Collision attack

개별 Cryptography 위키피디아 문서에서 많이 발견되어 추가했다.  

**`Collision attack`은 같은 해시를 갖는 두 개의 입력(메시지)을 찾는 공격이다.**  

이는 'preimage attack'과는 대조되는 공격으로 이 공격은 특정 타겟 해시에서 메시지를 찾는 공격이라고 한다.

---

	



<br id="3">

## 3. 마치며

---

암호학의 기본 용어에 대한 정리를 마쳤다. 개인적으로 hash와 message digest에 대해 개념을 잡은 것이 매우 만족스럽다. 이제는 더 이상 해시라는 말에 막연한 무감각을 느끼지 않을 것 같다.  

하지만 아쉬움도 분명 있다. 내가 관련 지식이 너무 없어 이 이상의 공부를 하지 못했고 내용도 풍부하게, 더 알차게 구성 못했다는 느낌이 들기도 한다. 애초에 꿈이 너무 원대했었나? 내 지식의 한계를 알고 인정하는 자세를 가져야겠다.

이상 포스트를 마칩니다.


<br id="4">

## 4. 자료 출처

---

* [IBM: What is 'message digest'?](https://www.ibm.com/support/knowledgecenter/en/SSFKSJ_7.1.0/com.ibm.mq.doc/sy10510_.htm){:target="_blank"}
* [Python dictionary implementation](https://www.laurentluce.com/posts/python-dictionary-implementation/){:target="_blank"}
* [Python's _hash_ builtin functions](https://www.bogotobogo.com/python/python_hash_tables_hashing_dictionary_associated_arrays.php){:target="_blank"}
* [Quora: What-are-the-major-differences-of-cryptography-and-encryption](https://www.quora.com/What-are-the-major-differences-of-cryptography-and-encryption){:target="_blank"}
* [Wikipedia: Collision attack](https://en.wikipedia.org/wiki/Collision_attack){:target="_blank"}
* [Wikipedia: hash function](https://en.wikipedia.org/wiki/Hash_function){:target="_blank"}
* [Wikipedia: 해시(음식)](https://ko.wikipedia.org/wiki/%ED%95%B4%EC%8B%9C_(%EC%9D%8C%EC%8B%9D)){:target="_blank"}
* [wordhippo: meaning of 'crypta' in Latin](https://www.wordhippo.com/what-is/the-meaning-of/latin-word-3d123f3b16e94bf56e17a93d316b9d8bd708f16b.html){:target="_blank"}
