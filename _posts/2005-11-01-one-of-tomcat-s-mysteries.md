---
layout: post
permalink: blog/one_of_tomcat_s_mysteries
title: One of Tomcat's mysteries solved
category: Java
---

<p>
For a very long time I have been unable to have hot-deploy work under
Tomcat, as Tomcat would lock some random JARs. This meant to redeploy
I had to shutdown Tomcat, delete the JARs, start Tomcat and deploy the
application. It was slowly driving me insane.

</p>
<p>
Luckily I found the answer here - <a href="http://blog.exis.com/colin/archives/2005/08/23/i-put-a-spell-on-you-because-youre-mine-aka-why-is-tomcat-holding-onto-jars/">I Put A Spell On You, Because you're mine: Aka Why is TomCat Holding Onto Jars?</a>. Glad I was not alone in having this problem.

</p>
