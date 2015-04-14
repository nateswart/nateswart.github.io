---
layout: post
title: 'Branching Out'
tags:
- news
- byword
- dropbox
- hazel
- octopress
- textexpander
- workflow
---

Don't be fooled. I still love Drupal.

However, a perfect storm hit me:

*   some recent discussions with folks about how the Drupal community can be rather insulated and myopic
*   my need for a new blog
*   a my desire to use [Markdown][1] and some iOS tools
*   was curious about static site generators
*   vacation time!

So I decided to branch out a bit and just play. What I've come up with so far is a combination of [Byword][2], [Dropbox][3], [Hazel][4], [Octopress][5], and rsync with SSH keys. It may be easiest to see the overview first ...

<!--more-->

* * *

*Update 2013-12-25: Of course this is already outdated, as I've switched to using [Jekyll][6] directly instead of the Octopress wrapper around it. It's largely the same, though. I'm going to play a bit, come up with some more automations, and then post a followup at some point the future after the dust from my playing settles down.*

* * *

![Blogging system overview][7]

The basic workflow goes like this:

1.  I write a post in Markdown using Byword. I love the consistency of being able to use the same app on my iPhone, iPad, and Macbook Air.
2.  When I'm ready to publish I move the file from any of my devices into a specific folder on Dropbox.
3.  Dropbox syncs this file across all my machines and devices, which includes an old Mac mini I have running in my basement.
4.  The Mac mini has Hazel monitoring this specific folder that has been synced. When Hazel sees a new file (or change to an existing file), it runs the Octopress scripts to regenerate the site and rsync it to my server. ![Hazel screenshot][8]

Now, in order for this to all be seamless I also needed a way to host and reference images (like the diagram in this post) easily. My solution follows a similar, albeit simpler, approach:

1.  I set up a subdomain just for images (images.nateofnine.com)
2.  I set up another Dropbox folder for images and another Hazel rule to watch it
3.  When Hazel notices a new file it files the image away into a date-based subfolder then runs rsync with the server to sync the image up. ![Hazel screenshot][9]
    
    Because I know the file path is predictable i also set up a [TextExpander][10] snippet to create the URL to the image so i could more easily put it in my markdown

There you have it; a flexible, lightweight, fast, secure blogging platform that lets me edit in whatever app I'd like. Of course, as soon as I finished it I thought of 15 more things I can do to enhance it!

 [1]: http://daringfireball.net/projects/markdown/
 [2]: http://bywordapp.com
 [3]: https://db.tt/Ky7oLc1
 [4]: http://www.noodlesoft.com/hazel.php
 [5]: http://octopress.org
 [6]: http://jekyllrb.com
 [7]: /public/post-images/2013/BlogWorkflow.png
 [8]: /public/post-images/2013/refresh_blog.png
 [9]: /public/post-images/2013/upload_image.png
 [10]: http://smilesoftware.com/TextExpander/index.html