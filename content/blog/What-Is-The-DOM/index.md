---
title: What is the DOM?
date: "2020-06-29"
description: A small recap of the Document Object Model
---

<iframe src="https://player.vimeo.com/video/433631753" width="640" height="480" frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>

First published in 1998, the **Document Object Model (DOM)** is a programming interface that creates a model of an HTML or XML page in the form of a hierarchical “DOM tree.” With twelve node types in total, the four main ones used in javascript are:

* **Document Node** - This is your root node.  It represents the entire page.
* **Element Nodes** - These represent your h1 - h6, div, p, form, etc. elements.
* **Attribute Nodes** - This node is used to trigger new CSS rules.  Note that it is not a child of the element node.
* **Text Node** - This is the final node that contains the text within the element.  This node has no children attached to it.

The DOM is referred to as an **API or Application Programing Interface.** An API lets programs and scripts talk to one another. The DOM is the “middle man” between the script and the browser. It is built for any language and different browsers have different DOMs. It is NOT language dependent, nor is it a programming language. The DOM simply allows one to access a web document. It relays what the script requests of the browser and how this should be updated on the page for the user.  

For more information on the DOM and how to manipulate it you can visit the [Mozilla Developers Network](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction) or check out the book by [John Duckett Javascript & JQuery - Interactive front-end web development](http://javascriptbook.com/)!
