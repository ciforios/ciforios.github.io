---
layout:     post
title:      "Talking to Jenkins"
subtitle:   "Preparing Gerrit for Jenkins integration"
date:       2015-06-02 09:12:13
author:     "The Crew"
header-img: "img/post-bg-03.jpg"
tags: [code-review, continuous-integration]
---

## Setting up Gerrit for Jenkins (Gerrit Trigger)
####Adding Jenkins user
In order to allow jenkins to make changes to projects (eg. review a PatchSet based on whether it builds or not) jenkins needs its own user account in gerrit.
>As discussein in the previous post, our accounts had to be OpenID accounts, so we had to create another Launchpad account for jenkins using a new email address

After the user is created, you have to add it to a special group, in our case called "Non-Interactive Users".
>NOTE: Log in with your Admin account.

You can achieve this by clicking People -> List Groups (in case the group already exists) or People -> Create New Group (in case you dont't have a group for external tools).<br>
You will also have to add a SSH Public Key to the jenkins user.

You also have to change the project settings accordingly, so that the "Non-Interactive Users" are allowed to set the label (in our case "verified" +1 or -1 and "Code-Review" +1 or -1).<br>
This can be achived by selecting the project (Projects -> List -> <Project Name>). This should redirect you to the Access tab of this project. Then select "Edit" to edit the Access Settings.
>NOTE: In case you are not allowed to edit the settings, you might not be logged in, or you don't have admin rights

In order to allow a secure communication the jenkins user also requires a ssh key. Therefore you will have to create a private and public key on the host machine that is running jenkins, and allow communication from the machine running gerrit.<br>
In gerrit, you also have to add the public key to the jenkins user.
>NOTE: Log in with the jenkins user

To add the Public key, hit the username in the top right corner (should be jenkins) and click "Settings". In the settings menu choose "SSH Public Keys" and add the Public Key you created on the jenkins machine.




####The verified label bug

The Jenkins Plugin "Gerrit Trigger" expects Gerrit to have the label "Verified" set, which is not by default included in the gerrit config.<br>
The gerrit label can be added in:<br>
Projects -> List -> All Projects -> General -> Edit Config<br>
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
Depending on your project settings you might not want the verified label to have the -2 value. In our case we wanted to be able to override the jenkins opinion if necessary (partly because in the beginning Jenkins was not 100% reliable). Merging a PatchSet in Gerrit is not possible, when the lowest value of a label is set(once a user reviews a PatchSet with the lowest value, the PatchSet is blocked).
		

>NOTE: Alternatively to adding the verified label, you can also change the ssh command of gerrit trigger and remove the "-v" part.

After adding the Verified Label, it is also necessary to add the permissions for groups to change the verified status of a review.
Projects -> List -> All Projects -> Access -> Edit<br>
Under the point "Reference: refs/heads/*" hit "Add Permission" and choose "Label Verified". Then add the groups that should be allowed to change the verified state. E.g. Admins and Non-Interactive Users (the group containing Jenkins).

>This error is not easily visible since no error is thrown in the jenkins log. In our case the symptoms were, that jenkins did set the "jenkins started building" message, but did not set a review after the build was done. You can identify this problem by taking a look at the ssh log files of gerrit/jenkins.

Further info on Gerrit labels see: <br>
[https://gerrit-review.googlesource.com/Documentation/config-labels.html](https://gerrit-review.googlesource.com/Documentation/config-labels.html)<br>
Regarding the Gerrit Trigger "bug" see: <br>
[https://code.google.com/p/gerrit/issues/detail?id=1963](https://code.google.com/p/gerrit/issues/detail?id=1963)