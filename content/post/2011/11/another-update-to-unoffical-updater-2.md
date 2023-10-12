+++
author = "David Epler"
categories = ["Unofficial Updater 2", "ColdFusion"]
date = "2011-11-04T10:40:00-04:00"
draft = false
title = "Another update to Unoffical Updater 2"
slug = "another-update-to-unoffical-updater-2"
+++

I have just updated [Unoffical Updater 2](https://github.com/dcepler/unofficial-updater2) so that it will apply [Cumulative Hot Fix 2 for ColdFusion 9.0.1](http://kb2.adobe.com/cps/918/cpsid_91836.html) and it also fixes applying [APSB11-14](http://kb2.adobe.com/cps/907/cpsid_90784.html) to ColdFusion 8.0.1 since it was "silently" updated on September 16th. ~~I say "silently" because there was nothing from Adobe saying they had updated it (blogs, email, tweets).~~ It actually was announced on the [ColdFusion Server Team Blog](http://blogs.adobe.com/coldfusion/2011/09/16/updated-bug-83514-session-is-invalid-issue/) but isn't all that clear. I found out when a user of UU2 said it was failing. UU2 uses SHA-512 hashes to verify the downloads. There are only two reasons for the hashes to be incorrect, either the file got corrupted during download, or Adobe updated the file.

<!--more-->

Adobe has been much better getting security updates out, but the last two, [APSB11-04](http://kb2.adobe.com/cps/890/cpsid_89094.html) was revised **once** and [APSB11-14](http://kb2.adobe.com/cps/907/cpsid_90784.html) was revised **twice**. In both instances bugs were introduced that to me seem like they should have been caught in the QA process before they were released. The updating of the security updates has me a bit concerned particularly when Zeus is released with the automated hotfix mechanism. Hopefully everyone patches properly by applying to development and test before production, or waits a month or two to make sure Adobe does need to revise them. This is why UU2 is just getting updated now instead of when Adobe released CHF2 on September 16th.

I still wish Adobe would just package up **ALL** the existing hotfixes/cumulative hotfixes/security updates and [update the JVM](http://www.carehart.org/blog/client/index.cfm/2011/10/28/CF911-Have-you-updated-your-ColdFusion-JVM-to-24-yet-Important-security-fix-for-CF-89) to release proper Update 2 packages for both ColdFusion 8 and 9.