---
layout: post
title:  "Emacs 2024 Changes"
categories: blog
---

Wow, it has been nearly two years since I have blogged - time to see if I can still do it. Let's blog about how my Emacs configuration has changed over the last year (2024).

I have now been using Emacs for over thirty years. It used to be the main IDE I wrote code with, but I have long since moved to a dedicated IDE, these days being IntelliJ and VSCode. But, I still using Emacs heavily into two contexts:

1. Work - I use [org-mode](https://orgmode.org/) **heavily** for my personal project management and note keeping.
2. Home - I use [ledger-mode](https://github.com/ledger/ledger-mode) for managing my personal finances.

Across both contexts, I lean heavily on:

1. [Dired](https://www.gnu.org/s/emacs/manual/html_node/emacs/Dired.html) as a cross-platform file manager. I used to use [Midnight Commander](https://midnight-commander.org/) but I found it buggy in the end (on MacOS). Since investing time in learning `dired` it's _good enough_.
2. [Magit](https://magit.vc/) for using Git - I would be lost without this.

As a [friend of mine](https://www.linkedin.com/in/robbieg8s/) said when I asked why he kept working on his `zsh` configuration, _"it's my version of golf!"_. Similarly I am often looking to improve my Emacs configuration. I keep up to date by tracking the blogs of [Sacha Chua](https://sachachua.com/blog/) and [Irreal](https://irreal.org/blog/), and seeing what takes my fancy.

In the last year I did 25 commits to my `.emacs` file (yes, it's under Git source control). Here are the major changes I made over the last year:

- For my templating needs, I moved to [tempel](https://github.com/minad/tempel) (from [yasnippet](https://github.com/joaotavora/yasnippet)). I have found it to be way more powerful and grok-able.
- For completions, I finally embraced using [corfu](https://github.com/minad/corfu), which is nice (especially the integration with `tempel`). I almost gave up until I realised that I needed to also install [cape](https://github.com/minad/cape).
- I gave up on trying to use a terminal emulator in Emacs, and instead now use [terminal-here](https://github.com/davidshepherd7/terminal-here) to open a _proper_ terminal in the current working directory. This approach works much better for me.
- I improved my `dired` setup by installing [dired-single](https://codeberg.org/amano.kenji/dired-single), [dired-collapse](https://github.com/Fuco1/dired-hacks#dired-collapse) and [dired-subtree](https://github.com/Fuco1/dired-hacks#dired-subtree). I also learned about [wdired-mode](https://www.gnu.org/software/emacs/manual/html_node/emacs/Wdired.html) which makes the `dired` buffer editable (a game changer). 🤯
- I use [asdf](https://asdf-vm.com/) and [direnv](https://direnv.net/) to manage my toolchain at the project level, so to improve the integration with Emacs I installed [envrc](https://github.com/purcell/envrc).
