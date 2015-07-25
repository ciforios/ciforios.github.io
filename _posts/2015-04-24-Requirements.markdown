---
layout:     post
title:      "Requirements"
subtitle:	"All you need is ..."
date:       2015-04-24 14:12:00
author:     "The Crew"
header-img: "img/introduction.jpg"
tags: [introduction]
---

> Note: Throughout this tutorial we'll frequently be using the command line. Basic knowledge about using a command line interface is assumed.

	To Do: Check the links
	
First of all, since we're developing for iOS, you will need **any Macintosh** (e.g. MacBook, Mac mini, ...) in order to compile your source code for this platform. The compiler is included within the standard IDE 'Xcode', which is free to download from the App Store.

> Note: The Swift programming language has been declared open source by Apple just recently. This might indicate that in the future, developers will be able to compile source code for iOS from different platforms, too.

Secondly, an [**Apple Developer Program Membership**](https://developer.apple.com/programs/) is required if you're planning to get your app into the App Store or distributing your beta versions via TestFlight.

Compiling source code is essential for [**automated building**](http://ciforios.github.io/jenkins/) including [**automated testing**](http://ciforios.github.io/jenkins/), as well as for [**deploying your beta software**](http://ciforios.github.io/workflow/) via TestFlight. If you are only interested in implementing a [**code-review**](http://ciforios.github.io/gerrit/) process into your development workflow, you **won't need a Mac**.

Next on our checklist are the **server components**. If you're forced to use a Mac, you might as well use it as your build & code review server - this is what we did ourselves. Otherwise, just set up a VM or real server of your choice (e.g. Linux or Windows) but keep in mind that the installation for those systems will not be covered in this tutorial.