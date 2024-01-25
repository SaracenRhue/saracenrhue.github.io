---
title: MediaWiki Markup
date: 2024-01-25 +0000
categories: [readme]
tags: [documentation]
---

## Introduction to MediaWiki Markup

MediaWiki is a free and open-source wiki software, best known for powering Wikipedia. It uses its own markup language to allow for easy editing of pages.

## Basic MediaWiki Syntax

### Headings and Subheadings
Headings and subheadings are created using equal signs (`=`). The number of equal signs used denotes the level of the heading.

```mediawiki
= Heading 1 =
== Heading 2 ==
=== Heading 3 ===
==== Heading 4 ====
===== Heading 5 =====
====== Heading 6 ======
```

### Text Formatting

#### Bold and Italic
Text can be emphasized in different ways:

```mediawiki
''italic''
'''bold'''
'''''bold and italic'''''
```

### Lists

#### Unordered Lists
Unordered lists are created using asterisks (`*`).

```mediawiki
* Item 1
* Item 2
** Subitem 2a
** Subitem 2b
```

#### Ordered Lists
Ordered lists are created using number signs (`#`).

```mediawiki
# First item
# Second item
## Subitem 2a
## Subitem 2b
```

### Links

#### Internal Links
Internal links to other pages within the same wiki:

```mediawiki
[[Page title]]
[[Page title|Display text]]
```

#### External Links
External links to websites:

```mediawiki
[https://www.example.com]
[https://www.example.com Display text]
```

### Images and Media
To add images and other media files:

```mediawiki
[[File:Example.jpg]]
[[File:Example.jpg|thumb|Caption text]]
```

### Formatting Code

#### Inline Code
For inline code, use `<code></code>` tags.

```mediawiki
<code>inline code</code>
```

#### Code Blocks
For code blocks, use `<pre></pre>` tags.

```mediawiki
<pre>
Line 1 of code
Line 2 of code
</pre>
```

### Blockquotes
Blockquotes are created using a colon (`:`) at the start of a line.

```mediawiki
: This is a blockquote.
:: Nested blockquote.
```

### Tables
Tables are created with curly braces and pipes.

```mediawiki
{| class="wikitable"
|-
! Header 1 !! Header 2 !! Header 3
|-
| Row 1, Cell 1 || Row 1, Cell 2 || Row 1, Cell 3
|-
| Row 2, Cell 1 || Row 2, Cell 2 || Row 2, Cell 3
|}
```

### Horizontal Rules
Horizontal rules are created using four dashes (`----`).

```mediawiki
----
```

## Advanced MediaWiki Features

### Templates
Templates are reusable wiki elements:

```mediawiki
{{TemplateName}}
{{TemplateName|Parameter1|Parameter2}}
```

### Categories
Add a page to a category:

```mediawiki
[[Category:Category name]]
```

### Redirects
To redirect a page to another:

```mediawiki
#REDIRECT [[Page title]]
```

### Magic Words
Magic words are a series of keywords used to perform specific functions:

```mediawiki
__TOC__
__NOTOC__
__NOEDITSECTION__
```

### Transclusion
Including the content of one page into another:

```mediawiki
{{:Page title}}
```

### Variables
MediaWiki provides various variables for dynamic content:

```mediawiki
{{CURRENTDAY}} {{CURRENTMONTHNAME}} {{CURRENTYEAR}}
```
