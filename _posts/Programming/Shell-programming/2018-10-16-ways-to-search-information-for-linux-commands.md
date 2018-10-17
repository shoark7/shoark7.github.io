---
layout: post
title: 새로운 리눅스 Shell 커맨드를 만났을 때 대처법
date: 2018-10-16
description: 수없이 많이 접하게 되는 새로운 쉘 커맨드를 빠르게 파악하는 방법을 몇 가지 소개합니다.
img:  /shell-programming/shell-logo.png
categories: [Programming, Shell-programming]
tags: [Python, shell, shell_commands]
---

## 들어가며

---

리눅스든 macOs든 쉘을 자주 사용하다보면 내가 알고 있는 기본적인 커맨드만으로는 세련된 활용이 힘들다는 것을 알게 된다. 또는 쉘 프로그래밍 등을 위해 쉘을 좀더 진지하게 사용하다보니 '세상에 이런 일이'에 나올 법하게 새로운 커맨드를 연신 만나게 될 수도 있다. 리눅스 배포판마다, 또 설치한 패키지마다 달라지기 때문에 공식적인 숫자는 나오지 않았지만 리눅스 쉘에는 상상 이상으로 커맨드가 많다.  

[핵심 쉘 커맨드 9개](https://shoark7.github.io/programming/shell-programming/Top-basic-unix-shell-command.html){:target="_blank"} 편에서도 언급했지만 우리가 유닉스 쉘에 있는 모든 명령어를 다 알 수도 없고 알 필요도 없다. 하지만 때로 정말 중요한 커맨드를 나오면 기본적인 활용법까지 공부하거나 더 깊게 설명 문서까지 읽어볼 필요가 있을 수 있다. 그게 아니더라도 급작스럽게 새 커맨드를 만났을 때 문서까지 읽지는 못하더라도 적어도 이 명령어가 하는 일이 무엇인지 확인하고 싶을 수 있다.  

**그래서 이번 편에서는 새로운 커맨드를 만났을 때의 대처법을 몇 가지 알아보려고 한다.** 리눅스에는 명령에 대한 구체적인 설명 문서를 확인할 수 있는 방법이나 간략하게 용도를 파악하는 방법, 그리고 커맨드의 종류를 확인할 수 있는 방법들이 있는데 이 방법들을 적절하게 활용하면 새로운 커맨드를 만났을 때 쉽게 내 것으로 만들고 사용해볼 수 있다.  

**포스트는 커맨드를 간단하게 용도나 종류만 파악하는 방법과, 자세하게 설명문서를 찾아보는 방법, 이렇게 두 가지 방법을 살펴보도록 하자.**


## 간단히 파악하기

---

이 방법은 새로운 커맨드를 만났을 때 간단하게 그 역할이나 종류를 파악하는 방법이다. 

## whatis

**`whatis`는 이중 가장 간단한 방법으로 프로그램이 하는 기능을 간략히 한 줄로 표현한다.** 가령 내가 _pwd_ 기능이 하는 일을 알고 싶다면 다음과 같이 확인할 수 있다.

```sh
$ whatis pwd

pwd (1)              - print name of current/working directory
```

_pwd_ 가 하는 일은 '현재/작업 디렉토리의 이름을 출력한다'이다. `(1)`과 같이 숫자가 써져 있는데 이 숫자의 의미는 명령어의 종류를 숫자로 표현한 것이다.

---

## type

**`type`은 커맨드의 종류를 출력한다.** 단순히 커맨드가 하는 일뿐 아니라 커맨드의 종류를 확인할 수 있으면 이해가 좀더 빠를 수 있다. 여기서 종류의 의미가 궁금할텐데 우리가 쉘에 입력하는 명령어는 크게 다음과 같이 나뉜다.

\1. shell built-in
  * 쉘이 기본적으로 가지고 있는 함수. 파이썬에서 `print` 함수가 기본 내장되어 있는 것과 비슷하다.

```sh
$type pwd

pwd is a shell builtin
```

\2. 리눅스 프로그램
  * 우리가 접하는 대부분의 명령어는 리눅스 프로그램이다. 우리는 단순히 '명령어를 입력한다'고 생각하지만 실제로는 누군가 개발한 프로그램을 실행하는 것이다.

```sh
$ type lscpu

lscpu is /usr/bin/lscpu
```

* `type`에서 인자가 리눅스 프로그램의 경우 이 프로그램의 위치를 보여준다. 위의 `lscpu`는 컴퓨터의 CPU 정보를 출력해주는 기능이다.


\3. shell scripts
* 쉘 스크립트는 쉽게 말해 쉘 명령어를 모아놓은 파일로 실행가능으로 설정되어 있을 시 실행가능하다. 근데 실행 방법이 일반 명령어를 입력하는 방법과 같기 때문에 쉘 스크립트인지 모를 수 있는데 `type`을 통해 확인 가능하다.

```sh
$ type open-tmux

open-tmux is /home/sunghwanpark/bin/open-tmux
```

`open-tmux`는 개인적으로 사용하는 쉘 스크립트이다. 결국 우리가 하려는 것은 쉘 스크립트를 짜려는 것이니까.


\4. 유저 정의 함수

* 앞서 쉘에서 미리 정의된 빌트인 함수가 있다고 살펴봤다. 반대로 유저가 함수를 정의할 수도 있다.

```sh
$ function hi() { echo hi }
$ hi

hi

$ whatis hi

hi is a shell function
```


<br>

이렇게 명령어의 타입은 크게 네 가지인데 `type`을 통해 그 종류를 확인할 수 있다. 물론, 그 종류가 곧 기능을 말하지는 않는다. 그렇지만 새로운 명령어를 만났을 때 어느 종류에 속하는지를 알면 그 명령의 중요도를 가늠해볼 수는 있다.

---



## apropos

**apropos는 _whatis_ 를 확장한 프로그램으로 입력한 문자열을 포함하는 _whatis_ 출력들을 모두 출력한다.** 아까 `whatis cp`와 같이 입력하면 _cp_ 에 관한 한 줄 짜리 설명문서가 나왔던 것을 확인했다.  **apropos는 모든 프로그램의 설명 중에서 입력받은 문자열이 조금이라도 포함된 프로그램들을 모두 나열한다.** 바로 예를 보자.

리눅스에서 매우 중요한 프로그램 중에는 파일에서 매칭되는 정규표현식 문장을 찾는 `grep`이라는 기능이 있다. 이 기능은 나중에 단독으로 다룰 예정이다.  
내가 _grep_ 과 관련한 다른 프로그램이 뭐가 있는지 알고 싶다고 하자. 이때 `apropos`를 쓰면...

```sh
$ apropos grep

...
fgrep (1)            - print lines matching a pattern
git-grep (1)         - Print lines matching a pattern
grep (1)             - print lines matching a pattern
grepdiff (1)         - show files modified by a diff containing a regex
lzegrep (1)          - search compressed files for a regular expression
lzfgrep (1)          - search compressed files for a regular expression
lzgrep (1)           - search compressed files for a regular expression
msggrep (1)          - pattern matching on message catalog
pgrep (1)            - look up or signal processes based on name and other at...
ptargrep (1)         - Apply pattern matching to the contents of files in a t...
rgrep (1)            - print lines matching a pattern
...
```

**_grep_ 과 관련된 수많은 프로그램들의 `whatis` 문자열이 나온다.** _grep_ 이 얼마나 중요한 기능이면 이를 응용한 정말 많은 프로그램이 있다. **이렇게 `apropos`는 이렇게 관련 기능을 알고 싶거나, 또는 이름이 정확히 기억나지 않을 때 이름의 부분이나 기능과 관련한 문자열을 입력할 때 유용하다.** 이때 매칭되는 부분은 꼭 이름이 아니라 설명 문자열이어도 같이 검색된다.  

참고로 `apropos`는 영어로 '~에 관하여'라는 뜻이라고 한다.

## 구체적인 활용 파악하기 

---

앞서는 명령어를 간단하게 스윽 보는 방법을 살펴보았다. 하지만 중요한 명령어나 어려운 명령어는 간단히 한 번 살펴볼 것이 아니라 사용방법이나 설명서를 한 번은 정독해야 할 때도 있다. 이번 절에서는 명령어를 구체적으로 알아보는 방법을 살펴보자.


### \-\-help

내가 사랑하는 헬핑 방법이다. 앞서 말했듯이 명령어는 그 종류에 상관없이 모두 누군가가 잘 쓰라고 만들어놓은 프로그램이기 때문에 대부분의 경우(개인적인 쉘 함수, 쉘 스크립트 제외) 설명문서를 꼭 가지고 있다. `--help` 옵션은 명령어의 사용방법과 가지고 있는 모든 옵션을 출력한다. 

```sh
$ python --help


usage: python [option] ... [-c cmd | -m mod | file | -] [arg] ...
Options and arguments (and corresponding environment variables):
-b     : issue warnings about str(bytes_instance), str(bytearray_instance)
         and comparing bytes/bytearray with str. (-bb: issue errors)
-B     : don't write .pyc files on import; also PYTHONDONTWRITEBYTECODE=x
-c cmd : program passed in as string (terminates option list)
-d     : debug output from parser; also PYTHONDEBUG=x
-E     : ignore PYTHON* environment variables (such as PYTHONPATH)
-h     : print this help message and exit (also --help)
...
```

우리가 자주 쓰는 파이썬이다. 파이썬도 누군가가 만들어놓은 프로그램이고 자신의 헬프 문서를 가지고 있다.

**항상 강조하고 강조하지만 처음 보는 기능이나 명령에는 꼭 헬핑을 해보자.**


### man


**man은 'manual'의 약자로 명령(프로그램)에 대한 설명문서를 출력한다. 리눅스에서는 명령들에 대해 구체적인 설명을 담은 문서를 온라인으로 유지, 관리하고 있는데 `man`은 그 자체를 출력한다.**  

앞서 살펴본 **_\-\-help_ 는 man 문서 중 프로그램 사용과 관련한 필수적인 내용만 추려서 보여준 것이고, _whatis_ 는 문서의 '이름' 부분만 가져와서 한 줄로 보여준 것이다.**  

`man`은 단순히 사용방법 의외에 버그, 저작권, 프로그램의 종료상태, 유사한 명령 소개 등 명령에 관한 모든 내용을 담고 있다.  

```sh
$ man grep


NAME
       grep, egrep, fgrep, rgrep - print lines matching a pattern

SYNOPSIS
       grep [OPTIONS] PATTERN [FILE...]
       grep [OPTIONS] [-e PATTERN]...  [-f FILE]...  [FILE...]

DESCRIPTION
       grep  searches  the  named input FILEs for lines containing a match to the given PATTERN.  If no files are specified, or if the file “-” is
       given, grep searches standard input.  By default, grep prints the matching lines.
...
```

시간이 날 때 man 문서를 읽으면 도움이 정말 많이 되는데, 그만큼 길고 복잡한 것은 사실이다. 사실 나도 `man` 문서를 보더라도 사용법과 옵션 등만 볼뿐 그 이외의 부분은 보지 않는다. 그래도 헬핑과 _whatis_ 모두 이 `man` 문서의 일부분인만큼 그 원본을 보는 방법을 아는 것도 중요하다고 생각한다.


---

## 마치며

---

리눅스에서 새로운 명령어를 마주쳤을 때 그것을 파악할 수 있는 여러 가지 방법을 알아보았다. 나같은 경우는 여기서 `whatis`와 헬핑을 가장 많이 쓰는 것 같다. 자신에게 맞는 방법을 사용하면 되겠다. 이상!
