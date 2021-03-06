---
layout: post
permalink: blog/eclipse_code_formatter_is_lame
title: Eclipse Code Formatter is lame
category: Java
---

<p>
I tend to use <a href="">Eclipse</a> as my primary IDE. This is
largely due to the fact that I know it the best, not that I think it
is better/worse than <a href="http://www.intellij.com/idea/">IDEA</a>. On the whole I quite
like it, but the one area where I think Eclipse is really lame is the
much vaunted Code Formatter. I have been battling with it for a long
time and it shows not signs of improving.

</p>
<p>
By way of an example, I would like really like to be able to write
code like the following:

</p>
{% highlight java %}
final MyInputTokeniser mit = new MyInputTokeniser(
    new GZIPInputStream(new FileInputStream(f)));
{% endhighlight %}

<p>
But when I reformat the code, Eclipse changes it to:

</p>
{% highlight java %}
final MyInputTokeniser mit = new MyInputTokeniser(
                                                  new GZIPInputStream(
                                                                      new FileInputStream(
                                                                                          f)));
{% endhighlight %}

<p>
This as far as I am concerned is <b>really lame</b>! To make matters
worst, there does not appear to be a way to mark regions of text to
not be touched by the Code Formatter. This is real pain in the butt,
as it means you can never safely run the Code Formatter on a file.

</p>
<p>
The only workaround I have for examples like above is to rewrite my
code in a way that the Code Formatter will do a reasonable job on. It
irks me that Eclipse is dictating my coding style, Eclipse should be
there to help, not dictate!

</p>
<p>
For the example above, I have had to write:

</p>
{% highlight java %}
final FileInputStream fis = new FileInputStream(f);
final GZIPInputStream gis = new GZIPInputStream(fis);
final MyInputTokeniser mit = new MyInputTokeniser(gis);
{% endhighlight %}
