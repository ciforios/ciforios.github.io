---
layout:     post
title:      "Preparing Gerrit for Jenkins Integration"
subtitle:   "Setting up a Gerrit trigger"
date:       2015-01-26 09:12:13
author:     "The Crew"
header-img: "img/codereview-bg.jpg"
tags: [code-review, continuous-integration]
---

####Adding Jenkins user
In order to allow Jenkins to make changes to projects (eg. review a PatchSet based on whether it builds or not), it needs its own user account in Gerrit.
> As discussed in the [previous post](http://ciforios.github.io/2015/01/27/Gerrit/), our accounts had to be OpenID accounts, so we had to create another Launchpad account for Jenkins using a new email address.

After the user is created, you have to add it to a special group, in our case called "Non-Interactive Users".
> Note: You must be logged into your admin account to do that.

You can achieve this by selecting People > List Groups (in case the group already exists) or People > Create New Group (in case you dont't have a group for external tools).

You also have to change the project settings accordingly, so that the "Non-Interactive Users" are allowed to set the label (in our case "verified" +1 or -1 and "Code-Review" +1 or -1).

> Note: If you don't have the verified label, but would like to add it, please follow the instructions [below](#verifiedLabel).

![Access Settings in Gerrit](/img/gerrit/project_access_settings_gerrit.PNG)

This can be achived by selecting the project (Projects > List > *Project Name*). This should redirect you to the access tab of the project. Then select "Edit" to edit the Access Settings.
> Note: In case you aren't allowed to edit the settings, you might not be logged in, or you don't have admin rights.
> In case the verified label doesn't exist, follow the steps [below](#verifiedLabel).

In order to allow a secure communication the Jenkins user also requires a SSH key. Therefore you'll have to create a private and public key on the host machine that is running Jenkins and allow communication from the machine running gerrit. If you're on a UNIX system, you should be able to run *ssh-keygen* in your terminal and follow the instructions until you have your pair of keys.
> Note: Make sure **not** to enter a passphrase when creating the SSH keys because otherwise, Jenkins won't be able to log into Gerrit. It will show the error "Bad SSH key or passphrase" when testing the connection, see [https://issues.jenkins-ci.org/browse/JENKINS-20879](https://issues.Jenkins-ci.org/browse/JENKINS-20879).

In Gerrit, you also have to add the public key to the Jenkins user.
> Note: Don't forget to log in with the Jenkins user.

To add the public key, hit the username in the top right corner (should be Jenkins) and click "Settings". In the settings menu choose "SSH Public Keys" and add the Public Key you created on the Jenkins machine.

You also have to set the username of the Jenkins user. You can do that in the user Settings within "Settings". This is the username you have to enter for Gerrit Trigger in Jenkins.

####<div id="verifiedLabel"/>The verified label bug

The Jenkins Plugin "Gerrit Trigger" expects Gerrit to have the label "Verified" set, which isn't included in the Gerrit config by default.<br>
The Gerrit label can be added in:<br>
Projects > List > All Projects > General > Edit Config<br>
by adding the following in the bottom of the document:
{% highlight bash %}
[label "Verified"]
	function = MaxWithBlock
	value = -2 This shall not be merged
	value = -1 fail
	value =  0 No score
	value = +1 Verified
	defaultValue = 0
{% endhighlight %}
After saving, go to All > Open and you will see an open review "Change Config". Open it, hit "Publish" then "Code-Review +2" and then Submit.<br>
Depending on your project settings, you might not want the verified label to have the -2 value. <br>
In our case we wanted to be able to override the Jenkins opinion if necessary (partly because in the beginning, Jenkins was not 100% reliable). Merging a PatchSet in Gerrit is not possible, when the lowest value of a label is set (once a user reviews a PatchSet with the lowest value, the PatchSet is blocked).

> Note: Alternatively to adding the verified label, you can also change the ssh command of Gerrit trigger and remove the "-v" part.

After adding the verified label, it's also necessary to add the permissions for groups to change the verified status of a review.<br>
Therefore, navigate to Projects > List > All Projects > Access > Edit<br>
Just below "Reference: refs/heads/*" hit "Add Permission" and choose "Label Verified". Then add the groups that should be allowed to change the verified state, e.g. Admins and Non-Interactive Users (the group containing Jenkins).

> Note: This error is not easily visible since no error is thrown in the Jenkins log. In our case the symptoms were, that Jenkins did set the "Jenkins started building" message, but did not set a review after the build was done. You can identify this problem by taking a look at the ssh log files of Gerrit/Jenkins.

Further info on Gerrit labels see: <br>
[https://gerrit-review.googlesource.com/Documentation/config-labels.html](https://gerrit-review.googlesource.com/Documentation/config-labels.html)

Regarding the Gerrit Trigger "bug" see: <br>
[https://code.google.com/p/gerrit/issues/detail?id=1963](https://code.google.com/p/gerrit/issues/detail?id=1963)