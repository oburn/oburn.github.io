---
layout: post
permalink: blog/getting_closure_with_groovy_curry
title: Getting closure with Groovy curry
category: Java
---

<p class="first">
I have been using <a href="http://groovy.codehaus.org/">Groovy</a> for a while now. Initially for small scripts, but overtime for bigger tasks. The more I use it, the more I am impressed with it's features. Recently I had to generate a number of detailed reports on the performance of the web applications that make up the system I'm working on. During this process I discovered a whole new appreciation for <a href="http://groovy.codehaus.org/Closures">Closures</a> and, in particular, <a href="http://en.wikipedia.org/wiki/Currying">currying</a> them. A good tutorial on this is <a href="http://www.ibm.com/developerworks/java/library/j-pg08235/index.html">here</a>.

</p>
<p>
To show my readers a practical example of what is possible, here is the class I wrote for tracking the statistics associated with a <a href="http://en.wikipedia.org/wiki/Uniform_Resource_Identifier">URI</a>.

</p>
{% highlight groovy %}
package htanalysis

public class UriStat {
    // The properties. Groovy will generate the set/get methods.
    String uri
    BigDecimal totalCpu
    BigDecimal totalResponse
    BigDecimal totalAccessCount
    BigDecimal worstCpu // yes, you can be lazy with ';'s
    BigDecimal worstResponse

    // Declare closures to get a value from an instance. The value
    // may be based on a formulae. To keep things small, using that
    // in Groovy:
    //     - The default argument to a closure is "it"; and
    //     - Do not need a "return" statement on the last line.
    public static final def VALUE_TOTAL_CPU = { it.totalCpu }
    public static final def VALUE_TOTAL_RESPONSE = { it.totalResponse }
    public static final def VALUE_TOTAL_ACCESSCOUNT = { it.totalAccessCount }
    public static final def VALUE_WORST_CPU = { it.worstCpu }
    public static final def VALUE_WORST_RESPONSE = { it.worstResponse }
    public static final def VALUE_AVG_CPU =
        { it.totalCpu / it.totalAccessCount } // See a formulae
    public static final def VALUE_AVG_RESPONSE =
        { it.totalResponse / it.totalAccessCount }

    // This closure compares the values obtained from a two objects
    // using the first closure to obtain the values from the object.
    // This is to do something spicy.....
    private static final def C_GENERIC = { v, o1, o2 -> v(o2) <=> v(o1) };

    // Declare java.util.Comparator instances for comparisons. The
    // first bit of magic is to use curry(). This allows you to
    // define a closure based on another closure, but fixing the first
    // argument to a constant. In this case, the Closure to be used
    // to obtain the value for comparison. If it makes you feel better,
    // it took a me a bit of time to realise the power of Curry.
    //
    // The second piece of magic is to use "as Comparator" on the
    // end of the Closure to coerce the type to be java.util.Comparator.
    public static final Comparator COMP_TOTAL_CPU =
        C_GENERIC.curry(VALUE_TOTAL_CPU) as Comparator;
    public static final Comparator COMP_TOTAL_RESPONSE =
        C_GENERIC.curry(VALUE_TOTAL_RESPONSE) as Comparator;
    public static final Comparator COMP_TOTAL_ACCESSCOUNT =
        C_GENERIC.curry(VALUE_TOTAL_ACCESSCOUNT) as Comparator;
    public static final Comparator COMP_WORST_CPU =
        C_GENERIC.curry(VALUE_WORST_CPU) as Comparator;
    public static final Comparator COMP_WORST_RESPONSE =
        C_GENERIC.curry(VALUE_WORST_RESPONSE) as Comparator;
    public static final Comparator COMP_AVG_CPU =
        C_GENERIC.curry(VALUE_AVG_CPU) as Comparator;
    public static final Comparator COMP_AVG_RESPONSE =
        C_GENERIC.curry(VALUE_AVG_RESPONSE) as Comparator;

    // Cache the property names. Means that when more properties are
    // added to the class, the methods below will take them into account.
    // Very nice <-- please say it like Borat. :-)
    private static final List<String> PROPNAMES =
        UriStat.metaClass.properties.collect({it.name})
            .findAll({it != "class" &amp;&amp; it != "metaClass"}).sort();

    // Return a nice formatted string of the property values.
    public String toString() {
        // Again, you can skip the "return" if you want.
        "[" + PROPNAMES.collect({ "${it}='${this[it]}'" }).join(',') + "]"

    }

    // I like default parameters - ah the good old Ada days. :-)
    public String csvHeader(String sep = ",") {
        PROPNAMES.join(sep)
    }
    // I could have written the above as

    // public String csvHeader(String sep = ",") { PROPNAMES.join(sep) }

    public String csvValues(String sep = ",") {
        return PROPNAMES.collect({this[it]?:""}).join(sep)
    }
}
{% endhighlight %}
