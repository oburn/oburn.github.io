---
layout: post
permalink: blog/teach_an_old_dog_new
title: Teach an old dog new tricks (or now using Classycle)
category: Java
---

<p>
Thanks to <a href="http://blog.adjective.org/">Tim Vernum</a> for responding to my last post about <a href="../detecting_cycles_with_ant_jdepend/">Detecting Cycles with ANT/JDepend</a>, I now know about the tool <a href="http://classycle.sourceforge.net/">Classycle</a> which is much better suited for the task. Here is the ANT target I added to my <code>build.xml</code> file replacing the old approach:

</p>
{% highlight xml %}
  <target name="classycle" depends="-init">
    <taskdef name="classycleDependencyCheck"
             classname="classycle.ant.DependencyCheckingTask"
             classpath="${project.root}/build-stuff/tools/classycle-1.3.3/classycle.jar"
             />
    <classycleDependencyCheck failOnUnwantedDependencies="true">

      <fileset dir="${mother.target}/dist">
        <include name="shared-${build.revision}.jar"/>
        <include name="datareceipt-DO-NOT-USE-${build.revision}.jar"/>
        <include name="webapp-DO-NOT-USE-${build.revision}.jar"/>
      </fileset>

      show allPaths onlyFailures
      {root} = au.gov.defence.mldef
      [all] = ${root}.*
      check absenceOfPackageCycles > 1 in [all]
    </classycleDependencyCheck>

  </target>
{% endhighlight %}

<p>
As you can see this is a lot smaller and simpler than the previous approach.

</p>
<p>
Some notes:

</p>
<ul>
<li>
Another nice advantage of this approach is that you do not need to <code>classcyle.jar</code> to your <code>${ANT\_HOME}/lib</code> directory. With the JDepend approach you need to add the JDepend JAR file to the <code>${ANT\_HOME}/lib</code> directory.

</li>
<li>
I still use the Checkstyle <a href="http://checkstyle.sourceforge.net/config_imports.html#ImportControl">ImportControl check</a> for enforcing the project layering/dependency rules. The immediate feedback this gives in the Eclipse IDE via the <a href="http://eclipse-cs.sourceforge.net/">eclipse-cs</a> is invaluable. That said, Classycle looks <a href="http://classycle.sourceforge.net/ddf.html">very capable</a>.

</li>
</ul>
