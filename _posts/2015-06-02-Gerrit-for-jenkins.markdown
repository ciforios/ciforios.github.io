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
In order to allow jenkins to make changes to projects (review code based on whether int builds or not) jenkins needs its own user account in gerrit.
>As discussein in the previous post, our accounts had to be OpenID accounts, so we had to create another Launchpad account for jenkins using a new email address

After the user is created, you have to add it to a special group, in our case called "externalReviewers".

You also have to change the project settings accordingly, so that the "externalReviewers" are allowed to set the label (in our case "verified" +1 or -1) accordingly.


####The verified label bug

The Jenkins Plugin "Gerrit Trigger" expects Gerrit to have the label "Verified" set, which is not by default included in the gerrit config.<br>
The gerrit label can be added in:<br>
Projects -> List -> All Projects -> General -> Edit Config<br>
>NOTE: Alternatively to adding the verified label, you can also change the ssh command of gerrit trigger and remove the "-v" part.

After adding the Verified Label, it is also necessary to add the permissions for groups to change the verified status of a review.
Projects -> List -> All Projects -> Access -> Edit<br>
Under the point "Reference: refs/heads/*" hit "Add Permission" and choose "Label Verified". Then add the groups that should be allowed to change the verified state. E.g. Admins and Non-Interactive Users (the group containing Jenkins).

>This error is not easily visible since no error is thrown in the jenkins log. In our case the symptoms were, that jenkins did set the "jenkins started building" message, but did not set a review after the build was done. You can identify this problem by taking a look at the ssh log files of gerrit/jenkins.

Further info on Gerrit labels see: <br>
[https://gerrit-review.googlesource.com/Documentation/config-labels.html](https://gerrit-review.googlesource.com/Documentation/config-labels.html)<br>
Regarding the Gerrit Trigger "bug" see: <br>
[https://code.google.com/p/gerrit/issues/detail?id=1963](https://code.google.com/p/gerrit/issues/detail?id=1963)