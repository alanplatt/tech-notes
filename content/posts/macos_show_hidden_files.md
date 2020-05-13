---
title: "Macos_show_hidden_files"
date: 2020-05-13T14:31:31+01:00
draft: true
toc: false
images:
tags:
  - mac
  - macos
  - catalina
  - mojave
  - high sierra
  - sierra
---

# Show hidden files in Finder on MacOS
Add the following to your shell rc file eg `~/.zshrc` or `~/.bashrc`
```
alias showFiles='defaults write com.apple.finder AppleShowAllFiles YES; killall Finder /System/Library/CoreServices/Finder.app'
alias hideFiles='defaults write com.apple.finder AppleShowAllFiles NO; killall Finder /System/Library/CoreServices/Finder.app'
```

Now from a terminal you can run `showFiles` or `hideFiles` to show and hide files respectively.

This has worked for me on the following:
* MacOS 10.15: Catalina
* MacOS 10.14: Mojave
* MacOS 10.13: High Sierra
* MacOS 10.12: Sierra