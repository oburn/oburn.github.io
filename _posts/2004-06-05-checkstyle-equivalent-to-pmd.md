---
layout: post
permalink: blog/checkstyle_equivalent_to_pmd
title: Checkstyle equivalent to PMD
category: Java
---

<p>
As one of the developers of Checkstyle, I am always interesting in articles about Checkstyle and similar tools like <a href="http://pmd.sf.net">PMD</a>. So I read the recent article <a href="http://www.ociweb.com/jnb/jnbJun2004.html">Improving Project Quality with PMD</a> with some interest. The comment about Checkstyle not being geared towards <i>"identifying latent defects&quot;</i> was disheartening as this has been a major thrust for well over a year.

</p>
<p>
So for a bit of fun I thought I would rewrite the example given in the article showing how to find classes that are not declared in a package. The resulting Check for Checkstyle is:

</p>
{% highlight java %}
package sample;

import com.puppycrawl.tools.checkstyle.api.Check;
import com.puppycrawl.tools.checkstyle.api.DetailAST;
import com.puppycrawl.tools.checkstyle.api.TokenTypes;

public class AllClassesMustHaveAPackage extends Check {
    private boolean mNoPackage;

    public int[] getDefaultTokens() {
        return new int[]{TokenTypes.PACKAGE_DEF};
    }

    public void beginTree(DetailAST root) {
        mNoPackage = true;
    }

    public void visitToken(DetailAST ignored) {
        mNoPackage = false;
    }

    public void finishTree(DetailAST root) {
        if (mNoPackage) {
            log(root, &quot;All types must have a package.&quot;);
        }
    }
}
{% endhighlight %}

<p>
This check will only report of files that do not have a declared package. I suspect the example shown by Tom Wheeler in the article will fire for every class declared in a file. It also will not fire for interfaces. I would be interested to hear from people more skilled in PMD than me if I am wrong.

</p>
