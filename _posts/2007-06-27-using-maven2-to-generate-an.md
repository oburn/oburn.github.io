---
layout: post
permalink: blog/using_maven2_to_generate_an
title: Using Maven2 to generate an executable JAR
category: Java
---

<p>
This entry is part rant and part sharing the knowledge. For the record
I think that <a href="http://maven.apache.org/maven-1.x">Maven 1.x</a>
sucks, and if it was not for the excellent <a href="http://www.mergere.com/m2book_download.jsp">Better Builds with Maven</a> book I would not be using Maven 2.

</p>
<p>
There is a lot to like about Maven 2, in particular I use the <a href="http://maven.apache.org/plugins/maven-eclipse-plugin/">maven-eclipse-plugin</a>
to generate Eclipse projects, and the integration with the <a href="http://jetty.mortbay.org/maven-plugin/howto.html">Jetty</a>
plug-in for doing rapid webapp development totally rocks. The <a href="http://maven.apache.org/plugins/maven-site-plugin/">maven-site-plugin</a>
is great for making you feel like you are creating documentation. :-)

</p>
<p>
But things get (unnecessarily?) hard when you try and doing things
that Maven does not support out of the box. Yesterday I was trying to
generate an standalone executable JAR file for my project, the type
that is simple to generate using the <a href="http://fjep.sourceforge.net/">Fat Jar Eclipse Plug-In</a>. This
type of JAR file includes all the required dependencies. This makes
distribution a breeze.

</p>
<p>
First up I tried to use <a href="http://maven.apache.org/plugins/maven-jar-plugin/">maven-jar-plugin</a>
and followed the instructions in <a href="http://maven.apache.org/plugins/maven-jar-plugin/examples/executable-jar.html">Creating an executable jar file</a>. This was not successful as it does not
include the required dependencies, but instead creates a manifest
entry to refer to them.

</p>
<p>
Next attempt involved trying to use the <a href="http://maven.apache.org/plugins/maven-assembly-plugin/">maven-assembly-plugin</a>
with the predefined assembly <a href="http://maven.apache.org/plugins/maven-assembly-plugin/descriptor-refs.html#jar-with-dependencies">jar-with-dependencies</a>. This
attempt failed as the plug-in does not keep the `Main-Class:`
entry in the manifest, but it did however include the dependencies as
advertised.

</p>
<p>
My third attempt was to use the <a href="http://mojo.codehaus.org/minijar-maven-plugin">minijar-maven-plugin</a>
and hopefully get the added benefit of a smaller JAR
file. Unfortunately it just generated a corrupt JAR file.

</p>
<p>
Next up was the <a href="http://pyx4me.com/pyx4me-maven-plugins/proguard-maven-plugin/">proguard-maven-plugin</a>. Basically
I was unable to get it to run successfully, despite my repeated attempts.

</p>
<p>
Finally up was <a href="http://www.dstovall.org/onejar-maven-plugin/">onejar-maven-plugin</a>. Initially
the generated JAR file did not work as when run it would hang. I
realised that I was missing the manifest entry in my
<i>pom.xml</i>. Once this was added, it worked like a charm.

</p>
<p>
Hopefully this blog will save people some time. Here is what I finally
had in my <i>pom.xml</i>:

</p>
{% highlight xml %}
...
<pluginRepositories>
  <pluginRepository>
    <id>dstovall.org</id>
    <url>http://dstovall.org/maven2/</url>
  </pluginRepository>
</pluginRepositories>

<build>
  <plugins>
    <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-jar-plugin</artifactId>
      <configuration>
        <archive>
          <manifest>
            <mainClass>com.puppycrawl.tools.cruft.Main</mainClass>
            <addClasspath>false</addClasspath>
          </manifest>
        </archive>
      </configuration>
    </plugin>

    <plugin>
      <groupId>org.dstovall</groupId>
      <artifactId>onejar-maven-plugin</artifactId>
      <executions>
        <execution>
          <phase>package</phase>
          <goals>
            <goal>one-jar</goal>
          </goals>
        </execution>
      </executions>
    </plugin>
 ...
{% endhighlight %}
