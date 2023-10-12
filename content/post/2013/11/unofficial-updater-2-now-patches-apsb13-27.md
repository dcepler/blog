+++
author = "David Epler"
categories = ["ColdFusion", "Security", "Unofficial Updater 2"]
date = "2013-11-13T19:45:00-05:00"
draft = false
title = "Unofficial Updater 2 now patches APSB13-27"
slug = "unofficial-updater-2-now-patches-apsb13-27"
+++

This has been one of the faster turn around times to get an updated [Unofficial Updater 2](https://www.uu-2.download) out. One of the items that stuck out was that one of the acknowledgments was to Alex Holden who co-discovered the [Adobe password and software breach](http://krebsonsecurity.com/2013/10/adobe-to-announce-source-code-customer-data-breach/).

<!--more-->

In the news of the latest patch, there is contention of whether the hole reported by Alex Holden is actively being exploited, from the [second to last paragraph](http://krebsonsecurity.com/2013/11/zero-days-rule-novembers-patch-tuesday/).

> Holden maintains this flaw was being used by attackers prior to today. "Hold Security identified an attack attempt against a ColdFusion version 8 resource by the same hackers behind breaches like LexisNexis, Adobe, and others," Holden said. Unaware of the possible effectiveness of this attack, Hold Security reached out to Adobe. While Adobe did not find the precise attack effective against any of supported CF versions, they did identify a critical flaw in the same resource which led to the patch issued today.

The first thing that struck me was that ColdFusion 8 was specifically mentioned. Now ColdFusion 8 core support ended _July 31, 2012_ which means Adobe **will not** issue a patch to close this hole on ColdFusion 8 (the last patch was APSB12-21 on September 11, 2012). The only effective measure is to make sure you properly lockdown ColdFusion 8 or upgrade to a supported version (and properly secure it). The other thing is Adobe's statement about being "effective against any supported CF version" and since ColdFusion 8 is no longer supported it is probably valid. 
  
Regardless of if it is being exploited, the best defense is to be running a supported version of ColdFusion, staying current on patches, and properly securing ColdFusion using the published lockdown guides for [ColdFusion 9](http://www.adobe.com/content/dam/Adobe/en/products/coldfusion/pdfs/91025512-cf9-lockdownguide-wp-ue.pdf) or [ColdFusion 10](http://www.adobe.com/content/dam/Adobe/en/products/coldfusion/pdfs/cf10/cf10-lockdown-guide.pdf).
  
Also tomorrow (11/14) at 2pm ET, I will be giving a free webinar on the security enhancements that have been made in ColdFusion 10. To register, please visit http://events.carahsoft.com/event-detail/2919/aboutweb/.