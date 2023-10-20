---
author: David Epler
date: 2012-09-04T18:10:00-04:00
draft: false
title: Thoughts on ColdFusion 10 Update 1
slug: thoughts-on-coldfusion-10-update-1
categories:
  - "ColdFusion"
---

So if you didn't see it via the [ColdFusion Blog](http://blogs.coldfusion.com/post.cfm/coldfusion-10-update-1-10-0-1-released) or by the new indicator inside ColdFusion Administrator, the first update for ColdFusion 10 dropped on August 31st.
  
First, I have to say "Thank You" to the ColdFusion Team. **FINALLY** there is an easy way to patch ColdFusion and I can get out of the business of building a patch tool for ColdFusion. The other good thing is that the [TechNote](http://helpx.adobe.com/coldfusion/kb/coldfusion10-update-01.html) actually links the bug IDs back to the ColdFusion bugbase.

<!--more-->

There is one item in the TechNote that does concern me, Prerequisite #1 which says:

> On non-windows platforms (Unix, Solaris, and Mac OS X), ensure ColdFusion server is started with root user privileges. On Windows, ensure ColdFusion server is started with administrative privileges.

This is **_dangerous_** if you do this and forget to restart ColdFusion with the proper down-privileged user after the update is applied.
  
The update functionality should be able to update ColdFusion without requiring **root** or an administrative account. Preferably, it should be able to update using the user ColdFusion runs as, but the wording doesn't seem to indicate that. It might be refering to when you apply the update from command line. I was able to apply the update fine on a CentOS 6 test box from the ColdFusion Administrator, running as non-root user, **cfusion**. So I just think it is documentation that needs to be cleaned up (hopefully).
  
Now for the other issue which have been noted by others ([Adam Cameron](http://adamcameroncoldfusion.blogspot.com/2012/09/which-version-of-coldfusion-am-i.html)), the version number in ColdFusion doesn't reflect **10.0.1** which is being used to describe it. Both in `server.coldfusion` struct and when one uses `cfinfo` from command line, still reports **10,0,0,282462** after the update is applied. Adobe has specific [Release Terminology](http://www.adobe.com/support/updaters/terms.html) but doesn't seem to be following it. An explaination is offered [here](http://www.krishnap.com/2012/09/coldfusion-10-hotfix-update-installer.html) which says:

> No. It won't change. As explained above, Under System Information the Version & Build number will be shown same as the ColdFusion 10 Final released build (i.e ColdFusion 10, 282462). However, under Version field the new Update Level field shows the Update Level Number. Not changing the the Version value to 10.0.1 is a conscious decision to avoid some unwanted maintenance. 

What unwanted maintenance? If it is Update 1, based upon Adobe's _own terminology_ the version number should be incremented in the product to reflect it, **10.0.1**. If it is really a cumulative hotfix then nothing on the version number changes and is consistent with previous versions of ColdFusion. If this is something totally new, then the update level shown in the ColdFusion Administrator needs to be added to the `server.coldfusion` struct and `cfinfo`.
  
 