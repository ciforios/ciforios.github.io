---
layout:     post
title:      "Uploading Betas to iTunes Connect and Testflight Distribution"
subtitle:   "Distribute your cool stuff"
date:       2015-01-24 12:35:33
author:     "The Crew"
tags: [continuous-delivery, jenkins]
---

Instead of manually distribute our ipa files to users/testers we decided to have a Jenkins Job for that.<br>
###General Settings
We created a new Job called "Build and upload master branch" with the mentioned settings which you can find under section "Jobs" in the post of [**Continuous Integration with Jenkins**](http://ciforios.github.io/2015/04/21/Jenkins/).<br>
***
But instead of building ipa files from the dev branch we deploy from the master branch. So in the section *"Source-Code-Management"* for Git we changed "Branches to build" to "*/master_demo" in our case. "Additional Behaviours" can also be left empty because we don't need to listen to a specific branch which is build up by Gerrit.<br>

![image](/img/jenkins/jobITunesConnectSCM.png)
***
In **Build Triggers** we modified the "Gerrit event".

* **Trigger on** we selected "Change Merged"
* **Dynamic Trigger Configuration** needs from the Gerrit project our master branch "master_demo".

***
###Xcode Plugin
Now we setup our Xcode Plugin, therefore you need to add a new build step and select "Xcode". 
####General build settings
* As **Target** you choose your Xcode scheme which you want to build for.
* For **Configuration** we choose "Release". The other posibility would be "Debug" but because this builded ipa would also go live to the iTunes store it's no recommended to do so. 
* Select also **Pack apllication and build .ipa**. As a filename we choosed the project name attached with the current Jenkins Job build number "badgme_${BUILD_ID}".
![image](/img/jenkins/pluginXcodeBuildSettings.png)

####Code signing & OS X keychain options
* That we can generate ipa files for distribution they need to be code signed otherwise you could only run the ipa file in a simulator. We installed the certificates on the server (double-click on those files and it get installed into the keychain) which we generated in the blog post in [**Code-Signing**](http://ciforios.github.io/2015/05/08/Code-Signing/).<br>
You need to checkmark **Unlock Keychain?** and insert the path to your local keychain where you installed your certificates under **Keychain path** with your given **Keychain password**.<br>
![image](/img/jenkins/pluginXcodeCodeSigning.png)

####Versioning
In order to have different version numbers in your project you need to set the **Technical version**. Also, otherwise when you try to upload it, iTunes Connect would complain that you want to upload the same ipa with the same version which already exists.<br>

* Check mark **Provide version number and run avgtool?**. In **Technical version** we set the Jenkins build number as our version number with "${BUILD_ID}".
![image](/img/jenkins/pluginXcodeVersioning.png)


***
###Upload your ipa to iTunes connect
Last but not least we want to upload the generated ipa file to Testflight aka iTunes Connect. Therefore we added a new **build step** and selected "Execute shell". In the command box we added following command:<br>
```
/Applications/Xcode.app/Contents/Applications/Application\ Loader.app/Contents/Frameworks/ITunesSoftwareService.framework/Support/altool --upload-app -f "/Users/Shared/Jenkins/.jenkins/jobs/${JOB_NAME}/workspace/build/Release-iphoneos/badgeme_${BUILD_ID}.ipa" -u %USERNAME% -p %PASSWORD%
```
<br>
What does this command do? First of all we're giving the path to a tool called **altool**. This tool is needed if you want to upload your ipa file to iTunes Connect. It's delievered with Xcode, so no additonal installations are needed.<br>
With ```--upload-app -f``` you specify the path to your ipa file.<br>
```-u %USERNAME% -p %PASSWORD%``` are also required to login to your iTunes Connect account.

