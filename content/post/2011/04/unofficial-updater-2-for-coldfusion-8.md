---
author: David Epler
date: 2011-04-18T09:20:00-04:00
draft: false
title: Unofficial Updater 2 for ColdFusion 8
slug: unofficial-updater-2-for-coldfusion-8
categories:
  - "Unofficial Updater 2"
  - "ColdFusion"
  - "Apache Ant"
tags:
  - "Ant Installer"
---

So earlier this month, I wrote [What does a fully patched ColdFusion 8.0.1 Server look like?](/post/what-does-a-fully-patched-coldfusion-8-0-1-server-look-like/) which outlined my frustration and problems with the way Adobe currently releases hot fix and security updates for ColdFusion. Ultimately, my conclusion was that Adobe needs to release Update 2 for ColdFusion 8. While it felt good to write it all up, it didn’t solve the basic problem of getting a fully patched ColdFusion 8.0.1 Server. I still have to update multiple servers and applying all the published hot fix and security updates in order by hand just isn’t an option. It is too time consuming and error prone.

<!--more-->

So after studying all of the published hot fix and security updates for ColdFusion 8.0.1, I was able to produce this [matrix](https://github.com/dcepler/unofficial-updater2/blob/master/cf801-hotfix-matrix.pdf?raw=true). Out of the 24 items published, only 5 had to be completely installed and another 5 are partially installed. Of the remaining 14 items, 10 were superseded (mostly from CHF4 and ASPB11-04) and the last 4 items were system configuration specific or didn’t need files applied. Cutting down on the number of patches that need to be applied was great. Now I just needed a way of doing it repeatedly against multiple servers.

## Automating the process

For me it was clear that writing an [Apache Ant](http://ant.apache.org/) script would be the best choice since I only want to write it once and have it run on Windows, Mac, Linux/Unix. The process was simple, get information about how ColdFusion is installed, backup the files, download the updates from Adobe and finally apply them based upon the published instructions. I got the script working great, but required that Java 1.5+ and Ant 1.7+ with [ant-contrib](http://ant-contrib.sourceforge.net/) to be installed to run. The Java requirement wasn’t a problem, but I couldn’t guarantee that Ant with ant-contrib would be available on the server since I had to hand it off to the system administrators to run it. The solution, [AntInstaller](http://antinstaller.sourceforge.net/). It allows you to package Ant scripts in a run-able installer that only requires Java. AntInstaller had another bonus in the ability to create both a GUI and text based installer. This got me thinking.

## Creation of Unofficial Updater 2

If I tweaked my Ant script to work with all the ColdFusion installation types and package it with AntInstaller, I could create my own Unofficial Updater 2. Given the fact that others have to be encountering the same problems and it is extremely doubtful that Adobe will be releasing an Update 2 any time soon, I have released it to [github](https://github.com/dcepler/unofficial-updater2).  All the scripts and information is there. The run-able installer is also available to download, [Unofficial-Updater2.jar](https://github.com/dcepler/unofficial-updater2/downloads). The installer does not contain any of the updates inside it, you must have an internet connection so they can be downloaded.

Please read the instructions that are packaged with Unofficial Updater 2, but here are some of the important items.

Unofficial Updater 2 is **NOT** endorsed by or have any ties to Adobe. I have tried to make sure Unofficial Updater 2 works in all possible configurations, but you use it at your own risk. It only updates files and will not modify any system configuration files such as jvm.config, web server connectors, or system registry. Make sure the ColdFusion Server/process is **NOT** running before using Unofficial Updater 2.

Lastly, if you have any comments, ideas, or updates please feel free to share them, that was one of the reasons I released Unofficial Updater 2 on github.