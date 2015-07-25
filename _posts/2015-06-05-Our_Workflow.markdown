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
Our overall workflow includes two stages: Development Stage and Master Stage.<br>
In the development stage code is created and submitted for review. Aftwerwards jenkins tries to build it and to run the unit tests, depending on the results jenkins will then set the verified label of the PatchSet in Gerrit. Then the code can be reviewed by the team and, in case it does what it is supposed to do, and complies with the teams regulations, it can be merged into the dev branch.

The Master Stage includes merging the dev into the master branch. This again starts with a developer merging locally and creating a merge commit which is then submitted for review in gerrit. In case the merge commit is accepted, the dev branch is merged into the master branch. This leads jenkins to building the Project, creating an .IPA file and distributing it through iTunesConnect and TestFlight between the testers.

![Workflow](/img/workflow-master.jpg)


## Branching

We decided to go with a simple dev and master branching scheme. The dev branch contains the most current work, but should still only contain code that allows the App to be built.<br>
The master contains the newest, stable code which can be rolled out and tested on real devices. 

![Branching](/img/branching.PNG)



## Releases
Alpha releases are automatically created by merging the dev into the master branch. This increments the version number and puthe new version to the shes tester devices.