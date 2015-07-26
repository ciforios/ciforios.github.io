---
layout:     post
title:      "What we learned about Gerrit"
subtitle:	""
date:       2015-05-24 15:20:05
author:     "The Crew"
header-img: "img/lesson-learned.jpg"
tags: [lessons-learned, code-review]
---

## A quick summary about what we learned about Gerrit

- Does not work "out of the box"
	- When we first started started setting up Gerrit, we  (naively) assumed it would just work, and that everything would be set up for an easy integration with Jenkins. The things that especially threw us back were the [verified label bug](/2015/06/02/Gerrit-for-jenkins/Gerrit-for-jenkins/#verifiedLabel) and the missing integrated authentication management.
- Is highly configurable 
     - You can configure gerrit to your very needs. Especially if you have many projects with different hirarchical permission structures, gerrit allows for efficient management. 
- Adds complexity to the pipeline 
     - Wehereas with git you mostly deal with pull, push, commit and merge, with gerrit you also have to deal with git review, commit msg hooks, PatchSets...
- Needs some training time   
     - the "git review" part and the whole process of code review took us some time of getting used to, and understanding what happens. This is also something, that all developers have to go through.
- Needs external authentication
- Deleting projects not possible by design
- Does add quality assurance layer
	 - By forcing/allowing developers to let others take a look at their work, before it actually gets pushed into the project, the code quality and conventions can be enforced more easily.