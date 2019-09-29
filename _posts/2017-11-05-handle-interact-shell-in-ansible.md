---
title: "handle interact shell in ansible"
layout: single
categories: 'blog devops ansible'
tags: 'devops ansible'
navigation: True
subclass: 'post tag-speeches'
comments: true
date: 2017-11-05 13:23:55 EST
---


I have been using [ Ansible ](http://docs.ansible.com/) to automate some of environment setup work during my daily development/test. One thing I recently run across is to handle the interact shell in ansible.

I have been using [Byobu](http://byobu.co/) as the terminal manager for my remote server. Since the server will be recreated every time I have to update a new build (usually every week or two). So it's a good use case to use Ansible to automate this, so I don't have to run the configuration manually.

When I tried to configure [fzf](https://github.com/junegunn/fzf.git) in the server, it prompts me to type `yes` during the `install` script.  And this script will hang there if I just use the [ Shell ](http://docs.ansible.com/ansible/latest/shell_module.html#shell) command in Ansible.

By some research, I found there are two ways to deal with this interactive shell:

## Using `yes`

Basically you can use `/usr/bin/yes` command to automatically respond `y` when running a script. Here is an example:

```bash
yes | script
```

Here is the explanation from the man page:

>
> NAME
>        yes - output a string repeatedly until killed
>
> SYNOPSIS
>        yes [STRING]...
>        yes OPTION
>
> DESCRIPTION
>        Repeatedly output a line with all specified STRING(s), or 'y'.

Here is a good answer is [askubuntu.com](https://askubuntu.com/questions/338857/automatically-enter-input-in-command-line)

And here is how I use `yes` to install `fzf`:

```yaml
- name: "install fzf"
  shell: "git clone --depth 1 https://github.com/junegunn/fzf.git ~/.fzf && yes | ~/.fzf/install"
  args:
      creates: ~/.fzf
```

## Using `expect` in Ansible

Ansible actually has a module called [expect](http://docs.ansible.com/ansible/latest/expect_module.html) to handle the interactive scenario. This module works very similar to the `expect` command in U(L)nix. So it can handle more complex scenario than `yes`, e.g. for scenario where you need to provide something specific as a response, not just `yes` or `no`.

Here is the example from the ansible website.

```yaml
- name: Case insensitve password string match
  expect:
    command: passwd username
    responses:
      (?i)password: "MySekretPa$$word"

- name: Generic question with multiple different responses
  expect:
    command: /path/to/custom/command
    responses:
      Question:
        - response1
        - response2
        - response3
```

## Summary

As you can see, both `yes` and the `expect` module can handle the scenario I have. But `expect` is definitely more powerful to handle more complex scenario.

Here are some other helpful readings:

- [“Yes/No” in Bash Script – Prompt for Confirmation](https://www.shellhacks.com/yes-no-bash-script-prompt-confirmation/)
