---
layout: post
title: 'My Mac Setup'
tags:
- osx
- software
---

I get asked from time to time how I have things set up. Here's a high-level checklist of most of the main things I do to a new Mac and the tools I use regularly.

<!--more-->

## Operating System

*   Install OSX
*   Turn on extra mouse gestures 
    *   Settings > Trackpad
*   Turn on Firewall 
    *   Settings > Security & Privacy > Firewall
    *   Also enable Stealth mode (in Firewall Options)
*   Turn on FileVault 
    *   Settings > Security & Privacy > FileVault
*   Configure Finder 
    *   Finder > Preferences > General 
        *   Turn off all “Show these items on the desktop”
    *   Finder Preferences > Sidebar 
        *   Check Devices > [ComputerName]
        *   Uncheck “Recent Tags”
    *   Finder > Preferences > Advanced 
        *   Check Empty Trash securely
    *   System Preferences > General 
        *   Sidebar icon size: Small
*   Kill Dashboard 
    *   `defaults write com.apple.dashboard mcx-disabled -boolean true`
    *   `killall Dock`
*   Configure Spaces 
    *   System Preferences > Mission Control 
        *   Uncheck Automatically rearrange Spaces based on most recent use
*   Safari 
    *   Extensions 
        *   [Ghostery][1]
        *   [Pocket][2]
        *   [Duck Duck Go][3]
        *   [Click to Flash][4]
        *   [Ultimate Status Bar][5]
        *   Google Hangouts plugin
        *   [AdBlock Plus][6]
        *   [ResizeMe][7]
    *   Config 
        *   Menu 
            *   Show tab bar
            *   Hide bookmarks bar
        *   Preferences 
            *   General 
                *   New windows open with: Empty Page
                *   New tabs open with: Empty Page
                *   Autofill
                *   Turn off all options
            *   Privacy 
                *   Limit website access to location services: Prompt for each website one time - only
                *   Website tracking: Ask websites not to track me
                *   Smart Search Field: Do not preload Top Hit in the background
            *   Advanced 
                *   Show Develop menu in menu bar
*   Run Software Update
*   Dictation 
    *   System Preferences > Dictation & Speech 
        *   Dictation: On
        *   Use Enhanced Dictation
        *   Shortcut: Press Either Command Key Twice

## Utilities

*   [Dropbox][8]
*   [GoogleDrive][9]
*   [1Password][10] 
    *   Install browser extension for Safari
*   [Alfred][11] 
    *   System Preferences > Spotlight 
        *   Uncheck Spotlight menu keyboard shortcut
    *   Alfred Preferences > General 
        *   Alfred Hotkey: Command-Space
*   [Flux][12]
*   [iStat Menus][13]
*   [Contacts Cleaner][14]
*   [Hazel][15]
*   [Delibar][16]
*   [CheatSheet][17]
*   [Dash][18] 
    *   Download needed/desired docsets
