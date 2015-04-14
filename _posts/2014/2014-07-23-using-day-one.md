---
layout: post
title: 'Using Day One'
tags:
- dayone
- workflow
- launchcenterpro
---

I'm going to presume you already know what Day One is. If not I'm not going to go beyond saying it's a journaling app, so [go check it out][1] and come back. Then I can get to the good stuff!

I've used Day One on and off since it was originally released. I've always loved using it, but haven't always been able to find the perfectly-fit itch that I needed to scratch with it until the last year or so. Generally speaking I don't do open journaling very well so a more structured approach has worked well for me. It's also gamified portions of it which adds its own sort of fun!

## Historical Markers

If you've read my blog this isn't new, but I mention it here for completeness. For the full description check out my post on [Tracking Historical Markers][2]. Basically my kids and I stop whenever we see a historical marker sign, read it, take a picture, and log it in Day One with the tag "historicalmarker". Almost invaribally it generates discussion in the car wherever we are going.

Recently, we've even noticed first hand a very important lesson; history is incredibly influenced by the author.

On the edge of our town is posted [this historical marker about the Sullivan Campaign][3]. It is straightforward, factual, and seems to imply a sense of importance and pride in the fact that our town hosted General Sullivan while he planned for over a month for "this major expedition of the Revolution aimed at the Indian-Tory alliance". Good stuff, right?

Well, it's far to easy to forget that history, **especially wars** have at least two sides to every story. This past weekend we were visiting friends near Rochester, NY where we saw [this sign for Squaw Island][4]. It tells the story of the smallest State Park in New York State, which is the (alleged) site where the wives and children of the Seneca Indian Nation "sought refuge ... during the invation of their home land by General Sulivan."

Now without judging either side or getting into huge debates over the content of two simple historical signs, I think it is easy to point out how different the tone is in each of these. As we try to raise our children (and grow as adults ourselves also) to know the whole truth about as much in life as possible this was a great illustration that there is always more to learn and understand.

And by the way ... the kids still love the simple game of yelling "BLUE SIGN" anytime we're in the car travelling :)

## Quantified Self

I love data, and Quantified Self (QS) is a great way for me to play with more data. Someday, I may even do something useful with it! Day One, especially with it's support for [URL schemes][5] and therefore [Launch Center Pro][6], has made this even more customizable and extensible.

All of the following things I do with QS in Day One via iOS also generate the following additional data points:

*   Timestamp
*   GPS location
*   Weather at that location

Since Day One stores its data in a very readable/parsable format, access to all of this after the fact is very simple.

### Bathroom Log

At first I didn't know why I'd track this. I felt it was an easy test and pretty straightforward to track. Recently I started some new medication that may change these habits - turns out I have the process and historical data to track that now and determine what effects the medicine may have!

I use a simple Launch Center Pro action to kick off the creation of a new entry in Day One and fill it will the appropriate details. The data format for the note that is entered is simple. I stuck with markdown so I can parse it later and still keep it readable/meaningful (and nice display) in Day One. It looks like this:

    Bathroom Log
    
    - Urinate: yes
    - BM: yes
    
    #bathroomlog
    

Hopefully that is self-explainatory enough that I don't need to go in to more detail. Here's a quick video of how fast I can log that info with Launch Center Pro:

<iframe width="560" height="315" src="//www.youtube.com/embed/4cq5Osq3sVc" frameborder="0" allowfullscreen></iframe> 
### Medicine Log

This follows the exact same process as Bathroom Log, with a small difference in format (obviously) and the addition of a measurement of medicine included.

    Medicine Log
    
     - Ranitidine
     - 150mg
    
     #medicinelog
    

For prescription medication, I know the amount remains (relatively) constant so I can hardcode the amount into the Launch Center Pro action to make entering faster. If I think the amount could change I configure it to be a select list that pops up for me to click on quickly and move on my merry way.

<iframe width="560" height="315" src="//www.youtube.com/embed/0CgOAUUWzD8" frameborder="0" allowfullscreen></iframe> 
### Gratitude Log

Awhile ago I read and article about focusing on happiness to make yourself happier. This isn't new, nor is it rocket science, but it hit me as an adult that it's far to easy to lose sight of that. I suppose if we all listened we really do learn everything we need to know in Kindergarten as I still recall this song I was taught way back then:

> Input. Output. What goes in, must come out.
> 
> Input. Output. That is what it's all about.
> 
> Input. Output. Your mind is a computer whose ...
> 
> Input. Output. Daily you must choose.

Now aside from the obvious afinity I had even back then to claiming I was a computer, there is much truth in how our surroundings affect us. To this end I decided to keep a gratitude log to record one thing I am grateful for every day. Launch Center Pro kicks up a reminder every evening for me to accepted and type in a response. I don't even have to enter "I am greatful for"; it fills that out for me automatically. Here is an example of the data format from one I just logged for today:

    Gratitude Log
    
    I am grateful for sweet children. Getting tender hugs and kisses every night at bedtime is simply unmatchable.
    
    #gratitudelog
    

What I realized in doing this for awhile, is that this in and of itself is a form of journaling that isn't so data-driven. It may be templatized but that only ensures that I focus not just on what is important, but also what I want to carry forward in my heart and attitudes. It may be taking a revisionist stance towards journaling but I think the world contains enough struggle and heartache that I already remember - I need a little extra help stay positive.

