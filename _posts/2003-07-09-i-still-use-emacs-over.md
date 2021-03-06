---
layout: post
permalink: blog/i_still_use_emacs_over
title: I still use Emacs over jEdit
category: Java
---

<p>
I have been trying recently to use <a href="http://www.jedit.org/">jEdit</a> as a replacement for <a href="http://www.gnu.org/software/emacs/windows/ntemacs.html">Emacs</a>, but I found that I prefer Emacs. It is worth knowing at least one editor really well for all your general text processing needs. For me that is Emacs - though I also know Vim very well.

</p>
<p>
I know that talking about editors is a religious thing that can start a flame war. So before I say why I use Emacs over jEdit, let me state some things:

</p>
<ul>
<li>
I used to use be an absolute Vi zealot back when I used a vt100 terminal on a shared computer (a novel thought these days). I still use Vim frequently

</li>
<li>
I started using Emacs in anger in 1994

</li>
<li>
I had numerous failed attempts to learn Emacs before I finally succeeded

</li>
<li>
I use Eclipse for all my Java development (though I would use IDEA if it was free)

</li>
<li>
I cannot extend Emacs by writing Lisp (one day I plan to learn Lisp). This is not a huge drawback as Emacs has record-able macros (like every great editor must)

</li>
<li>
I continue to actively use jEdit for editing XML documents - the XML editing mode is superb

</li>
</ul>
<p>
Emacs is a real pain to setup. If I was starting out today from scratch, there is no doubt in my mind that I would be using jEdit and not Emacs. But since I started using it 9 years ago, I have managed to add and refine my .emacs file to include many of the excellent extensions to Emacs. So it is the extensions that keep me using Emacs. Here are the extensions that I use that make Emacs IMHO more enjoyable to use than jEdit:

</p>
<ul>
<li>
<a href="http://www.cua.dk/cua.html">cua-mode</a> - these enables CUA key bindings, which is the classic Control-C to copy, Control-V to paste stuff. It also provides support for editing rectangular blocks of text.

</li>
<li>
<a href="http://www.cua.dk/ido.html">ido-mode</a> - provides a very efficient mechanism to switch buffers and navigate to files. I notice that jEdit has a plug-in to emulate the switching of buffers.

</li>
<li>
<a href="http://www.wonderworks.com/download/filladapt.el">adaptfill-mode</a> - provide **very** intelligent text wrapping support. For example, when editing a Javadoc comment, it will wrap long lines and understand that it is a Javadoc comment and prefix lines with '\*'.

</li>
<li>
<a href="http://www.sunsite.ualberta.ca/Documentation/Gnu/emacs-20.7/html_chapter/emacs_14.html">flyspell-mode</a> - performs spell checking of words as you type them (similar to what Microsoft Word does). I really miss this feature in jEdit

</li>
<li>
<a href="http://www-es.fernuni-hagen.de/cgi-bin/info2html?(emacs)File%20Archives">archive-mode</a> - allows you to view and edit the contents of an archive file (like a ZIP file). I remember impressing somebody one day when I edited a JSP buried inside of a WAR file that was inside of an EAR file, and then saving the changes.

</li>
</ul>
<p>
There a number of people who over the years I have attracted to using Emacs. To get started they took a copy of my .emacs file and tailored it. I can highly recommend the <a href="http://www.dotemacs.de/">http://www.dotemacs.de/</a> website for good samples to get started. A good .emacs file is essential to really get the best out of Emacs.

</p>
