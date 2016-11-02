---
layout: post
permalink: blog/variable_naming_convention
title: Variable naming convention
category: Java
---

<p>
I just read Tor Norbye's latest blog entry <a href="http://blogs.sun.com/roller/page/tor?entry=code_advice_11_initialize_fields">Code Advice \#11: Initialize fields using the property name</a>, and I have
to say I disagree with him. I used the coding style where the name of the variable is prefixed with a character to indicate the scope. The following table outlines the rules.

</p>
<table border="1">
<thead>
<tr>
<th>
Variable

</th>
<th>
Rule

</th>
<th>
Example

</th>
</tr>
</thead>
<tbody>
<tr>
<td>
member

</td>
<td>
Prefix with <code>'m'</code>

</td>
<td>
mTemperature

</td>
</tr>
<tr>
<td>
parameter

</td>
<td>
N/a

</td>
<td>
temperature

</td>
</tr>
<tr>
<td>
local

</td>
<td>
N/a

</td>
<td>
temperature

</td>
</tr>
<tr>
<td>
static

</td>
<td>
Prefix with <code>'s'</code>

</td>
<td>
sTemperature

</td>
</tr>
<tr>
<td>
static final

</td>
<td>
All uppercase

</td>
<td>
MAX\_TEMP

</td>
</tr>
</tbody>
</table>
<p>
So to use Tor's example, the setter method would be written as:

</p>
{% highlight java %}
void setTemperature(int temperature) {
    mTemperature = temperature;
}
{% endhighlight %}

<p>
Advantages of this style are:

</p>
<ul>
<li>
Misalignments stand out, as in:
{% highlight java %}
void setTemperature(int temperature) {
    mTemperature = mTemperature;
}
{% endhighlight %}

</li>
<li>
You can still use <i>nice</i> English names for parameters and
local variables.

</li>
<li>
It is easier when reading code fragments (for example diffs) to determine the scope of a variable. For example, it is easy to read the following code fragment:
{% highlight java %}
if (mTemperature < predictedTemperature) {
    mTemperature = predictedTemperature;
    fireNewMaximum(mTemperature);
}
{% endhighlight %}

</li>
<li>
It is readily supported by IDE's that generate setters and getters.

</li>
</ul>
<p>
I enforce this style with the following checks in my <a href="http://checkstyle.sf.net">Checkstyle</a> configurations:

</p>
{% highlight xml %}
<module name="ConstantName"/>
<module name="ParameterName"/>
<module name="LocalFinalVariableName"/>
<module name="LocalVariableName"/>
<module name="MemberName">
  <property name="format" value="^m[a-zA-Z0-9]*$"/>
</module>
<module name="StaticVariableName">
  <property name="format" value="^s[a-zA-Z0-9]*$"/>
</module>
{% endhighlight %}
