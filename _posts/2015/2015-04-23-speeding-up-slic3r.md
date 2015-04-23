---
layout: post
title: 'Speeding Up Slic3r'
tags:
- 3dprinting
---

I'm fairly new to 3D printing, but one of the first things I noticed was how slow [Slic3r][1] can be when generating gcode files to print. After some quick Googling it seems as though slic3r grew in popularity back when it was faster but has since slowed down with each subsequent release. There's no doubt that people are posting and printing more complex and higher resolution models which I'm sure adds to this.

Fortunately, the "fix" is really easy. I say "fix" in quotes because it is more of a workaround and with most things there is a tradeoff. The magic happens in the Print Settings tab in Slic3r. Simply uncheck the "Avoid crossing perimeters" setting and you'll notice a vast performance improvement!

![Slic3r crossing settings][2]

So what is this setting and what is the tradeoff? From the Slic3r docs:

> Will force the nozzle to follow perimeters as much as possible to minimise the number of times it must cross them when moving around, and between, islands. This has a negative impact on both G-code generation and print times.
> 
> [Slic3r manual][3]

Basically, this feature tries to make sure that when moving around the print area, the extruder never (as much as possible) crosses over the perimiter of an object and instead mvoes around it. This keeps an potentially oozing extruder from leaking extra plastic onto the clean outer shells of your object. When it is absolutely necessary to cross over a perimeter it tries to do so at a vertex instead of a flat surface to minimize any noticable artifacts.

So far I have not noticed any major issues from turning this setting off. Occassionally I will see a few extra nibs or bumps on my flat surfaces but it's nothing that I can't sand off - something I do to make the surfaces look nicer on my prints anyway. 


[1]: http://www.slic3r.org
[2]: /public/post-images/2015/slic3r_crossing_settings.png
[3]: http://manual.slic3r.org/expert-mode/fighting-ooze