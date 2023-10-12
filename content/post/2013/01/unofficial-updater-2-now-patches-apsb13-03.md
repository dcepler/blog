+++
author = "David Epler"
categories = ["ColdFusion", "Security", "Unofficial Updater 2"]
date = "2013-01-21T18:45:00-05:00"
draft = false
title = "Unofficial Updater 2 now patches APSB13-03"
slug = "unofficial-updater-2-now-patches-apsb13-03"
+++

I had intended to get this posting out earlier when I updated [Unofficial Updater 2](https://www.uu-2.download) on the 16th. Here are the changes that were made with the latest release UU2.

* Now works with all releases of ColdFusion 9. (9.0.0, 9.0.1, and 9.0.2)
* Applies [APSB13-03](http://www.adobe.com/support/security/bulletins/apsb13-03.html)
* New website to download https://www.uu-2.download, since github ended support for [uploads](https://github.com/blog/1302-goodbye-uploads)

<!--more-->
  
[APSA13-01](http://www.adobe.com/support/security/advisories/apsa13-01.html) does note that ColdFusion 8 and earlier is susceptible to the attack that APSB13-03 fixes. Based upon the security advisory it does not seem that Adobe will be providing a patch for ColdFusion 8 since core support for ColdFusion 8 ended last year. For ColdFusion 8 and earlier please make sure you properly secure the `CFIDE` directory and other mitigations steps noted in the security advisory.
  
I have also published an updated set of hashesets that can be used with hashdeep at https://github.com/dcepler/cfide-integrity to check the validity of CFIDE after applying APSB13-03. For details please see my previous [post](/post/file-integrity-checking-cfide).