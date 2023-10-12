+++
author = "David Epler"
categories = ["Unofficial Updater 2"]
date = "2012-03-19T07:00:00-04:00"
draft = false
title = "Unofficial Updater 2 Updates (APSB12-06)"
slug = "unofficial-updater-2-updates-apsb12-06"
+++

There have been several updates to [Unofficial Updater 2](https://github.com/dcepler/unofficial-updater2) over the past few days.

<!--more-->

* Support for [APSB12-06](http://www.adobe.com/support/security/bulletins/apsb12-06.html) 
 * Adobe truely seems to be getting on a quarterly release schedule for ColdFusion security updates since the last one, [APSB11-29](http://www.adobe.com/support/security/bulletins/apsb11-29.html), was released on December 13, 2011
 * Given that the last few have been cumulative, UU2 now just applies the latest one following the Section 2 instructions
* UU2 only needs to be run once with an Internet connection 
 * This was a [suggestion](https://github.com/dcepler/unofficial-updater2/issues/14) from Adrian Moreno and was something I had been thinking about doing for a bit
 * On the first run, UU2 will download all the hotfixes and security bulletins for both ColdFusion 8.0.1 and 9.0.1 from Adobe and then pack them into **_Unofficial-Updater2-with-downloads.jar_** which can be run later. This was done since UU2 can not directly package the updates from Adobe
 * UU2 will also create **_unofficial-updater2.txt_** in `<cfusion-home>/lib/updates` which will contain the date that UU2 was run and the date the files were downloaded from Adobe
* Updates for download URLs that Adobe changed
* Wiki updates 
 * [Using Unofficial Updater 2](https://github.com/dcepler/unofficial-updater2/wiki/Using-Unofficial-Updater-2) has been updated to reflect the changes in the screens
 * Still putting together the instructions on how to [Restore ACF from UU2 Backups](https://github.com/dcepler/unofficial-updater2/wiki/Restore-ACF-from-UU2-backups)

The latest installer is available for download from [github](https://github.com/dcepler/unofficial-updater2/downloads).