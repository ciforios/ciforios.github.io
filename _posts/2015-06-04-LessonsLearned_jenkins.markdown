---
layout:     post
title:      "What we learned about Jenkins"
subtitle:	""
date:       2015-06-04 10:06:56
author:     "The Crew"
header-img: "img/lesson-learned.jpg"
tags: [lessons-learned, continuous-integration]
---

## A quick summary of what we learned about Jenkins
- Is very powerful and versatile
 - There are many open source plugins, even for  the integration of newer services like slack
- Easy setup and integrated authentication and user management
- Plugins are useful, but not perfect
	 - Since the plugins are mostly open source and jenkins as well, there are often changes that are not immediately recognized by one another. Hence the plugins might not always be up to date and might also have bugs that are not fixed right away (we have seen bugs being open since 2012!)
- Once everything is set up your done. WRONG!
	- Especially when you work with tools that have to be updated from time to time, it can always happen that a plugin breaks ans blocks your toolchain. This is especially true when working with beta software.