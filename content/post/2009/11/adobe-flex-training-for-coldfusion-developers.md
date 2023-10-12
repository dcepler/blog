+++
author = "David Epler"
categories = ["ColdFusion", "ColdFusion Builder", "Flex", "Flash Builder"]
date = "2009-11-23T10:55:00-05:00"
draft = false
title = "Adobe Flex Training for ColdFusion Developers"
slug = "adobe-flex-training-for-coldfusion-developers"
+++

On Friday (November 20th), I spent my day at the free [Adobe Flex Training for ColdFusion Developers](http://www.ce1.com/adobe/2009/flextrainingforcfdevelopers/). If you are (like me) working day in, day out with ColdFusion and haven't played with or explored Flex, ColdFusion Builder, or Flash Builder you should go. While it is an "Intro", it is enough to get your feet wet to explore more once you leave.
  
Another date that has been added for Washington, DC on December 17th and hopefully Adobe will add more dates and locations for next year.

<!--more-->

## Laptop Setup

I can not stress enough, _**follow the instructions exactly**_ on how to setup your laptop for the training class. There is a slight variation due to a bug installing ColdFusion Builder into Flash Builder as a plugin. The fix is to install both as standalone applications, which I did not find out about until I got to the training (and it is corrected in the printed training materials). The reason I say to follow the instructions exactly is to cut down on having the instructor and TAs running around dealing with problems due to configuration variations. It wasn't a huge problem since people helped each other out as well, but it did slow down the pace.
  
I had intended to just install [Flash Builder 4](http://labs.adobe.com/technologies/flashbuilder4/) on to my MacBook Pro (since all the other software was already installed), but I ran into a problem since Flash Builder 4 apparently [does not like case sensitive file systems](http://forums.adobe.com/thread/460031) (yes, I installed Leopard with case sensitivity, it is a hold over from using Solaris and Linux). **_<span class="text-danger">Adobe needs to fix this!</span>_**
  
Actually, not installing Flash Builder 4 directly turned out to be better. I used [Windows 7 Enterprise 90-day evaluation](http://technet.microsoft.com/en-us/evalcenter/cc442495.aspx) in Parallels for the training class environment. Figure if I'm playing with new Adobe technology, why not Windows as well.
  
Other things not noted in the instructions. Install Flash Player with debugging which can be found in **_C:\Program Files\Adobe\Adobe Flash Builder Beta 2\player\win_** on Windows or **_/Applications/Adobe Flash Builder Beta 2/Player/mac_** on Mac. Also be sure to have Adobe Reader installed as well.
  
The only other weird thing I ran into (and several others did as well) is that the class example files when unzipped were read-only with encryption turned on. This prevented them from being run in ColdFusion. The files show up in **<span class="text-success">green</span>** inside Windows Explorer. To fix the problem all you needed to do is go into the file properties in Windows Explorer and remove the encryption and read-only on the file.

## Training and what I learned

The training was conducted by [Figleaf](http://training.figleaf.com/) and Dave Watts was the instructor. The facilties were nice and the room was quite full. It was a bonus to have [Adam Lehman](http://www.adrocknaphobia.com/) there from Adobe.
  
While I have played around with new features in ColdFusion 9 and
  
seen various demos of using ColdFusion as a Service (CFaaS) and the ORM functionality, I had not really used them. The training provided an opportunity to be hands-on with them and to be "forced" to use [ColdFusion Builder](http://labs.adobe.com/technologies/coldfusionbuilder/). I say "forced" since I made the switch to Eclipse/[CFEclipse](http://cfeclipse.org/) a long time ago and have a really stable setup with my prefered plugins. The training provided a structured hands-on experience with ColdFusion Builder to hopefully get a better impression of the new IDE. Simply put, I am **impressed**! I like the integration they have done and it is significantly better than the Eclipse plugin that was released for ColdFusion 8. I probably will buy it when it is released, if the price is right (under $200).
  
Flash Builder is quite impressive with the design view and network monitor. I really wish ColdFusion Builder could have been installed as a plugin to Flash Builder they do make a very powerful combination in a single IDE.
  
The training was clear and provided a good way to introduce each new feature. I particularly liked Exercise 4 where it put Flex, AIR, and ColdFusion all together. I wish they would remove Exercise 0 from the training since it doesn't really provide anything other than a way to ensure your environment is setup. Exercise 1 is much better since it shows connecting to remoting and web services. Another reason to do so, is so that you can get the the end of Exercise 4 where you upload a file to ColdFusion and send email which we were not able to get to (but that left me with more to look at on my own over the weekend).
  
Overall, it really showed me the power of what can be done with Flex and ColdFusion, even if just small examples. If you have the opportunity to go, you should. It is free and really worth the day.