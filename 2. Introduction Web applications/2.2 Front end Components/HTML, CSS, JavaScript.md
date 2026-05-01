`HTML (Hyper Text Markup language)` is the core of web applications and contains all basic elements including titles, forms, images, and many other elements. The web browser, in turn, interprets these elements and displays them to the end-user.

Example

```html
<!DOCTYPE html> 
<html>     
<head>        
	<title>Page Title</title>    
</head>    
<body>        
	<h1>A Heading</h1>        
	<p>A Paragraph</p>    
</body> 
</html>`
```

The above will display this web page in browser

![[web_apps_html_2.jpg]]

Each element can contain other `HTML` elements while the main html should contain all other elements, which falls under `document`, distinguishing between `HTML` and documents written for other languages, such as `XML` documents.
 
![[hierarchy of html page.png]]

HTML element is opened and closed with a tag that specifies the element's type 'e.g. `<p>` for paragraphs', where the content would be placed between these tags. Tags may also hold the element's id or class 'e.g. `<p id='para1'>` or `<p id='red-paragraphs'>`', which is needed for CSS to properly format the element. Both tags and the content comprise the entire element.

## URL Encoding

It is important concept to learn also called percent-encoding. For browsers to display web page contents properly, it has to know charset in use. In URLs, for example, browsers can only use [ASCII](https://en.wikipedia.org/wiki/ASCII) encoding, which only allows alphanumerical characters and certain special characters. Therefore, all other characters outside of the ASCII character-set have to be encoded within a URL. URL encoding replaces unsafe ASCII characters with a `%` symbol followed by two hexadecimal digits.

For example, the single-quote character '`'`' is encoded to '`%27`', which can be understood by browsers as a single-quote. URLs cannot have spaces in them and will replace a space with either a `+` (plus sign) or `%20`. Some common character encodings are:

