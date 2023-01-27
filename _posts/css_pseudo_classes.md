---
title: CSS Pseudo Classes
date: 2023-09-18 +0000
categories: [CSS,webdev]
tags: [CSS,webdev]
---

## :is()

### Before

```css
.example h3,
.example h4,
.example a {
  color: red;
  }

```

### Now

```css
.example :is(h3, h4, a) {
  color: red;
  }
```

## :has()

### Before

```css
.example img {
  color: red;
  }

```

### Now

```css
.example :has(img) {
  color: red;
  }
```
