---
layout: post
permalink: blog/correction_eclipse_code_formatter_is
title: "Correction: Eclipse Code Formatter is <i>not</i> lame"
category: Java
---

<p>
I recently <a href="/page/oburn/20041111#eclipse_code_formatter_is_lame">blogged</a>
that the Code Formatter is lame. This got a few comments that I should
be using the <a href="http://jalopy.sourceforge.net/">Jalopy</a>
plug-in. I am not keen to go down this path as development on the open
source project appears to <a href="http://www.triemax.com/products/">have stopped</a>.

</p>
<p>
<a href="/comments/oburn/?anchor=eclipse_code_formatter_is_lame#comment5">Jonathan Aquino</a> questioned what version of Eclipse I was running as the
formatter worked just fine for him. Since I am running <i>3.0.1</i>, I
did not think this would be the problem. But it got me thinking, the
code formatter setup I have was developed on an earlier version
3<i>M</i> build. So I rebuilt the setup from scratch using the <i>Java
Conventions</i> profile that is built-in. Well, I will be darned, it
now works! I looked at the profile settings and cannot see any visible
differences that would change the way the formatter works.

</p>
<p>
So I guess the lessons learnt were:

</p>
<ul>
<li>
It pays to blog about your problem

</li>
<li>
The Eclipse Code Formatter is <b>not</b> lame - if you properly
configure it.

</li>
<li>
Be wary about migrating profiles through upgrades to Eclipse
(which is far enough).

</li>
</ul>
