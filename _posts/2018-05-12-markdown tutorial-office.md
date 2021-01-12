---
layout: post
title: Markdown Tutorial - Office
key: 20180512
tags:
  - front end
  - markdown
---

## Links

[Henrik's Site](http://localhost:4000/2018/05/12/markdown-tutorial-office.html)

**markdown:**
```
[Henrik's Site](path-to-site)
```
<!--more-->

### With Title

[Henrik's Site](http://localhost:4000/2018/05/12/markdown-tutorial-office.html "Henrik's Site")

**markdown:**
```
[Henrik's Site](path-to-site "Henrik's Site")
```

### Reference Links

My Blog is called [Henrik's blog] [BLOG].

**markdown:**
```
My Blog is called [Henrik's blog][BLOG].
[BLOG]: path-to-site "Henrik's blog"
```
Remember [BLOG] tag must be defined at the bottom of markdown document.
{:.warning}

### Link Within A Paragraph

Some Information about this blog and me can be found [here](http://localhost:4000/2018/05/12/markdown-tutorial-office.html).

**markdown:**
```
Some Information about this blog and me can be found [here](path-to-site)
```
[BLOG]: http://localhost:4000/2018/05/12/markdown-tutorial-office.html

## Images

![Northeastern](/../Pic/N.png "Northeastern"){:width="128px" :height="128px"}

**markdown:**
```
![Northeastern](path-to-image.png "Northeastern"){:width="128px" :height="128px"}
```

## Footnote

Here is a footnote reference,[^1] and another.[^longnote]

[^1]: Here is the footnote.

[^longnote]: Here's one with multiple blocks.

Here is second paragrah with footnote reference,[^3] and another.[^shortnote]

[^3]: Here is the footnote.

[^shortnote]: Here's one with multiple blocks.


**markdown:**
```
Here is a footnote reference,[^1] and another.[^longnote]

[^1]: Here is the footnote.

[^longnote]: Here's one with multiple blocks.

Here is second paragrah with footnote reference,[^3] and another.[^shortnote]

[^3]: Here is the footnote.

[^shortnote]: Here's one with multiple blocks.
```
