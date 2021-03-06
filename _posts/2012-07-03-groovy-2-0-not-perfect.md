---
layout: post
permalink: blog/groovy_2_0_not_perfect
title: Groovy 2.0 not perfect (but still awesome)
category: Java
tags:
  - groovy
---

<p>
I have been a <a href="http://groovy.codehaus.org">Groovy</a> user for a long time. I have dabbled a bit with Scala, being lured by the promise of static type checking. Being a huge fan of static type checking I tried to love Scala (even just like it), but I always ended up back in Groovy because it is more productive for me.

</p>
<p>
So, with the <a href="http://www.infoq.com/articles/new-groovy-20">recent announcement</a> of the Groovy 2.0 release, I hoped that the new <a href="http://groovy.codehaus.org/gapi/groovy/transform/TypeChecked.html">TypeChecked</a> annotation would be the <i>silver bullet</i> I had been waiting for. Alas, I have found that, although the <a href="http://groovy.codehaus.org/gapi/groovy/transform/TypeChecked.html">TypeChecked</a> annotation does indeed turn on static type checking, it does not translate to the real world if you are using <a href="http://groovy.codehaus.org/gapi/groovy/lang/Closure.html">closures</a> (which you would if programming in Groovy).

</p>
<p>
Below is a snippet of code, which you would expect on quick inspection to not compile. This is because the code is attempting to iterate of a list of <code>String</code> objects and treat them as <code>Integer</code> objects.

</p>
{% highlight groovy %}
@TypeChecked
static void example(List<String> args) {
   args.each { Integer it -> println it }
}
{% endhighlight %}

<p>
In fact this code will compile, but will fail when executed with a run-time error (since you cannot cast a <code>String</code> to an <code>Integer</code>).

</p>
<p>
The reason is that the <a href="http://groovy.codehaus.org/groovy-jdk/java/lang/Object.html#each(groovy.lang.Closure)">each()</a> method signature takes a <a href="http://groovy.codehaus.org/gapi/groovy/lang/Closure.html">Closure</a> which is untyped. As such, the Groovy compiler is unable to detect that the Closure is expecting objects of the type that are contained in the list being iterated over.

</p>
<p>
Overall, I am still very bullish over the adoption of Groovy 2.0 in the enterprise.

</p>
