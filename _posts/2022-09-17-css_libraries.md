---
title: Useful CSS Libraries
date: 2022-09-17 12:00:00 -500
categories: [CSS,webdev,libraries,frameworks]
tags: [CSS,webdev,libraries,frameworks]
---

## Bootstrap

Bootstrap is a free and open-source CSS framework directed at responsive, mobile-first front-end web development. It contains CSS- and JavaScript-based design templates for typography, forms, buttons, navigation, and other interface components.

### pros

* easy to use
* responsive
* lots of components
* lots of documentation

### cons

* not very customizable
* not very lightweight
* html gets bloated with classes
* all bootstrap sites look essentialy the same

### start template

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-iYQeCzEYFbKjA/T2uDLTpkwGzCiq6soy8tYaI1GyVh/UjpbCx/TYkiZhlZB6+fzT" crossorigin="anonymous">
    <script defer src="https://cdn.jsdelivr.net/npm/bootstrap@5.2.1/dist/js/bootstrap.bundle.min.js" integrity="sha384-u1OknCvxWvY5kfmNBILK2hRnQC3Pr17a+RTT6rIHI7NnikvbZlHgTPOOmMi466C8" crossorigin="anonymous"></script>

    <title>Hello, world!</title>
  </head>
  <body>
    <h1>Hello, world!</h1>
  </body>
</html>
```

[website](https://getbootstrap.com/docs/5.2/getting-started/introduction/)

## Water CSS

Water.css is a tiny, responsive, modern CSS framework. It makes your websites look beautiful at any size, be it a 17" laptop screen or an iPhone 5.

### pros

* very lightweight
* responsive
* easy to use
* customizable with css variables

### cons

* only CSS (no JS)
* "only" responsiveness
* no components

### start template

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/water.css@2/out/dark.css">
    <title>Hello, world!</title>
  </head>
  <body>
    <h1>Hello, world!</h1>
  </body>
</html>
```

[website](https://watercss.kognise.dev/)

## myLibrary

myLibrary is my own CSS / JS framework. It is very lightweight and responsive. It is still in development.
My goal is to manage as much as possible with CSS variables and tag selectors to keep the html as clean as possible.

### pros

* very lightweight
* responsive
* easy to use
* customizable with css variables

### cons

* still in development

### start template

```html
<!doctype html>
<html>

<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <meta name="color-scheme" content="dark light">
    <link rel="stylesheet" href="https://saracenrhue.github.io/myLibrary/src/style.css"/>
    <script defer src="https://saracenrhue.github.io/myLibrary/src/script.js"></script>
    <link rel="stylesheet" href="src/style.css">
    <script defer src="src/script.js"></script>
    
    <title>Hello World!</title>
</head>
<body>
    <h1>Hello World!</h1>

</body>
</html>
```

[website](https://github.com/SaracenRhue/myLibrary)
