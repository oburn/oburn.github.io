---
layout: post
permalink: blog/simulate_override_in_jdk_1
title: Simulate @Override in JDK 1.4
category: Java
---

<p>
One of the nice features in Java 5 is the annotation <a href="http://java.sun.com/j2se/1.5.0/docs/api/java/lang/Override.html">@Override</a>. It prevents a base class changing underfoot without you realising. For example, consider the base class:

</p>
{% highlight java %}
public class Base
{
    protected void record(String name)
    {
        //...
    }
}
{% endhighlight %}

<p>
Now I can extend the <code>Base</code> class and override the <code>record</code> method as follows:

</p>
{% highlight java %}
public class SafeOverride extends Base
{
   @Override
   protected void record(String name)
   {
       //...
   }
}
{% endhighlight %}

<p>
If the signature of the <code>record</code> method changes in the <code>Base</code> class, then a compilation error will occur when compiling <code>SafeOvverride</code>. This is very useful for preventing subtle bugs.

</p>
<p>
Now naturally JDK 1.4 does not support <code>`Override</code>, but you can simulate the behaviour using the Javadoc tool and the Javadoc tag <code>{`inheritDoc}</code>. In JDK 1.4 write the <code>SafeOverride</code> class as follows:

</p>
{% highlight java %}
public class SafeOverride extends Base
{
    /** {@inheritDoc} */
    protected void record(String name)
    {
        //...
    }
}
{% endhighlight %}

<p>
Now if the signature of the <code>record</code> method changes in the <code>Base</code> class, then Javadoc will report a warning like:

</p>
<p>
<code> C:\\tmp\\SafeOverride.java:6: warning - @inheritDoc used but record(String) does not override or implement any method.</code>

</p>
