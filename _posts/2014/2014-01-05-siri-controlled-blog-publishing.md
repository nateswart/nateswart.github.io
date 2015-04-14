---
layout: post
title: 'Siri-controlled Blog Publishing'
tags:
- workflow
- automation
- drafts
- dropbox
- hazel
- ifttt
- iphone
- launchcenterpro
- reminders
- siri
---

Hot on the heels of setting up my [markdown-dropbox-blog][1] workflow, I realized I needed a more reliable way to regenerate and rsync the rendered files. The workflow I had set up worked fine for new articles, but not for edits to already-published articles, it assumed I wanted to publish immediately, and didn't offer any easy way to handle any sort of failure.

What I came up with seems like the digital equivalent of a [Rube Goldberg machine][2] but it works and affords flexibility for automating other tasks as well. Besides, [Rube Goldberg machines are awesome][3].

tl;dr - Simply hit a button or say "Siri, add refresh blog to the automation list" and sit back while your Jekyll-based blog rebuilds and republishes itself.

<!--more-->

* * *

*Update 2014-01-12: [A Far More Direct Siri Blog Publishing Method][4]*

* * *

Maybe you'd like a demo before we start?

<iframe width="560" height="315" src="http://www.youtube.com/embed/LMA6SMZJ41k?vq=hd720" frameborder="0" allowfullscreen></iframe> 
The basic workflow goes as follows:

1.  Create a "job" (task) via Siri, Launch Center Pro, or in Reminders.app directly.
2.  IFTTT notices a new task has been added, and converts it to a text file on Dropbox.
3.  Dropbox syncs the file to my Mac mini.
4.  Hazel sees the new file and fires off an AppleScript to process the file and then archive it as a sort of log.
5.  The AppleScript can do any number of things, but in thus scenario it builds the Jekyll site and rsyncs it to my server.

![Workflow diagram][5]

## Creating the "job"

As you may notice later in the process, the first few steps could be eliminated by going to Dropbox directly. I chose to inject these steps for two main reasons; so I could leverage Siri to kick off jobs (common, thats just plain cool) and so I could keep a consistent interface across (potentially) multiple workflows.

The first step is to create a new task list in Reminders called "Automation" (or whatever you want). Any job you want to automate want ultimate be recorded in this list as a sort of queue. You have a few options to get tasks in this list beyond adding tasks directly to Reminders.

### Siri

Very simple. Just kick off Siri and say something like "Add refresh blog to the automation list"

Siri will then add a task to the "Automation" list entitled "refresh blog". Boom. You're living in the future.

### Launch Center Pro (and Drafts)

The other way to kickstart this process is to use [Launch Center Pro][6] and [Drafts][7]. If you're not familiar with these apps, URL schemes in iOS, or putting them all together then I highly recommend you go read [this post by Federico Viticci][8]. This option is a bit more involved to set up however you end up with a simple button to push and a higher level of reliability; Siri doesn't always cooperate with me.

The Launch Center Pro action you'll want to set up goes like this:

Name: Refresh blog

URL: `{% assign action = '{{List in Reminders}}' %}`

    drafts://x-callback-url/create?text=%23Automation%0A
    Refresh%20blog&action={{ action }}&x-success=launchpro:&key=xxx
    

The action parameter tells Drafts you want it to use the text value and create an entry in the Reminders app. {{List in Reminders}} is the name of a Drafts-default action to do this. This particular action will take a text block in this format:

    # Automation
    refresh_blog
    

and create a Reminder task out of it. The first line with # specifies the list to put it in (Automation) and the second line specifies the name of the task. `%23Automation%0ARefresh%20blog` is the URL-encoded version of that. The `x-success=launchpro:` value tells Drafts to kick you back to Launch Center Pro when it's done with the action. Drafts allows you to specify a private key value to launch actions. I recommend setting this up (and then specifying it in this URL) to protect yourself.

Now, when you hit a button in Launch Center Pro you'll be quickly sent to Drafts where it will create a Reminder task for you, then kick you back to where you started.

## IFTTT

So you've got a task in Reminders, what's next? IFTTT ... [for iOS specifically][9]. IFTTT has a trigger for new tasks in Reminders. Here is what I set up:

