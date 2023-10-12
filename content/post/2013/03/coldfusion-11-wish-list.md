+++
author = "David Epler"
categories = ["ColdFusion"]
date = "2013-03-25T15:25:00-04:00"
draft = false
title = "ColdFusion 11 Wish List"
slug = "coldfusion-11-wish-list"
+++

So last week the ColdFusion product team announced a survey to get selected into the [pre-release program](http://blogs.coldfusion.com/post.cfm/pre-release-for-coldfusion-splendor) for the next version of ColdFusion (refuse to call it by the code name since all I think of is [Splenda](http://www.splenda.com/)). A lot of this has been rolling around in my head since they published the [roadmap](http://blogs.coldfusion.com/post.cfm/product-roadmap-for-coldfusion) last August and really need to get this out before there is a possibility of being included in the pre-release and the requisite NDA. 

<!--more-->

## Security

ColdFusion 10 did focus on security and by far was the most significant release to address the issue. It is listed on the roadmap, but can still be improved.

### Installation

One of the areas that would improve the security of ColdFusion would be to make several changes to the installer.
  
First, **Secure Profile** should be an **_opt-out_** with a checkbox "_Disable Secure Profile_". In the ColdFusion 10 installer it is an **_opt-in_** with "_Enable Secure Profile_". There are too many administrators that just click through the installer. By explictly making them **_opt-out_** of **Secure Profile**, it would make them think about the implications of not selecting it and most would probably leave it as is. No one wants a less secure install.
  
Second, the installer on Windows should allow one to change the default user that ColdFusion runs as just like the installer for Linux has done for ages. Those that attack ColdFusion specifically look for Windows installs since the majority of installs are left running as **SYSTEM**.
  
Lastly, while the [lockdown guide](https://www.adobe.com/content/dam/Adobe/en/products/coldfusion/pdfs/cf10/cf10-lockdown-guide.pdf) is well done and extremely useful, it should be published as soon as the version is released (May 14, 2012), not 6 months afterwards (November 28, 2012). The lockdown guide should also be prominently displayed on the ColdFusion download page and within the ColdFusion Administrator.

### Sandboxing

Sandboxing within ColdFusion is probably one of the more under utilized security features the product has had for the longest time. Part of that is due to the fact it requires an Enterprise license to create multiple sandboxes. This is one area where the distinction between Standard and Enterprise should be dropped. **Security should never be a for pay feature**.
  
There are several enhancements to sandboxing that should be done as well. The CFIDE sandbox does not apply to scheduled tasks or system probes and **it should**. If they aren't part of CFIDE sandbox, they should have their own sandbox defined for themselves. All sandboxes should be pre-defined to only allow for access to 127.0.0.1 port 80 so the administrator has to explicity open access to external systems, as opposed to allowing all connections which is the current default. Another minor issue is that it only allows for IP addresses and should allow for fully qualified domain names. Finally, sandboxing should be enabled by default when **Secure Profile** is enabled.

## PDFs

The ability to create PDFs was one of the best additions to ColdFusion back in version 7. Unfortunately though the functionality has seemed to stagnate. This is the **one** area that ColdFusion can really set itself apart and excel at; better rendering of HTML to PDF for Section 508 support as noted in bug id [3041212](https://bugbase.adobe.com/index.cfm?event=bug&id=3041212), more integration with PDF forms like noted in bug id [3117809](https://bugbase.adobe.com/index.cfm?event=bug&id=3117809), and handling signatures. The dependence ColdFusion has on iText, jPedal, and OpenOffice should be removed. It was understandable back in ColdFusion 7 and 8 when it was developed by Macromedia. PDF is an Adobe technology, as is ColdFusion; this should be do-able. Hopefully this will happen since the roadmap says, "_Revamped and new PDF functionalities_".

## Integration

The strength of ColdFusion has always been its ability to integrate with various back-end technologies like Java, .Net, Exchange, SharePoint, and Office documents. One of the main problems has always been things are never fully baked or key functionality is missing. A prime example is the lack of NTLM and Digest support on HTTP calls. It has been a long requested feature originally logged as bug id [72751](http://www.elliottsprehn.com/cfbugs/bugs/72751) and migrated as bug id [3035879](https://bugbase.adobe.com/index.cfm?event=bug&id=3035879). It is currently marked as **_Deferred/Not Enough Time_** from ColdFusion 9.0 Alpha 1 (probably has been asked for longer, but can't find references). There is another bug id [3175165](https://bugbase.adobe.com/index.cfm?event=bug&id=3175165) which is strictly NTLM support and is set as **_To Fix_** from ColdFusion 9.0.1, but nothing on Digest. One could argue that this should have been addressed by now so ColdFusion can stay ahead of requirements coming from clients (seriously look at bug id [3175165](https://bugbase.adobe.com/index.cfm?event=bug&id=3175165), the developer is pleading for it so that ColdFusion can stay relevant at a large US Government agency).

## Reporting

Reporting is one area where integration is lacking. It is time to face the fact that ColdFusion Reports and ColdFusion Report Builder are defunct; no real update has occurred since version 8. Just kill it off. Integrating with a modern version of Crystal Reports for all platforms (not just Windows) and allowing for easy integration with Jasper Reports or BIRT should be the focus to solve the lack of good reporting solutions in ColdFusion.

## Social Media

The one area of the roadmap that is of concern is "_Enabling Enterprise to easily integrate with Social Media Streams_". It is extremely [buzzword compliant](http://www.buzzphraser.com). Hope this does not mean `<cftwitter>`, `<cffacebook>`, or `<cfsocialmedia>` tags or functions. While these sound good in concept, just look at the issues with `<cfmap>` and the changing of Google Maps API from v2 to v3. There are projects on [riaforge.org](http://www.riaforge.org) like [(monkeh)Tweet Twitter API](http://monkehtweet.riaforge.org) that can provide the same integration and faster turnaround to API changes. 
  
Getting a feed from Twitter is easy; integrating NTLM and Digest authenication is hard. Get back to making hard things easy.

## Deployment

This is an area where ColdFusion has been severely lacking. While there are ColdFusion Archives (CAR) and J2EE Archives (WAR/EAR) in Enterprise, neither for these solutions easily integrates with a build environment. Both require interaction with the ColdFusion Administrator. There needs to be an easy way to script deployments, probably with Ant since pretty much every build environment can interact with it. The other issue with the existing J2EE Archives is that the resulting output is ridiculously large to support even the most basic ColdFusion Application. There needs to be a way to select only needed functionality into the WAR/EAR. If the ColdFusion Application isn't using Flex or `<cfform>` stuff, should be able to pull it out of the deployment.

## Vote Up Existing Bugs, Suggest Enhancements

So even if you don't get into the pre-release for ColdFusion 11, what can you do? The best thing would be to go through the existing bugs to see if any issues you have are currently reported and vote it up. While the [Adobe Bugbass](https://bugbase.adobe.com/index.cfm?event=search) is a pain to search, try the [simple interface](http://adamcameroncoldfusion.cfmldeveloper.com/cfbugs/search.html) that [Adam Cameron](http://adamcameroncoldfusion.blogspot.com) created. If you have an enhancement, submit it to the Adobe Bugbase and then get people to vote it up. Follow [@cfbugnotifer](https://twitter.com/cfbugnotifier) on Twitter. See something on the Twitter feed, vote it up, retweet, get involved in the future of ColdFusion.
