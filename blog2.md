---
layout: page
title: Blog2
permalink: /blog2/
---

This is my personal blog, which you can see is almost completely dormant. Who knows, I may get active again in the future, but it's unlikely.

Posts:

{% for post in site.posts %}

- {{ post.date | date: "%b %-d, %Y" }} - {{ post.title }}

{% endfor %}

Subscribe [via RSS]({{ "/feed.xml" | prepend: site.baseurl }}).
