# DOM
#
## What is the DOM? 
##### The **Document Object Model (DOM)** is a programming interface for web documents. It represents the page so that programs can change the document **structure**, **style**, and **content**. 
#
#
##### The DOM is a W3C (World Wide Web Consortium) standard.
##### The W3C DOM standard is separated into 4 different parts:
- Core DOM - standard model for all document types
- XML DOM - standard model for XML documents
- HTML DOM - standard model for HTML documents
- SVG DOM - standard model for SVG documents (new)
#
## What is a DOM tree?
##### A DOM tree is a kind of tree whose nodes represent an HTML or XML or SVG document's contents.
#
##### A document tree is a node tree whose root is a document (html).
#
##### DOM trees contain several kinds of nodes, in particular a **DocumentType node**, **Element nodes**, **Text nodes**, **Comment nodes**.
#
#
```
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>My Document</title>
</head>
<body>
<h1>Header</h1>
<h2>Description</h2>
<p>Paragraph</p>
<!-- This is a comment -->
</body>
</html>
```
![](https://cdn-media-1.freecodecamp.org/images/3n6SPcMH0mmG6cFeB3SJBEA-9Yyfgp3xYZ7u)
##### Check the DOM tree online here - https://software.hixie.ch/utilities/js/live-dom-viewer/
#
##### (Note that, although the above tree is similar to the above document's DOM tree, it's not identical, as the actual DOM tree preserves [whitespace](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Whitespace).)
#
#
## How the DOM works?
##### For example, each HTML **<form>** element is represented by a **HTMLFormElement object** in the DOM, which is an implementation of the **HTMLFormElement interface** (not the vise versa).
    [For mor interfaces](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction#fundamental_data_types)
#
##### Other interfaces extend the Node interface and inherit its properties and methods, but as each interface can have children, inheritance works at multiple levels
![N|Solid](https://developer.mozilla.org/en-US/docs/Web/API/HTML_DOM_API/html-dom-hierarchy.svg)
#
#
## What is the DOM API?
##### **API** is a collection of classes, interfaces, properties, methods, and other code structures that developers can use to access the functionality of an application.
##### The DOM API is written in JavaScript, and you can use it to manipulate the DOM of a web document using JavaScript.
#
##### The following is a brief list of common APIs in web and XML page scripting using the DOM.
- document.querySelector(selector)
- document.querySelectorAll(name)
- document.createElement(name)
- parentNode.appendChild(node)
- element.innerHTML
- element.style.left
- element.setAttribute()
- element.getAttribute()
- element.addEventListener()
- window.content
- GlobalEventHandlers/onload
- window.scrollTo()
#
#
# BOM and DOM
##### Browser Object Model (BOM).
##### Browsers feature a Browser Object Model (BOM) that allows access and manipulation of the browser window. Using the BOM, developers can move the window, change text in the status bar, and perform other actions that do not directly relate to the page content. Because no standards exist for the BOM, each browser has its own implementation, meanwhile the DOM has W3C specification (standart).
#
![](https://www.w3docs.com/uploads/media/default/0001/05/e4b9eba4ca04af8858bb8f14a8ae6b1f6006c21b.png)
#
#
# CSS Object Model (CSSOM)
##### The CSS Object Model is a set of APIs allowing the manipulation of CSS from JavaScript. It is much like the DOM, but for the CSS rather than the HTML. It allows users to read and modify CSS style dynamically.
##### [See more about CSSOM](https://developer.mozilla.org/en-US/docs/Web/API/CSS_Object_Model)
#
#
#
# HTML
##### HTML (Hypertext Markup Language) is the code that is used to structure a web page and its content.
#
#### HTML Specification
##### HTML is the World Wide Web's core markup language. Originally, HTML was primarily designed as a language for semantically describing scientific documents.
#
```
<html>
<head>
  <title>My Document</title>
</head>
<body>
  <h1>Header</h1>
  <p>Paragraph</p>
<!-- Comment —->
</body>
</html>
```
#
##### Anatomy of html element
![](https://ianrmedia.unl.edu/images/resources/html-anatomy.png)
#
#### What's new in HTML5?
##### In HTML, there are a host of new **semantic elements** intended to indicate the basic structure of a page:
- header
- nav
- main
- article
- aside
- section
- footer
#
- Video and Audio
- canvas
- header
- footer
- New types for input tags - ContentEditable, Required Attribute, Email attribute
- Progress,
- section,
- main
- Figure and Figcaption
- Placeholders
- Inline elements - 
-- mark – It highlights the content that is marked in some or the other way.
-- time – This helps in adding current time as well as date to the webpage.
-- meter – It helps in indicating that how much space in the storage disk is still there.
-- progress bar – It helps in knowing the progress of the task that has been assigned for its completion.

##### A “null” or “empty” element is an element that has no content. These include:
- <img> (before with self closing tag...)
- <br>
- <hr>
#
#
Zero width images

Accessibility
##### To validate your HTML - https://validator.w3.org/
#
#
#
#### The history.
##### With the creation of the W3C HTML's development changed venues again:
- 1995 known as HTML 3.0
- 1997 known as HTML 3.2 (after HTML4)
- W3C membership decided to stop evolving HTML and instead begin work on an XML-based equivalent, called **XHTML**(2000)
- DOM Level 1 (in 1998) and DOM Level 2 Core and DOM Level 2 HTML (starting in 2000 and culminating in 2003)
- DOM Level 3 specifications published in 2004 but the working group being closed before all the Level 3 drafts were completed
- 2004 HTML development reopened by W3C workshop, but for only form elements - rejected by Mozilla and Opera
-  Apple, Mozilla, and Opera jointly announced their intent to continue working on the effort under the umbrella of a new venue called the WHATWG.
-  2006, the W3C indicated an interest to participate in the development of HTML5
-  2007 formed a working group chartered to work with the WHATWG on the development of the HTML5 specification
-  2011, however, the groups came to the conclusion that they had different goals: the W3C wanted to publish a "finished" version of "HTML5", while the WHATWG wanted to continue working on a Living Standard for HTML
-  2019, the WHATWG and W3C signed an agreement to collaborate on a single version of HTML going forward
#
#
#
#
# Whitespaces
#### Whitespace is any string of text composed only of spaces, tabs or line breaks
##### In the case of HTML, whitespace is largely ignored
#
```
 <h1>       Hello       World!      </h1>
```
#
##### What happens?
- There will be some text nodes that contain only whitespace, and
- Some text nodes will have whitespace at the beginning or end.
![](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Whitespace/dom-string.png)
#### How does CSS process whitespace?
##### Most whitespace characters are ignored, not all of them are.
#
```
<h1>   Hello
        <span> World!</span>   </h1>
<!--
<h1>◦◦◦Hello◦⏎
⇥⇥⇥⇥<span>◦World!</span>⇥◦◦</h1>
-->
```
##### [For example click here](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Whitespace#how_does_css_process_whitespace)
#

#
#
#
#
#
#
#
#
