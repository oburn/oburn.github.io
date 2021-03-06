---
layout: post
permalink: blog/ratcheting_findbugs_errors_with_ant
title: Ratcheting FindBugs errors with ANT
category: Java
---

<p>
On a previous project the excellent tool <a href="http://findbugs.sf.net">FindBugs</a> was added to the tool chain well after development has underway (500,000 lines of Java code already written). I used an approach termed <a href="http://skizz.biz/blog/2008/03/11/fixing-broken-windows-with-ratcheting/">ratcheting</a> to ensure that no more errors were introduced to the code base, and that over time the number of errors were reduced.

</p>
<p>
The approach involves the follow strategy:

</p>
<ul>
<li>
Run FindBugs and record the number of errors found. This is done once to determine the <i>low water mark</i>.

</li>
<li>
Each time the build is run, calculate the number of errors found, and then use the following logic:

<ul>
<li>
If the number of errors is lower than the existing <i>low water mark</i>, then record the new <i>low water mark</i>.

</li>
<li>
If the number of errors is higher than the existing <i>low water mark</i>, then fail the build as more errors have been introduced.

</li>
<li>
Otherwise, be silent.

</li>
</ul>
</li>
</ul>
<p>
I implemented this approach using ANT + Groovy, but it could be equally applied with Maven.

</p>
<p>
Since all our builds were done using Hudson CI server, it was run automatically as part of the normal build. We did not use the Hudson plug-ins to implement this strategy, because at the time (2009), the available plug-ins did not have a way to automatically update the <i>low water mark</i> when it reduced.

</p>
<p>
Here is the ANT task I used implement the logic above:

</p>
{% highlight xml %}
  <target name="run-findbugs" depends="-init">
    <!-- RUN FINDBUGS (exercise left for reader) -->

    <!-- Logic to check if the count has got worst -->
    <groovy>
      <arg value="${target}/logs/data/findbugs/bier-bugs.xml"/>
      <arg value="${project.root}/.findbugs-lowwatermark"/>
// Get then number of errors found
def errors = (new XmlSlurper().parse(args[0])).BugInstance.size()

// Get the current number, defaulting to a HUGE number
def lwmf = new File(args[1])
int lowWaterMark = Integer.MAX_VALUE
if (lwmf.canRead()) {
    lwmf.eachLine { lowWaterMark = it.toInteger().intValue() }
}

if (errors &lt; lowWaterMark) {
    // We have a new record!
    new File(args[1]).withWriter { out -> out.writeLine("${errors}") }
}
else if (errors &gt; lowWaterMark) {
    // Oh dear, we are going backwards.
    properties["findbugs.watermark"] = "Findbugs error count has increased from ${lowWaterMark} to ${errors}."
}
    </groovy>
  </target>
{% endhighlight %}

<p>
The reason for setting the property <code>findbugs.watermark</code> was that other quality checks can be run (like Checkstyle) and reports generated, before failing the build. At the end of the build, the following task is run:

</p>
{% highlight xml %}
<target name="-check-failure">
  <!-- check for unit test failure -->
  <property file="${target}/test-failure.properties"/>
  <if>
    <isset property="bier.test.failed"/>
    <then>
      <my-play-sound
          fname="${project.root}/build/config/sounds/unittests-failed.wav"
          />
      <fail message="Unit tests failed. Refer to junit reports for details."/>
    </then>
  </if>

  <property file="${target}/checkstyle-failure.properties"/>
  <if>
    <isset property="bier.checkstyle.failed"/>
    <then>
      <my-play-sound
          fname="${project.root}/build/config/sounds/checkstyle-failed.wav"
          />
      <fail message="Problems with Checkstyle."/>
    </then>
  </if>

  <if>
    <isset property="findbugs.watermark"/>
    <then>
      <echo message="${findbugs.watermark}"/>
      <echo file="${project.root}/.findbugs-failure"
            message="${findbugs.watermark}"
            />
    </then>
    <else>
      <delete file="${project.root}/.findbugs-failure"/>
    </else>
  </if>

  <echo>The build has finished successfully.</echo>
</target>
{% endhighlight %}
