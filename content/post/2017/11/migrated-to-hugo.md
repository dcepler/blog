---
author: "David Epler"
title: "Migrated to Hugo"
slug: "migrated-to-hugo"
date: "2017-11-11T09:47:53-05:00"
categories:
  - "Hugo"
draft: false
---

I really haven't paid much attention to my blog in a few years. Part of that was probably due to the fact it was running on ColdFusion (Railo 3.3 really) using [Mango Blog](https://www.mangoblog.org/). Both are extremely out of date and started looking for an alternative. First thought was to convert to [WordPress](https://wordpress.org/), but given the hassles to set it up and run it securely with seemingly constant [vulnerabilties reported](https://wpvulndb.com/) pretty much ruled it out.

I wanted to simplify the stack and reduce attack surface, so static generators seemed like a good place to start. I looked at [Jekyll](https://jekyllrb.com/) first and then several others but ultimately decided on [Hugo](https://gohugo.io/).

<!--more-->

The main reason I chose Hugo was that its [quick start](https://gohugo.io/getting-started/quick-start/) was straight forward and really do like the simplicity of install on macOS

```shell
brew install hugo
```


## Migration

So like all things, migration is really the biggest hurdle. It was a multi-step process to get the data out of Mango and in to Hugo, using WordPress as an intermediate step since just about everything can convert to/from it. All the work to convert was done in an Ubuntu VM that had both ColdFusion and WordPress installed with a MySQL database dump of the existing Mango Blog database.

Marcos Placona wrote a [script](https://github.com/mplacona/Mango2Wordpress) to [migrate from Mango to WordPress](https://www.placona.co.uk/317/coldfusion/migrating-mango-blog-to-wordpress/). I had to do some [modifications to the code](https://github.com/mplacona/Mango2Wordpress/pull/4) since there was a variable scoping issue and it did not retain full date time stamps for posts and comments. With those were dealt with, it worked great and got the data into a shell WordPress site.

Once in WordPress, I tried using [WordPress to Hugo Exporter](https://github.com/SchumacherFM/wordpress-to-hugo-exporter) but could not get it to work. I was able to use [Jekyll Exporter](https://wordpress.org/plugins/jekyll-exporter/) instead since all I really wanted was the post content exported to Markdown files. Hugo has several options to [convert Jekyll to Hugo](https://gohugo.io/tools/migrations/#jekyll) but I did not use them and manually modified the exported Markdown into Hugo. Some of the posts had a lot of extraneous HTML markup that I wanted removed.

For comments, I needed to export a WordPress WXR file so I could [import it to Disqus](https://help.disqus.com/customer/portal/articles/466255). I did need to modify the URLs for the posts in the WXR file to match what the new ones would be before importing.

## Setup

With Hugo's [excellent documentation](https://gohugo.io/documentation/) it wasn't hard to setup. Biggest thing for me was to get a theme in place that had the features I wanted, mostly that it was based on [Bootstrap 3](https://getbootstrap.com/docs/3.3/). There are [plenty of themes](https://themes.gohugo.io/) to choose from. [Hugo Phlat Theme](https://themes.gohugo.io/hugo-phlat-theme/) met my needs once I did a few tweaks to it.

The other change was using [nginx](https://nginx.org/) instead of [Apache httpd](https://httpd.apache.org/). Used [Mozilla SSL Configuration Generator](https://mozilla.github.io/server-side-tls/ssl-config-generator/?server=nginx-1.10.1&openssl=1.0.1e&hsts=yes&profile=modern) to generate nginx configuration to work with.

The other item needed were URL re-writes since the URLs no longer contained `.cfm`. Several posts of mine that are linked to various Stack Overflow answers, without the URL re-writes the links would fail.

```nginx
# rewrites to map specific .cfm to new pages
rewrite    ^/feeds/rss.cfm$                              /index.xml permanent;
rewrite    ^/post.cfm/(.*)$                              /post/$1/ permanent;
rewrite    ^/archives.cfm/category/(.*)$                 /categories/$1/ permanent;
rewrite    ^/archives.cfm/page/(\d)$                     /page/$1/ permanent;
rewrite    ^/page.cfm/(about-me|projects|presentations)$ /$1/ permanent;
rewrite    ^/assets/content/presentations/(.*)$          /presentations/$1 permanent;
```

I'm sure there are going to be a few more things done to nginx configuration once I dig into it a bit more.

There are a few different ways to [host and deploy content](https://gohugo.io/hosting-and-deployment/) with Hugo. For now going with [rsync](https://gohugo.io/hosting-and-deployment/deployment-with-rsync/) until need a different flow.

Overall, I am quite happy with the change to Hugo and hopefully it will lead to me writing more frequent posts.
