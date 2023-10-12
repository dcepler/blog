+++
author = "David Epler"
categories = ["ColdFusion", "Security", "Unofficial Updater 2"]
date = "2013-01-06T19:30:00-05:00"
draft = false
title = "File Integrity Checking CFIDE"
slug = "file-integrity-checking-cfide"
+++

So with the most recent attack on ColdFusion (detailed by Charlie Arehart, [Part #1](http://www.carehart.org/blog/client/index.cfm/2013/1/2/serious_security_threat), [Part #2](http://www.carehart.org/blog/client/index.cfm/2013/1/2/Part2_serious_security_threat)) there was a comment left on the post that got me a bit concerned where the comment said all you had to do is search for `h.cfm` to remove the file placed by the attacker. My experience has been if an attacker has had access to the server there is no absolute way of knowing what they might have done, even with good log reconstruction. As I noted in my comment in one instance I have previously encountered a situation where an attacker put a file called `fck_dialog_common.cfm` into `CFIDE/scripts/ajax/FCKeditor/editor/dialog/common`. At first glance of the directory it looks right, but inactuallity it a file that was buried and hidden so the attacker could come back through it instead of the original entry point. 
  
The only way to know is to have a way of doing file integrity checks against a good known source. The initial attack that was posted to the [Adobe forum](http://forums.adobe.com/message/4962104) was found because an [intrustion detection system (IDS)](http://en.wikipedia.org/wiki/Intrusion_Detection_System) alerted the administrator that a file had been written to CFIDE that was called `h.cfm`.

<!--more-->
  
There are several types of IDS, the one that caught this type of attack was a [host-based IDS](http://en.wikipedia.org/wiki/Host-based_intrusion_detection_system). The most well known is [Tripwire](http://www.tripwire.com/) which is a commercial product, although there is an open source version on [SourceForge](http://sourceforge.net/projects/tripwire/). There is also another called [OSSEC](http://www.ossec.net/) which is quite full featured, cross-platform, and open source. Now deploying a full host-based IDS can be complex and time consuming, since they have many more features than just file integrity checking.
  
You could manually write a script that traverse directories and creates MD5 or SHA-1 hashes of all the files, but there is a utility called [md5deep and hashdeep](http://md5deep.sourceforge.net/) that makes it easier and provides a way to compare directories against a list of known hashes. The utility is free and available for every OS that is out there.
  
Below is a listing of hashdeep hashsets that will validate CFIDE for ColdFusion 8.0.1, 9.0.1, and 9.0.2 patched through APSB12-21 using Unofficial Updater 2 on a clean install. Because Adobe has made the security hotfixes cumulative, it is possible to check CFIDE in various security patch revisions for given versions of ColdFusion. APSB12-21 was the last security hotfix for ColdFusion 8.0.1 and APSB12-26 did not modify any files in CFIDE. For ColdFusion 10 there is one for Update 6 (APSB12-26) but should be valid going all the way back to Update 4. It is possible to use the hashdeep hashsets for ColdFusion 8.0.1 and 9.0.1 going all the way back to APSB11-14 but it will report that `CFIDE/adminapi/security.cfc` and `CFIDE/administrator/security/_cffunctionsoptions.cfm` do not match since they where changed in APSB12-21. Since Unofficial Updater 2 does not run against ColdFusion 8.0.0 or 9.0.0 there are no hashdeep hashsets for those versions. The hashsets are OS specific for Windows and Unix/Linux/Mac OS X since it seems hashdeep does not translate between \ and / for paths.

| Hash Set | MD5 Hash |
| -------- | -------- |
| [CFIDE-CF801-patched-APSB12-21-unix.txt](https://raw.github.com/dcepler/cfide-integrity/master/CFIDE-CF801-patched-APSB12-21-unix.txt) | a5e0c09ba46f3454b1274520dd1d51c5 |
| [CFIDE-CF801-patched-APSB12-21-win.txt](https://raw.github.com/dcepler/cfide-integrity/master/CFIDE-CF801-patched-APSB12-21-win.txt) | baa69cc859612d86b044e4c2dd177b5b |
| [CFIDE-CF901-patched-APSB12-21-unix.txt](https://raw.github.com/dcepler/cfide-integrity/master/CFIDE-CF901-patched-APSB12-21-unix.txt) | a29865a0d5f7148e05b0fd297996ffe5 |
| [CFIDE-CF901-patched-APSB12-21-win.txt](https://raw.github.com/dcepler/cfide-integrity/master/CFIDE-CF901-patched-APSB12-21-win.txt) | f97d974f59fab2fa655b46d87e783d76 |
| [CFIDE-CF902-patched-APSB12-21-unix.txt](https://raw.github.com/dcepler/cfide-integrity/master/CFIDE-CF902-patched-APSB12-21-unix.txt) | 7b8f046f4526530335c08ba053e4fd1f |
| [CFIDE-CF902-patched-APSB12-21-win.txt](https://raw.github.com/dcepler/cfide-integrity/master/CFIDE-CF902-patched-APSB12-21-win.txt) | 254143a19f50b104bdae67ee1c3a8cf6 |
| [CFIDE-CF10U6-patched-APSB12-26-unix.txt](https://raw.github.com/dcepler/cfide-integrity/master/CFIDE-CF10U6-patched-APSB12-26-unix.txt) | 52e5b6cc7d761e3d161b4d4d2f7fdc98 |
| [CFIDE-CF10U6-patched-APSB12-26-win.txt](https://raw.github.com/dcepler/cfide-integrity/master/CFIDE-CF10U6-patched-APSB12-26-win.txt) | d9ec43aa354b6f2f76cc1052bd300f0c |

To check your CFIDE against the hashdeep hash for your version, you need install hashdeep and to go to the directory above CFIDE as shown below (Windows):

```shell
cd \ColdFusion9\wwwroot

hashdeep -k c:\temp\CFIDE-CF901-patched-APSB12-21-win.txt -l -a -v -v -r CFIDE
```

The **-k** tells hashdeep to compare against a file that has the hashes, **-l** is for relative path, **-a** is for audit mode, the double **-v** is so the audit reports the files that failed the audit along with the audit statistics, and **-r** is recursive.
  
To create your own hashes:

```shell
cd \ColdFusion9\lib

hashdeep -l -r *.jar > c:\temp\cfusion-lib-jars.txt
```

This will create a hashdeep hash file of all the jar files which can be used to check against.
  
Now it is possible to make a poor-man's IDS with hashdeep if you create a script that runs through an OS scheduled task and emails if a file check fails. Also note that this is all done command line on the OS. The reason is that you do not want the integrity checking dependent upon any part of the web stack (web server, applications server) that could be attacked. 
  
I am looking into how to integrate hashdeep with [Unofficial Updater 2](http://www.uu-2.download), so that when the updater is run it can report if it finds something that shouldn't be there. Hopefully Adobe puts something like this into the Automatic Updater that is in ColdFusion 10. Also since Adobe has announced with security advisory [APSA13-01](http://www.adobe.com/support/security/advisories/apsa13-01.html) that there will be a security patch to fix this on January 15, 2013, I do plan on getting Unofficial Updater 2 updated that day so it applies the new security patch for ColdFusion 9.0.1 and 9.0.2.