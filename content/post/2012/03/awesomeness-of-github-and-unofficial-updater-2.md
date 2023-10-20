---
author: David Epler
date: 2012-03-15T08:00:00-04:00
draft: false
title: Awesomeness of github and Unofficial Updater 2
slug: awesomeness-of-github-and-unofficial-updater-2
categories:
  - "Unofficial Updater 2"
tags:  
  - "github"
---

So originally I was going to post a note that Unofficial Updater 2 was broken since I got several emails saying that it was failing when trying to download files from Adobe. Instead, I'm going to rave about having the project on [github](https://github.com/dcepler/unofficial-updater2).
  
So Adobe has changed some the URLs to the hot fix downloads (really no URL rewrites/redirects?) and I wasn't sure when I'd get them fixed exactly. It probably would have been by this weekend since I already need to update Unofficial Updater 2 with [APSB12-06](http://www.adobe.com/support/security/bulletins/apsb12-06.html) that was released this past Tuesday.

<!--more-->

But while I was sleeping, [Dennis Clark](https://github.com/boomfish) had already updated the [cf_hotfixes.properties](https://github.com/dcepler/unofficial-updater2/blob/master/cf_hotfixes.properties) that contains the URLs and sent a [pull request](https://github.com/dcepler/unofficial-updater2/pull/16). All I had to do in the morning was accept the pull request and repackage the installer. Luckly, Adobe only changed the URLs for the hot fix downloads and not the actual files (that would have shown up with SHA-512 hash failures). The only problem Dennis had was that he couldn't re-package Unofficial-Updater2.jar. To do that requires having [Ant Installer](http://antinstaller.sourceforge.net/) and modifiying [create-installer.xml](https://github.com/dcepler/unofficial-updater2/blob/master/create-installer.xml) since it is setup with paths for my computer.

It is actually possibly to slip-stream files into the **_Unofficai-Updater2.jar_** by using `jar` so you don't need Ant Installer or wait for me.

```shell
jar uf Unofficial-Updater2.jar cf_hotfixes.properties
```

The fixed Unofficial-Updater2.jar is now available on [github](https://github.com/dcepler/unofficial-updater2/downloads). As I said earlier, there will be another update to it to support the latest security hot fix shortly.

Again, thanks to Dennis for getting the pull request to me and to github for making it just so damn easy.