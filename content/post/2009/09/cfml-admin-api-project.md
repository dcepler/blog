---
author: David Epler
date: 2009-09-28T23:00:00-04:00
draft: false
title: CFML Admin API Project
slug: cfml-admin-api-project
categories:
  - "Projects"
  - "ColdFusion"
tags:
  - "Adobe ColdFusion"
  - "Railo"
  - "OpenBD"
  - "CFML"
  - "CFMLAdminAPI"
---

Well, this isn't exactly a new project. I actually started it back in 2005 when I wrote an Admin API for BlueDragon 6.2 and had a compatibility layer to map **_cfide.adminapi_** calls back to the BlueDragon Admin API.

For the past several years the code has been available on [various locations](/page.cfm/code). Ultimately, the Admin API for BlueDragon 6.2 that I wrote became the basis for the Open BlueDragon Admin API, but the compatiblity layer was not used. The direction of building a compatibility layer to match ColdFusion MX 7 (or later) didn't seem to be a sustainable idea, since I'd always have to chase how the ColdFusion Admin API was implemented for calls and returns.

<!--more-->

I don't know why it didn't occur to me earlier, but it became clear while sitting in the [The CFML Advisory Committee - Happy First Birthday! BOF](http://cfunited.com/2009/topics/323). Forget making all the other CFML engine Admin API interfaces match ColdFusion Admin API, but make a single common Admin API interface. That is exactly what [CFML Admin API](http://cfmladminapi.riaforge.org/) is. Its goal is to provide a common Admin API methods for dealing with datasources and mappings that work on any CFML engine, particularly when creating/installing CFML applications.

The code is still very alpha and hopefully will get comments for improvements.