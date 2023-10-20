---
author: David Epler
date: 2012-09-19T21:30:00-04:00
draft: false
title: Final update to Unofficial Updater 2 for ColdFusion 8.0.1 (APSB12-21)
slug: final-update-to-unofficial-updater-2-for-coldfusion-8-0-1-apsb12-21
categories:
  - "Unofficial Updater 2"
  - "ColdFusion"
---

Well, the long nightmare known as patching Adobe ColdFusion 8.0.1 is now over. With the release of [APSB12-21](http://www.adobe.com/support/security/bulletins/apsb12-21.html) last week and [core support ending](http://www.adobe.com/support/products/enterprise/eol/eol_matrix.html#63) on July 31 for ColdFusion 8 there will be no more security hot fixes released for it (noted at the bottom of the [technote](http://helpx.adobe.com/coldfusion/kb/coldfusion-security-hotfix-apsb12-21.html)).

<!--more-->

Over 5 years, there were 28 hot fixes and 4 cumulative hot fixes (CHF) released for ColdFusion 8.0.1 ([hot fix matrix](https://github.com/dcepler/unofficial-updater2/blob/master/cf801-hotfix-matrix.pdf?raw=true))

## Additional changes to Unofficial Updater 2

Unofficial Updater 2 now supports ColdFusion 9.0.2 since APSB12-21 needs to be applied to it as well and there is no easy way to do it since the Hotfix Update functionality in ColdFusion 10 doesn't seem like it will get back ported any time soon.
  
UU2 will now try to write and then delete a text file to the directories supplied. This is done before any of the updates are even applied to the system. If test fails in any of the directories, UU2 will stop and report the directory it couldn't work with. This should hopefully resolve several of the "Unable to expand" errors that have been noted as issues and not leave ColdFusion in an indeterminate state of patches applied.
  
New disclaimer #7 which points to Charlie Arehart's [cf411.com](http://www.cf411.com/) listing of [CF-Oriented Troubleshooting Consultants](http://www.cf411.com/cfconsult). Since UU2 cannot deal with all possible configurations, it really might be necessary to engage with a consultant to make sure ColdFusion is properly patched.

## Final Thoughts

I have been asked if I would consider modifying UU2 to patch ColdFusion MX 7. I looked at what it would take and it really isn't worth the effort. Adobe ended core support on February 7, 2010 and extended support on February 7, 2012 for ColdFusion MX 7. If you are still on such an old version, you really need to just upgrade or migrate over to [Railo](http://www.getrailo.org/).
  
Lastly, thank you to everyone that continues to provide feedback and uses Unofficial Updater 2, the previous release was downloaded over 720 times from [github](https://github.com/dcepler/unofficial-updater2).