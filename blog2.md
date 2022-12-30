---
layout: page
title: Blog2
permalink: /blog2/
---

This is my personal blog, which you can see is almost completely dormant. Who knows, I may get active again in the future, but it's unlikely. Just incase, you can subscribe [via RSS]({{ "/feed.xml" | prepend: site.baseurl }}).

Posts:

{% for post in site.posts %}

- {{ post.date | date: "%Y %b %-d" }} - [{{ post.title }}]({{ post.url }})

{% endfor %}

