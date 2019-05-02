---
layout: post
title: "Web vs Internet, what's the difference?"
date: 2019-05-02
description: "Let's briefly look through significant differences between the Web and the Internet"
img:  /knowledge/web-vs-internet-logo.jpeg
categories: [Programming, Knowledge]
tags: [Web, Internet, Web_vs_Internet]
---

### 0. Index

> 1. [Prologue](#1)
> 2. [Web](#2)
> 3. [Internet](#3)
> 4. [Differences](#4)
> 5. [Epilogue](#5)
> 6. [Data source](#6)


<br id="1">

## 1. Prologue

---

Everyone uses Web and Internet everyday. It enables us to connect to other people, look for information we need as you're doing now, watch streaming videos and many other things with this platforms. But many of us are not that aware of differences between Web and Internet. And so was I.

I had been also curious about the differences when I just jumped into web Programming with Django, Python main framework. Now many years after studying network and TCP/IP protocol suite, I know the differences are not that trivial but quite structural. It's not a problem of just 'coining difficult words to sweet-talk peole'.  And I'll look through the differences on today's post.

First, we shortly skim through Web and Internet independently. And we look for their differences with OSI network hierarchy model.


<br id="2">

## 2. Web

---

**`The Web` or `The World Wide Web`(below as just "Web") is a vast information space where web page documents are spread all over the world and connected to each other through hyperlinks.**  

Understanding Web is easy when we look at what we do with our phones and desktops. We look for information with our browsers installed on our machines. We type addresses like 'shoark7.github.io' and you can access to any pages you want. It's not over. You can tranfer to other pages with clicking at links on the page. We can jump hop to hop of pages with this method, right?
  
**Any single page contains any information as it intends to do, and set of them which are connected via links constitue the Web we know.** So, your browser is actually called 'Web browser', meaning it searches information through vast areas of interconnected web pages. And there are web servers, counterparts of web browsers, and what they do is returning web pages(most often) to web browsers.

**Web page is not just text file. It's formatted by HTML language and web pages written in HTML contains formatting data along with information. Formatting data means how to represent the page with visual or auditory effects on the browser.** When you type 'shoark7.github.io' in the address section in your browser, you see visual representation of the page interpreted by the browser. Most of parts here was written by me. But I didn't draw this.(I suck at drawing) **Original page written in HTML is just text and it orders what and how to draw and color things to the browser.**

<br>

So, Web is not difficult. Web is just collections of web pages connected via links. But remember that **the Web means web pages spread worldwide.** I cannot say my blog 'shoark7.github.io' is the Web for it's connected to my blog posts at the homepage. Mine is just a tiny part of the huge Web. Dream big. I, currently in Seoul, can connect to web pages in USA by some link-clicking with Google. The Web is so huge that counting the number of total pages in the Web is now not possible.




<br id="3">

## 3. Internet

---

`Internet` is a much bigger concept constituing our network lives. We know we can read news articles of opposite side of the earth with our web browser. But how? How can we know existence of web pages in other side of the earth, beyond our local area? It's a simliar question to 'how can I upload my homespun HTML page on the Web?' and it's not easy.  

The fundamental answer is we can send information with physical equipments like routers, wirelss access points or wired cables buried under the roads and even underwater. **This physical equipments are spread all over the world and send and receive information as we we want.** Without this, we cannot know the cutting-edge news of other countries.

And this is not over. There are many abstraction layers constituting the whole network. Physical layer is undermost layer of worldwide network and layers above this share responsibilities to connect the whole world as one.  

And **in the middle section of the network, there is the Internet. Internet is the global network system of interconnected networks worldwide and many network applications include the Web, email service, DNS, NFS and etc. It's the basis of our daily usage network and bridge between our familiar network applications and real network hardwares sending and receiving data stream.**

And I'm sure you must have heard of 'TCP/IP'. It's like main framework of middle section of the Internet. There were other options to constitue the network like IPX/SPX, but they're mostly dead. We don't need to study this.

<br>

And you shouldn't be confused of the Internet with internet. Actually, 'internet' itself means 'inter-network', which means networks connected to each other. Network can be made of just several machines: in our homes, in companies or in local area. This small networks can be connected to other networks and these are called 'internet'. It's a common name. **But when they gather and make a worldwide single network, it's called 'Internet', and it's a proper name.** The world is accessible from any points to any points within single 'I'nternet.


<br id="4">


## 4. Differences

---

Now let's check out differences between them. I said earlier that their differences are not just quantitative, but rather literally structural. **Computer network worldwide is way too huge and complicated so we cannot understand it as whole. Instead, we categorize the network into hierarchy and its well-known standard is OSI model.**

![OSI hierarchy rainbow](/assets/img/knowledge/web-vs-internet-osi.png)

**OSI model briefly describes stages of what is continuously going on during the network communication. It has 7 layer hierarchy and as its stage number gets bigger, it means getting close to end users like us, less close to computer hardware like routers, AP or cables underground. And as lower the stage numbers, more close to computer hardware, farther from end users.** Each stage needs different kinds of actions and requirements for it to work properly.  

Scrutinizing OSI network model is not important and possible now. **What's important is that lower stage supports higher stage functions.** For example, the application layer(layer 7) is close to us and one of important elements is HTTP. HTTP is a high level protocol and it cannot deliver messages over the network by itself alone. **Instead, it uses service of lower stage protocols like TCP(transport layer, No.4), IP(Network layer, No.3) and routers.(No.1) Lowers deliver the messages from higher layers and it's the very core of OSI model.** We use web browsers(main participants of HTTP transactions) but without TCP, IP and others, we cannot search information at all.

<br>

And here are the differences between Web and Internet. Web a is collection of web pages(in HTML) and these web pages are communicated through HTTP protocol. HTTP protocol is one of application layer protocols and others include DNS, SMTP, Telnet and etc. These protocols are very close to end users so you might have heard any of them. So we can say **Web is based upon application layer.**

However, Internet is more deeper. Internet is the worldwide spread network of inter-networks and they're mostly based upon TCP/IP as mentioned above. It serves services to upper layer protocols like DNS, SMTP, gopher and most importantly HTTP. You can use Internet not only through web browsers, but also through FTP clients, DNS utilities, email services and many other application layer protocols. **We use web browsers everyday but it's not the only way to use Internet. It's an option of many other usages** and you shouldn't be confused of Web and Internet. **Internet is based upon network or transport layer.(you can include both because they're strongly connected in modern TCP/IP network)**

**Putting together, the hierarchy layer they're based upon is totally different: Web is based upon HTTP, which is the main product of application layers and Internet is based upon network or transport layers and TCP/IP is the most dominant framework covering those layers.**

![Based layers upon which Web and Internet are based](/assets/img/knowledge/web-vs-internet-based-layer.png)


<br id="5">

## 5. Epilogue

---

We simply checked out differences between Web and Internet. **The most dominant usage of Internet in our daily lives is Web so we often get confused of Web and Internet are same. But it's totally, structurally not true. In Web environment, we communicate through HTTP protocol and it's based on protocol layer. But Internet can serve many more layers and they constitue the vast, wide area of network and it's based upon more deeper layers: TCP(maybe UDP too) and IP.** So their differences are qualitative, not quantitative. It's a huge gap and we're clear about it now.

Modern network is so complicated and difficult so checking out every detail doesn't help out the topic today. So I just introduced shallow concept of OSI model and we now know each layer serves specific functions and serves higher layers' communication. I hope it's enough for you to grasp at the differences even though simply.

Ok. Thank you for reading. See you on another post.

Post ended.


<br id="6">

## 6. Data source

---

* [Wikipedia: Internet](https://en.wikipedia.org/wiki/Internet){:target="\_blank"}
* [Wikipedia: OSI model](https://en.wikipedia.org/wiki/OSI_model){:target="\_blank"}
* [Wikipedia: World Wide Web](https://en.wikipedia.org/wiki/World_Wide_Web){:target="\_blank"}
* [networks.land: physical](http://networks.land/reference/physical/){:target="\_blank"}
