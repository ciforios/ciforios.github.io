---
layout:     post
title:      "Code Signing"
date:       2015-05-08 15:23:00
author:     "The Crew"
header-img: "img/post-bg-01.jpg"
tags: [ios]
---

>Note: Like mentioned in [requirements](http://ciforios.github.io/2015/04/24/Requirements/), an Apple Developer Program is required if you intend to distribute your apps via TestFlight or get them into the App Store.

Unlike Android's plug-and-play mechanisms for deploying software onto your development devices, Apple requires you to code-sign your application before you can actually use it on a real device.

> Note: Apple stated that starting from Xcode version 7, developers will no longer have to be part of the Apple Developer Program in order to run apps on real devices which are attached via USB. This does not include distribution.

This post will give you all the information about getting your code-signing up and running.

1) Head over to the [Apple Developer Center](https://developer.apple.com/membercenter) and log into your account

The next thing we're going to do is to create certificates for development and distribution purposes.

> Note: If you don't intend to distribute your apps via TestFlight, you won't need a distribution certificate

Therefore, add new entries in the respective sections within the "Certificates, Identifiers and Profiles" > "Certificates".

2) Create a new development and/or distribution certificate

Development Certificate:

![image](/img/development-certificate.png)

Distribution Certificate:

![image](/img/distribution-certificate.png)

3) Create App IDs

> Note: Developing for the Apple Watch forces you to create 2 supplementary App IDs for the WatchKit App and the WatchKit Extension in addition to your "normal" iOS App ID

![image](/img/app-ids.png)

4) Register your devices you wish to deploy your app onto

> Note: You can add up to 100 devices per category (e.g. iPhone, iPad, Apple Watch). If you're unable to find your devices' UDID - [follow these steps](http://whatsmyudid.com).

5) Create new development and/or distribution provisioning profiles

> Note: For each App ID you registered earlier in Step 3 you need to create one profisioning profile for development and distribution purposes. So if you are working on an Apple Watch project which uses 3 targets you will end up with 6 provisioning profiles (3 development profiles and 3 distribution profiles).

Once you are done it should look something like the screenshot below:

![image](/img/provisioning-profiles.png)