<iframe width="560" height="315" src="//www.youtube.com/embed/AbzqBbQp35g" frameborder="0" allowfullscreen></iframe> 
## Photography

Oh, photography. iPhoneography. Hipster-term-of-the-week-for-visually-remembering-stuff. I love and hate you both. You're a wonderful creative outlet. Smartphones have made you always easily available. The advent of digital has made you ... an organizational mess.

It also seems that the times I want to take photos the most is when I am least likely to have an internet connection. This isn't a problem if all you want to save is an image - what if I want to take an integrated note as to what I saw? What if I want to remember the name of a plant I saw at an arboretum without trying to squeeze in the little placard? Day One is ... so close to being my solution for this. I'll outline my ideal use case, and leave it to the wish list to outline the one major flaw I am experiencing.

![enter image description here][7]

Day One affords me all of the following with photos:

*   Store photos
*   Read the timestamp and geo location information from photos
*   Store the photo and text I write with it locally and sync back to the cloud whenever I get an internet connection in the future
*   Tag posts (images)
*   Act as my own private Flickr store for my images where I always have access to local copies of all my images
*   Have a ubiquitous display capability with my Mac, iPhone, and iPad with the respective versions of Day One on all those devices! 
*   Given it's URL scheme support, any of my photo editing software can send the image directly to Day One for storage with a simple "open in" command
*   Perhaps most importantly, leverage an app that I am happy with and always enjoy using

I'm really close to using this full time for all photo storage, browsing, and organization. What's keeping me back? My first wish list item ...

## Wish List

### Full-size Image Support

Day One currently automatically scales down your image before saving it into its storage system. This makes a ton of sense, especially when you consider synching issues, cloud storage limits, device storage limits (how many full-res photos do you really need cached locally on your phone?), etc. I have a suggestion for solving this, and perhaps making Day One even more efficient in this regard.

**Proposed Solution:** Add an option to allow Day One to store full-size images in the cloud. The key here is that it isn't storing them on the device itself. As a matter of fact, Day One may even be able to further compress the images on devices since they would be of even more limited use; just small-screen digital displays. The original should be sent up to iCloud/Dropbox and referenced or linked to. I suppose the desktop version of Day One could also have the option of just using the full-size image directly, though that may be overkill in both options and return on file size. The important thing to note is that I have an archived copy of the full-size image linked with all the tags and textual goodness I've entered in Day One.

Side benefit? I suppose if Day One ever needed to integrate with a higher-resolution display (4k display, Apple TV, start your drooling now) it would have access back to the original full-res image to use in those cases - a scaled-down 1,600 pixel image may not get you very far in the frighteningly-near future.

### x-callback-url Support

[Tech explaination here][8]. Basically this would allow me in my hyper-automated Launch Center Pro world, to log something to Day One and be returned immediately back to Launch Center Pro, and even sent to another app if that would be valuable in that scenario. Here are two use case examples:

**Example 1**

I've just taken 2 medications using the Medicine Log example outlined above. Using a quick touch and swipe I log one medicine into Day One and am immediately piped back to Launch Center Pro and am ready to touch-swipe enter the second one. Sliiiiiick.

**Example 2**

I want to take a photo and record info about it, but am not ready to store it in Day One yet because I'll want to edit it (happens a lot). I could have a Launch Center Pro action that does the following:

1.  Asks a title for the photo
2.  Asks a textual description for the photo (optional)
3.  Sends me to Day One to create a new entry with that information, and via x-callback-url sends me directly on to the camera app to take a photo. 

Now, while I know the photo will be saved to the camera roll not Day One, I can edit it later and based on the timestamps being within a few seconds of each other I know exactly which Day One entry to attach the photo to after I've edited it. Even without that benefit, I'm able to record text and take a photo exceptionally quickly and efficiently ... once again using an app I love!

### Hashtag Support Improvement

I love that I can enter a hastag and Day One will detect it and convert it into a Day One entry tag. What I have noticed, however, is that when using URL schemes (via Launch Center Pro) the hashtag isn't automatically detected in Day One. I have to either manually hit "return" in Day One before saving, or go to settings page and tell Day One to scan all entries for hashtags to convert.

I'd be happy with either of the following solutions:

1.  Ensure Day One processes the hashtag without those manual steps
2.  Even better: expose hashtags directly to the URL scheme support so I could specify them in the URL instead of in the text body. 

## Day One Rocks

Even though (or perhaps due to the fact that) I've outlined a few small shortcomings in Day One, I feel compelled to ensure I end this on an up note. Day One simply rocks. It's the best money I've spent on apps in a long time and I'd happily spend it again! It's an incredible balance of great design, usefulness, and functionality that just resonates with me every day.

There's even more I could write about - did anyone notice that I used the dayone.me publishing service to share my historical marker example earlier in the post? I'd love to hear more ideas on how people are using Day One. And if, developers willing, my wishlist items are addressed I'll be posting even more details on how I use those functionalities!

 [1]: http://dayoneapp.com
 [2]: /2014/01/27/tracking-historical-markers
 [3]: https://dayone.me/xMlzfW
 [4]: https://dayone.me/xMrzkh
 [5]: https://developer.apple.com/library/ios/featuredarticles/iPhoneURLScheme_Reference/Introduction/Introduction.html
 [6]: http://contrast.co/launch-center-pro
 [7]: /public/post-images/2014/photo.png
 [8]: http://x-callback-url.com