*   [TimeSink][19]
*   [GeekTool][20]
*   [TextExpander][21]
*   [Healthier][22]
*   [Knock][23]
*   [Evoluent Drivers][24]
*   \[ScanSnap ix500\](http://www.fujitsu.com/global/services/computing/peripheral/- scanners/product/ix500)
*   [CloudApp][25]
*   [Onyx][26]
*   [Bartender][27]

## Internet

*   [Airmail][28]
*   [Twitterrific][29]
*   [Skype][30]
*   [Radium][31]
*   [Textual IRC Client][32]
*   [Transmission][33]
*   [Google Chrome][34]

## Productivity

*   [OmniGraffle][35]
*   [OmniFocus][36]
*   [MS Office][37]
*   Pages
*   Numbers
*   Keynote
*   [MindNode Pro][38]
*   [Soulver][39]
*   [PDFPen Pro][40]
*   [DayOne][41]
*   [Marked][42]
*   [Fantastical][43]
*   [Screenflow][44]

## DevTools

*   [TotalTerminal][45]
*   [Xcode][46]
*   [OS X Server][47]
*   \[Update OSX Server (via MacPorts)\] (http://www.gigoblog.com/2013/11/14/install-memcache-and-apc-on-mavericks-server-3-mac-os-x-10-9/)
*   [MySQL Community Server for OSX][48] 
    *   [Extra installation instructions][49]
*   [VirtualBox][50]
*   [Tower][51]
*   [SequelPro][52]
*   [Vagrant][53]
*   [Homebrew][54]
*   [Composer][55]
*   [Drush][56]
*   [SublimeText 3][57] 
    *   SublimeText 3 Configuration
    *   Enable key repeat in OSX: https://gist.github.com/kconragan/2510186 
        *   `defaults write com.sublimetext.3 ApplePressAndHoldEnabled -bool false`
    *   SublimeText 3 Plugins 
        *   [Plugin Manager][58]
        *   [MarkdownEditing][59]
        *   [Theme Soda][60]
        *   [Tomorrow Color Schemes][61]
        *   [BracketHighlighter][62]
        *   [GitGutter][63]
        *   [DocBlockr][64]
        *   [Sublime Linter][65]
        *   [Xdebug Client][66]
        *   [SublimeCodeIntel][67]
        *   [Sublime-Phpcs][68]

SublimeText 3 Preferences:

    {
    "color_scheme": "Packages/Tomorrow Color Schemes/Tomorrow-Night-Bright.tmTheme",
    "default_line_ending": "unix",
    "ensure_newline_at_eof_on_save": true,
    "fallback_encoding": "UTF-8",
    "ignored_packages":
    [
    ],
    "rulers":
    [
    80
    ],
    "shift_tab_unindent": true,
    "soda_classic_tabs": false,
    "soda_folder_icons": true,
    "tab_size": 2,
    "theme": "Soda Light.sublime-theme",
    "translate_tabs_to_spaces": true,
    "trim_automatic_white_space": true,
    "trim_trailing_white_space_on_save": true,
    "use_tab_stops": true,
    "word_separators": "./\\()\"'-:,.;<>~!@#%^&*|+=[]{}`~?"
    }
    

## Personal

*   [MacFamilyTree][69]
*   iPhoto
*   iMovie
*   GarageBand
*   [Last.fm][70]
*   [MacFamilyTree][69]
*   [Pixelmator][71]
*   [Paprika][72]
*   [Pocket][73]

 [1]: https://www.ghostery.com
 [2]: http://help.getpocket.com
 [3]: https://duck.co/help/desktop/safari
 [4]: http://hoyois.github.io/safariextensions/clicktoplugin
 [5]: http://ultimatestatusbar.com
 [6]: https://adblockplus.org/en/safari
 [7]: http://aaronholla.webs.com
 [8]: https://www.dropbox.com
 [9]: https://drive.google.com
 [10]: https://agilebits.com/onepassword
 [11]: http://www.alfredapp.com
 [12]: https://justgetflux.com
 [13]: http://bjango.com/mac/istatmenus
 [14]: http://spanningtools.com/mac
 [15]: http://www.noodlesoft.com/hazel.php
 [16]: http://www.delibarapp.com
 [17]: http://www.cheatsheetapp.com/CheatSheet
 [18]: http://kapeli.com/dash
 [19]: http://manytricks.com/timesink
 [20]: http://projects.tynsoe.org/en/geektool
 [21]: http://smilesoftware.com/TextExpander/index.html
 [22]: http://healthier.lessapps.net
 [23]: http://www.knocktounlock.com
 [24]: http://www.evoluent.com/download.htm
 [25]: http://www.getcloudapp.com
 [26]: http://www.onyxmac.com
 [27]: http://www.macbartender.com
 [28]: http://airmailapp.com
 [29]: http://twitterrific.com/ios
 [30]: http://skype.com
 [31]: http://catpigstudios.com
 [32]: http://www.codeux.com/textual
 [33]: http://www.transmissionbt.com
 [34]: https://www.google.com/chrome/browser
 [35]: https://www.omnigroup.com/omnigraffle
 [36]: https://www.omnigroup.com/omnifocus
 [37]: http://www.microsoft.com/mac
 [38]: http://mindnode.com
 [39]: http://acqualia.com/soulver
 [40]: http://www.smilesoftware.com/PDFpenPro
 [41]: http://dayoneapp.com
 [42]: http://marked2app.com
 [43]: http://flexibits.com/fantastical
 [44]: http://www.telestream.net/screenflow/overview.htm
 [45]: http://totalterminal.binaryage.com
 [46]: https://developer.apple.com/xcode
 [47]: https://www.apple.com/osx/server
 [48]: http://dev.mysql.com/downloads/mysql/
 [49]: http://akrabat.com/computing/setting-up-php-mysql-on-os-x-mavericks/
 [50]: https://www.virtualbox.org
 [51]: http://www.git-tower.com
 [52]: http://www.sequelpro.com
 [53]: http://www.vagrantup.com
 [54]: http://brew.sh
 [55]: https://getcomposer.org
 [56]: https://github.com/drush-ops/drush
 [57]: http://www.sublimetext.com/3
 [58]: https://sublime.wbond.net/installation
 [59]: http://sublimetext-markdown.github.io/MarkdownEditing
 [60]: https://github.com/buymeasoda/soda-theme
 [61]: https://github.com/theymaybecoders/sublime-tomorrow-theme
 [62]: https://github.com/facelessuser/Brac[ketHighlighter
 [63]: http://www.jisaacks.com/gitgutter
 [64]: https://sublime.wbond.net/packages/DocBlockr
 [65]: https://github.com/SublimeLinter/SublimeLinter3
 [66]: http://www.sitepoint.com/debugging-xdebug-sublime-text-3
 [67]: https://sublime.wbond.net/packages/SublimeCodeIntel
 [68]: http://www.soulbroken.co.uk/code/sublimephpcs
 [69]: http://www.syniumsoftware.com/macfamilytree
 [70]: http://www.last.fm/download
 [71]: http://www.pixelmator.com
 [72]: http://www.paprikaapp.com
 [73]: http://getpocket.com