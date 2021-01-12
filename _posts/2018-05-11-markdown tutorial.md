---
layout: post
title: Markdown Tutorial - Font
key: 20180511
tags:
  - front end
  - markdown
---

# Heading

## Heading

### Heading

#### Heading
<!--more-->

##### Heading

###### Heading

**markdown:**
```
# Heading
## Heading
### Heading
#### Heading
##### Heading
###### Heading
```

when using headings, remmeber there must be at least one space between `#` and heading content like `# Heading`.
{:.warning}

`<!--more-->` is a sign to indicate from where above to show in the home page
{:.warning}

The two largest sizes of headings have long underscore and only first two level headers get header lines.
{:.info}

First level header
==================

Second level header
-----------------

**markdown:**
```
First level header
==================

Second level header
-----------------
```
for two consecutive headers, there should be at least one row space, otherwise the second level header will considered as content of the first level header.
{:.warning}

## Emphasis
*should Old Acquaintance be forgot*

_should Old Acquaintance be forgot_

**should Old Acquaintance be forgot**

__should Old Acquaintance be forgot__

**_should Old Acquaintance be forgot_**

**markdown:**
```
*should Old Acquaintance be forgot*
_should Old Acquaintance be forgot_
**should Old Acquaintance be forgot**
__should Old Acquaintance be forgot__
**_should Old Acquaintance be forgot_**
```
both symbol `*` and symbol `_` change the character to italic form, both symbol `**` and symbol `__`change the character to bold form.
{:.info}
always create a new row space for returning a new line.
{:.warning}

## Alert

Succes Text.
{:.success}

Info Text.
{:.info}

Warning Text.
{:.warning}

Error Text.
{:.error}

**markdown:**
```
Succes Text.
{:.success}
```
```
Info Text.
{:.info}
```
```
Warning Text.
{:.warning}
```
```
Error Text.
{:.error}
```

