---
layout: post
title: 'Archiving Web Articles to PDF'
tags:
- automation
- workflow
- fakeapp
- readability
- readkit
- reeder
- tweetbot
---

a.k.a. How I skim, read, and archive information on the web.

The more information I come across the faster and more efficiently I need to be able to separate the wheat from the chaff. Additionally, I need to make each moment worth more; each moment I spend working or scouring the internet as well as each moment I spend with my wife or kids. And whether or not we chose to publicly admit it, we all know down down that we're not efficient multi-taskers and context-switching is very expensive.

So ... here is how I've tried to divide up my time and make my information gathering more effective, efficient, and out of the way.

It all starts with the input. The two main input sources for me are RSS (in your face, Google Reader!) and Twitter. There's no reason you can't have other inputs, these are just the ones I use most. The reasons for software choices will become apparent as I walk through how I process this information.

For Twitter I use [Tweetbot][1]. There are two very straightforward reasons for this:

1.  It's available on all the platforms I use (OSX, iPhone, iPad) and *reliably* syncs my read location across all of them.
2.  It integrates with a variety of read-later services, the use of which becomes essential later in subsequent steps

RSS isn't quite as straightforward but works just as well. My aggregation point is (currently) [Feedly][2] though I do have a license for [Fever][3] that I'm strongly considering a switch to. I use two main apps to read RSS, which doesn't cause a sync problem since any hosted RSS solution has the concept of "read" articles that provides the syncing for you.

On my laptop I use [ReadKit][4], though to be honest I check my RSS news streams on my laptop far less often than on mobile devices. ReadKit connects to a number of RSS hosted aggregators **and** a number of read-later services. Combination options galore!

For the iOS devices I use [Reeder 2][5] which follows the same trend, a lot of various connection options.

At this point in the process what I have is:

*   Two main article/news input sources, RSS and Twitter
*   Apps to read those sources across all my platforms
*   The ability to sync what I've skimmed
*   The ability to send what I want to really read to another (centralized) service. In my case, I've chosen [Readability][6].
*   When I'm reading articles in Readability and want to add them to my personal archive I simply "favorite" them

My basic process is to set time aside to skim through all the inputs. I treat those times as little bonuses throughout my day to take a break and see what's going on in the rest of the world. It really is a "skim" - I usually don't spend much time on this at all. If anything looks like something I want focus on and dive in to I'll send it to Readability for reading when I have more time and focus.

All of this is rather straightforward, until you get to my archival process. There are articles I find that I may want to reference later. I've tried just using Google to bring them back up. What I've found is that between the transient nature of websites and my own lack of memory (let's face it, it my memory was perfect I wouldn't need to refer back to 1 out of a million articles I previously read) my Google foo rarely finds what my conscious mind is vaguely recalling from a distant digital past. My own archive of favorite articles is the only way to reliably retrieve them and limit the search pool so I have a chance of needle-haystack success of finding them. My format of choice for archiving things like this is PDF.

This is where my choice of Readability as a read-later service becomes important. Read-later services usually provide the wonderful service of stripping out all the site-specific graphics and advertisements leaving just the valuable content behind for you to focus on. This feature is perfect for my archiving as well since I'm interested in archiving the information, not the styles and trends (or often times lack-thereof) of web design. Readability was the only service that reliably (and script-ably) could Print-to-PDF this stripped down view of the article.

![Readability export][7]

To accomplish this archiving I use [Fake][8]. I don't use Fake for a lot of things, but when I do it's invaluable. Most times it is in lieu of APIs that don't exist or aren't available to me. You can think of Fake as Automator for Safari. Non-Mac people may respond better to similar to [Selenium][9]. If you're not familiar with Fake be sure to check out the video on their homepage, it gives a great explanation.

So here's the Fake part of my workflow:

![Web article archive workflow][10]

In english, it does the following:

1.  Goes to the Readability website
2.  Logs in to the site with my credentials
3.  Clicks on the "Favorites" link
4.  Sets up a loop - for each article in my favorites list it does the following: 
    1.  Clicks on the favorited article to load it
    2.  Grabs the article title
    3.  Uses keyboard shortcuts to tell OSX to Print-to-PDF (more on this next)
    4.  In the file save dialog, it enters the article title (grabbed previously) and hits return to save the file
    5.  Clicks on the link to un-favorite the article so it's not processed again on a subsequent run
    6.  Clicks on the "Favorites" link to go back to the main favorites listing
5.  Now that all the favorited articles have been processed, it logs out

Inside the loop above, in step 3, I mention keyboard shortcuts in OSX. By default most apps recognize command-p as the shortcut to print. You can see in the screenshot above of my Fake workflow that the embedded AppleScript actually calls this command-p shortcut twice. Why is this? MacSparky has a [great video over on his site][11] that outlines this trick. Basically, I've set up a separate keyboard shortcut that maps to command-p as well to choose the Save as PDF option once the print dialog comes up. This way my scripting can depend on the more reliable keyboard shortcuts instead of trying to code in ways to simulate mouse clicks on buttons.

Obligatory video demo:

<iframe width="560" height="315" src="//www.youtube.com/embed/uK9B2Q2ISAg" frameborder="0" allowfullscreen></iframe> 
At this point I'm running the Fake workflow manually as a vetting process to ensure it runs reliably. At some point it will be relegated to my Mac mini to run on a schedule (nightly?) and dump the PDFs into a watched folder for Hazel to process and file away for me.

You can download this Fake script on the [here][12].

 [1]: http://tapbots.com/software/tweetbot/
 [2]: http://feedly.com
 [3]: http://feedafever.com
 [4]: http://readkitapp.com
 [5]: http://www.reederapp.com/ios/
 [6]: https://www.readability.com
 [7]: /public/post-images/2014/readability_export.png
 [8]: http://fakeapp.com
 [9]: http://docs.seleniumhq.org
 [10]: /public/post-images/2014/web_article_archive_workflow.png
 [11]: http://macsparky.com/blog/2013/10/print-to-pdf-revisited
 [12]: https://dl.dropboxusercontent.com/u/1719003/nateofnine/Downloads/2014/archive_web_article.zip