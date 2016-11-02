---
layout: post
permalink: blog/checkstyle_a_victim_of_it
title: Checkstyle, a victim of its early success
category: Java
---

<p>
When I started work on the open-source version of <a href="http://checkstyle.sf.net/">Checkstyle</a> in 2000, I planned to make it a tool to find as many problems as possible before code reviews (and you do code reviews, don't you? ;). And sometimes it may even be used as a substitue for code reviews - on the theory that something is better than nothing.

</p>
<p>
I tend to follow the rule of going after <a href="http://www.wordspy.com/words/low-hangingfruit.asp">low-hanging fruit</a>, so the initial emphasis went into checking the easy stuff like the use of <a href="">braces</a> and the proper use of <a href="http://checkstyle.sourceforge.net/config_whitespace.html">whitespace</a>. IMHO, probably the best early stuff was the support for checking <a href="http://checkstyle.sourceforge.net/config_javadoc.html">Javadoc comments</a> and <a href="http://checkstyle.sourceforge.net/config_naming.html">naming conventions</a>.

</p>
<p>
Unfortunately to this day most people think this is all that Checkstyle does. The other day a friend of mine referred to the Checkstyle 2.4 release as being the "<i>"Gold Release"</i>, which is all people ever use. But this is far from the truth, as Checkstyle has evolved a long way since then.

</p>
<p>
One of the major problems with the early version of Checkstyle was the architecture. It was not easy for other people to develop their own checks, and plug them into Checkstyle. This meant that new checks had to be developed mainly by myself and Lars. So in the long-term it was not good approach.

</p>
<p>
When <a href="http://pmd.sf.net/">PMD</a> appeared on the scene, it was clear that a cleaner architecture could be achieved. I remember discussing with Lars whether we should effectively stop work on Checkstyle and port our checks into PMD. In the end we decided not to because one of the advantages of Checkstyle over PMD is that is much faster. So it became a challenge to come up with an architecture for Checkstyle that would support plug-ins as easily as PMD, but not suffer the performance costs. In the end we jointly came up with an <a href="http://checkstyle.sourceforge.net/api/com/puppycrawl/tools/checkstyle/api/Check.html">optimised visitor pattern</a> which formed the core of Checkstyle 3.

</p>
<p>
The benefits of this change can be clearly seen now. The number of <a href="https://sourceforge.net/project/memberlist.php?group_id=29721">committers</a> for the project has grown from 2 to 4. The number of checks available has grown significantly to include checks for <a href="http://checkstyle.sourceforge.net/config_coding.html">common coding problems</a>, <a href="http://checkstyle.sourceforge.net/config_design.html">class design techniques</a> and <a href="http://checkstyle.sourceforge.net/config_misc.html">other miscellaneous checks</a>. The other day we received a contribution containing over 20 checks that are going to be incorporated into the main distribution. There is even be the <a href="https://sourceforge.net/mailarchive/forum.php?thread_id=2531814&forum_id=12011">suggestion</a> to use the core of Checkstyle to support other languages. This is entirely possible given the fact that a lot of the Checkstyle architecture is language independent.

</p>
<p>
But after reading <a href="http://www.cardboard.nu/archives/000072.html">this blog</a> from Alan I was left thinking, but if only he knew how easy it was to write a Check for this kind of stuff. The irony is that I have <a href="http://www.cardboard.nu/archives/000072.html">had drinks</a> with Alan, and I should add, it was a good night.

</p>
<p>
I am not sure what is the best way to go about communicating how Checkstyle has changed since the old 2.4 release. If you have a good idea, please let me know.

</p>
