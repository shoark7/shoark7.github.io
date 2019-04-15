---
layout: post
title: "[Python] Useful tips when importing modules in Python"
date: 2019-04-10
description: "Let's take a more closer look at what happens when we import modules in Python."
img:  /python/import-logo.png
categories: [Programming, Python]
tags: [import]
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


<br id="1">

## 1. Prologue

---

We use Python and we surely **import** other modules everyday. Importing other modules is so common that usually we don't pay much attention to it. I wasn't that interested in this topic too. But I bumped into situations that I needed to know more about 'import' and 'modules'. Below are some issues I encountered while using Python.

1. Python's _math_ module has many useful mathematical functions. But sometimes theirs wouldn't match your needs. **What should we do when we want to define our own mathematical functions and make our 'math' module? When we run _import math_, what shall be imported, Python's or ours?**
2. Sometimes we may need a higher rank set of modules and it's called **package** in Python. Package is a bundle of relevant modules and is also a module itself. In this case, **we need to carefully consider absolute import and relative import.** This can be tricky.

**Today's post focuses on issue No.1.** Issue No.2 is a huge area and I'll post it later with my personal experience of constructing a package.

So today,  
1. **I'll look through basic usage of _import_ statement. It's a way of reusing code in Python.**
2. **And I'll introduce some interesting tricks on _import_. For example, I'll answer 'can we name our modules without `.py` suffix', 'can we use characters besides english for modules? And how about punctuation characters?'**
3. **At last, I'll cover module import order in Python and how to register our own modules in Python.**

I assume readers have 'shell' programs in their systems.

Let's go guys :)

<br id="2">

## 2. Way of loading and using other modules: _import_

---

**Code reusability** is really import in programming languages and other high-level languages contain many useful others' code in the name of library or STL. Some boring routines are essential in almost any projects, but it can be hell if we have to implement not creative, boresome jobs everytime.   

**Python supports others' code in the name of 'module'.** Python has long maintained '**_batteries included_**' philosophy, meaning Python supports many versatile and rich standard libraries. In fact, there're so many standard libraries that people don't know: _ipaddress_, _pickle_, _shutil_, _pprint_, _smtp_, ... I cannot even mention them all because it really has a lot. With these modules you don't need to repeat boring codes but use Python's efficient and ready-made codes. This is why we python lovers say '_Life is short, use Python_'. You can put your energy into what is most creative and interesting to you.

<br>

To load a module, you use '_import_' statement.

```python
import math
import numpy

import os, sys
```

This is very basic use of '_import_' statement. Codes above imported _math_, _numpy_, _os_, _sys_ modules. They're all important and famous in Python.

**Sometimes you don't need all module functions but only need one single part.** Then you can import only a small part of modules with _from ... import ..._ statement

```python
from sys import getrecursionlimit

getrecursionlimit()

3000
```

As we know, **_sys_ modules controls Python interpreter environments.** And I only wanted to check function call recursion limit in my ipython environment. So I didn't import _sys_ a whole but only imported _getrecursionlimit_ from it. And we can see my ipython has recursion upper limit of 3000.

<br>

You can separate module's attributes from module's name.


```python
from math import *

print(pi)
print(log2(4))
print(log10(1000))

3.141592653589793
2.0
3.0
```

In regular expression, `*` means a single character and it covers **all** ranges of unicode characters. In Python module importing, it has a similar meaning. **Importing with `*` from a module can import all attributes(functions, constants) of that module.** Above shows that example. **I imported all attributes from _math_ module using `*` and I could use _pi_, _log2_ and _log10_ which are constants and functions of _math_ module without 'math.' prefix.**

**This can be used but not recommended.** Here are some reasons:

1. **It adds too many attributes to global namespace.** Global namespace should be maintained and controlled carefully. But asterisk importing spoils namespace hierarchy and flattens all names.
2. **Code review can be harder with `*` import.** In most cases, we import less than 5 attributes from a module even though a module can hold a bunch of functions. **If you specify names of what you use, code reviewers get to know the intention of importing the module.** But the above example literally imports all so you cannot guess what I would do. 
 
