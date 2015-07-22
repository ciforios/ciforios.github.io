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

2) Create a new Development and/or Distribution Certificate

Development Certificate:

![image](/img/development-certificate.png)

Distribution Certificate:

![image](/img/distribution-certificate.png)

Once you have created your certificates you have to download these and import them into your keychain by double-clicking on the downloaded *.cert files.

3) Create App IDs

An App ID is a unique identifier whose primary use is to specify which apps are authorized to be signed and launched. App IDs are usually created in reverse-domain-name notation. Enter something like this when creating your App ID:

*com*.*domainname*.*applicationname*

> Note: Developing for the Apple Watch forces you to create 2 supplementary App IDs for the WatchKit App and the WatchKit Extension in addition to your "normal" iOS App ID

![image](/img/app-ids.png)

4) Register your devices you wish to deploy your app onto

> Note: You can add up to 100 devices per category (e.g. iPhone, iPad, Apple Watch). If you're unable to find your devices' UDID - [follow these steps](http://whatsmyudid.com).

5) Create new Development and/or Distribution Provisioning Profiles

A Development Provisioning Profile contains a set of Development Certificates, Device Identifiers and an App ID. The Provisioning Profile has to be installed on each device on which you are planning to run your application code.

> Note: For each App ID you registered earlier in Step 3 you need to create one profisioning profile for development and distribution purposes. So if you are working on an Apple Watch project which uses 3 targets you will end up with 6 provisioning profiles (3 development profiles and 3 distribution profiles).

Once you are done it should look something like the screenshot below:

![image](/img/provisioning-profiles.png)

Congratulations - now you've created everything you need and you are now able to proceed setting up your Xcode project. This will be covered in the [next post]() of this section