![IFTTT rule for new automation reminders][10]

Not much more here. When IFTTT sees a new task in the Automation list in Reminders, it writes those values to a file in the specified folder on Dropbox.

There is one caveat: IFTTT can't always run realtime. If it's not actively running it leverages geofencing to know when it should evaluate local tasks. If I'm on the move and need a mobile task trigger this is fine. If I'm at home I am currently just accepting this limitation knowing the rule will fire later. If I need it fired immediately I can always launch the IFTTT app, or hey ... just run the Jekyll build/rsync command myself from a Terminal window.

Moving on ...

## Dropbox

Dropbox syncs the file IFTTT wrote over to my Mac mini. Quick-n-simple.

## The Hazel Rule

Hazel is watching the Dropbox folder that IFTTT writes to. Here is the rule I set up:

![Hazel blog rule][11]

'Processed' is the name of a sub-folder I have in that directory. I don't want that folder to be touched hence the extra rule check at the beginning.

You can see that the last two steps of the rule is to rename (based on date and time) the task file and move it to a date-based sub-folder under 'Processed'. This means I have a log I can check if anything goes wrong.

The embedded AppleScript reads as follows:

    -- Find out what to do
    tell application "Finder" 
        set filename to name of theFile set AppleScript's text item delimiters to "." 
        set pieces to filename's text items set automationCommand to text item 1 of pieces
    end tell
    
    -- Action 
    set automationScript to "/Users/clu/Dropbox/Toolbox/AppleScripts/" & automationCommand & ".scpt" set scpt to POSIX file automationScript
    
    run script scpt
    
    -- Now remove the finished task 
    tell application "Reminders" 
    
        -- Put the space back in the task name (IFTTT replaced it with an underscore) 
        set AppleScript's text item delimiters to "_" 
        set tempList to every text item of automationCommand 
        set AppleScript's text item delimiters to " " 
        set theText to the tempList as string 
        set AppleScript's text item delimiters to "" 
        set reminderTask to theText
    
        delete reminder reminderTask
    
    end tell
    

The two big takeaways here are:

1.  I set up a standard to call separate AppleScripts based on the name of the task. I know my refresh blog task will always be written to Dropbox as `refresh_blog.txt`. That filename gets passed in to this script where I pull out just the name portion and map it to a corresponding Applescript, `refresh_blog.scpt`.
2.  Once the external script has been called I want to clean things up. The last part of this script reaches back in to the Reminders app (synced to the Mac mini via iCloud) and deletes the task it just processed. This brings us full-circle and keeps things from becoming cluttered.

## AppleScripts

My big plans stem from #1 above; this system is generic enough to let me expand it to automate a lot of other tasks as well. Because my folder for AppleScripts is actually stored on Dropbox all I need to do is write a new appropriately named AppleScript on any of my machines and save it. Suddenly, I can start sending new tasks to it via Siri if I wish.

Currently, there is only one additional script: `refresh_blog.scpt` and it is **very** simple:

    tell application "Terminal"
        activate
        do script "cd PATH_TO_YOUR_JEKYLL_SITE && jekyll build && rsync -avzr --delete PATH_TO_YOUR_JEKYLL_SITE -e ssh YOUR_USER@YOUR_SERVER:/PATH_TO_YOUR_WEBROOT/ && exit"
    end tell
    

And there you have it. One-button (or voice-activated) Jekyll blog publishing!

 [1]: /2013/12/24/branching-out/
 [2]: http://en.wikipedia.org/wiki/Rube_Goldberg_machine
 [3]: http://www.youtube.com/watch?v=qybUFnY7Y8w
 [4]: /2014/01/12/a-far-more-direct-siri-blog-publishing-method/
 [5]: /public/post-images/2014/siri-blog.png
 [6]: http://contrast.co/launch-center-pro/
 [7]: http://agiletortoise.com/drafts/
 [8]: http://www.macstories.net/tutorials/use-whatsapps-url-scheme-with-drafts-launch-center-pro-or-a-bookmarklet/
 [9]: https://itunes.apple.com/us/app/ifttt/id660944635?mt=8
 [10]: /public/post-images/2014/Reminders-IFTTT.png
 [11]: /public/post-images/2014/hazel-blog-rule.png