---
layout:     post
title:      "Setting up your Xcode project"
date:       2015-01-29 10:55:00
author:     "The Crew"
header-img: "img/post-bg-01.jpg"
tags: [ios]
---

Now that we have created everything we need for code signing our application in the [previous post](http://ciforios.github.io/2015/05/08/Code-Signing/), we're ready to set up the Xcode project.

####Creating a new project
When you create a new project, Xcode will ask you for a product name, an organization name and an organization identifier. At this point it's important that these values match the related ones of the App ID(s) you've created earlier.

> Note: Make sure that you pay attention to case sensitivity!

![image](/img/xcode-create-project.png)

####Configure the Provisioning Profiles
We also recommend that you specify which Provisioning Profiles should be used by Xcode instead of using the default value (Automatic). This gives you more control about what Xcode is really doing in the background. If the automatic setting worked for you in the past you may skip this step.

The utilization of Provisioning Profiles can be specified in the "Build Settings" tab of your target. Navigate to the "Code Signing" section and expand the "Provisioning Profile" tab. Set your development Provisioning Profile for the associated target as "Debug" and the belonging distribution profile as "Release".

> Note: Like mentioned, the default Apple Watch project has 3 targets. Please proceed with the other targets accordingly.

![image](/img/xcode-provisioning.png)