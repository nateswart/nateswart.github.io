---
layout: post
title: 'A Far More Direct Siri Blog Publishing Method'
tags:
- workflow
- applescript
- automation
- siri
- reminders
---

[Previously I set up][1] a Rube Goldberg method of publishing my Jekyll-based blog via Siri. Here's a more streamlined update.

<!--more-->

Every step in the process is a potential breaking point. Fortunately, the two biggest that were breaking on me are also fairly simple to replace. IFTTT works great, but wasn't always real-time. Dropbox had a major outage this week that meant it couldn't be used at all. I replaced both of them with a far more direct AppleScript:

    #!/usr/bin/osascript
    on run
        tell application "Reminders"
            set theList to "Automation"
            repeat with i from 1 to (count of every reminder of list theList)
                set theReminder to reminder i of list theList
                set reminderName to the name of theReminder
                set reminderId to the id of theReminder
                if theReminder is not completed then
                    tell application "Finder" to get folder of (path to me) as Unicode text
                    set workingDir to POSIX path of result
                    set theScript to workingDir & reminderName & ".scpt"
                    run script theScript
                    delete (every reminder whose id is reminderId)
                end if
            end repeat
        end tell
    end run
    

The basic concept is the same, only now instead of creating an IFTTT rule to generate a text file on Dropbox that gets synced to my Mac mini where Hazel notices it and fires off an AppleScript ...

... I have an AppleScript that checks Reminders.app directly and put it on a launchd job to check every 15 seconds, similar to the process I set up in my post [Create Reminder Tasks from Email][2]. Now I'm keying directly off of Reminders.app and have the same flexibility to add new automation tasks at any point.

 [1]: /2014/01/05/siri-controlled-blog-publishing/
 [2]: /2014/01/08/create-reminder-tasks-from-flagged-email/