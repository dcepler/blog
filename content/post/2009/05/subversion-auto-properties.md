---
author: David Epler
date: 2009-05-16T13:00:00-04:00
draft: false
title: Subversion Auto Properties
slug: subversion-auto-properties
categories:
  - "Conferences"
tags:
  - "cfobjective"
  - "subversion"
  - "svn"
---

At [cf.Objective()](http://www.cfobjective.com/) I attended **_Subversion for Smarties - Do More With Subversion_** given by Cameron Childress and it was a good presentation. I picked up a few things that I didn't know before like changelists which were added in Subversion 1.5. The presentation did cover other things like svn properties on files like `svn:keywords` and how to add them with `svn propset`. While `svn propset` works, it is possible to set svn properties on files globally on the create of the file without having to manually setting them. This is done my modifying the subversion client configuration.

<!--more-->

On Mac or Linux the subversion client configuration file is:
```shell
~/.subversion/config
```

On Windows the subversion configuration file is:
```shell
C:\Documents and Settings\{username}\Application Data\Subversion\config
```

Or using TortoiseSVN on Windows:

  1. Right click on any Windows folder
  2. Select **TortoiseSVN -> Setting**
  3. Click on "**Edit**" for Subversion configuration file

The config file is used by all subversion clients, so that once you make the change it will be used by Subclipse, TortiiseSVN, svnX, etc. The config file is nothing more than a text file with name value pairs. The file uses "**#**" to denote comments, remove the "**#**" to uncomment the line.
  
The first thing you need to do is find the **[miscellany]** section of the config file to uncomment and modify the line as shown below:

```ini
enable-auto-props = yes
```

Next in the **[auto-props]** section, remove everything below **[auto-props]** and replace it with below:


```bash
# Code formats
*.as         = svn:eol-style=native; svn:keywords="Author Date Id Rev URL"; svn:mime-type=text/plain
*.bat        = svn:eol-style=CRLF; svn:keywords="Author Date Id Rev URL"; svn:mime-type=text/plain; svn:executable
*.cmd        = svn:eol-style=CRLF; svn:keywords="Author Date Id Rev URL"; svn:mime-type=text/plain; svn:executable
*.c          = svn:eol-style=native; svn:keywords="Author Date Id Rev URL"; svn:mime-type=text/plain
*.cfc        = svn:eol-style=native; svn:keywords="Author Date Id Rev URL"; svn:mime-type=text/plain
*.cfm        = svn:eol-style=native; svn:keywords="Author Date Id Rev URL"; svn:mime-type=text/plain
*.cgi        = svn:eol-style=native; svn:keywords="Author Date Id Rev URL"; svn-mine-type=text/plain
*.cpp        = svn:eol-style=native; svn:keywords="Author Date Id Rev URL"; svn:mime-type=text/plain
*.groovy     = svn:eol-style=native; svn:keywords="Author Date Id Rev URL"; svn:mime-type=text/plain
*.gsp        = svn:eol-style=native; svn:keywords="Author Date Id Rev URL"; svn:mime-type=text/plain
*.h          = svn:eol-style=native; svn:keywords="Author Date Id Rev URL"; svn:mime-type=text/plain
*.java       = svn:eol-style=native; svn:keywords="Author Date Id Rev URL"; svn:mime-type=text/plain
*.js         = svn:eol-style=native; svn:keywords="Author Date Id Rev URL"; svn:mime-type=text/javascript
*.jsp        = svn:eol-style=native; svn:keywords="Author Date Id Rev URL"; svn:mime-type=text/plain
*.m          = svn:eol-style=native; svn:keywords="Author Date Id Rev URL"; svn:mime-type=text/plain
*.php        = svn:eol-style=native; svn:keywords="Author Date Id Rev URL"; svn:mime-type=text/x-php
*.pl         = svn:eol-style=native; svn:keywords="Author Date Id Rev URL"; svn:mime-type=text/x-perl; svn:executable
*.pm         = svn:eol-style=native; svn:keywords="Author Date Id Rev URL"; svn:mime-type=text/x-perl
*.py         = svn:eol-style=native; svn:keywords="Author Date Id Rev URL"; svn:mime-type=text/x-python; svn:executable
*.sh         = svn:eol-style=native; svn:keywords="Author Date Id Rev URL"; svn:mime-type=text/x-sh; svn:executable

# Image formats
*.bmp        = svn:mime-type=image/bmp
*.gif        = svn:mime-type=image/gif
*.ico        = svn:mime-type=image/ico
*.jpeg       = svn:mime-type=image/jpeg
*.jpg        = svn:mime-type=image/jpeg
*.png        = svn:mime-type=image/png
*.tif        = svn:mime-type=image/tiff
*.tiff       = svn:mime-type=image/tiff

# Data formats
*.avi        = svn:mime-type=video/avi
*.doc        = svn:mime-type=application/msword
*.eps        = svn:mime-type=application/postscript
*.gz         = svn:mime-type=application/gzip
*.jar        = svn:mime-type=application/java-archive
*.mov        = svn:mime-type=video/quicktime
*.mp3        = svn:mime-type=audio/mpeg
*.pdf        = svn:mime-type=application/pdf
*.ppt        = svn:mime-type=application/vnd.ms-powerpoint
*.ps         = svn:mime-type=application/postscript
*.psd        = svn:mime-type=application/photoshop
*.rtf        = svn:mime-type=text/rtf
*.swf        = svn:mime-type=application/x-shockwave-flash
*.tar        = svn:mime-type=application/x-tar
*.tgz        = svn:mime-type=application/gzip
*.wav        = svn:mime-type=audio/wav
*.xls        = svn:mime-type=application/vnd.ms-excel
*.zip        = svn:mime-type=application/zip

# Text formats
.htaccess    = svn:eol-style=native; svn:keywords="Author Date Id Rev URL"; svn:mime-type=text/plain
*.cfg        = svn:eol-style=native; svn:keywords="Author Date Id Rev URL"; svn:mime-type=text/plain
*.css        = svn:eol-style=native; svn:keywords="Author Date Id Rev URL"; svn:mime-type=text/css
*.csv        = svn:eol-style=native; svn:keywords="Author Date Id Rev URL"; svn:mime-type=text/plain
*.dtd        = svn:eol-style=native; svn:keywords="Author Date Id Rev URL"; svn:mime-type=text/xml
*.htm        = svn:eol-style=native; svn:keywords="Author Date Id Rev URL"; svn:mime-type=text/html
*.html       = svn:eol-style=native; svn:keywords="Author Date Id Rev URL"; svn:mime-type=text/html
*.ini        = svn:eol-style=native; svn:keywords="Author Date Id Rev URL"; svn:mime-type=text/plain
*.properties = svn:eol-style=native; svn:keywords="Author Date Id Rev URL"; svn:mime-type=text/plain
*.sql        = svn:eol-style=native; svn:keywords="Author Date Id Rev URL"; svn:mime-type=text/x-sql
*.txt        = svn:eol-style=native; svn:keywords="Author Date Id Rev URL"; svn:mime-type=text/plain
*.xhtml      = svn:eol-style=native; svn:keywords="Author Date Id Rev URL"; svn:mime-type=text/xhtml+xml
*.xml        = svn:eol-style=native; svn:keywords="Author Date Id Rev URL"; svn:mime-type=text/xml
*.xsd        = svn:eol-style=native; svn:keywords="Author Date Id Rev URL"; svn:mime-type=text/xml
*.xsl        = svn:eol-style=native; svn:keywords="Author Date Id Rev URL"; svn:mime-type=text/xml
*.xslt       = svn:eol-style=native; svn:keywords="Author Date Id Rev URL"; svn:mime-type=text/xml
*.xul        = svn:eol-style=native; svn:keywords="Author Date Id Rev URL"; svn:mime-type=text/xul
*.yml        = svn:eol-style=native; svn:keywords="Author Date Id Rev URL"; svn:mime-type=text/plain
AUTHORS      = svn:eol-style=native; svn:keywords="Author Date Id Rev URL"; svn:mime-type=text/plain
BUGS         = svn:eol-style=native; svn:keywords="Author Date Id Rev URL"; svn:mime-type=text/plain
CHANGES      = svn:eol-style=native; svn:keywords="Author Date Id Rev URL"; svn:mime-type=text/plain
COPYING*     = svn:eol-style=native; svn:keywords="Author Date Id Rev URL"; svn:mime-type=text/plain
DEPENDENCIES = svn:eol-style=native; svn:keywords="Author Date Id Rev URL"; svn:mime-type=text/plain
DEPRECATED   = svn:eol-style=native; svn:keywords="Author Date Id Rev URL"; svn:mime-type=text/plain
INSTALL*     = svn:eol-style=native; svn:keywords="Author Date Id Rev URL"; svn:mime-type=text/plain
LICENSE      = svn:eol-style=native; svn:keywords="Author Date Id Rev URL"; svn:mime-type=text/plain
Makefile*    = svn:eol-style=native; svn:keywords="Author Date Id Rev URL"; svn:mime-type=text/plain
MANIFEST*    = svn:eol-style=native; svn:keywords="Author Date Id Rev URL"; svn:mime-type=text/plain
PLATFORMS    = svn:eol-style=native; svn:keywords="Author Date Id Rev URL"; svn:mime-type=text/plain
README       = svn:eol-style=native; svn:keywords="Author Date Id Rev URL"; svn:mime-type=text/plain
TODO         = svn:eol-style=native; svn:keywords="Author Date Id Rev URL"; svn:mime-type=text/plain
```

Make sure none of the lines start with spaces, or you will get an error message. The list above is not complete, but pretty much covers all the file types I have run into.  For more information on svn properties the best source is the online book, _[Version Control with Subversion](http://svnbook.red-bean.com/en/1.5/index.html)_, in particular chapter 3.