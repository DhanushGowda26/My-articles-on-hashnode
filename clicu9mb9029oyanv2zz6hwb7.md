---
title: "Responsive Drop down"
seoTitle: "Responsive Drop down menu using java script"
seoDescription: "A Drop down menu which is responsive built using html.css and js. front end dev and Webdev are most trending jobs so one must know these skills in software"
datePublished: Thu Jun 01 2023 07:52:39 GMT+0000 (Coordinated Universal Time)
cuid: clicu9mb9029oyanv2zz6hwb7
slug: responsive-drop-down
tags: javascript, web-development, webdev, frontend-development

---

Welcome to this comprehensive blog post where we will delve into creating a dynamic dropdown menu using HTML, CSS, and JavaScript. In this tutorial, we will explore the JavaScript code in detail, explaining each function and built-in method used. By the end, you will have a solid understanding of the concepts involved and be able to implement similar functionality in your own projects. Let's dive in!

```xml
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="style.css">
    <title>Document</title>
</head>
<body>
    <div class="dropdown">
        <input type="text" id="in" placeholder="choose Area" onclick="dis()" oninput="suggest(this.value)" >
        <div class="dropdown-content" id="lists">
            <!-- Lot of "a" tags starting with "B", comment down what diffrence does it make -->
            <a href="">India</a>
            <a href="#">USA</a>
            <a href="#">UK</a>
            <a href="#">Japan</a>
            <a href="#">Spain</a>
            <a href="#">Italy</a>
            <a href="#">Bangladesh</a>
            <a href="#">Austrilia</a>
            <a href="#">Newzeland</a>
            <a href="#">Westindies</a>
            <a href="#">Delhi</a>
            <a href="#">Mumbai</a>
            <a href="#">Russia</a>
            <a href="#">Iran</a>
            <a href="#">Iraq</a>
            <a href="#">Karnataka</a>
            <a href="#">Bengaluru</a>
            <a href="#">Bhopal</a>
            <a href="#">Bengali</a>
            <a href="#">Bevanlli</a>
            <a href="#">BC cross</a>
            <a href="#">Bhevnalli</a>
            <a href="#">Benkikuppa</a>
            <a href="#">Bakasura</a>
            <a href="#">Byariranagal</a>
            <a href="#">Besninsuliya</a>
            <a href="#">Bangok</a>
            <a href="#">Belekuppa</a>
            <a href="#">Byanandur</a>
            <a href="#">Bantval</a>
            <a href="#">Bannur</a>
            <a href="#">Basvangudi</a>
            <a href="#">Banshankri</a>
            <a href="#">Btm layout</a>
            <a href="#">Bendakaluru</a>
            <a href="#">Brazil</a>
            <a href="#">Belgium</a>
            <a href="#">Bengaluru</a>
            <a href="#">Belgavi</a>
            <a href="#">Bangalore</a>
            <a href="#">Mandya</a>
            <a href="#">Musuru</a>
            <a href="#">South africa</a>
            <a href="#">Nagarbhavi</a>
        </div>
    </div>
    <script src="drop.js"></script>
</body>
</html>
```

HTML Structure: Let's begin by examining the HTML structure of our dropdown menu. The menu consists of an input field and a dropdown content div. The input field allows the user to type or click to select an option, while the dropdown content div contains the list of available options.

```scss
input{
    width: 200px;
    height: 30px;
    background-color: rgb(246, 208, 158);
}
input:hover{
    background-color: rgb(196, 222, 163);
}
.dropdown-content{
    display: none;
    position: absolute;
    width: 200px;
    max-height: 150px;
    overflow-y: scroll;  
}
.dropdown-content a{
    display:block;
    text-decoration: none;
    color: rgb(0, 0, 0);
}
 a:nth-child(even){
    background-color: rgb(206, 183, 183);
} 
.dropdown-content a:hover{
    color: rgb(149, 249, 18);
}
```

CSS Styling: To make our dropdown menu visually appealing, we will apply some basic CSS styles. These styles include defining the width and height of the input field, specifying background colours for different states (normal and hover), and determining the appearance of the dropdown content.

```javascript
var a = document.getElementById("lists");
var b = a.getElementsByTagName("a");
```

These two lines of code retrieve elements from the HTML document. `document.getElementById("lists")` gets the element with the ID "lists" and assigns it to the variable `a`. Then, `a.getElementsByTagName("a")` retrieves all the anchor tags (`<a>`) within the element `a` and assigns them to the variable `b`. In other words, it collects all the links within the dropdown content.

