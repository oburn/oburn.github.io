---
layout: post
permalink: blog/howto_freeroller_comments
title: "HOWTO: FreeRoller comments"
category: Java
---

<p>
I maybe slow, but I finally got comments working in FreeRoller. To get there, I had to change the following line in my Weblog page:

</p>
{% highlight velocity %}
    $macros.showWeblogEntries()
{% endhighlight %}

<p>
to:

</p>
{% highlight velocity %}
    $macros.showWeblogEntries("_day")
{% endhighlight %}

<p>
This will make the rendering of the weblog entries use my "\_day" template. I then used the following for the "\_day" template:

</p>
{% highlight velocity %}
<div class="entry">
   $macros.showDayPermalink()
   $macros.showEntryDate()
</div>

#foreach( $entry in $entries )
<p>
   <b>$entry.title</b> $entry.text 
   <span class="dateStamp">($entry.pubTime)</span>
    $macros.showEntryPermalink( $entry )
    $macros.showCommentsLink($entry)
</p>
#end
{% endhighlight %}

<p>
I hope that some people out there find this information useful. If you do, please feel free to leave a comment. ;-)

</p>
