+++
author = "David Epler"
categories = ["ColdFusion", "Railo", "CFML", "Grails", "Security"]
date = "2013-02-01T13:00:00-05:00"
draft = false
title = "Better XSS Protection for CFML"
slug = "better-xss-protection-for-cfml"
+++

So like quite a few [others](http://compiledammit.com/about-us/), I have been working with [Groovy](http://www.groovy-lang.org/) and [Grails](http://grails.org/) much more. I'm not going to go into how much better or more joyful it is to work with than CFML but to take ideas from it and lobby to get them implemented in Adobe ColdFusion and Railo.
  
The [ESAPI encoders](https://github.com/ESAPI/esapi-java-legacy/blob/develop/src/main/java/org/owasp/esapi/Encoder.java) are now baked into the language for both Adobe ColdFusion 10 and Railo 4 and can help prevent XSS by using the proper encoder depending upon output context, `EncodeForHTML(string)` [ACF, Railo] or `ESAPIEncode("HTML", string)` [Railo] in most cases. It is possible to get the same functionality in older versions using [ESAPI4CF](https://github.com/damonmiller/esapi4cf) or [CFBackPort](https://github.com/misterdai/cfbackport#readme). But the problem is to fully protect against XSS you need to go through all the code in an application that renders output and modify it to use the proper encoder.

<!--more-->

Now where Grails makes this easy is that they offer a way to set a default encoder on an application level through Config.groovy [kind of like Application.cfc]

```groovy
grails.views.default.codec = "html"
```

Instead of having to write `${params.firstName.EncodeAsHTML()}` [for ACF this would be like `#EncodeForHTML(form.firstName)#`], Grails just does the EncodeAsHTML automatically on `${params.firstName}`; no need to add .EncodeAsHTML(), so no code change.
  
In Grails there is also the ability to toggle the behavior on a per-page basis with `<%@page defaultCodec="html" %>` [for CFML probably `<cfprocessingdirective>`, maybe `<cfsetting>` never really got the difference other than the attributes]
  
As you can see writing better XSS defended applications in Grails is a bit easier (um, making hard things easy?). It is possible to get the same functionality into CFML but there needs to be several additions to the language:
  
1. **_EncodeFor_** attribute for `<cfoutput>`, `<cfprocessingdirective>`, and `writeOutput()`

  * The default value for EncodeFor would be "none" to allow for backwards compatability unless set in Application.cfc (or possibly server/context level in the Administrator) 
      * Personally think it should be "HTML" but would probably break way too much code, maybe for Secure Profile
  * All the ESAPI encoders would be valid values for EncodeFor 
      * HTML, HTMLAttribute, CSS, Javascript, URL, XML, XMLAttribute, XPath, LDAP, DN, VBScript, and None

2. New **_this.defaultEncodeFor_** variable in Application.cfc

  * Following the outline for the addition to the tags/function for default and values listed above

3. If there is an EncodeFor\* inside a block, the closest EncodeFor\* takes precedence

```html
<cfouput encodeFor="HTML">
#url.name#
<a href="whatever.cfm?id=#EncodeForURL(url.id)#">Link</a>
</cfoutput>
```

In the example above everything would be `EncodeForHTML` except for what was directly inside the `EncodeForURL()`. 
  
A little over a month ago I did submit it to Adobe as a Enhancement Request [3434473](https://bugbase.adobe.com/index.cfm?event=bug&id=3434473), but like others have found it seems to be a "blackhole". It is a bit surprising that there has been nothing noted on it by Adobe even though I clasified the request as Security for the product area and they claim to put a priority on security. If you think this would be a good enhancement, please go vote it up.