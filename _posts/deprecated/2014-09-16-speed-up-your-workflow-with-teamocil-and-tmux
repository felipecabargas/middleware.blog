---
author: juanpintoduran
title: 'Teamocil: speeding up your Tmux workflow '
layout: post
category:
  - Design
tags:
  - vectors
  - sketch
  - design
  - mac
---

This week I started using [tmux](http://tmux.sourceforge.net/) & [vim](http://www.vim.org/) on top of ZSH as my default editor. I was looking for the right time to drop the mouse use, and I fell in love with vim+tmux after seeing a lot of screencasts and speechs about the great power of using a command-line based editor.

So, when that was installed on my Macbook, I wondered "now what?"... because, for changing <kbd>⌘</kbd>+<kbd>S</kbd> for <kbd>ESC</kbd>+<kbd>:</kbd>+<kbd>w</kbd>+<kbd>q</kbd> is not a good reason.

So at the moment that I finally discovered the benefits of **vim** but then I realized that **tmux** was there only because I readed they were good friends.

And then, appeared [**teamocil**](https://github.com/remiprev/teamocil), an awesome RubyGem (take that Python) that creates tmux sessions by only running 1 simple line.

In order to create a session file (it uses YAML syntax), you have 2 options:

	vim ~/.teamocil/session-name.yaml
	teamocil --edit session-name
	
Then, you can use a layout like the next one inside of that file (see [Teamocil Docs](http://www.teamocil.com/) for more info, this is just an example):

	name: reciclario
 	windows:
      - name: git
        root: ~/Hacking/Rails/reciclario
        panes:
           - ggpull

      - name: rails server
        root: ~/Hacking/Rails/reciclario
        panes:
           - commands:
                - bundle install
                - rake db:migrate
                - bin/rails server

      - name: rails console
        root: ~/Hacking/Rails/reciclario
        panes:
            - bin/rails console

      - name: vim
        root: ~/Hacking/Rails/reciclario
        focus: true
        panes:
            - vim

When that's ok, you can run your session with the command:

	teamocil session-name
	
As you can see, that creates a new *tmux* session with the given name and executes all the stuff defined previously.


I hope you guys learned something on this little article, and I'm also pleased to tell you that I'm publishing all my dotfiles on GitHub, for you to download. Also, I published my custom terminal themes & color palettes so feel free to use them.

 [1]: https://photos-1.dropbox.com/t/0/AADeiLgvAsH-kZzm0ifNkVVVD8EOxWW9nLAN-5ue-W4O_A/12/38222680/png/1024x768/3/1410840000/0/2/Screenshot%202014-09-15%2023.58.15.png/COH-F1YvddHKx5AACYMNFjNXrktFAtf-Lp9kTnS4iCg
 [2]: https://photos-5.dropbox.com/t/0/AAAB0glwxGWtIDUR3g79Pu5Gixu0J9pFjPXGU1B9aDq-Sw/12/38222680/png/1024x768/3/1410843600/0/2/Screenshot%202014-09-16%2000.16.33.png/yeSVmvIM19FUaTyrwbBxhio6F3mQnK-ioy09Y5F8XGs
