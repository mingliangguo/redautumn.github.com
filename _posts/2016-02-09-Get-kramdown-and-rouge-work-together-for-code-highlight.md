---
title: "Get Kramdown and Rouge work together for code highligher"
layout: post
cover: false
categories: 'blog jekyll'
tags: 'blog github jekyll'
navigation: True
fullview: true
comments: true
subclass: 'post tag-speeches'
logo: 'assets/images/ghost.png'
cover: 'assets/images/cover4.jpg'
date: 2016-02-09 22:02:06 EST
---

I have upgraded to the most recent jekyll version and was prompted by Github that the code highlighter(redcarpet) I have been using is out of support soon in May 1, 2016.

> You are currently using the 'redcarpet' Markdown engine, which will not be supported on GitHub Pages after May 1st. At that time, your site will use 'kramdown' for markdown rendering instead. To suppress this warning, remove the 'markdown' setting in your site's '_config.yml' file and confirm your site renders as expected. For more information, see https://help.github.com/articles/updating-your-markdown-processor-to-kramdown.

Based on this message, I switched to [kramdown](http://kramdown.gettalong.org/) and use [rouge](https://github.com/jneen/rouge) as code highlighter. However no matter which [syntax](https://help.github.com/articles/creating-and-highlighting-code-blocks/) I used, it will not render the code properly for me. I have tried various ways to fix it, but no luck!! It is really frustrating and wasted me a lot of time. 

Fortunately, I finally figured out how to get it working. And credit belongs to [Syntax Highlighting in Jekyll With Rouge](https://sacha.me/articles/jekyll-rouge/). To make the highlighter work, you actually need to configure it as this:

```
markdown: kramdown

kramdown:
  input: GFM
  syntax_highlighter: rouge
```

rather than:

```
markdown: kramdown
syntax_highlighter: rouge
```

Enjoy it now!!




