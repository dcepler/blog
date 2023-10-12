+++
author = "David Epler"
categories = ["ColdFusion"]
date = "2011-04-05T09:20:00-04:00"
draft = false
title = "What does a fully patched ColdFusion 8.0.1 Server look like?"
slug = "what-does-a-fully-patched-coldfusion-8-0-1-server-look-like"
+++

Seems like that should be an easy question to answer but it isn't. It really depends upon how ColdFusion was installed (standalone, multi-server JRun4, or J2EE EAR/WAR), what web server it is connected to, the underlying operating system, and if you need the hot fix that resolves a specific problem.

At work I need to patch the ColdFusion 8.0.1 servers. Luckily (or unluckily) they have had nothing applied to them. They are installed as multi-server JRun4 using the stock Java runtime 1.6.0_04 connected to Apache 2.2 running on Red Hat Enterprise Linux 5 64-bit. The goal is to get them fully patched with everything that Adobe has published (to date) as a hot fix, security bulletin, and tech note.

<!--more -->

The next three sections detail my frustration with trying to get to my end goal. I admit that it is very verbose but I feel like it has to be. If you like, you can skip to my [proposed solution](#there-has-to-be-a-better-way).

## Starting with Cumulative Hot Fix 4

I know that [Cumulative Hot Fix 4](http://kb2.adobe.com/cps/529/cpsid_52915.html) (CHF4) is the latest for ColdFusion 8.0.1 and would seem to be the best starting point since it is the most complete package of hot fixes. I read through the instructions for CHF4 and I didn’t get a good feeling. It looks like it was cut and pasted from several documents, particularly the [Additional Security Fixes Information](http://kb2.adobe.com/cps/529/cpsid_52915.html#main_Security). Start off with the pre-installation step to remove any previously installed individual hot fixes that are now in the cumulative and any previous installed cumulative hot fixes. The instruction to remove previous hot fixes is vague since Adobe does not explicitly list out which individual hot fixes are now contained, leaving it to me to figure out from the table of bug ids and from the list of security hot fixes that should be removed listed all the way at the bottom (hf801-73122.jar, hf801-77218.jar, hf801-1875.jar, and hf801-1878.jar). Since the ColdFusion servers I am dealing with don’t have anything applied, I can skip this step. Yay for patching laziness!

The actual installation of CHF4 is Step 1 and is pretty straight forward. Step 2 has two hot fixes listed in it (hf801-71975 and hf801-71557) but only applies if you are running ColdFusion on Java runtime 1.5. Since I am running on Java runtime 1.6, I can skip the step. Step 3 are all the security hot fixes and is marked as optional. Here I disagree with Adobe, security fixes should never be optional, so on to the steps to apply the security fixes.

The first section under Additional Security Fixes Information is, **Security hot fix**. And immediately I find a mistake in the CHF4 instructions, it has the **WRONG** link for the hot fix. It is pointed to hf800-71471.zip, subtle but big problem in that what you download will be for ColdFusion 8.0.0 not 8.0.1. The correct link is http://www.adobe.com/support/coldfusion/ts/documents/kb403328/hf801-71471.zip which I got after Googling for the hot fix and landing at [TechNote 403328](http://kb2.adobe.com/cps/403/kb403328.html). Reading the tech note, I noticed that the instructions did not match with what is in CHF4. CHF4 only says to put hf801-71471.jar into _lib/updates_ directory and mentions nothing about replacing **administrator.cfc** in _CFIDE/adminapi_ which is an additional step in the tech note. So which one is right, do you skip updating **administrator.cfc** or should you do it? My gut says to update it, besides I (always) make a backup of the original just in case the gut is wrong. Also nowhere in the instructions does Adobe identify what security bulletin this hot fix is from. It is actually [APSB08-12](http://www.adobe.com/support/security/bulletins/apsb08-12.html).

At this point I do not trust any of the instructions in CHF4, but continue to the next section, **Hot Fix related to CFIDE**, which has 3 sub-sections.

**Hotfix 1** doesn’t identify what security bulletin it is from as well, so off to Google again, first link [APSB09-09](http://www.adobe.com/support/security/bulletins/apsb09-09.html). At least the file download link is correct in CHF4, but the security bulletin has optional steps which would be helpful information to have included in CHF4.

**Hotfix 2** and **Hotfix 3** include references to the Common Vulnerabilities and Exposures (CVE) they are part of. This made finding the security bulletin easier, [APSB09-12](http://www.adobe.com/support/security/bulletins/apsb09-12.html). One has to sift through the security bulletin to pull out the strictly ColdFusion issues (CVE-2009-1872, 1875, 1877, 1878) from the Apache connector (CVE-2009-1876) and JRun (CVE-2009-1873, 1874) fixes. 

Step 1 for both **Hotfix 2** and **Hotfix 3** says the file downloaded will be CFIDE-8.0.1.zip but it is really CF8.0.1.zip for **Hotfix 2** and 8\_0\_1.zip for **Hotfix 3**. Otherwise the instructions and file download links in CHF4 matchup with the security bulletin. It would have been nice if Adobe had repackaged the three hot fixes into a single file download say, CFIDE-8.0.1-CHF4.zip.

The last section is **Hot fix related to JRun**. Now again Adobe is kind enough to list the CVEs (CVE-2009-1873 and CVE-2009-1874) which are apart of APSB09-12. This hot fix only applies if you installed ColdFusion as multi-server JRun4 which my ColdFusion servers were installed as. 

So I have finished installing CHF4 with all the security fixes. Well not quite when I see this block:

> An update for ColdFusion resolves a double-encoded null character vulnerability that could potentially lead to information disclosure (CVE-2009-1876). Only apply this update to ColdFusion installations that are configured with Apache

This applies to me since I am using Apache, but there are no instructions or file downloads linked. At least there is a CVE to search on (CVE-2009-1876) and again it goes to APSB09-12. I follow the instructions in the security bulletin to update my Apache connector.

## So am I fully patched to CHF4?

Well I thought so until I went back to re-read Charlie Arehart’s post [cfmyths: "If/when I apply Cumulative Hotfixes, I need apply only the latest CHF, right?"](http://www.carehart.org/blog/client/index.cfm/2010/12/12/cfmyths_cumulative_hotfixes) and saw this:

> The problem is, there are sometimes multiple steps involved in applying a given CHF, or there may be specific hotfixes that are indicated as requiring a manual effort. I'll explain the differences in more detail in a moment.

> If you have NOT done those manual steps, you WILL still need to do them, even if you "skip" that CHF in question.

If you have not read Charlie’s [post](http://www.carehart.org/blog/client/index.cfm/2010/12/12/cfmyths_cumulative_hotfixes), I highly recommend that you do.

So technically to be fully patched I need to apply [Patch for CFImage and Image functions in ColdFusion 8.0.1](http://kb2.adobe.com/cps/403/kb403411.html) that was listed in CHF3. I pull up the information and it lists the hot fix as hf801-71557. **_What?_** 

That was listed in CHF4 as Step 2 but only if I was on Java runtime 1.5.  The documentation for the hot fix doesn’t specify any Java runtime. So do I have to apply it or not? According to Charlie’s post I should. Given the errors so far in CHF4, I think I also have to look at hf801-71975 which is [ColdFusion 8.0.1: Fixes for Sandbox, Adminapi, and CFMX\_COMPAT bugs](http://kb2.adobe.com/cps/529/cpsid_52916.html) and is also listed in Step 2 for CHF4. 

And this is where it gets fun, hf801-71975 lists four bug ids it resolves 71975, 73122, 72932, and 75800. Bug id 71975 is listed as being resolved in CHF4. I am assuming bug id 73122 is implicitly resolved since CHF4 says to remove hf801-73122.jar but it is not explicitly listed in the table of bug ids on CHF4. Bug id 75800 has nearly identical description to bug id 75676 in CHF4. Are they the same bug or different? Searching the [ColdFusion bug database](http://cfbugs.adobe.com/) doesn’t give any results on the bug ids or “CFMX\_COMPAT”. Marvelously useless.

So that leaves one, bug id 72932 "_ColdFusion does not clear trusted cache using adminapi under certain circumstances_". I remember reading something about the clearing trusted cache with the adminapi awhile ago, more Googling and excellent info from [Brian Ghidinelli](http://www.ghidinelli.com/2008/07/04/clearing-trusted-cache-with-admin-api-fails) and apparently it was included in [Cumulative Hot Fix 3](http://kb2.adobe.com/cps/511/cpsid_51180.html) (CHF3). _**WTF!**_

The bug id is listed in CHF3 but not in CHF4. Bug id 75800 listed in CHF3 is _Fix for error “error SchedulerService not found” thrown in the logs when sandbox security and J2EE sessions are enabled_ but not listed in CHF4. Bug id 75676 in both CHF3 and CHF4 match as _Fix for error "The input and output encodings are not same" thrown when decrypting an encrypted string using CFMX\_COMPAT_. At this point I really don’t know what bugs CHF4 has resolved since the bug ids in CHF4 should be inclusive of CHF3 but they are not.

Adobe **PLEASE** rewrite the entire CHF4 documentation! The number of errors contained in it are atrocious. I shouldn’t have to rely on Google to correctly install CHF4.

Anyway, I installed hf801-71557 and skipped hf801-71975 since they should already be included in CHF4 (hopefully). So I think I now have a patched ColdFusion 8.0.1 to CHF4. This is just too much work, no wonder no one has bothered to update the ColdFusion Servers.

## And there is still MORE.

Yes, more. There have been two hot fixes released since CHF4, that depending upon the ColdFusion configuration might need to be applied. Also there are other [ColdFusion 8.0.1 Hot Fixes](http://kb2.adobe.com/cps/402/kb402604.html#main_ColdFusion_8_0_1_Hot_Fixes) that have not been rolled into a CHF that might be applicable as well, like:

  * [Updated ColdFusion 8.0.1 ServerMonitorUI.swf](http://kb2.adobe.com/cps/403/kb403515.html)
  * [Patch for Performance Monitor with ColdFusion 8.0.1](http://kb2.adobe.com/cps/404/kb404026.html)

Next, [ColdFusion Security Bulletins](http://www.adobe.com/support/security/#coldfusion) that as of April 5, 2011 have twelve listed for ColdFusion 8. There is no way without clicking through them to know if they apply to 8.0.1. The bottom four, ASPB07-19, APSB08-08, APSB08-07, and APSB08-06, do not apply to 8.0.1. The next four, APSB08-12, APSB08-21, APSB09-09, APSB09-12 were applied with CHF4 if you did the security fixes that were listed in it. That leaves four, APSB10-05, APSB10-11, APSB10-18, APSB11-04, that still need to be applied.

Lastly, [Oracle Security Alert CVE-2010-4476](http://kb2.adobe.com/cps/894/cpsid_89440.html).

## There has to be a better way

I know I am not the only one that has to do this, so went looking for a solution. I found an interesting solution in John Mason’s [cfUpdater](http://www.codfusion.com/blog/page.cfm/projects/cfupdater). It is a custom extension for the ColdFusion Administrator that lets you see and install updates that Adobe has released. Very nicely done, but has one problem in that it can’t handle manual updates. Adobe should look at cfUpdater and see if something similar could be done for ColdFusion X.

Adobe is heading down the exact same road with ColdFusion 9, it just isn’t as bad yet. The current way of delivering hot fixes and security bulletins works if you need it immediately but not when there are several that need to be applied. Maybe a yearly updater is the answer for ColdFusion. Adobe updates Reader quarterly, so I don’t think it is too much to ask for a yearly ColdFusion update.

The definite solution for ColdFusion 8.0.1 is that Adobe needs to package all of the hot fixes, security bulletins, and JVM update into ColdFusion 8 Update 2 (8.0.2). It is now over 3 years since [Update 1](http://www.adobe.com/support/coldfusion/downloads_updates.html#cf8) was released. Update 2 is long over due.