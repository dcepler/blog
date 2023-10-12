+++
author = "David Epler"
categories = ["Unofficial Updater 2"]
date = "2012-04-06T19:00:00-04:00"
draft = false
title = "Update to APSB12-06 and Unofficial Updater 2"
slug = "update-to-apsb12-06-and-unofficial-updater-2"
+++
 
So last Thursday (March 29th) Adobe published an update to [APSB12-06](http://www.adobe.com/support/security/bulletins/apsb12-06.html) to address a defect introduced that prevented file uploads from working properly on ColdFusion 8.0.1, see the [Adobe forum post](http://forums.adobe.com/message/4304046) for details. I have just updated [Unofficial Updater 2](https://github.com/dcepler/unofficial-updater2) to apply the corrected files for ColdFusion 8.0.1.

So, good they fixed the issue, but my problem with Adobe lays with how they comunicate the change. I didn't even know there was an update until I saw a post aggregated on [ColdFusionBloggers.org](http://coldfusionbloggers.org/) from the [Adobe ColdFusion Blog](http://blogs.coldfusion.com/post.cfm/march-2012-security-hot-fix-is-updated-for-coldfusion-801). I am signed up to Adobe's [Security Notification Service](http://www.adobe.com/cfusion/entitlement/index.cfm?e=szalert), but I have never seen a notification come in regarding ColdFusion. And when you go to the updated [ColdFusion Security Hotfix APSB12-06](http://helpx.adobe.com/coldfusion/kb/coldfusion-security-hotfix.html) where is the information that it has been updated, at the **BOTTOM** of the page. But at least it was updated, that counts for something right?

<!--more-->

The next fun thing is that Adobe is not consistently publishing the files associated with the technote. The original files and the non-updated files are linked from `http://helpx.adobe.com/content/dam/kb/en/930/cpsid_93043/attachments/` where as the updated ones for CF801 are at `http://helpx.adobe.com/content/dam/help/attachments/`. It is still possible to download the "broken" CF801 files. Seems to me the updated CF801 files should have been put at the original published URL and overwritten the "broken" CF801 files. Minor details.
  
And everyone is pointing to ColdFusion 10's server update (auto hotfix managment) as the cure to all of this, but I don't think it will be the panacea everyone thinks it will be. Over the last four security hotfixes that Adobe has released, three of them have been updated atleast once to fix bugs that were introduced by it. APSB11-04 **once**, APSB11-14 **_twice_**, APSB12-06 **once**. Just not feeling good about the Adobe QA process these days. 
  
The only true fix for this mess is for Adobe to produce annual updates that are fully tested and packaged installers. I really doubt it will ever happen for ColdFusion 8.0.1 since it has been over 4 years since the last updater and ColdFusion 8 core support is ending on [July 31, 2012](http://www.adobe.com/support/products/enterprise/eol/eol_matrix.html#63).
