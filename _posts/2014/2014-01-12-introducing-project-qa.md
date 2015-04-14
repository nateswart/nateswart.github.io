---
layout: post
title: 'Introducing Project QA'
tags:
- development
- metrics
- drupal
- php
- projectqa
---

Ever wish there was a better way to keep an eye on a project you're working on? After being inspired by [this presentation at Drupalcon Portland][1] I decided to create a Drupal module to help automate the code evaluation process: Project QA.


* * *

This is part 1 of a 3 part series overviewing the Project QA Drupal module:

*   Introducing Project QA
*   [Introducing Project QA: Part 2 (Writing a submodule)][2]
*   [Introducing Project QA: Part 3 (With great power)][3]

* * *

*Don't want to read? Skip ahead, there's a video introduction and demo!*

## Overview

At its heart, Project QA is a Drupal module that scans git repos and offers hooks for processing them. By itself, Project QA does not evaluate your code at all.

When you tell Project QA to scan a repo, it checks the repo out locally (or updates it if it already has a copy from a previous run), and then begins stepping backwards through the git history one commit at a time. A record of the commit is saved, including the commit hash, the timestamp of the commit, and the author of the commit. After each commit is checked out a hook is fired to allow submodules to act on the repo in its current state. After all commits have been processed, Project QA evaluates the existing tags in the repo and matches them up with the imported commits.

It is pretty generic except for one major condition: every action or piece of data is always linked back to a specific git commit. The code being evaluated doesn't need to be Drupal code, or even PHP code; as long as it exists in a git repo you can access.

## Submodules

The real fun begins when you consider submodules. With this initial release I've included one submodule based on the [PHPLOC][4] tool. PHPLOC "is a tool for quickly measuring the size and analyzing the structure of a PHP project." One of its great strengths is measuring [cyclomatic complexity][5] alongside a host of stats about the number of files, methods, lines of code, comments, etc.

The PHPLOC submodule uses the Project QA hook to run on every commit in a repository's history. All data is saved into custom entities, as well as delta information from between git commits for faster and easier reporting. All of this information is exposed to views so writing custom reports is easy.

Some report ideas include:

*   Who is introducing the most complexity (for good or bad)?
*   Is code being checked in regularly during a project?
*   How does a particular module stack up against others?
*   Are your developers commenting their code enough?
*   Were there any major changes or spikes in the history of the code, indicating things such as a bad merge, extra modules or files, or maybe an onslaught of sloppy or duplicate code?

## Plans

I have plans for implementing submodules to run other PHP tools like the copy-paste detector, mess detector, and perhaps even code sniffer. Beyond that I'd love to see JavaScript evaluations taking place in submodules as well. I've also wanted to make this as easy as possible for writing your own reports but know that including some default common reports to get you started is beneficial as well. In that vein, if you have suggestions let me know!

You can check out [the project page on Drupal.org][6].

## Demo

<iframe width="560" height="315" src="//www.youtube.com/embed/Ab_r0bNAYUA" frameborder="0" allowfullscreen></iframe>

 [1]: https://portland2013.drupal.org/node/1078
 [2]: /2014/01/21/introducing-project-qa-part-2/
 [3]: /2014/01/27/introducing-project-qa-part-3/
 [4]: https://github.com/sebastianbergmann/phploc
 [5]: http://en.wikipedia.org/wiki/Cyclomatic_complexity
 [6]: http://drupal.org/project/projectqa