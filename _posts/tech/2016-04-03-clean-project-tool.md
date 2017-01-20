---
layout: post
category: tech
tags: tech
keywords: runtime 清理工具
description: 基于runtime的清理工具
title: 基于runtime的清理工具
---

上周五突发奇想，我们的project为什么不做一个自动清理的工具？

因为基于runtime的工程如果大起来了，项目里肯定会产生一些垃圾文件。

但是人工去处理肯定是一个很头疼的事情，因此有一个自动化垃圾文件清理的工具是必要的。

于是想着应该从哪方面入手。

像eclipse或者android studio这样的IDE是有一些小工具清理工程的。基于Java的Android进行自动化清理时比较好实现的。

Java的所有class文件开头都会有文件依赖申明，因此只要从程序入口逐个检查文件及依赖，便可达到清理目的。

我们的runtime是基于JS，特别是我们脱离了IDE的runtime来开发大型项目时，就会有很多编程规范没有严格按照runtime的规则来编写，因此会给项目清理带来一定困难。

我们基于IDE的runtime去做app，那工程是易维护的，所有组件和模板以及页面都是通过json申明进行引用，因此我们按照json文件来清理整个项目是可以达到目的的。

虽然我们的项目没有严格按照IDE的runtime要求的规则来开发，但是同样也可以先根据json文件来清理项目。

思路是这样的，由于我们的runtime的代码渲染出界面来是依赖浏览器的，因此清理工作也可以浏览器界面化。

<b>在浏览器里发起一个清理请求，后台遍历json，找出脱离依赖的文件，展示到前端,前端可以一览可能是垃圾的文件，然后通过一键清理或者手动清理这些文件。</b>

这个方法的可靠性是不大的，因为部分自定义组件和模板我们没有在json文件里申明依赖，而是直接在代码中去使用，因此也会当成垃圾文件扫描出来，这时我们就得依靠开发者对工程的熟练度来处理这种文件了。

后续是可以强化这个工具的，比如可以检查每个文件是否在js代码里有用到。

但另一方面也说明，我们应该严格按照runtime的规则，自定义组件和模板只能通过json文件去引用，这样就更易于项目的管理和维护。
