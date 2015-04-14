---
layout: post
title: 'Introducing Project QA: Part 2 (Writing a submodule)'
tags:
- development
- metrics
- drupal
- php
- projectqa
---

Let\'s walk through building a submodule for Project QA, shall we?

* * *

This is part 2 of a 3 part series overviewing the Project QA Drupal module:

*   [Introducing Project QA][1]
*   Introducing Project QA: Part 2 (Writing a submodule)
*   [Introducing Project QA: Part 3 (With great power)][2]

* * *

Unfamiliar with Project QA? You can check out [the project page on Drupal.org][3].

There's three main steps to implementing your own extension to projectqa:

1.  Create a fresh module
2.  Create entities to store your data
3.  Implement `hook_eval_gitcommit`

## Set up your module

Creating a new module is outside the scope of this post. If you are new to module development or need a refresher, head over to drupal.org for [all the resources][5].

I am curious what modules people are working on, though. if you start one I'd love to hear about it. It may be something valuable to a wide enough audience to consider including in the main module.

## Create entities to store your data

This part of projectqa is intentionally left wide open. You are expected to develop the entities to store your data. This also means you have complete control over the structure and accessing abilities of that data. I highly recommend leveraging the [Entity API][6] module. It will make your life easier as well as the lives of anyone building off of your work. Additionally it's already a dependency for projectqa so you'll have access to it on any system that you're building your projectqa submodule for.

Consider how you want to leverage your data but also try to keep it as normalized as possible. For PHPLOC I decided to store in two tables; one table for the extracted data and one table for the delta data that was calculated. Putting it all in one table would've made a far too large table as well as too much information if I'm only interested in the delta. A bit more description on this will be in the next step.

## Implement hook_eval_gitcommit

    hook_eval_gitcommit($repo_path, $git_commit)
    

This hook gets fired by the main projectqa module on each git commit in the history of a repo. You don't need to worry about walking the repo history, that is taking care of for you. You also don't need to execute any git commands as the repo is already checked out to the proper location for you.

### Parameters

**$repo_path:** The system path where the repo is located.

**$git_commit:** The git commit to process.

The most important piece of information is the repo path that gets passed to you. This tells you were on the filesystem to look in order to start your processing of the code. Be sure not to alter any of the files as that would pollute the code to be processed for both your module and any other module accessing that git commit after your code is executed.

The git commit hash that is passed to you is more of an optional piece of information. You don't need to do anything with it unless it is valuable to whatever data processing algorithm you are utilizing. The git commit hash is already being saved to the projectqa_gitcommit table for you.

In the case of the projectqa_phploc submodule I was interested in calculating the deltas between commits and storing them so reporting could be easier and more performant. In order to accomplish this, I made this call from within my hook implementation:

    function projectqa_phploc_eval_gitcommit($repo_path, $git_commit) {
      // some code ...
       $parent_hash = projectqa_get_parent_hash($repo_path, $git_commit->sha1);
      // some more code ...
    }
    

This way I can now access the correct records in my own table for the previous commit (remember, do not alter the file system or execute git commands) and generate the diff against my current commit and save to the database along with my current values. For better organization and scaleability I keep all delta values in a separate table (entity).

If you end up developing a submodule for projectqa be sure to stay in contact and keep an eye out for updates. I already have plans for a few more hooks to implement that may help a number of developers. I will also be implementing some functionality to help validate, reprocess, and catch up data if needed.

 [1]: /2014/01/12/introducing-project-qa/
 [2]: /2014/01/27/introducing-project-qa-part-3/
 [3]: http://drupal.org/project/projectqa
 [5]: https://drupal.org/developing/modules
 [6]: http://www.drupal.org/project/entity