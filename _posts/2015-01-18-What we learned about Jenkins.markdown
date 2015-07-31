---
layout:     post
title:      "What we learned about Jenkins"
subtitle:	"Can continuous integration help you and your team?"
date:       2015-01-18 10:06:56
author:     "The Crew"
header-img: "img/lesson-learned.jpg"
tags: [lessons-learned, continuous-integration]
---

## A quick summary of what we learned about Jenkins
From what we learned, Jenkins is a great continuous integration tool which makes it easy for you to do repetetive tasks for you automatically - be it building projects, running software tests or triggering notifications to participating users. Simply put, Jenkins will do stuff for you, depending on what you tell it to do. This makes it a very **powerful and versatile** tool. Getting Jenkins up and running is not a very big deal since all you need is the latest Java version. Another big plus is that it can be run independent of the underlying system (e.g. Mac OS X, Windows). You must however keep in mind that the Xcode plugin requires you to have a Mac OS X system because it relies on an installed Xcode on the system. Other plugins might impose further restrictions onto the running system but Jenkins itself doesn't restrict you from using any system you want.

Another big advantage of Jenkins is that it is **open source** and has a **broad community**. That's why a **huge amount of plugins** are available and you can **integrate new services** like Slack easily. While it's really nice to have a lot of plugins to choose from, **plugins aren't perfect**. Since both Jenkins and most of the plugins are open source, there are frequent changes that are not immediately recognized by one another. Hence, the plugins might not always be up to date and might even have bugs that aren't fixed right away (we've seen bugs being open since 2012!).

Apart from this you can **easily secure** your Jenkins. Under the "Global Security settings" you just set up your own database, link to an LDAP server and so on. This makes **authentication and user management** really easy.

One more point to pay attention to is that if you believe **once everything is set up, you're done. Then you're wrong!** Especially when you work with tools that have to be updated from time to time, it can always happen that a plugin breaks and blocks your toolchain. This is especially true when working with beta software.

What we also found very helpful was the **immediate feedback** you get when you push your changes. Depending on your configured jobs, it can give you feedback if Jenkins was able to successfully run your tests, build the project and so on.