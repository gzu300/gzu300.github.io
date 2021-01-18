---
title: HTML CSS JS in one day
date: 2021-01-18
---

# HTML
basic structure
```html
<!DOCTYPE HTML>
<html> <!this is called a tag>
    <head>
    <script src="js/somefile.js" type="text/javascript"></script> <! include a js file>
    <link href="styles.css" rel="stylesheet"> <!include a css file>
    hello, title
    </head>
    <body class="centered"> <!call css function>
    hello, body
    </body>
</html>
```
# CSS
```CSS
/*this file is called 'style.css'. but in the same folder as the above html file*/
.centered
{
    text-aligned: center;
}
```
# JavaScript
## DOM
- document object model. a specific object in JS that contains hierarchy of the html file. By changing the attributes of the DOM, it makes changing the website dynamically possible.  
- DOM has properties and methods to manipulate html files. example methods: getElementbyId(id), appendChild(node), removeChild(node), etc.  
- combine events and js function in html tag to trigger the effect.  
- jQuery libary in JS is popular to shorten the syntax.  
Syntax example:
```JavaScript
document.getElementbyId('colorDiv').style.backgroundColor='green' //vernilla JS
$('#colorDev').css('backgroundColor', 'green'); //jQuery libary way to set background color
``` 
[cheatsheet for HTML, CSS, JS and jQuery](https://htmlcheatsheet.com)  
[jQuery API](https://api.jquery.com)
