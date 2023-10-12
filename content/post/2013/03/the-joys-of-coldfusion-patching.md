+++
author = "David Epler"
categories = ["Unofficial Updater 2", "ColdFusion"]
date = "2013-03-12T15:00:00-04:00"
draft = false
title = "The Joys of ColdFusion Patching"
slug = "the-joys-of-coldfusion-patching"
+++

So if you have been following things, Adobe released [cumulative hotfixes](http://blogs.coldfusion.com/post.cfm/new-updates-for-coldfusion-9-9-0-1-9-0-2-and-10-java-7-now-supported) to allow for Java 7 support and to update `<cfmap>` to use Google Maps API v3 instead of v2. Only problem is along the way they have had to [update](http://blogs.coldfusion.com/post.cfm/new-chfs-for-cf-9-and-cf-9-0-1) them [a few times](http://blogs.coldfusion.com/post.cfm/jpedal-jar-for-coldfusion-9-0-1-cumulative-hotfix-4). It is exactly this situation which drove me to create Unofficial Updater 2 originally. 
  
Frankly, the entire past 2 weeks should not have occurred. This really shines a light on how poorly thought out the Adobe ColdFusion update product teams's release process is. And this is not the first time they have had to do multiple re-releases of hot fixes. [APSB11-04](http://helpx.adobe.com/coldfusion/kb/security-hotfix-coldfusion-8-8.html) once, [APSB11-14](http://helpx.adobe.com/coldfusion/kb/coldfusion-security-hotfix-apsb11-14.html) twice, [APSB12-06](http://helpx.adobe.com/coldfusion/kb/coldfusion-security-hotfix.html) once for CF801 only and pulled [Update 3](http://blogs.coldfusion.com/post.cfm/coldfusion-10-update-3-released) for CF10. That track record does not inspire confidence.

<!--more-->

As for some general notes regarding the CHFs. They provide Java 7 support for ColdFusion 9.0.x for all OSes [**EXCEPT** for Mac OS X 10.7 and 10.8](http://blogs.coldfusion.com/post.cfm/new-updates-for-coldfusion-9-9-0-1-9-0-2-and-10-java-7-now-supported#comment-869ED317-0670-4D3C-6CADD847164930CE). Java 7 is supported on all OSes for ColdFusion 10.0.8+. The update to support Google Maps API v3 should never have happened; `<cfmap>` should be depricated in accorance to what I'll call the ["Forta Rule"](http://forta.com/blog/index.cfm/2012/11/25/When-Using-ColdFusion-No-Longer-Makes-Sense) and can only hope this happens for ColdFusion 11.

## Update Process for UU2

Given that I found multiple issues that prompted the re-releases and updates to the technotes, I wanted to share how I go about updating [Unofficial Updater 2](https://www.uu-2.download).
  
The process starts with complete reading of the technote(s) to see what has changed and what exactly the steps are. From that the hotfix matrices ([9.0.0](https://github.com/dcepler/unofficial-updater2/blob/master/cf900-hotfix-matrix.pdf?raw=true), [9.0.1](https://github.com/dcepler/unofficial-updater2/blob/master/cf901-hotfix-matrix.pdf?raw=true), [9.0.2](https://github.com/dcepler/unofficial-updater2/blob/master/cf902-hotfix-matrix.pdf?raw=true)) are updated as part of the project to note items such as download files, CVEs fixed, and what needs to be installed or is superseded. This is how the missing 81860 for CF 9.0.0 CHF2 was found. Then [uu2.properties](https://github.com/dcepler/unofficial-updater2/blob/master/uu2.properties) is updated to add the download location and hashes for the files. It was the changing of the hashes which prompted me to inquire about the "silent" update of the CHFs that occurred between February 27th and March 1st. Finally [build.xml](https://github.com/dcepler/unofficial-updater2/blob/master/build.xml) is updated to reflect the steps in the technote to apply the files.
  
After the update to `build.xml`, UU2 is then tested against both Windows (2008 R2) and Linux (CentOS 5.8). So there are VMs for each OS that have installs of ColdFusion 9.0.0, 9.0.1, and 9.0.2 installed as both standalone and as JRun multi-server. In each instance there is a clean install maintained, an install with the previous hotfix applied, and an install with the new hotfix applied so comparisions can be done. UU2 is tested against a clean install and the previous hotfix install. This is how the missing jpedal.jar was found in CF 9.0.1 CHF4. UU2 isn't tested as rigorously against Mac OS X since I don't know of any one running it in production with OS X Server. No testing is done against Solaris since I don't have access to a Sun Server, but the Linux testing should cover it. 
  
Then all the associated documentation for UU2 is updated and packaged for release. Generally want to get UU2 out as soon as possible but if there are issues reported, it will be delayed until they are resolved. UU2 only goes out once everything for a given set of updates from Adobe have been resolved.
  
So with all of that, [Unofficial Updater 2](https://www.uu-2.download) was updated last night (March 11, 2013 at 8:00PM EDT) to support applying the various ColdFusion 9.0.x CHFs (issue [33](https://github.com/dcepler/unofficial-updater2/issues/33)). It also changed the behavior of the default directory for backing up (issue [31](https://github.com/dcepler/unofficial-updater2/issues/31)). On Windows it will default to the current running directory of UU2 and on Unix will default to `/tmp`. 
  
Again, thank you all that use and provide feedback to make Unofficial Updater 2 better. Also thank you to [CFHour](http://cfhour.com/) for the mentions (finally made [Boyzoid](http://www.boyzoid.com/) a convert!)
  
 