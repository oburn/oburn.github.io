---
layout: post
permalink: blog/slickrun_autohotkey_magic
title: SlickRun + AutoHotkey magic
category: Computing
---

<p class="first">
For people who do not use Windows, stop reading now!

</p>
<p>
OK, you have been warned. I am a long time fan of <a href="http://www.bayden.com/slickrun/">SlickRun</a> as I am the type of person that does not like taking his hands off the keyboard. I use it to launch programs quickly by typing a hot-key to bring up a floating window, and then entering a keyword (or first part of). For example, the following screen-shot shows that when I type in <code>fi</code>, it gets completed to <code>firefox</code> automatically.

</p>
<p style="text-align: center;">
<img src="/images/blog-sr-01.png" alt="" />

</p>
<p>
Recently, it occurred to me that I would like to have the <code>firefox</code> keyword perform the following steps:

</p>
<ol>
<li>
If Mozilla Firefox is already running, just bring it to the front; ELSE

</li>
<li>
Launch the program.

</li>
</ol>
<p>
With this behaviour I am then able to use the same action to bring up Firefox regardless of whether it is running. Previously I would have to see if Firefox is already running and then switching to it, or alternatively launching it.

</p>
<p>
I decided to write a small <a href="http://www.autohotkey.com/">AutoHotkey</a> script to support this.

</p>
{% highlight autohotkey %}
    ;; Script for running a process. It will first see if the required window
    ;; is running and if so, bring to the foreground. Otherwise will run the
    ;; specified command.
    ;;
    ;; Arguments:
    ;;   arg 1 - regexp for Window title
    ;;   arg 2 - path to process to execute

    ;; Check for arguments
    if 0 < 2
    {
        MsgBox Need to pass in Window Title and Executable to run
        ExitApp
    }

    SetTitleMatchMode, RegEx
    IfWinExist, %1%
    {
        WinActivate
    }
    else
    {
        Run, %2%
    }
{% endhighlight %}

<p>
I then used the AutoHotkey compiler to create a standalone executable. I could then use the following command-line to either activate the running instance of Firefox or launch it if it is not already running.

</p>
{% highlight winbatch %}
    prompt% O:\myhome\bin\activate-or-run.exe ^
                ".* - Mozilla Firefox$" ^
                O:\FirefoxPortable\FirefoxPortable.exe
{% endhighlight %}

<p>
The arguments are:

</p>
<ol>
<li>
<code>".\* - Mozilla Firefox$"</code> - regular expression to match on the title of the Mozilla Firefox Window.

</li>
<li>
<code>O:\\FirefoxPortable\\FirefoxPortable.exe</code> - the command to launch firefox no matching window title was found.

</li>
</ol>
<p>
Here is how this is configured as a SlickRun keyword:

</p>
<p style="text-align: center;">
<img src="/images/blog-sr-02.png" alt="" />

</p>
<p>
I wish I had thought of this technique back when I started using SlickRun. Note that this was just an example using Mozilla Firefox. I use the same technique to access a number of common programs like <a href="http://www.gnu.org/software/emacs/">this</a> and <a href="http://zabkat.com/">this</a>.

</p>
<p>
Finally, I know about the <a href="http://lifehacker.com/5390086/the-master-list-of-new-windows-7-shortcuts">Windows 7 Taskbar Shortcuts</a> where <code>Win+number (1-9)</code> starts the application pinned to the taskbar in that position, or switches to that program. This is what inspired the idea, I just find using keywords easier, and I use <a href="http://portableapps.com/">PortableApps</a> which do not pin nicely to the taskbar.

</p>
