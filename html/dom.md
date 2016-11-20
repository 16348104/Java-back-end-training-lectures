# Chapter 3 DOM

> Document Object Model

[JavaScript HTML DOM Navigation](http://www.w3schools.com/js/js_htmldom_navigation.asp)

> Source code

```html
<html>
  <head>
    <title>DOM Tutorial</title>
  </head>
  <body>
    <h1>DOM Lesson one</h1>
    <p>Hello world!</p>
  </body>
</html>
```

### From the HTML above you can read:

- `<html> is the root node`
- `<html> has no parents`
- `<html> is the parent of <head> and <body>`
- `<head> is the first child of <html>`
- `<body> is the last child of <html>`

### and:

- `<head> has one child: <title>;`
- `<title> has one child (a text node): "DOM Tutorial"`
- `<body> has two children: <h1> and <p>`
- `<h1> has one child: "DOM Lesson one"`
- `<p> has one child: "Hello world!"`
- `<h1> and <p> are siblings`
