---
layout: post
title: 'Create Reminder Tasks from Email'
tags:
- applescript
- automation
- launchd
- mail
- reminders
- workflow
---

For a while I've wanted to be able to add emails to whatever task manager I'm using, from any device I'm using. Currently I'm keeping things simple by using the default Reminders app for OSX and iOS, but this solution could work for any task management app that has an OSX counterpart and supports AppleScript.

I didn't come up with this script entirely on my own, but I did customize it, alter the overall workflow, and work through some Gmail + Mavericks issues (now I'm starting to understand why Gmail's IMAP bastardization is a real pain).

The process is pretty simple:

1.  Flag an email you want to have turned into a task
2.  Archive the email [^gmail]
3.  Go about your business

[^gmail]: Gmail and IMAP caused some real issues in Mail.app in Mavericks resulting in me being unable to properly archive the email via the AppleScript. The script pulls all flagged emails out of "All Mail", so you can safely archive it out of your inbox knowing it will still be processed.

On my Mac mini I have running at home, I set up Reminders (already set up from my crazy [Siri-controlled Blog Publishing][1] post) and Mail.app with my standard email accounts configured.

The key piece is the AppleScript that takes all flagged emails, creates a Reminders task out of them, and then un-flags them. Here it is:

    #!/usr/bin/osascript on run

    -- This script is designed to work with Gmail and OSX Mavericks
    
    
    -- Make sure Mail.app is actually running
    if not (application "Mail" is running) then
      return
    end if
    
    -- Make sure Reminders.app is actually running
    if not (application "Reminders" is running) then
      return
    end if
    
    -- We'll put a double newline between segments of the message in the notes field
    set newline to (ASCII character 10) & (ASCII character 10)
    
    tell application "Mail"
    
      -- Look through all email accounts
      repeat with _account in imap accounts
    
        set _inbox to _account's mailbox "[Gmail]/All Mail"
    
        -- Get a list of all flagged messages for this box
        set _messages to (a reference to (every message in _inbox whose flagged status is true))
        set _msglist to contents of _messages
    
        -- Walk through all flagged messages in this box
        repeat with _message in _msglist
          set fromMsg to (extract name from sender of _message as string)
          set subjMsg to (subject of _message as string)
          set msgID to message id of _message
          set msgBody to content of _message
    
          tell application "Reminders"
            make new reminder with properties {name:subjMsg, body:"From: " & fromMsg & newline & msgBody & "message://%3c" & msgID & "%3e"}
          end tell
    
          -- unflag the message
          set flagged status of _message to false
        end repeat
    
      end repeat
    end tell
    

    end run

That will check all enabled accounts. If you want to only process one account you'll have to modify the script a bit. You can adjust what goes in the notes field as well if you want (msgBody). I opted to copy in the text of the entire email in case I needed to reference it while I was on the go. The link to the original email is at the bottom, but that only works on OSX. I also tried to keep the From text short (and stripped out the email address) so that the display in Reminders is more readable.

To get the AppleScript running periodically to check do this task you'll need to set it up to run via launchd or cron. I'm more familiar with cron, but it seems as though Apple leaning towards launchd and adding additional functionalities. I figured this would be a good simple task to learn launchd on so I'll have it in my toolbelt for later on.

What you need to do is create a new .plist file in ~/Library/LaunchAgents. Mine is named `com.nateofnine.FlaggedEmailToReminders.plist` and looks like this:

        <?xml version="1.0" encoding="UTF-8"?>
        <!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
        <plist version="1.0">
        <dict>
                <key>Disabled</key>
                <false/>
                <key>Label</key>
                <string>com.nateofnine.FlaggedMailToReminders</string>
                <key>Program</key>
                <string>/usr/bin/osascript</string>
                <key>ProgramArguments</key>
                <array>
                        <string>osascript</string>
                        <string>/PATH_TO_YOUR_APPLESCRIPT/flagged_mail_to_reminders.scpt</string>
                </array>
                <key>RunAtLoad</key>
                <true/>
                <key>StartInterval</key>
                <integer>60</integer>
        </dict>
        </plist>
    

Now all you need to do is log out and back in and this will start executing your AppleScript every 60 seconds!

 [1]: /2014/01/05/siri-controlled-blog-publishing/