<br>

These are very basic examples of importing modules in Python. I'm sure you all know these. Now let's dive into deeper parts of import.


<br id="3">

## 3. Some hidden features of 'import'

---

Chapter 2. covers simple import examples. And those used Python standard libraries like _math_, _os_ and _sys_. **Now, let_s assume when we make our own modules and import them in other projects.** It's different from just using standard modules. These can bring some issues about module names. **Let's check it out some hidden features for our customized-named modules.**


<br id="3a">

### 3.1. Using other characters besides english for modules

As the title itself says, **can we use another characters like Korean, Japanese and punctuation chars for module names?** Built-in and Python standard modules' names are all in english like _math_, _os_, _sys_. But... Not all people's mother tounge is English and I'm also a Korean. **For usability, it's more recommended to use english but sometimes, we might want to use other languages to name our modules.** And Python supports it.

```sh
$ echo "print('hi')" > 안녕.py


$ python 안녕.py

hi
```

I created the module printing 'hi'. '안녕' means 'hi' in Korean and I created the module printing 'hi' to module users. And this module is perfectly OK and executable as you see even though name is not in english characters. Actually, you can use non-english characters when assigning variables. It's basic but some people don't know.

<br>

Ok. We just checked we can use other languages for our module names. But how about punctuations? **Can we use punctuations for module names?**


```python
from string import punctuation

print(punctuation)


!"#$%&'()*+,-./:;<=>?@[\]^_`{|}~
```

There are over 30 punctuation characters supported in Python. But how about these characters? We use punctuation chars often for file names in daily lives, right? Is it OK in Python modules?


```sh
$ echo "print('hi')" > greetings-to-you.py
$ python greetings-to-you.py

hi
```

**We made a greeting module above and named it again using `-` punctuation chars.** Well, we could execute the module even though it contains punctuation characters. But the problem happens when we import the module inside other scripts.


```python
# A new module importing 'greetings-to-you'

import greetings-to-you

def foo(bar):
    eggs()


## !!! A SyntaxError is raised !!!
    import greetings-to-you
                    ^
SyntaxError: invalid syntax
```

Jesus, what's wrong? A _SyntaxError_ is raised. Why? It's related to **Python variable naming rules.**  

While using Python, I think you could have seen many underscore(`_`) characters in variable names. But I'm sure you would (almost) never have seen other punctuation characters.  

In Python, **you can't use punctuation characters for variable names except for underscores('\_').** That's why you cannot import modules using other punctuation characters in Python script with _import_ statement.

<br>

It's too sad because we can use any chars for files in Windows and Xnix. But don't be frustrated. There's a detour to use punctuation chars for module names.  

**The way is to use *\_\_import\_\_* built-in function to import a module.**

```python
# In Python script,

# instead of 'import greetings-to-you',
__import__('greetings-to-you')


def foo(bar):
    eggs()

hi
```

What happened? Rather, what is that function?   

__*\_\_import\_\_* is a built-in function that gets module name in str type and imports it. Internally, when we import a module with _import_ statement, *\_\_import\_\_* function is called to import the module in Python.__

And instead of using _import_ statement, **we can import any modules containing any characters(including whitespaces) if we give names in _str_ type in *\_\_import\_\_* function.** It's syntatically correct while '_import greeting-to-you_' breaks variable naming rules of Python.

<br>

Okay. **We proved that we can use non-english characters, Japanese, Korean, punctuation and even whitespaces for module names.**  

---

<br id="3b">

### 3.2. Do all Python module names have to end with '.py'?

We take it for granted that all Python modules should end with '.py' suffix. Because we learn to name it that way at first time we learn Python. But let's ask, ask for everything. Is it True?

Who knows? Let's test it right away :)


```python
echo "print('hi')" > greetings.py
echo "print('bye')" > farewells 
# farewells is a module without '.py' suffix.


