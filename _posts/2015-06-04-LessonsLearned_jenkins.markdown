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
Getting Jenkins up and running isn't that difficult. It only requires the latest Java version. Jenkins seems to be very **powerful and versatile**. Compared to the continuous integration service on OS X Server from Apple it won't restrict you to the Apple world. Nevertheless we needed a Mac because we need an environment where Xcode can be running. And that's only the case where OS X is installed. But that is independent for Jenkins.

One big advantage of Jenkins is that it is **open source** and has a **broad community**. That's why a **shitload of plugins** are available and you can **integrate new services** like Slack easily. You would't have that broad support for the CI of Apple.
It's really nice to have so many of them however **Plugins are not perfect**. Since the Plugins are mostly open source and Jenkins as well, there are often changes that are not immediately recognized by one another. Hence the Plugins might not always be up to date and might also have bugs that are not fixed right away (we have seen bugs being open since 2012!).

Apart from this you can **easily secure** your Jenkins. Under the "Global Security settings" you just setup your own database, link to an LDAP and so on. This makes **authentication and user managament** really easy.

Nevertheless if you believe **once everything is set up your done. Then you are wrong!** Especially when you work with tools that have to be updated from time to time, it can always happen that a plugin breaks and blocks your toolchain. This is especially true when working with beta software.

Very helpful is the **immediately feedback** you get when you push your changes. Depending on your configured Jobs it can give you feedback if Jenkins was able to successfully run your tests, build the project and so on.
