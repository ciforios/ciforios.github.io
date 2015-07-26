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
	- When we first started started setting up Gerrit, we  (naively) assumed it would just work, and that everything would be set up for an easy integration with Jenkins. The things that especially threw us back were the [verified label bug](/Gerrit-for-jenkins/#verifiedLabel) and the missing integrated authentication management.
- Is highly configurable
- Adds complexity to the pipeline
- Needs some training time
- Needs external authentication
- Deleting projects not possible by design
- Does add quality assurance layer