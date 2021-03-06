---
layout: post
permalink: blog/log4j_hangs_my_application
title: Log4J hangs my application
category: Java
---

<p>
I have been a staunch user and supporter of <a href="http://logging.apache.org/log4j/docs/">Log4J</a> for a long
time. In fact a long time ago I wrote a contribution called
<a href="http://logging.apache.org/log4j/docs/api/org/apache/log4j/chainsaw/package-summary.html">Chainsaw</a>. Till today I held the view that Log4J was bulletproof and
above suspicion. However, I have discovered that I was naive.

</p>
<p>
My current assignment is a large J2EE project, made up of a number of
web-applications deployed to WebSphere 6. Occasionally we have been
experiencing the main web-application locking up. So I decided to
investigate, rather than just blaming WebSphere and applying the
latest fix-pack.

</p>
<p>
Today when the application locked up, I collected a number of JVM
thread dumps. WebSphere makes it very easy to collect using the
wsadmin tool (documented <a href="http://publib.boulder.ibm.com/infocenter/wasinfo/v6r0/topic/com.ibm.websphere.nd.doc/info/ae/ae/txml_dump.html">here</a>). Having
never looked at JVM thread dumps before I found the <a href="http://websphere.sys-con.com/">WebSphere Journal</a> article <a href="http://websphere.sys-con.com/read/113368.htm">WebSphere Application Server Java Dumps</a> very useful.

</p>
<p>
I hoped to use the <a href="http://www.ibm.com/developerworks/websphere/downloads/thread_analyzer.html">WebSphere
ThreadAnalyzer</a> tool to analyse the thread dumps. Unfortunately I
was to quick and overlooked that it does <a href="http://www-128.ibm.com/developerworks/websphere/downloads/techpreviews.html">not support</a> WebSphere 6. Going back to square one, well Google, I
found the JavaOne presentation <a href="http://developers.sun.com/learning/javaoneonline/2004/newcooltech/TS-1646.pdf">View from the Trenches: Thread Dumps thread</a>, which gave me pointers to
a couple of useful tools.

</p>
<p>
I had good success using <a href="http://yusuke.homeip.net/samurai/?english">Samurai</a> which is easy to run thanks to a <a href="http://yusuke.homeip.net/samurai/samurai.jnlp">webstart link</a>. <a href="http://dev2dev.bea.com/pub/a/2004/01/thread_dumps.html">ThreadDumpAnalyzer</a> is useful as it can do a time series across multiple dumps, but it is
awkward to setup.

</p>
<p>
The image below is a screen shot of the Samurai application in the
overview mode. You can see that a number of threads are blocked as
they have a red box. Only the <i>WebContainer : 4</i> thread is
potentially working, signified by the white box.

</p>
<p>
<img src="/images/samurai-overview.png" alt="Samurai"/>

</p>
<p>
As the <i>WebContainer : 4</i> thread stayed in this state
permanently, I used Samurai to investigate where it was stuck. I was
able to get the following stack trace.

</p>
{% highlight text %}
Thread dump :&quot;WebContainer : 4&quot;  Shrink idle threads:on. - disable

Thread dump 1/1
&quot;WebContainer : 4&quot; (TID:0x104496D8, sys_thread_t:0x51658DB0, state:R, native ID:0x12C4) prio=5
  at java.net.SocketOutputStream.socketWrite0(Native Method)
  at java.net.SocketOutputStream.socketWrite(SocketOutputStream.java(Compiled Code))
  at java.net.SocketOutputStream.write(SocketOutputStream.java(Compiled Code))
  at java.io.ObjectOutputStream$BlockDataOutputStream.drain(ObjectOutputStream.java(Compiled Code))
  at java.io.ObjectOutputStream$BlockDataOutputStream.setBlockDataMode(ObjectOutputStream.java(Compiled Code))
  at java.io.ObjectOutputStream.defaultWriteObject(ObjectOutputStream.java(Compiled Code))
  at org.apache.log4j.spi.LoggingEvent.writeObject(LoggingEvent.java:398)
  at sun.reflect.GeneratedMethodAccessor2726.invoke(Unknown Source)
  at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java(Compiled Code))
  at java.lang.reflect.Method.invoke(Method.java(Compiled Code))
  at java.io.ObjectStreamClass.invokeWriteObject(ObjectStreamClass.java(Compiled Code))
  at java.io.ObjectOutputStream.writeSerialData(ObjectOutputStream.java(Compiled Code))
  at java.io.ObjectOutputStream.writeOrdinaryObject(ObjectOutputStream.java(Compiled Code))
  at java.io.ObjectOutputStream.writeObject0(ObjectOutputStream.java(Compiled Code))
  at java.io.ObjectOutputStream.writeObject(ObjectOutputStream.java(Compiled Code))
  at org.apache.log4j.net.SocketAppender.append(SocketAppender.java:224)
  at org.apache.log4j.AppenderSkeleton.doAppend(AppenderSkeleton.java(Compiled Code))
  at org.apache.log4j.helpers.AppenderAttachableImpl.appendLoopOnAppenders(AppenderAttachableImpl.java(Compiled Code))
  at org.apache.log4j.Category.callAppenders(Category.java(Compiled Code))
  at org.apache.log4j.Category.forcedLog(Category.java:379)
  at org.apache.log4j.Category.debug(Category.java:248)
  ...
{% endhighlight %}

<p>
The stack trace reveals that the thread was blocked in the Log4J code,
which was configured to log to file and a <a href="http://logging.apache.org/log4j/docs/api/org/apache/log4j/net/SocketAppender.html">SocketAppender</a>.
Now knowing that Log4J was the problem, I did some searching to find
<a href="http://wiki.jboss.org/wiki/Wiki.jsp?page=Logging">this</a>
and <a href="http://comments.gmane.org/gmane.comp.jakarta.log4j.devel/10016">this</a>. What
is very worrying is to search for the word <i>deadlock</i> in a <a href="http://www.mail-archive.com/log4j-dev@logging.apache.org/msg05460.html">recent bug-list</a>.

</p>
<p>
I concluded that Log4J is deadlocking, and most likely because of the
SocketAppender. As most of the time Chainsaw is not being run on the
server, Log4J generates loads of warning messages. It will do this if
you do not call <a href="http://logging.apache.org/log4j/docs/api/org/apache/log4j/helpers/LogLog.html#setQuietMode(boolean)">setQuietMode(true)</a>.

</p>
<p>
In the end I changed the applications to call the setQuietMode(true)
method on startup, and removed the SocketAppender from the production
configuration. I have learnt a lot today. :-)

</p>
