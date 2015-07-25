---
layout:     post
title:      "Our Workflow"
subtitle:   "This is how we flow"
date:       2015-06-05 11:31:11
author:     "The Crew"
header-img: "img/post-bg-03.jpg"
tags: [workflow]
---

## The Workflow
Our overall workflow includes two stages: Development Stage and Master Stage.

![Workflow](/img/workflow-master.jpg)


## Branching

We decided to go with a simple dev and master branching scheme. The dev branch contains the most current work, but should still only contain code that allows the App to be built.<br>
The master contains the newest, stable code which can be rolled out and tested on real devices. 

![Branching](/img/branching.PNG)



## Releases
Alpha releases are automatically created by merging the dev into the master branch. This increments the version number and puthe new version to the shes tester devices.