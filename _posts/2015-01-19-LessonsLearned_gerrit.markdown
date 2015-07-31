---
layout:     post
title:      "What we learned about Gerrit"
subtitle:	"What can you expect from a code reviewing tool?"
date:       2015-01-19 15:20:05
author:     "The Crew"
header-img: "img/lesson-learned.jpg"
tags: [lessons-learned, code-review]
---

### A quick summary of our experiences with Gerrit

Generally speaking, Gerrit gives you a handy way to create and **manage Git repositories** internally. This means that you won't have to use external services like BitBucket or other similar sites. It offers **web-based code reviewing** as its main feature and excels at that: You can see a side-by-side comparison for any file in a repository, add comments / annotations to submitted work from your fellow developers and enables you to change the source code in the browser before saving it to the repository, if necessary.

We experienced that these features deeply affect the way that the developers work together because of the additional **quality assurance** layer it imposes onto everyone that's involved. One becomes more aware of the fact that others are looking into each other's work and progress is transparent. By forcing / allowing developers to let others take a look into their work before it actually gets pushed into a Git repository, both code quality and compliance to coding conventions can be enforced quite easily. This is particularly helpful for larger projects with many developers because it's so much harder to make a large group respect guidelines. Also, the process of giving each other **feedback** is dealt with quite handily when using Gerrit because individual changes or PatchSets can be commented and given back to the original creator in order to adjust a few things.

Another advantage of using Gerrit is the fact that the system is **highly configurable**: You should easily be able to configure it for your very needs. Ranging from access rights to allowing / prohibiting certain Git commands, configuration can be made to the things you need. Also, if you have many projects with different hierarchical permission structures, Gerrit allows for efficient management.

But then again, there are also some aspects of the systems that might cause problems for users - mostly things that occur when you're initially getting started with the system or when you're first introducing the system into your development team. Firstly, one must keep in mind that switching to Gerrit from nothing - meaning that before, you only used Git locally and each developer pushed / merged for himself - will add quite a bit of **complexity** to your development pipeline. Before, developers will mostly deal with pull, push, commit and merge tasks while Gerrit will make you deal with review, commit message hooks and different version of PatchSets.
In terms of setup, we had to learn the hard way that a complex system like Gerrit simply doesn't work out of the box. While it might be easy to install Gerrit itself, it's a lot harder to integrate it with other systems (in our project, we faced difficulties integrating Jenkins) and will need quite some time and effort to be dealt with. The things that threw us back in particular were the [verified label bug](/2015/01/26/Talking to Jenkins/#verifiedLabel) and the non-existing integrated authentication management.
Furthermore, introducing Gerrit or similar systems will simply take (training) time. The whole process of code reviewing in contrast to pushing code into a repository took us some time getting used to. Understanding the different steps of this new process and understanding what each thing does is something that will have to be internalized by everyone involved.
Another thing that bothered us quite a bit while using Gerrit was the **authentication** problem that forced us to create yet another account on an external website (e.g. Yahoo). And finally, not being able to delete projects in the browser felt very strange and makes you install more plugins that you're not exactly sure about what they really do.