```javascript
function dis() {
  a.style.display = "block";
}
```

The `dis()` function is called when the user clicks on the input field. Its purpose is to display the dropdown content by changing the `display` style property of the element `a` to "block". This makes the dropdown content visible to the user.

```javascript
function suggest(input) {
  var filter = input.toUpperCase();
  for (var i = 0; i < b.length; i++) {
    var data = b[i].innerText || b[i].textContent;
    if (data.toUpperCase().startsWith(filter)) {
      b[i].style.display = "block";
      a.style.overflow = "auto";
    } else {
      b[i].style.display = "none";
    }
  }
}
```

The `suggest(input)` function is responsible for filtering and displaying suggestions based on the user's input. It takes the `input` parameter, which represents the user's input value. The input value is converted to uppercase using `toUpperCase()` and stored in the variable `filter`.

The function then iterates over each link (anchor tag) stored in the variable `b`. For each link, it retrieves the text content using `innerText` or `textContent` and stores it in the variable `data`. The text content is also converted to uppercase.

If the text content starts with the filter value (i.e., the user's input), the link is displayed by setting its `display` style property to "block". Additionally, the `overflow` style property of the dropdown content div (`a`) is set to "auto" to enable scrolling if the number of displayed links exceeds the maximum height.

If the text content doesn't start with the filter value, the link is hidden by setting its `display` style property to "none".

```javascript
function arrangeAlphabetically() {
  var links = Array.from(b);
  links.sort(function(a, b) {
    var textA = a.textContent.toUpperCase();
    var textB = b.textContent.toUpperCase();
    if (textA < textB) {
      return -1;
    } else if (textA > textB) {
      return 1;
    } else {
      return 0;
    }
  });
  for (var i = 0; i < links.length; i++) {
    a.appendChild(links[i]);
  }
}
```

The `arrangeAlphabetically()` function is responsible for sorting the links alphabetically. It converts the collection of links (`b`) into an array using `Array.from(b)` and assigns it to the variable `links`.

The `sort()` function is then used to sort the links in alphabetical order. It takes a comparison function as an argument, which compares the text content of two links (`a` and `b`). The comparison is performed by converting the text content to uppercase using `toUpperCase()`.

Inside the comparison function, a series of conditions (`if` and `else if`) compare the text content

```javascript
 window.addEventListener("DOMContentLoaded", arrangeAlphabetically);
```

The line `window.addEventListener("DOMContentLoaded", arrangeAlphabetically);` adds an event listener to the `window` object for the `"DOMContentLoaded"` event. This event is fired when the initial HTML document has been completely loaded and parsed, without waiting for stylesheets, images, and subframes to finish loading.

In this case, the event listener is set to execute the `arrangeAlphabetically` function when the `"DOMContentLoaded"` event occurs. The `arrangeAlphabetically` function is defined earlier in the code and is responsible for sorting and arranging the links alphabetically within the dropdown content.

By using the `"DOMContentLoaded"` event, the `arrangeAlphabetically` function will be called as soon as the HTML document has finished loading. This ensures that the links are sorted alphabetically and displayed correctly in the dropdown content before the user interacts with them.

```javascript
for (var i = 0; i < b.length; i++) {
  b[i].addEventListener("click", function() {
    var text = this.textContent;
    document.getElementById("in").value = text;
  });
}
```

* `var i = 0` initializes a variable `i` with a value of 0. This variable is used as the loop counter.
    
* `i < b.length` is the condition that specifies the loop should continue as long as `i` is less than the length of the `b` collection (number of anchor tags).
    
* `i++` increments the value of `i` by 1 after each iteration of the loop.
    
* `b[i]` represents the current anchor tag in the iteration. `b` is an array-like object that holds all the anchor tags.
    
* `.addEventListener("click", function() { ... })` adds an event listener to the current anchor tag for the "click" event. When the anchor tag is clicked, the function inside the event listener will be executed.
    
* `this.textContent` refers to the text content of the clicked anchor tag. It retrieves the text between the opening and closing tags of the anchor element.
    
* `document.getElementById("in")` retrieves the element with the ID "in". It assumes that there is an input field in the HTML document with the ID "in".
    
* `.value = text` sets the value property of the input field to the text content of the clicked anchor tag. This updates the value displayed in the input field when an anchor tag is clicked.
    

### Give a Follow for More Content

### Follow me on [**Twitter**](https://twitter.com/dhanuks26) **and** [**GitHub**](https://github.com/DhanushGowda26)