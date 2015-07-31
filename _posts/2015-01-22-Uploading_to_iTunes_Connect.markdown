---
layout:     post
title:      "Uploading your applications to iTunes Connect using Jenkins"
subtitle:   "Upload your builds"
date:       2015-01-23 12:35:33
author:     "The Crew"
header-img: "img/cd-bg.jpg"
tags: [continuous-delivery, jenkins]
---

Instead of manually distributing our IPA files to our users/testers, we decided to create a Jenkins Job for that.<br>
###General Settings
We created a new Job called "Build and upload master branch" with the mentioned settings which you can find under section "Jobs" in the post of [**Continuous Integration with Jenkins**](http://ciforios.github.io/2015/01/25/Jenkins/).<br>
***
But instead of building IPA files from the dev branch we deploy from the master branch. So in the section *"Source-Code-Management"* for Git we changed "Branches to build" to "*/master_demo" in our case. "Additional Behaviours" can also be left empty because we don't need to listen to a specific branch which is build up by Gerrit.<br>

![image](/img/jenkins/jobITunesConnectSCM.png)
***
In **Build Triggers** we modified the "Gerrit event".

* **Trigger on** we selected "Change Merged"
* **Dynamic Trigger Configuration** needs our master branch "master_demo" from the Gerrit project.

***
###Xcode Plugin
Now we setup our Xcode Plugin, therefore you need to add a new build step and select "Xcode". 
####General build settings
* Instead of choosing the "Debug" configuration, this job will use the "Release" configuration for distribution in TestFlight or App Store.

![image](/img/jenkins/pluginXcodeBuildSettings.png)

####Versioning
In order to have different (increasing) version numbers in your project you need to set the **Technical version**. Unless you update the technical version of your project, iTunes Connect would complain because you would be trying to upload the same IPA with the same version which already exists.<br>

* Check mark **Provide version number and run avgtool?**. In **Technical version** we set the Jenkins build number as our version number with "${BUILD_ID}".

![image](/img/jenkins/pluginXcodeVersioning.png)

***
###Upload your IPA to iTunes connect
Last but not least we want to upload the generated IPA file to Testflight aka iTunes Connect. Therefore we added a new **build step** and selected "Execute shell". In the command box we added the following command:<br>
```
/path/to/altool --upload-app -f "path/to/file.ipa" -u %USERNAME% -p %PASSWORD%
```
> Note: Normally the path to altool should look something like this: /Applications/Xcode.app/Contents/Applications/Application\ Loader.app/Contents/Frameworks/ITunesSoftwareService.framework/Support/altool

What does this command do? First of all we're giving the path to a tool called **altool** (= Application Loader, which can be started separately too). This tool is needed if you want to upload your IPA file to iTunes Connect from the command line. As you can see from its filepath, it ships together with Xcode, so no additonal installations are needed.<br>
With ```--upload-app -f``` you specify the path to your IPA file.<br>
```-u %USERNAME% -p %PASSWORD%``` are also required to login to your iTunes Connect account.