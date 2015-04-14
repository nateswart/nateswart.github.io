---
layout: post
title: 'Work and Rest'
tags:
- alfred
- workflow
- applescript
---

Here’s a quick [Alfred][1] workflow I made up to handle starting and ending the workday.

<!--more-->

![Alfred Work-flow][2]

There are two commands. Both are just super simple AppleScripts:

## Work

1.  Enabled work-related IM accounts
2.  Enabled work-related Mail accounts
3.  Activate OmniFocus
4.  Activate Calendar
5.  Activate Skype
6.  Fire notification

**work.applescript:**

    tell application "Messages"
        log in service "<work-account1>"
        log in service "<work-account2>"
    end tell
    
    tell application "Mail"
        set enabled of account "<work-account>" to true
    end tell
    
    tell application "OmniFocus"
        activate
    end tell
    
    tell application "Calendar"
        activate
    end tell
    
    tell application "Skype"
        activate
    end tell
    
    display notification "Ready to go"  with title "Time to work"
    

## Rest

1.  Disable work-related IM accounts
2.  Disable work-related Mail accounts
3.  Quit OmniFocus
4.  Quit Calendar
5.  Quit Skype
6.  Fire notification

**rest.applescript:**

    tell application "Messages"
        log out service "<work-account1>"
        log out service "<work-account2>"
    end tell
    
    tell application "Mail"
        set enabled of account "<work-account>" to false
    end tell
    
    tell application "OmniFocus"
        quit
    end tell
    
    tell application "Calendar"
        quit
    end tell
    
    tell application "Skype"
        quit
    end tell
    
    display notification "It's time to relax"  with title "Breathe"

 [1]: http://www.alfredapp.com
 [2]: /public/post-images/2014/alfred_workflow.jpg