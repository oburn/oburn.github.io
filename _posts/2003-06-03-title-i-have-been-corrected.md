---
layout: post
permalink: blog/title_i_have_been_corrected
title: I used the "old school way"
category: Java
---

<p>
I recently posted a <a href="/page/oburn/20030531#howto_freeroller_comments">HOWTO</a> on adding comments to your blog in FreeRoller now it has been upgraded. Unfortunately I showed how to do it using the <a href="http://www.rollerweblogger.org/comments/roller/Weblog/oliver_explains_the_old_school">old school way</a>. Luckily an entry has been added to RollerWiki showing the <a href="http://www.rollerweblogger.org/wiki/Wiki.jsp?page=EnablingComments">right way</a>.

</p>
<p>
Originally I gave the complete source to the <i>"\_day"</i> template. For completeness, here is my current <i>"Weblog"</i> template:

</p>
{% highlight html %}
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">
<html>
<head>
 <title>#showWebsiteTitle()</title>
 <style type="text/css">#includePage("_css")</style>
</head>

<body background="/roller/images/bg-greylines.gif">

<table cellpadding="5" cellspacing="5" border="1" align="center" width="98%">
  <tbody>
  <tr>
    <td width="20%" valign="top" bgcolor="#ffffff">
      #showBasicNavBar(true)<br>
      RSS Feed: #showRSSBadge()<br>
      <br>
      #showWeblogCalendar()<br>
      #showBookmarks("Fav Blogs" true false)<br> 
      #showReferers(15 10)<br>
      #showEditorNavBar(true)<br>
    </td>

    <td width="80%" valign="top" bgcolor="#ffffff">
      <h2>#showWebsiteTitle()</h2>
      #showWeblogCategoryChooser()<br>
      #showWeblogEntries("_day" 20)
    </td>
  </tr>
  </tbody>
</table>

</body>
</html>
{% endhighlight %}
