---
layout: post
permalink: blog/how_i_write_blog_entries
title: How I write Blog entries
category: Java
---

<h1 id="cbt3">
How I write Blog entries

</h1>
For a long I have been writing Blog entries using Emacs and the <a title="nxml-mode" href="http://www.thaiopensource.com/nxml-mode/" id="han3">nxml-mode</a> to ensure XHTML compliance. More recently I have started using the <a title="Emacs Muse" href="http://mwolson.org/projects/EmacsMuse.html" id="s0.u">Emacs Muse</a> publishing system, which I also use for personal notes and to manage a personal Wiki. Today I thought I would try out the facility to publish a document from Google Docs, which I found out about from <a title="here" href="http://bavatuesdays.com/publishing-google-docs-to-your-blog/" id="kz-b">here</a>.<br id="qr8y"><br id="xq_8">Alas it did not work. The problem was that I was using the URL <span id="mz6g" style="font-family: Courier New;">http://www.jroller.com/xmlrpc</span> which is suggested by the Google <a title="documentation" href="View?docid=afwwtkhg6gn_aj8z6fsv5kx" id="abw9">documentation</a>. This guy has the <a title="same problem" href="http://groups.google.com/group/Something-in-Writely-is-Broken/browse_thread/thread/c9f1de36d39e589d/4d845d2031f40a69?lnk=gst&q=#4d845d2031f40a69" id="xn0.">same problem</a>. Reading the JRoller manual revealed that I should be using the URL <span id="e3dk" style="font-family: Courier New;">http://jroller.com/roller-services/xmlrpc</span> instead. As this post demonstrates, it works!
<br/><br/>
