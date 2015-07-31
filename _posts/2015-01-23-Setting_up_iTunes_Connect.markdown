---
layout:     post
title:      "Setting up iTunes Connect"
subtitle:   "Distribute your applications"
date:       2015-01-23 12:35:33
author:     "The Crew"
header-img: "img/cd-bg.jpg"
tags: [continuous-delivery, ios]
---

When it comes to distributing your created applications you usually have to deal with iTunes Connect sooner or later. iTunes Connect is the place where you'll need to upload your compiled applications to so you can distribute them over the App Store or Testlight. 
iTunes Connect also lets you manage the meta data of your application like photos, descriptions as well as setting a price for your application.

Before you can upload any compiled code you first have to create an iTunes Connect record for your application.

Head over to [iTunes Connect](https://itunesconnect.apple.com/), log in with your developer account and add a new entry for your application in the "My Apps" section.

###Uploading your app to iTunes Connect
We chose to upload our builds automatically to iTunes Connect by using a Jenkins Job. This job is described in the [following post](http://ciforios.github.io/2015/01/22/Uploading_to_iTunes_Connect/) in detail. If you don't need an automated upload-job, you might as well do this manually by uploading your betas from within Xcode.

Once you've uploaded your first build, don't forget to enable your application for TestFlight Beta Testing by triggering the intended switch in My Apps > "Your Application" > Prerelease > Builds.

###Inviting internal TestFlight beta testers
In general there are two kinds of testers for your application. You can choose to invite internal or external testers. Internal testers are limited to a maximum of 25 compared to a maximum of 1000 people for external testers.

> Note: Distribution to external testers requires a review of your app by Apple. This is why we chose to use interal testers only.

Each internal tester has to be an iTunes Connect User in your account. Register them in "Users and Roles" which can be found in the iTunes Connect main menu.

> Note: Give these registered users at least a technical role.

Once the registration of the users you want to invite as internal beta testers is complete, make sure to also activate them as TestFlight Beta Testers in Users and Roles > TestFlight Beta Testers > Internal.

Head back to your created application in iTunes Connect and choose the users you want to add as beta testers of your application in Prerelease > Internal Testers.

All internal testers will now be automatically informed about new beta builds via E-Mail.