python greetings.py
python farewells


hi
bye
```

Well, we could see that it doens't matter if the script ends with '.py' or not when executing the script.

However, it's different when we import modules inside scripts.


```python
import greetings

# It's ok.

import farewells

## !!! A ModuleNotFoundError is raised !!!
ModuleNotFoundError: No module named 'farewells'
```

A _ModuleNotFoundError_ exception is raised. It's interesting because 'greetings.py' and 'farewells' are in the same folder where Python interpreter is working but 'farewells' module is not found.  

**So, We can think that Python assumes all proper module names should end with '.py' suffix. It doesn't consider file names that do not end with '.py' can be also python modules.** So we should add '.py' suffix to all Python modules we make. Also it's more recommended because people can guess files containing '.py' suffix would be Python modules. But we could see that **naming Python modules with '.py' suffix is not just recommended, but mandatory.**


<br>

We found answers for 2 module naming issues in Python:

1. **Python module names can contain any characters besides english if you want. It's possible, but not that ideal.**
1. **All Python modules should have '.py' suffix. Without it, you cannot import them in other Python sripts.**


<br id="4">

## 4. Registering our modules and module import order

---

This chapter is very core of this post. If we create our own scripts, we can use them as scripts and modules. Now we're great Python users and our code is fantastic. Who knows? Maybe we can create famous frameworks like Django, Pandas, etc someday. **This chapter deals with issues about importing our own modules**:

1. You can import standard modules(_math_, _sys_, _keyword_) wherever you are. Then how about ours? **How can we make our modules importable in any places?**
1. **You created 'math' module and it's duplicate with Python _math_ standard module.** It's not ideal but let's say you have to name it that way. **If we run '_import math_' it, what would be imported, ours or Python's?**


Isn't those interesting? Yeah, it sure is. Let's get into it :)



<br id="4a">

### 4.1. Make our modules system-wide!

Sometimes you need to count the execution time of code blocks, like when you compare several algorithms. I knew that it can be used in many cases so I made a time counting function with decorator(@). Here is the code.


```python
def calc_time(func):
    import time
    def wrapper(*args, **kwargs):
        s = time.time()
        v = func(*args, **kwargs)
        e = time.time()

        print("Total execution time for", func.__name__, "is", e-s)
        return v

    return wrapper
```

This is an easy example of decorator. Decorator function gets function as input and return wrapper function, which addes some actions to original functions. Decorator is really useful.


```python
@calc_time
def print_1_to_n(n):
    for i in range(1, n+1):
        print(i)


@calc_time
def repeat_word(word, n):
    return word * n


print_1_to_n(100)
repeat_word('parkito', 1000)


# I omitted execution results of both functions.
Total execution time for print_1_to_n is 0.01787590980529785
Total execution time for repeat_word is 7.62939453125e-06
```

Yeah, it's cool. **I love my _calc\_time_ function and I want it to be accessible from any places like other useful modules do.** But you can easily see that if the module containing that couting function is not where you import or use it, you can't automatically use it. It means you need some actions or solutions for it. What would it be? I introduce 2 ways for it.


<br id="4a!">

#### 4.1.1. Test case definition

Let's make a test exmple before going on. **I made a simple directory structure for this case.**

```sh
$ mkdir -p ~/deletemesoon/{a..c}
$ touch ~/deletemesoon/a/in_a.py
$ touch ~/deletemesoon/b/in_b.py
$ touch ~/deletemesoon/c/in_c.py
```

It's a simple shell usage to make folders. I made a 'deletemesoon' directioy(cause I'll remove it after posting) right inside home directory and created 'a', 'b', 'c' directories inside. And each directory has 'in\_\*'.py Python module. And each module has a function and we'll use it later. The directory structure would be like this:

![import example directory hierarchy](/assets/img/python/import-structure.png)


Each Python module has its unique function:

1. in\_a.py: it has _calc\_time_ function and we saw it earlier.
1. in\_b.py: In _main_ function, we'll import other 2 functions and use it.
1. in\_c.py: it has _say\_ok_ function and it prints out a calming phrase: 'ok!'.

And we didn't define _say\_ok_ function so let's make it.

```python
# in in_c.py

