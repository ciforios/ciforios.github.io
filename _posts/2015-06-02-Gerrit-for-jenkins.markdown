---
layout:     post
title:      "Jenkins integration"
subtitle:   "Preparing Gerrit for Jenkins"
date:       2015-06-02 09:12:13
author:     "The crew"
header-img: "img/post-bg-03.jpg"
tags: [gerrit]
---

## Setting up Gerrit for Jenkins (Gerrit Trigger)
The Jenkins Plugin "Gerrit Trigger" expects Gerrit to have the label "Verified" set, which is not by default included in the gerrit config.
The gerrit label can be added in:<br>
Projects -> List -> All Projects -> General -> Edit Config<br>
After adding the Verified Label, it is also necessary to add the permissions for groups to change the verified status of a review.
Projects -> List -> All Projects -> Access -> Edit<br>
Under the point "Reference: refs/heads/*" hit "Add Permission" and choose "Label Verified". Then add the groups that should be allowed to change the verified state. E.g. Admins and Non-Interactive Users (the group containing Jenkins).

Further info on Gerrit labels see: <br>
[https://gerrit-review.googlesource.com/Documentation/config-labels.html](https://gerrit-review.googlesource.com/Documentation/config-labels.html)<br>
Regarding the Gerrit Trigger "bug" see: <br>
[https://code.google.com/p/gerrit/issues/detail?id=1963](https://code.google.com/p/gerrit/issues/detail?id=1963)