+++
author = "David Epler"
categories = ["Ant"]
date = "2009-11-12T12:40:00-05:00"
draft = false
title = "Hiding password input in Ant"
slug = "hiding-password-input-in-ant"
+++

When writting Ant scripts I always have Ant prompt for passwords be it for SVN, SFTP, or anything else that needs to be logged into. Typically would have the following:

```xml
<input message="Please enter SVN password:" addproperty="svn.password" />
```

<!--more-->

The only problem is that it echos the password back at you, there has to be a better way. So of to Google I went and [found this](http://marc.info/?l=ant-user&m=119448947811275&w=2) with an interesting Ant script fragment:

```xml
<input message="secure-input:" addproperty="the.password">
    <handler classname="org.apache.tools.ant.input.SecureInputHandler" />
</input>
```

I did not know there could be nested elements in `<input>`. Apparently Ant 1.7 added `<handler>` nested element for [`<input>`](http://ant.apache.org/manual/CoreTasks/input.html). But nowhere is there any documentation on **SecureInputHandler**.
  
So I tried out the fragment and as the post noted there are a few requirements to get it to work:

  1. Ant 1.7.1
  2. Java 6, if it is run on Java 5 it will fallback to a "normal" `<input>`

One downside, I have not been able to get it to work from within Eclipse 3.5 (since Ant 1.7.1 is bundled with it) and using Java 6 runtime. Eclipse will just hang when it gets to the **SecureInputHandler** and you have to stop the build script. It does work great from command line which is how I run all my Ant scripts anyway so it is not a real issue for me, but might be for others.