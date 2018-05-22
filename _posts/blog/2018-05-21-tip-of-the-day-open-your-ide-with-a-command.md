---
author: juanpintoduran
title: '[Daily Tip] How to open your IDE with `code` in macOS '
excerpt:
layout: post
category:
  - Tips
tags:
  - development
post_format: [ ]
---

Visual Studio Code lets you "install" the `code` command to open files in VSCode from the terminal... But how about doing it ourselves? `alias` as always to the rescue. You just need to add the following to your `.bashrc` or `.zshrc` file

For VS Code:

```bash 
alias code="open -a Visual\ Studio\ Code"
```

For others:

```bash 
alias code="open -a <APPLICATION_NAME>"
```