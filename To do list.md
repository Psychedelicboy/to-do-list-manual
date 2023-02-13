# How to create a to-do list using javascript

## Table of contents:
1. [Before you begin](#before-you-begin)
2. [Creating the basic framework of the page](#creating-the-framework)
3. [Adding style to the page](#adding-style)
4. [Creating page behavior](#creating-behavior)

This tutorial shows how to create a to-do list using javascript with a help of HTML and CSS.

Before diving into this tutorial, it is advisable that you have a basic understanding of how javascript works, as well as HTML and CSS.

If you think you need to brush up on your front-end skills, please refer to the [MDN Web Docs](https://developer.mozilla.org/en-US/).

## Before you begin<a name="before-you-begin"></a>

Before you begin, make sure you have the latest version of [Google Chrome](https://www.google.com/chrome/?brand=YTUH&gclid=CjwKCAjw2OiaBhBSEiwAh2ZSP5Ek-1OiUUwDMM34V8m0OrCvSUB6FvvRpf8k98owzjz2zWs6qy02oxoCl90QAvD_BwE&gclsrc=aw.ds) or [Mozilla Firefox](https://www.mozilla.org/en-US/firefox/new/) installed.

Next, choose a code editor. The most popular code editors are [Visual Studio Code](https://code.visualstudio.com/) and [Sublime Text](https://www.sublimetext.com/), as well as many others.

<details>
    <summary>Why use a code editor?</summary>

>Code editors are especially useful when writing code because they include code highlighting and some code examples.

</details>

## Creating the basic framework of the page<a name="creating-the-framework"></a>

First, create a new folder. In it create 3 files: ***page.html***, ***style.css*** and ***script.js***.

Open ***page.html*** in the code editor of your choise. 

### ***Create a simple structure of the future to do list:***

```
<!DOCTYPE html>
<head>
    <link rel="stylesheet" href="style.css">
<body>

<div id="myDIV" class="header">
    <h2>My To-Do List</h2>
    <input type="text" id="myInput" placeholder="Title...">
    <span onclick="newElement()" class="addBtn">Add</span>
</div>
  
  <ul id="myUL">
  </ul>

<script src="script.js"></script>

</body>

</head>

```

Let us take a look at what happens here: External CSS is declared in the 'head' part of the HTML page. The page itself consists of several parts. The first part consists of the header with the input field and the 'Add' button. The second part consists of an empty list to be filled with user input.

Save the page and open it in the web browser. You should see the header with the text "My To-Do List", an input field and the "Add" button.

## Adding style to the page<a name="adding-style"></a>

Next, we need to add some styling to the page. To do this, open ***style.css*** file.

### Include the padding and border in an element's total width and height, remove margins and padding from the list:

```
* {
    box-sizing: border-box;
    font-family: Arial, Helvetica, sans-serif
  }

ul {
    margin: 0;
    padding: 0;
  }
```

### Style the list items:

```
  ul li {
    cursor: pointer;
    position: relative;
    padding: 12px 8px 12px 40px;
    background: #eee;
    font-size: 18px;
    transition: 0.2s;
  }
```

### Add a background color and strike out text for a to do item when it is clicked on:

```
  ul li.checked {
    background: #888;
    color: #fff;
    text-decoration: line-through;
  }
```

### Add a "checked" mark for a new to do item:
  
```  
  ul li.checked::before {
    content: '';
    position: absolute;
    border-color: #fff;
    border-style: solid;
    border-width: 0 2px 2px 0;
    top: 10px;
    left: 16px;
    transform: rotate(45deg);
    height: 15px;
    width: 7px;
  }
```

### Style the delete button

```
  .delete {
    position: absolute;
    right: 0;
    top: 0;
    padding: 12px 16px 12px 16px;
  }

    .delete:hover {
    background-color: #6DE3FB;
    color: white;
  }
```

### Style the header:

```
  .header {
    background-color: #6DE3FB;
    padding: 30px 40px;
    color: white;
    text-align: center;
  }
```

### Clear floats after the header:

```
  .header:after {
    content: "";
    display: table;
    clear: both;
  }
```

### Style the input:

```
  input {
    margin: 0;
    border: none;
    border-radius: 0;
    width: 75%;
    padding: 10px;
    float: left;
    font-size: 16px;
  }
```

### Style the "Add" button

```
  .addBtn {
    padding: 10px;
    width: 25%;
    background: #d9d9d9;
    color: #555;
    float: left;
    text-align: center;
    font-size: 16px;
    cursor: pointer;
    transition: 0.3s;
    border-radius: 0;
  }

    .addBtn:hover {
    background-color: #bbb;
  }
```
Save the ***style.css*** and reload the page. You should see how the page has changed.


## Creating page behavior<a name="creating-behavior"></a>

First, open ***script.js*** and add following code.

### Create a "delete" button and append it to each list item:

```
var myNodelist = document.getElementsByTagName("LI");
var i;
for (i = 0; i < myNodelist.length; i++) {
  var span = document.createElement("SPAN");
  var txt = document.createTextNode("\u00D7");
  span.className = "delete";
  span.appendChild(txt);
  myNodelist[i].appendChild(span);
}
```

### Hide the current list item by clicking on the delete button:

```
var delete = document.getElementsByClassName("delete");
var i;
for (i = 0; i < delte.length; i++) {
  delete[i].onclick = function() {
    var div = this.parentElement;
    div.style.display = "none";
  }
}
```

### Add checkmark symbol when clicking on a list item:

```
var list = document.querySelector('ul');
list.addEventListener('click', function(ev) {
  if (ev.target.tagName === 'LI') {
    ev.target.classList.toggle('checked');
  }
}, false);
```

### Create a new list item when clicking on the "Add" button:

```
function newElement() {
  var li = document.createElement("li");
  var inputValue = document.getElementById("myInput").value;
  var t = document.createTextNode(inputValue);
  li.appendChild(t);
  if (inputValue === '') {
    alert("You must write something!");
  } else {
    document.getElementById("myUL").appendChild(li);
  }
  document.getElementById("myInput").value = "";

  var span = document.createElement("SPAN");
  var txt = document.createTextNode("\u00D7");
  span.className = "delete";
  span.appendChild(txt);
  li.appendChild(span);

  for (i = 0; i < delete.length; i++) {
    delete[i].onclick = function() {
      var div = this.parentElement;
      div.style.display = "none";
    }
  }
}
```

Save ***script.js*** and reload the page. Now you should be able to add to do items by typing the name and clicking the "Add" button. When you click on the added item, you should be able to mark it as done and delete it by clicking on the "Delete" button.
