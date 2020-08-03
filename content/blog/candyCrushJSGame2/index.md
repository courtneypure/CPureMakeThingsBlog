---
title: Breaking Down Ania Kabow’s Build Your Own Candy Crush using JS Part 2 - Drag & Drop Candies
date: "2020-08-03"
description: In this series, I break down the functions, methods, and properties used in Ania Kabow's Candy Crush in JS tutorial.
---
>This post first appeared on my [Dev.to](https://dev.to/courtneypure/breaking-down-ania-kubow-s-candy-crush-game-in-js-part-2-kjn) blog on August 3, 2020. This is the second post in the series. [You can read Part 1 here.](https://dev.to/courtneypure/breaking-down-and-understanding-ania-kabow-s-build-your-own-candy-crush-using-javascript-part-1-8-create-the-game-board-3pck)

## setAttribute Method

Continuing on with the createBoard function we start off by giving the square a setAttribute input.  The two parameters we give in a setAttribute method is a name and value. In this case we are using the draggable attribute and setting it to true.  You can set the value of draggable to ‘true’, ‘false’, or ‘auto’.  

Note: Links and photos by default are automatically draggable.

```javascript
square.setAttribute(‘draggable’, true);
```

Next we set another attribute to the square, by giving it a string of id.  This is important to note that we are not using the id element but setting it as a string and as we loop over this we will get a number value.  We give the id a value of ‘i’ of i so that when it cycles through the board, it will give each square a value from 0-63.  Remember javascript is a zero based index so the zero counts as a number.

```javascript
square.setAttribute(‘id’, i)
```

The final createBoard function should look like this:

```javascript
function createBoard() {
	for (let i = 0; i < width*width; i++){
	const square = document.createElement(‘div’)
	square.setAttribute(‘draggable’, true)
	square.setAttribute(‘id’, i)
	let randomColor = Math.floor(Math.random() * candyColors.length)
	square.style.backgroundColor = candyColors[randomColor]
	grid.appendChild(square)
	square.push(square)
	}
}
```



## Creating Events to Drag Candies
We start by creating a forEach() function on the squares array and then inside the forEach() function we add an addEventListener to the object with the parameters; (event, function).  Each EventListener has a different event handle it is listening for; drag start, drag end, drag over, drag enter, drag leave, and drop.  When you give a node a handler through the attribute, it can only have one.  Since we have six events we want to happen, we use the addEventListener which lets us add any number of handlers.  

```javascript
square.forEach(square => square.addEventListener(‘dragstart’ , dragStart))
square.forEach(square => square.addEventListener(‘dragend’ , dragEnd))
square.forEach(square => square.addEventListener(‘dragover’ , dragOver))
square.forEach(square => square.addEventListener(‘dragenter’ , dragEnter))
square.forEach(square => square.addEventListener(‘dragleave’ , dragLeave))
square.forEach(square => square.addEventListener(‘drop’ , dragDrop))
```

Then we write the functions for each of those events once they are triggered.

```javascript
function dragStart() {
	console.log(this.id, ‘dragstart’);
}

function dragOver() {
	console.log(this.id, ‘dragover’);
}

function dragEnter() {
	console.log(this.id, ‘dragenter’);
}

function dragLeave() {
	console.log(this.id, ‘dragleave’);
}

function dragEnd() {
	console.log(this.id, ‘dragend’);
}

function dragDrop() {
	console.log(this.id, ‘dragdrop’);
}
```

Create a variable called colorBeingDragged and place it above the EventListeners.

```javascript
let colorBeingDragged
```

Then we add it to the function dragStart and set it equal to this.style.backgroundColor.

```javascript
function dragStart() {
	colorBeingDragged = this.style.backgroundColor
	console.log(colorBeingDragged)
	console.log(this.id, ‘dragstart’);
}
```

Since we want to reuse colorsBeingDragged on different events we have stored it in a variable. When we add colorBeingDragged variable we can see which color is being dragged.  You can check this by writing a console.log(colorBeingDragged) to the function code block.
*Stop review here for the night*….
We created another variable called colorBeingReplaced.

```javascript
let colorBeingReplaced;
```

And we attached that variable to the dragDrop function and set it to this.style.backgroundColor.

```javascript
function dragDrop() {
	console.log(this.id, ‘dragDrop’)
	colorBeingReplaced = this.style.backgroundColor
}
```


To replace them in the correct squares, this is where the IDs come into play. Here we used the parseInt() function (parse- meaning to analyze a string or text),  which takes a string argument and returns an integer.  Earlier we set the squares attribute and attached a number from 0 - 63 to it.  We use  the ‘this’ keyword because we want it to refer to the object it belongs to which is the square being dragged.  First we create two variables:

```javascript
let squareIdBeingDragged;
let squareIdBeingReplaced;
```

Note: Since the function is not written in strict mode, we are referring to the global variables.

```javascript
function dragStart() {
	colorBeingDragged = this.style.backgroundColor
	squareIdBeingDragged = parseInt(this.id)
	console.log(colorBeingDragged)
	console.log(this.id, ‘dragstart’);
}
```

In the dragDrop function is where we assign the id and set its background color. The squaresBeingReplaced is equal to the assigned number of that id.

```javascript
function dragDrop() {
	console.log(this.id, ‘dragDrop’)
	colorBeingReplaced = this.style.backgroundColor
	squareIdBeingReplaced = parseInt(this.id)
	squares[squareIdBeingDragged].style.backgroundColor = colorBeingReplaced
}
```

With the dragEnter and dragOver function we pass in e parameter which stands for event.  This will allow us to prevent the default behavior.  

An example of e.preventDefault() is when you create a registration form and the user has not completed the form.  You would want to prevent the user from submitting the form and give an error message as to what is wrong.

In the tutorial she mentions you could add animations to the square while you are dragging it but in the case of the tutorial we do not.

```javascript
function dragOver(e){
	e.preventDefault()
	console.log(this.id, ‘dragover’)
}

function dragEnter(e){
	e.preventDefault()
	console.log(this.id, ‘dragenter’)
}
```

After we enter in this code, the square being dragged (original square) is swapped with the a square it is replacing replaced. But the square we are dropping into stays the same color.  To fix this we added

```javascript
this.style.backgroundColor = colorBeingDragged
```

to the dragDrop function.   This changes the color of the square into the color being dragged.  Basically this will make sure that when you drag and drop a color it switches places with that color square.

```javascript
function dragDrop() {
	console.log(this.id, ‘dragDrop’)
	colorBeingReplaced = this.style.backgroundColor
	squareIdBeingReplaced = parseInt(this.id)
	this.style.backgroundColor = colorBeingDragged
	squares[squareIdBeingDragged].style.backgroundColor = colorBeingReplaced
}
```

And this concludes the breakdown of How to Drag & Drop Candies.  The next post in the series will focus on finding valid matches in the game.

## MDN web docs
###Functions Used:
* [forEach()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)

* [parseInt()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/parseInt)

* [e.preventDefault() ](https://developer.mozilla.org/en-US/docs/Web/API/Event/preventDefault)

### Loops, Iterations, Events & Properties Used:
* [for loop](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Loops_and_iteration)

* [setAttribute](https://developer.mozilla.org/en-US/docs/Web/API/Element/setAttribute)

* [this keyword](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)

* [Global Scope](https://developer.mozilla.org/en-US/docs/Glossary/Global_scope)

* [Event Reference for EventListeners Drag & Drop](https://developer.mozilla.org/en-US/docs/Web/Events)
* [Drag & Drop Events](https://developer.mozilla.org/en-US/docs/Web/API/HTML_Drag_and_Drop_API)


Each function and method above is linked to their respective MDN web doc pages.  This concludes the first part in this series of Breaking Down [Ania Kabow’s Candy Crush video](https://www.youtube.com/watch?v=XD5sZWxwJUk).

If there are any errors in my syntax or grammar please shoot me a comment or message to let me know!  This is my first technical blog post so I want to make sure I'm sharing the best information possible.
