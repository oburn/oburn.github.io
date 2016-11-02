---
layout: post
permalink: blog/out_of_touch
title: Out of touch
category: Java
---

<p class="first">
This week I went to the keynote by James Gosling at the Sun Tech Days here in Sydney. At the end of his presentation, I was left in know doubt that he has really <a href="http://en.wikipedia.org/wiki/Kool-Aid#.22Drinking_the_Kool-Aid.22">drunk the Kool-Aid</a>. Especially when he asked people to stop using Emacs and use Netbeans instead.

</p>
<p>
Now, as my <a href="../lego_animated_death_star_canteen/#comment-1741330742">four</a> readers <a href="../i_still_use_emacs_over/">will remember</a>, I am a long time user of Emacs. I would agree that using Emacs for developing Java code is madness, but as a general purpose editor, nothing beats Emacs. For example, in the last week I have been going through log files looking into some production support issues. I even ended up writing the report on the issues using <a href="http://mwolson.org/projects/EmacsMuse.html">Emacs Muse</a> (and this blog entry).

<p style="text-align: center;">
<a href="http://shop.oreilly.com/product/9781565922617.do?sortby=publicationDate"><img src="http://akamaicovers.oreilly.com/images/9781565922617/cat.gif"/></a>

</p>
<p>
It was also a real irony for me listening to Gosling, as this week I have been reading <a href="http://www.oreilly.com/catalog/gnuext/">Writing GNU Emacs Extensions</a> by <a href="http://www.oreillynet.com/pub/au/700">Bob Glickstein</a>. I cannot recommend this book highly enough to get a good overview on how to extend Emacs, or just to understand what is in that <code>.emacs</code> file. Bizarrely I have had the book in my bookshelf for over eight years before actually reading it.

</p>
<p>
After reading the book, I wrote my first Lisp function, including:

</p>
{% highlight lisp %}
(oli-filter-buffer-non-matching (regie)
  "Copies the contents of the current buffer and filters it for non matching lines"
  (interactive "sRegexp of lines to keep: ")
  (let ((buffer (get-buffer-create (concat "filtered-"
                                           (format-time-string "%y%m%d%H%M%S"
                                                               (current-time)))))
        (curr-buff (current-buffer)))
    (progn
      (set-buffer buffer)
      (insert-buffer curr-buff)
      (delete-non-matching-lines regie)
      (switch-to-buffer-other-window buffer))))
{% endhighlight %}
