---
layout: post
permalink: blog/use_javascript_to_block_ads
title: Use JavaScript to block ads
category: Java
---

<p>
I quite fond of the quote <i>"Great minds think alike"</i>, especially when people quote it as justification for doing something. So I have my own twist, which is <i>"Great minds think alike, fools never differ"</i>.

</p>
<p>
Well anyway a few months ago I finally discovered that you can <a href="http://wp.netscape.com/eng/mozilla/2.0/relnotes/demo/proxy-live.html">use JavaScript</a> to control which proxy your browser will use. Now I may be slow, the document does date back to 1996, but thought this could be useful as I am constantly battling with proxies and networks. I now have a JavaScript file that selects the correct proxy to use based on:

</p>
<ul>
<li>
The network I am in. I use this to determine which network I am in (home, work, dial-up, etc).

</li>
<li>
The URL being requested. For example, bypassing the proxy for single host names (for example <i>http://intranet</i>). My favourite it to return a fake proxy for known ad sites.

</li>
</ul>
<p>
I thought this was a pretty novel approach as none of my friends who like to think they are bleeding edge knew about this technique. Sorry <a href="http://jroller.com/page/bcarney">Bruce</a> and <a href="http://madbean.com/blog">Matt</a>. :-)

</p>
<p>
Anyway I just found an <a href="http://www.windowsdevcenter.com/lpt/a/4730">excellent article</a> about this exact technique. It takes what I was doing to the next logical level, especially the Black-hole Proxy stuff. So, do I have a great mind, or am I a fool, I will let you decide....... :-)

</p>
