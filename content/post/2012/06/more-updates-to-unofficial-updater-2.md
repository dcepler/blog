---
author: David Epler
date: 2012-06-26T16:30:00-04:00
draft: false
title: More Updates to Unofficial Updater 2
slug: more-updates-to-unofficial-updater-2
categories:
  - "Unofficial Updater 2"
---

It is nice that Adobe has moved to a regular release cycle of security hotfixes for ColdFusion 8.0.1 and 9.0.1. It is making my job easier to maintain [Unofficial Updater 2](https://github.com/dcepler/unofficial-updater2). There have been quite a few changes besides just updating for the latest security hotfix. Below is a detailed change log since the last release. 

<!--more-->

## Application of APSB12-15

On June 12th, Adobe released [APSB12-15](http://www.adobe.com/support/security/bulletins/apsb12-15.html) which is a security hotfix for ColdFusion 9.0.1 and earlier. UU2 now applies the hotfix as specified in Section 2 of the documentation.

## Process Termination and Automated Command Line Installs

While using [AntInstaller](http://antinstaller.sourceforge.net/) has been a great way to package and distribute UU2 it does have a downside in that it is not actively maintained and still has quite a few bugs. One of them which I never noticed was that on Windows and some Linux installs when running in text mode it never properly termininated the process when it was finished. This has been fixed by patching the AntInstaller code and creating a custom build for UU2.
  
One of the nice features that AntInstaller has is the ability to allow for [automated installs](http://antinstaller.sourceforge.net/auto.html) which is now available to use for UU2. The first time you run UU2 you must select **Yes** to **Enable cmdline automation**. By selecting **Yes**, UU2 will allow for an additional run type of **_text-auto_** which will tell UU2 to look for `ant.installer.properties` file to use for the values to run with.
  
It is recommended to run UU2 once with **_text_** to create the `ant.installer.properties` file that can be used on subsequent **_text-auto_** runs.

## Logging and File Ownership

So logging of what happened when UU2 ran was never quite straight forward. It relied upon both the Output and Errors tabs in the GUI or output to console in text mode. While both of those are still there, UU2 will now write a log in the current directory where UU2 is run called `uu2-{datetime-stamp}.log` which will log everything into a single place.
  
When running on UU2 on Linux/Unix, I never provided any guidance on whether it should be run as **root** or as the user that ColdFusion runs as. This was intentional since the administrator would be the best one to know. There are trade-offs to both. Running as **root** requires going back and making sure ownership and permissions of new files are correct. Running as a non-root user, one might encounter a failure due to inadequate permissions.
  
UU2 now identifies the user it is running as. If it is running as **root**, it will now change ownership of files to the ColdFusion user. If it is running as a non-root user, it will display a warning that it might encounter problems. In either case you should verify that ownership and permissions of the files are correct.

## ColdFusion 8.0.1 Build 196946

So I encountered this at work. We upgraded several ColdFusion 8.0.0 servers to 8.0.1 that were on RedHat and then went to run UU2 on them to patch them which promptly failed. Apparently Adobe created another build number, 196946, that was in the ColdFusion 8 Update 1 for Linux that didn't follow the [official published](http://helpx.adobe.com/coldfusion/kb/determine-version-information-coldfusion-8.html) build number **195765**. Since UU2 (and I) didn't know about it, UU2 properly failed. UU2 now can identify this build and properly patch it. The fun thing is that when you run `cfinfo` in this configuration it reports **8,0,1,196946** but **8,0,1,195765** in the ColdFusion Administrator when fully patched. Just an insight into Adobe's code since one would think the version number would be a constant.

## Wrap-up

I'd like to thank Steve Dean for suggestion for the automated installs and working through test builds. Also need to thank [Scott Stroz](http://www.boyzoid.com/) for suggestions on logging, Linux/Unix install procedure, and github pull request. This tool is really a combination of everyone that uses it and feedback for how to make it better. I do ask that if you encounter problems with UU2 to please email me or [submit an issue](https://github.com/dcepler/unofficial-updater2/issues) on github.