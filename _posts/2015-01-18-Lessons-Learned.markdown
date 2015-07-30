---
layout:     post
title:      "Do I need this?"
subtitle:	"It depends ..."
date:       2015-01-18 12:22:00
author:     "The Crew"
tags: [lessons-learned]
---

The tools we used can be really powerful if configured and used correctly. But they can also make your workflow more complicated.<br>
The biggest benefits of such a pipeline are the increased code quality and the automated building, testing & deploying of the project.<br>
If you are developing on your own or in a very small team though, the whole pipeline might be too much overhead, because of the additional time required to set up the pipeline and the overhead of using code review.<br>
On the other hand, once the pipeline is configured, it can be relatively easily adapted for the usage in new projects. <br>

In retrospect we also have to admit, that we had problems at some points, that could have been avoided if someone would already have had experience with Jenkins and Gerrit. Setting up a completely new CI pipeline with the knowledge we have now would be much easier and could probably be achieved within a couple of days.<br>
So in case you have someone in your team who has already set up Jenkins or Gerrit at some point, creating a CI pipeline even for relatively small projects and teams might be worth it.

To sum it up: A CI pipeline, as the one described on this site, can drastically increase code quality and can help to ensure always having buildable code in the repository. If you have longer term projects with relatively stable tools, CI is probably very helpful for you. If you are developing small projects or prototypes, where you need fast setup and fast iterations you might do better without it.