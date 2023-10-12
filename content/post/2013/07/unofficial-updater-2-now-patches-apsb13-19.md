+++
author = "David Epler"
categories = ["ColdFusion", "Unofficial Updater 2"]
date = "2013-07-11T17:12:48-04:00"
draft = false
title = "Unofficial Updater 2 now patches APSB13-19"
slug = "unofficial-updater-2-now-patches-apsb13-19"
+++

Well, I kind of missed blogging the last update to [Unofficial Updater 2](https://www.uu-2.download/) back in May while I was at [cf.Objective()](http://cfobjective.com/). The latest update [APSB13-19](http://www.adobe.com/support/security/bulletins/apsb13-19.html) dropped while I was on vacation at the beach, but still got it done two days after it was released by Adobe.

<!--more-->
  
For ColdFusion 9.0.x the latest security update only applies if you are running as a standalone install or as a JRun Multi-Server. If you are running ColdFusion 9.0.x on top of any other J2EE server like JBoss, Weblogic, or others you don't need to apply the fix.
  
As usual the best defense is to stay current on patches and properly secure ColdFusion using the published lockdown guides for [ColdFusion 9](http://wwwimages.adobe.com/www.adobe.com/content/dam/Adobe/en/products/coldfusion/pdfs/91025512-cf9-lockdownguide-wp-ue.pdf) or [ColdFusion 10](http://www.adobe.com/content/dam/Adobe/en/products/coldfusion/pdfs/cf10/cf10-lockdown-guide.pdf).