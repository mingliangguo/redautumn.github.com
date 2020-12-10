---
title: "cannot load python3 in vimr"
layout: single
cover: false
categories: 'blog'
tags: 'blog'
navigation: True
subclass: 'posts'
comments: true
category: blog
date: 2020-07-23 17:11:47 EDT
---

Sometimes when I try to edit in VimR, I got complaints about `No "python3" provider found. Run ":checkhealth providerr"`:

And when I run `:checkhealth` inside VimR, here is the result:

```bash
## Python 2 provider (optional)
  - INFO: pyenv: Path: /Users/gary/.pyenv/libexec/pyenv
  - INFO: pyenv: Root: /Users/gary/.pyenv
  - WARNING: No Python executable found that can `import neovim`. Using the first available executable for diagnostics.
  - ERROR: Python provider error:
    - ADVICE:
      - provider/pythonx: Could not load Python 2:
          /usr/bin/python2 does not have the "neovim" module. :help |provider-python|
          /usr/bin/python2.7 does not have the "neovim" module. :help |provider-python|
          python2.6 not found in search path or not executable.
          /usr/bin/python does not have the "neovim" module. :help |provider-python|
  - INFO: Executable: Not found

## Python 3 provider (optional)
  - INFO: pyenv: Path: /Users/gary/.pyenv/libexec/pyenv
  - INFO: pyenv: Root: /Users/gary/.pyenv
  - WARNING: No Python executable found that can `import neovim`. Using the first available executable for diagnostics.
  - ERROR: Python provider error:
    - ADVICE:
      - provider/pythonx: Could not load Python 3:
          /usr/local/bin/python3 does not have the "neovim" module. :help |provider-python|
          /Users/gary/.pyenv/shims/python3.7 does not exist: pyenv: python3.7: command not found

          The `python3.7' command exists in these Python versions:
          3.7.6


          python3.6 not found in search path or not executable.
          python3.5 not found in search path or not executable.
          python3.4 not found in search path or not executable.
          python3.3 not found in search path or not executable.
          /usr/bin/python is Python 2.7 and cannot provide Python 3.
  - INFO: Executable: Not found
```

I currently use `pyenv` to manage the python environment. And I've tried to install `neovim` by `pip3`, but the problem is still there.

And I noticed that somehow `VimR` is expecting the module in a different path. If I install `neovim` using the following command, it actually fixed the problem:

```bash
/usr/local/bin/pip3 install neovim
```

## Locale related error

When I upgraded to python3.8, I started seeing neovim throws errors as below in `checkhealth`


```bash
Output: Fatal Python error: config_get_locale_encoding: failed to get the locale encoding: nl_langinfo(CODESET) failedPython runtime state: preinitialized
```


What I ended up having to do is to add the following environment variables in my `.zshrc`:

```bash
# You may need to manually set your language environment
export LANG="en_US.UTF-8"
export LC_CTYPE=en_US.UTF-8
```

The above two together seems having solved the issues. Note, it's pretty weird that the issues only occur in the embedded neovim, e.g. [VimR](https://github.com/qvacua/vimr) or [firenvim](https://github.com/glacambre/firenvim)

## Todo

This seems to be related to the way I manage python in my MacOS. There are probably better ways to manage the python environment, which I need to figure out.

- [Homebrew and python](https://docs.brew.sh/Homebrew-and-Python)
