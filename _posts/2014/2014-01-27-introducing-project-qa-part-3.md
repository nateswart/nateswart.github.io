---
layout: post
title: 'Introducing Project QA: Part 3 (With great power)'
tags:
- development
- metrics
- drupal
- php
- projectqa
---

As I developed this module I became more and more excited about what these tools I kept finding could do if I were to integrate them. In discussing ideas with colleagues there was a central theme that kept coming up and was said best by [Peter Parker][1]:

> With great power comes great responsibility.

* * *

This is part 3 of a 3 part series overviewing the Project QA Drupal module:

*   [Announcing Project QA: Part 1 (Introductions)][2]
*   [Announcing Project QA: Part 2 (Writing a submodule)][3]
*   Announcing Project QA: Part 3 (With great power)

* * *

Unfamiliar with Project QA? You can check out [the project page on Drupal.org][4].

My goal in creating this module was to make some of the programming process a bit more transparent as well as quantifiable. With a few missteps in creating sample reports to demo to people I quickly realized how easy it would be to 1) use this as a litmus test and 2) deduce inaccurate meaning potentially leading to 3) unfortunate decisions and consequences.

To be more specific; I became aware of how this should **not** be used to determine someone's employability or value. That is not to say that it can't help educate a decision, but rather just that this tool should not be the judge and jury. Its intended purpose and most complimentary role is to help teams gain a higher level picture and historical understanding over their own or inherited projects. This understanding with undoubtedly raise questions and draw attention to certain aspects of a project, prompting further investigation. I find this to be both appropriate and healthy.

Let's take a quick example. Suppose you are comparing two developers on a project to see how they are performing. You find that both are checking in code regularly, commenting appropriately, and even producing roughly the same amount of code. However you see a major difference in code complexity. One developer's code is maintaining fairly consistent complexity levels (easy to maintain) while the other's code is rising steadily in complexity. Your initial concern could be that the code is not being structured properly or will be far too difficult to make changes to at a later date.

But what if there is something else going on? What if you forgot to consider the breakdown in roles between the two developers; one was responsible for writing simple helper functions while the other was implementing some pretty hairy business logic being handed to them via complex requirements? What actually may be happening here is not an indictment of each developer's skill but rather the manifestation of a requirements gathering phase that didn't expose some contradictory functionalities. The report itself is still proving to be very valuable, but as with anything involving interpretation it is essential to tread cautiously.

Another topic has come up in discussion as well. One of the great ideas shared with me was to use this tool as a gatekeeper of sorts to validate thresholds before allowing pushes to production. This can offer a great deal of stability to a project. It can also have two opposite side effects; a false sense of security and a roadblock preventing essential code from being deployed. In either case, nothing can replace a solid code review process. This tool definitely has a role but it should be in helping a code reviewer look in to various aspects of a project and glean insight, not replacing the code reviewer all together.

 [1]: http://en.wikiquote.org/wiki/Spider-Man_%28movie%29
 [2]: /2014/01/21/introducing-project-qa/
 [3]: /2014/01/21/introducing-project-qa-part-2/
 [4]: http://drupal.org/project/projectqa