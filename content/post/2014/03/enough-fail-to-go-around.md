---
author: David Epler
date: 2014-03-24T14:00:00-04:00
draft: false
title: Enough Fail to Go Around
slug: enough-fail-to-go-around
categories:
 - "ColdFusion"
 - "Security"
---

So the talk surrounding the Krebs on Security post, [The Long Tail of ColdFusion Fail](http://krebsonsecurity.com/2014/03/the-long-tail-of-coldfusion-fail/), continues. Some have taken issue with that he seems to be singling out ColdFusion. Personally, I like the fact that he is reporting on breaches. It helps bring to light issues with installs that are out there, so others can learn from the problems. The ones he has highlighted are severe since they involve credit card processing. 

The underlying problem is that hackers have identified ColdFusion as an easy target and are going after it. The only way to fix that is to make it more difficult to attack and compromise, but that requires involvement from everyone that touches a ColdFusion installation. 

<!--more-->

Now I have no involvement with eLightBulbs.com and these are my impressions based upon the information that is publicly available from the following sources:

* [The Long Tail of ColdFusion Fail](http://krebsonsecurity.com/2014/03/the-long-tail-of-coldfusion-fail/)
* Paul McLellan's [comment](http://krebsonsecurity.com/2014/03/the-long-tail-of-coldfusion-fail/comment-page-1/#comment-234075) on the post
* Wil Genovese's post [IIS Vulnerability Steals Payment Information](http://www.coldfusionmuse.com/index.cfm/2014/3/6/IIS.Vulnerability.CF.Task.Scheduler.API)


## Security Firm

eLightBulbs.com had a third party firm perform annual PCI compliance penetration testing and apparently this firm did not find any [ColdFusion 8 vulnerabilities](http://www.cvedetails.com/vulnerability-list/vendor_id-53/product_id-8739/version_id-49380/Adobe-Coldfusion-8.0.html) with the installation. I find that a bit hard to believe. They should have had at least one finding stating that the CFIDE directory was publicly available. Another risk that should have been noted was that ColdFusion 8.0.x had reached end of core support on July 31, 2012 (Extended support for ColdFusion 8.0.x ends on July 31, 2014).

There are many tools out there that will identify ColdFusion issues. [HackMyCF](https://foundeo.com/hack-my-cf/), by far, is the best ColdFusion specific tool to find configuration issues. [Nessus](http://www.tenable.com/products/nessus) currently has 40 plugins that deal with ColdFusion. Either tool most likely would have found issues. The specific issues found would depend upon the configuration and patches applied.

Without knowing the exact scope of the testing, tools used, and state of the ColdFusion install, it is hard to say how good of a test this firm actually performed. If I was using them, I'd really question them on how they do things because as it looks, they were just taking $6000 a year from eLightBulbs.com.

## Hosting Provider

While it has been stated that the hosting provider that eLightBulbs.com used wasn't contractually obligated to patch and secure the VPS they were using, one would hope that the hosting provider would have been a bit more hands-on regarding security. Given that the eLightBulbs.com hackers were able to inject a malicious IIS DLL, they had complete control of the VPS guest OS. Depending on virtualization software, it might have been possible for the hackers to break out of the guest OS that ran the VPS, take control of the host OS, and pivot to attack other servers the hosting provider runs.

It is really in the interest of the hosting provider to help customers maintain a secure environment.

## Business

eLightBulbs.com is a story where they thought they were doing everything right and it went terribly bad. They were handling credit cards and doing annual PCI compliance testing as they were required to. They had a service level agreement (SLA) with the hosting provider and thought the hosting provider was providing support to patch and secure their VPS through a managed service contract.

Unfortunately, they were too hands off regarding security and seems like they did not completely understand the scope of services or assumed some services were included in the various agreements they had with the security firm and hosting provider. 

The other area where eLightBulbs.com was at fault was not staying on a supported version of ColdFusion. While just upgrading would have put them on a supported version, the underlying problems of properly securing the environment probably would have still existed.

The positive from this is that eLightBulbs.com has been very forth coming with details of their experience and the steps they have taken to remedy their security issues.

## Software Vendor

Some will probably not like what I have to say in regards to Adobe, but Adobe has not done enough to help the situation. Unlike the first three sections, I can speak here from direct experience.

Adobe has not learned from the mistakes Microsoft made with early versions of IIS, to install the product with defaults that make it secure from the start. **Do not** rely on the sysadmins to come back around to secure it. This is precisely the problem with the published lockdown guides. There is an expectation that whoever is installing ColdFusion knows the lockdown guides exist and follows them properly. It also does not help that they have been published months after the release of the product. That at least will be rectified with ColdFusion 11 (hopefully).

There were improvements regarding security in ColdFusion 10, but as the past year has shown they are not enough. Adobe touted that they put ColdFusion 10 through Veracode, AppScan, and fuzzing ([slide 8](http://blogs.coldfusion.com/assets/content/Hemant/ncdevcon_2012/Security_CF_10.pdf)) to find security issues. Given the [ColdFusion 10 vulnerabilities](http://www.cvedetails.com/vulnerability-list/vendor_id-53/product_id-8739/version_id-134907/Adobe-Coldfusion-10.0.html) found so far, the code review process for security issues should be improved.

Another security feature in ColdFusion 10 that has been pushed is **Secure Profile**. While it does improve the security settings within ColdFusion, it is an OPT-IN option in the installer (appears this will be fixed in ColdFusion 11, Bug #[3529334](https://bugbase.adobe.com/index.cfm?event=bug&id=3529334)) but **does not protect** the _CFIDE_ directory as well as if one follows the lockdown guide. At [NCDevCon](http://ncdevcon.com/) last year I [showed](https://www.youtube.com/watch?v=XsQWK_UaASk) how ColdFusion 10 with Update 9 applied and Secure Profile turned on but not locked down as per the lockdown guide could be exploited using the [Sub-Zero v2 script](http://www.exploit-db.com/exploits/25305/).

Patching ColdFusion 8.0.x and 9.0.x is an absolute pain, which is how [Unofficial Updater 2](https://www.uu-2.download) (UU2) came about. While UU2 is not perfect, it does make it a hell of a lot easier for older versions.

Patching has gotten better in ColdFusion 10 with the **HotFix Installer** but there are still issues. Almost all of the issues regarding patching are about the quality of the patches issued. The track record has not been good.

As I showed in my previous post, [How patching ColdFusion 8.0.x made you more vulnerable in some cases (or fun with CVE-2013-0632 from APSB13-03)](/post/how-patching-coldfusion-8-0-x-made-you-more-vulnerable-in-some-cases-or-fun-with-cve-2013-0632-from-apsb13-03), Adobe caused CVE-2013-0632 with a security hotfix and was not dealt with for nearly 5 years until it became widely exploited. Adobe had to pull Update 3 for ColdFusion 10 completely. They have had to re-issue other updates due to errors. In the case of [APSB13-10](http://www.adobe.com/support/security/bulletins/apsb13-10.html) [Update 9] they broke functionality that was not related (Bug #[3540876](https://bugbase.adobe.com/index.cfm?event=bug&id=3540876)) and people had to wait over a month until [APSB13-13](http://www.adobe.com/support/security/bulletins/apsb13-13.html) [Update 10] to get it resolved. These patch quality issues directly impact the confidence people have in applying them and leaves more installations vulnerable because of the slower adoption rate of the patches.

The communication of security hotfixes and updates for ColdFusion could also be improved. ColdFusion 10 will generate a notification regarding updates, but only if it is configured to do so. What is needed is a notification service that is more like the [Adobe Security Notification Service](http://www.adobe.com/cfusion/entitlement/index.cfm?e=szalert) which notifies for all updates to ColdFusion not just security ones. Not everyone reads blogs or follows [@ColdFusion](https://twitter.com/coldfusion) on Twitter. Adobe should be contacting those with support agreements directly via email and telephone when any update to ColdFusion occurs, otherwise what are they really paying for?

Adobe needs to engage more with its customers regarding ColdFusion security. They need to ask their customers if they are having any problems and fix them or direct them to companies and people that can. [Marketing Plug: [AboutWeb](http://www.aboutweb.com) has experience in securing ColdFusion and the entire web stack. We have done this for numerous clients and if you need help, please contact us.] 

Also while I don’t expect them to comment on all the ColdFusion breaches that occur, silence does not help.

## Developers

While nothing in the eLightBulbs.com story directly talked about code developers wrote being exploited, developers have a role in security as well.

Unfortunately, too many ColdFusion applications are written poorly in regards to security. Part of that is due to the materials that are the _de-facto_ standard for teaching ColdFusion, [The ColdFusion Web Application Construction Kit](http://www.amazon.com/Adobe-ColdFusion-Application-Construction-Volume/dp/032166034X) (CFWACK). I respect all the authors of the series, but it is time for a complete re-write showing good, modern, and secure ColdFusion coding practices. The community itself tried to tackle this problem with [Learn ColdFusion in a Week](http://www.learncfinaweek.com/?campaign=DavidEpler), for which I contributed the chapter on security.

The reality is developers need to know how to write secure code. If you are a developer and have no idea what SQL injection is or why cross-site scripting (XSS) can be extremely dangerous, among others, you need to improve your skills. There are many resource out there, but the first one I’d point you to is [OWASP](https://www.owasp.org/index.php/Main_Page) with the [2013 Top Ten](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project) and various [cheat sheets](https://www.owasp.org/index.php/Cheat_Sheets).

The bottom line is that it takes everyone involved with a web application to ensure the security of it. A security breach can happen to anyone and does not matter the underlying technology used.
