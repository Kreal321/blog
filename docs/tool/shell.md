---
title: Shell
tags:
  - bash
  - zsh
---

# Shell

Shell is a program that takes commands from the keyboard and gives them to the operating system to perform. In the old days, it was the only user interface available on a Unix-like system such as Linux. Nowadays, we have graphical user interfaces (GUIs) in addition to command line interfaces (CLIs) such as the shell.

## Zsh vs Bash

Zsh is built on top of bash thus it has additional features. Zsh is the default shell for macOS and Kali Linux. Zsh provides the user with more flexibility by providing various features such as plug-in support, better customization, theme support, spelling correction, etc.

## Bash_profile vs Bashrc

Bashrc is executed each time you open a new terminal window, while bash_profile is executed only once when you log in to your account. This means that any changes you make to bashrc will take effect immediately, while changes to bash_profile will take effect only when you log out and log back in again.

## Order of Operations

* .zshenv (environment variables)
* .zprofile (login shell)
* .zshrc (interactive shell)
* .zlogin (login shell)
* .zlogout (when the shell exits)