def say_ok():
    print('ok!')
```

**And in _main_ function in in\_b.py, we'll calculate execution time of _say\_ok_ function using _calc\_time_ function.**

```python
# in in_b.py
from in_a import calc_time
from in_c import say_ok

# Decorate it with calc_time
say_ok = calc_time(say_ok)

# main function counts execution time of say_ok.
def main():
    say_ok()

# Execute main function
main()
```

And inside 'b' folder, run in\_b.py script. How was it?

```
ModuleNotFoundError: No module named 'in_a'
```

Yes, this is our problem. **We want in\_a and in\_c module to be accessible from any directory inside the system.** We'll solve it in 2 ways.

---

<br id="4a@">

#### 4.1.2. Dynamically add it!

First way is **'dynamically adding target modules'**. Here's some Python information.  

As you know, Python has _sys_ standard module and it deals with Python interpreter environment. It can control interpreter-related configurations like recursion limit of function calls, get version information of the interpreter, customize shell prompts('\>\>\>' is default) and etc.  

Also _sys_ contains a list named _sys.path_ and it contains paths of directories that the interpreter searches for modules when you try to import modules.**


```python
import sys

print(sys.path)


['',
 '/home/sunghwanpark/.pyenv/versions/3.6.3/bin',
 '/home/sunghwanpark/.pyenv/versions/3.6.3/lib/python36.zip',
 '/home/sunghwanpark/.pyenv/versions/3.6.3/lib/python3.6',
 '/home/sunghwanpark/.pyenv/versions/3.6.3/lib/python3.6/lib-dynload',
 '/home/sunghwanpark/.pyenv/versions/3.6.3/lib/python3.6/site-packages',
 '/home/sunghwanpark/.pyenv/versions/3.6.3/lib/python3.6/site-packages/IPython/extensions',
 '/home/sunghwanpark/.ipython']
```

It's my result and yours would be different.

**Each element in the list is a directory path and target module should be inside at least one directories here. Otherwise, _ModuleNotFound_ exception is raised as you saw.** We'll talk about this list more in the next paragraph.

**Solution here is to append paths containing our target modules to this list.** Let's add somd codes in in_b.py.

```python
# in_b.py 

### new code
import sys

sys.path.append('/home/sunghwanpark/deletemesoon/a')
sys.path.append('/home/sunghwanpark/deletemesoon/c')
###


from in_a import calc_time
from in_c import say_ok
...
```

Run it! What does it say?

```sh
$ python in_b.py

ok!
Total execution time for say_ok is 6.866455078125e-05
```

Perfectly worked. Just before now, in_b.py couldn't import in\_a module because Python interpreter couldn't find in_a module in all directories in _sys.path_. **When we added paths containing in\_a, in\_c modules, it could find both modules and code went well.** It supports only full absolute paths and others(e.g. '~/p/a/t/h') are not seen as paths here.

**I named this 'dynamic way' because we add directory paths to look through inside the script we work on.**  

How do you think about this way? Well... It's ok **but it's boring to put _sys.path_ related code everytime we use the target module.** So, we need a better option.

---

<br id="4a#">

#### 4.1.3. Use environment variable

Systems including Xnix and Windows have environment variables and they're used in programs as configuration options. If you have installed Python on Windows, I think you must have set environment variable configurations for Python.  

I'm using Linux(Ubuntu) and it's same too. This way is using environment variable named `PYTHONPATH`.

**If you set PYTHONPATH variable with concatenated string of directory paths, python interpreter look for these paths when you import a module.** Hoolay! Is it True? Let's test it.


```sh
$ PYTHONPATH=/home/sunghwanpark/deletemesoon/a:/home/sunghwanpark/deletemesoon/c
```
Execute this code in shell and comment _sys.path_ code block in in\_b.py

**PYTHONPATH is a concatenated string of paths and ':' is a seperator between them.** And from now on, Python interpreter will look through these directories to find target modules.  

Let's run the script

```sh
$ python in_b.py