| Character | Encoding |
| --------- | -------- |
| space     | %20      |
| !         | %21      |
| "         | %22      |
| #         | %23      |
| $         | %24      |
| %         | %25      |
| &         | %26      |
| '         | %27      |
| (         | %28      |
| )         | %29      |
A full character encoding table can be seen [here](https://www.w3schools.com/tags/ref_urlencode.ASP).

Many online tools can be used to perform URL encoding/decoding. Furthermore, the popular web proxy [Burp Suite](https://portswigger.net/burp) has a decoder/encoder which can be used to convert between various types of encodings. Try encoding/decoding some characters and strings using this [online tool](https://www.url-encode-decode.com/).

#### Usage
`<head>` defines elements which are not displayed on the web page content where all elements that are displayed comes under `<body>`. Other important includes `<style>` which holds all the styling for the elements and `<srcipt>` which includes the JS code for the page.  

Each of these elements is called a [DOM (Document Object Model)](https://en.wikipedia.org/wiki/Document_Object_Model). The [World Wide Web Consortium (W3C)](https://www.w3.org/) defines `DOM` as:

`"The W3C Document Object Model (DOM) is a platform and language-neutral interface that allows programs and scripts to dynamically access and update the content, structure, and style of a document."`

The DOM standard is separated into 3 parts:

- `Core DOM` - the standard model for all document types
- `XML DOM` - the standard model for XML documents
-  `HTML DOM` - the standard model for HTML documents

For example, from the above tree view, we can refer to DOMs as `document.head` or `document.h1`, and so on.

Understanding the HTML DOM structure can help us understand where each element we view on the page is located, which enables us to view the source code of a specific element on the page and look for potential issues. We can locate HTML elements by their id, their tag name, or by their class name.

This is also useful when we want to utilize front-end vulnerabilities (like `XSS`) to manipulate existing elements or create new elements to serve our needs.

# Cascading Style Sheets (CSS)

`CSS (Cascading Style Sheets)` is a style sheet language used alongside HTML to format and set the style of HTML elements. There are several versions of CSS, just like HTML which gives it new capabilities and then browsers are updated alongside to support these features.

#### Example

At a fundamental level, CSS is used to define the style of each class or type of HTML elements (i.e., `body` or `h1`), such that any element within that page would be represented as defined in the CSS file. This could include the font family, font size, background color, text color and alignment, and more.

```CSS
`body {   
	background-color: black; 
}
 
h1 {   
	color: white;  
	text-align: center; 
} 

p {   
	font-family: helvetica;  
	font-size: 10px; 
}`
```

As previously mentioned, this is why we may set unique IDs or class names for certain HTML elements so that we can later refer to them within CSS or JavaScript when needed.

## Syntax
CSS defines the style of each HTML element or class between curly brackets `{}`, within which the properties are defined with their values (i.e. `element { property : value; }`).

Many properties can be manipulated for example `height`, `position` , `color` etc to make the web pages visually appealing.

CSS can be used for advanced animations for a wide variety of uses, from moving items all the way to advanced 3D animations. Many CSS properties are available for animations, like `@keyframes`, `animation`, `animation-duration`, `animation-direction`, and many others.

## Frameworks

Many may consider CSS to be difficult to develop. In contrast, others may argue that it is inefficient to manually set the style and design of all HTML elements in each web page. This is why many CSS frameworks have been introduced, which contain a collection of CSS style-sheets and designs, to make it much faster and easier to create beautiful HTML elements.

Furthermore, these frameworks are optimized for web application usage. They are designed to be used with JavaScript and for wide use within a web application and contain elements usually required within modern web applications. Some of the most common CSS frameworks are:

- [Bootstrap](https://www.w3schools.com/bootstrap4/)
- [SASS](https://sass-lang.com/)
- [Foundation](https://en.wikipedia.org/wiki/Foundation_\(framework\))
- [Bulma](https://bulma.io/)
- [Pure](https://purecss.io/)
# JavaScript
[JavaScript](https://en.wikipedia.org/wiki/JavaScript) is one of the most used languages in the world. It is mostly used for web development and mobile development. `JavaScript` is usually used on the front end of an application to be executed within a browser. Still, there are implementations of back end JavaScript used to develop entire web applications, like [NodeJS](https://nodejs.org/en/about/).

While `HTML` and `CSS` are mainly in charge of how a web page looks, `JavaScript` is usually used to control any functionality that the front end web page requires. Without `JavaScript`, a web page would be mostly static and would not have much functionality or interactive elements.

---
#### Example

Within the page source code, `JavaScript` code is loaded with the `<script>` tag, as follows:

```html
<script type="text/javascript"> ..JavaScript code.. </script>`
```
A web page can also load remote `JavaScript` code with `src` and the script's link, as follows:

```html
<script src="./script.js"></script>`
```

An example of basic use of `JavaScript` within a web page is the following:

```javascript
document.getElementById("button1").innerHTML = "Changed Text!";`
```
The above example changes the content of the `button1` HTML element. From here on, there are many more advanced uses of `JavaScript` on a web page. The following shows an example of what the above `JavaScript` code would do when linked to a button click:

Original Text

As with HTML, there are many sites available online to experiment with `JavaScript`. One example is [JSFiddle](https://jsfiddle.net/) which can be used to test `JavaScript`, `CSS`, and `HTML` and save code snippets. `JavaScript` is an advanced language, and its syntax is not as simple as `HTML` or `CSS`.

## Frameworks

As web applications become more advanced, it may be inefficient to use pure `JavaScript` to develop an entire web application from scratch. This is why a host of `JavaScript` frameworks have been introduced to improve the experience of web application development.

These platforms introduce libraries that make it very simple to re-create advanced functionalities, like user login and user registration, and they introduce new technologies based on existing ones, like the use of dynamically changing `HTML` code, instead of using static `HTML` code.

These platforms either use `JavaScript` as their programming language or use an implementation of `JavaScript` that compiles its code into `JavaScript` code.

Some of the most common front end `JavaScript` frameworks are:

- [Angular](https://www.w3schools.com/angular/angular_intro.asp)
- [React](https://www.w3schools.com/react/react_intro.asp)
- [Vue](https://www.w3schools.com/whatis/whatis_vue.asp)
- [jQuery](https://www.w3schools.com/jquery/)

A listing and comparison of common JavaScript frameworks can be found [here](https://en.wikipedia.org/wiki/Comparison_of_JavaScript_frameworks).