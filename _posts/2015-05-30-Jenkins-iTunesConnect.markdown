---
layout:     post
title:      "iTunes Connect and Testflight"
subtitle:   "Distribute your cool stuff"
date:       2015-05-30 12:35:33
author:     "The Crew"
header-img: "img/post-bg-03.jpg"
tags: [continuous-delivery]
---

Instead of manually distribute our ipa files to users/testers we decided to have a Jenkins Job for that.<br>
We created a new Job called "Build and upload master branch" with the mentioned settings which you can find under section "Jobs" in the post of [**Continuous Integration with Jenkins**](http://ciforios.github.io/2015/04/21/Jenkins/). But instead of building ipa files from the dev branch we listen on the master branch. So in the section *"Source-Code-Management"* for Git we changed "Branches to build" to "*/master_demo" in our case. Additionaly we decided to trigger this Job manually that we can decide when we create a distributing version.

don't need to listen to Gerrit, Refspec wil be left empty.<br>
 


Changes:
- Git: Listen on master branch -> master_demo

XcodePlugin:
- Target: badgme
- Configuration: Release!
- Pack application and build .ipa:	ipa filename pattern: badgeme_${BUILD_ID}
- Unlock Keychain -> Keychain: 
Keychain Path: ${HOME}/Library/Keychains/login.keychain
Keychain password
- Versioning: Provide version number and run avgtool? Technical version: ${BUILD_ID}

Bash
/Applications/Xcode.app/Contents/Applications/Application\ Loader.app/Contents/Frameworks/ITunesSoftwareService.framework/Support/altool --upload-app -f "/Users/Shared/Jenkins/.jenkins/jobs/${JOB_NAME}/workspace/build/Release-iphoneos/badgeme_${BUILD_ID}.ipa" -u %USERNAME% -p %PASSWORD%