ok!
Total execution time for say_ok is 6.4849853515625e-05
```

It works. You don't need to paste additional boring codes to import your modules.

And last, **this way only lasts until you quit this shell session. If you want to maintain this configuration, paste and run this code in shell.**

```
echo 'export PYTHONPATH="your:wanted:paths:concatenated' >> ~/.bashrc
```

I assumed you use bash shell(default in many Xnix systems)

<br>

Ok. Now we can use our awesome and fantastic functions and classes anywhere we are in our system.

---

<br id="4b">

### 4.2. Modules with same names

We've come a long way. This is the final session:  

If there're modules with same names and both are detectable from Python interpreter, what would be imported? As I supposed above, **if I created my 'math' module, and execute '_import math_' statement, what module would be imported?**

The answer lies with _sys.path_. Let's call it again here.


```python
import sys

print(sys.path)


['',
 '/home/sunghwanpark/deletemesoon/a',
 '/home/sunghwanpark/deletemesoon/c',
 '/home/sunghwanpark/.pyenv/versions/3.6.3/lib/python36.zip',
 '/home/sunghwanpark/.pyenv/versions/3.6.3/lib/python3.6',
 '/home/sunghwanpark/.pyenv/versions/3.6.3/lib/python3.6/lib-dynload',
 '/home/sunghwanpark/.pyenv/versions/3.6.3/lib/python3.6/site-packages',
 '/home/sunghwanpark/.pyenv/versions/3.6.3/lib/python3.6/site-packages/IPython/extensions',
 '/home/sunghwanpark/.ipython']
```


We checked that Python interpreter looks through each of this directory path to find target module.  

**And the order of looking through is same to element order in _sys.path_ list. Interpreter iterates over each path in the list and if you find the module, exit the iteration and import that module.**  

So _sys.path[0]_ is searched first and [1], [2], ... will go on until it finds the module. If the iteration ends and couldn't find the module, exception is raised.  

At this point, We can redefine our problems.  

**How does _sys.path_ list is organized? How first, second and other elements are decided?**

<br>

Paths in which Python searches for modules is decided by these principles in order:

1. **Path that interpreter is working on.** It means current path.
1. **Paths registered in PYTHONPATH environment variable in the system.** We checked this out.
1. **Paths in which Python was installed initially.** These paths contain built-in and third-party packages(Django, Pandas, etc)


<br>

**We can understand _sys.path_ module now. First element is '', an empty string. It means 'current path' the interpreter is working on.**  

**And the following two paths are paths we just added by setting PYTHONPATH. They're searched second.**

**The rest are pre-set Python modules paths. These paths contain built-in, third-party modules.**

<br>

Now we got the answer of our issue: If I have my _math_ module, what module would be imported?

The answer is **our module will be either in current path or in paths registered in PYTHONPATH variable. They both precede pre-registered paths for built-in modules. So our 'math' module will be imported, not built-in one.**  


<br>

It was a long way for import. But we finished and have grown up now.


<br id="5">

## 5. Epilogue

---

It's my first time posting in English. I think I need this kind of challenges to improve my English and it's very effective. From now on, I'll try to write posts that at least belongs to DEV in English. And also, I would really appreciate any advice on my awkard English expressions.

We import modules everyday but pay less attention to what happens when we import modules. I didn't know this post would be so long like this and I think we have to keep looking for hidden logic in very simple and abstract functions.  


Our challenge to know more never ends.

Post ended. Thank you.
