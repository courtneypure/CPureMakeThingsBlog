---
title: Breaking Down and Understanding Ania Kabow’s Build Your Own Candy Crush using Javascript Part 1/7 - Create the Game Board
date: "2020-07-28"
description: In this seven part series, I break down the functions and methods in depth of Ania Kabow's Candy Crush tutorial.
---
>This post first appeared on my [Dev.to](https://dev.to/courtneypure/breaking-down-and-understanding-ania-kabow-s-build-your-own-candy-crush-using-javascript-part-1-8-create-the-game-board-3pck) blog on July 28, 2020.

For my second run of [#100 Days of Code](https://www.100daysofcode.com) I wanted to learn vanilla javascript with a focusing on building games and I stumbled upon a great youtube channel by [Ania Kubow #JavaScriptGames](https://www.youtube.com/channel/UC5DNytAJ6_FISueUfzZCVsw).


Here I am going to break down the methods and functions used for each step of Ania’s 30 minute video.  She does an excellent job of explaining as she goes along so, but I wanted to dig a bit deeper to understand why we were using what we were using.

Being new to the JavaScript language, my goal is to start to form connections on how to use each method and function in order to build the games and apps I want.  I will be breaking down the posts as follows:

1. Create Board and Randomly Create Candies

2. Swap Candies

3. Drag and Drop Candies

4. Check for Matches

5. Check for Valid Matches

6. Move Candies Down

7. Generate New Candies  





In this first post of this series, I will break down each part of the code that we use to create the game board.  We worked with three files: index.html, style.css, and app.js.  The IDE that I used for this project was [Visual Studio Code](https://code.visualstudio.com/) but Ania uses [Atom](https://atom.io/) in the video.  Both are free and great to use and perfectly fine, Visual Studio has more extensions you can add on.


**Methods Used:**
* querySelector
* for loop iteration statement
* createElement
* appendChild
* push


**Functions Used:**
* Math.random()
* Math.floor()

Let's jump in!



## Creating a Grid in HTML and CSS

We start off pretty simply by creating a div tag in the index.html document and give it a class of “grid.”

Then moving on to the stylesheet, we want to create a square 8 x 8 grid. With each square being 70px high and 70px wide, we created a board size of 560px(8 * 70px).

Initially grids will appear stacked, so to fix that we use flex grid and flex wrap.

```CSS
 .grid {
 height: 560px;
 width: 560px;
 display: flex;
 flex-wrap: wrap;
}
```

Next we create the squares for the “candies” on the board by making the height and width 70px by 70px.

```CSS
 .grid div {
 height: 70px;
 width: 70px;
 }
```

##Adding an EventListener

Switching over to the JS file, Ania starts off using a boiler plate set up.

```javascript
 document.addEventListener(‘DOMContentLoaded’), () => {

 })
```


From here all the code is written inside the EventListener code block.  

###First Argument - ’DOMContentLoaded’

The ‘DOMContentLoaded’ event is the first argument and fires when the initial HTML page has loaded and DOM tree is built.  We use the DOMContentLoaded versus the load event because the load event is used to detect a fully loaded page which includes images and stylesheets.

###Second Argument - Anonymous Arrow Function
The event is then followed by an anonymous arrow function.  We have to use the anonymous function as the second argument in the EventListener because we want it to wait until the event, in this case the HTML file and DOM tree, is loaded and triggers the function. We "wrap" the named functions inside an anonymous function because we want to make sure that the function is not invoked until the DOM content is loaded. If the interpreter was to see the parenthesis after a named function, it would fire right away. Ania mentions, "this is also a foolproof way to make sure events happen in order.”

_NOTE: EventListeners are not supported with IE8 or earlier versions.  In this case you would use .attachEvent for earlier versions._




##Creating the Square Spaces for the Candies

Next we create a constant with the name of grid and use a querySelector method to grab the grid class from the HTML page. Then we add another constant with a width of 8.

```javascript
 const grid = document.querySelector(‘.grid’);
 const width = 8;
```

We are using a constant in this case because we don’t want these to be reassigned later as compared to var or let where you can swap values.  If you want to learn more [Wes Bos has a great article on let vs const](https://wesbos.com/let-vs-const).


###for Loop
Create a function called createBoard and inside the code block we added a for loop to create a 64 square board (8x8).  Inside the for loop code block, we use the createElement method to create a div for the squares.  Then we use the appendChild, append meaning simply to add, to add each 70px square to the board.  This for loop will continue until 'i' hits 64 since 'i' is NOT less than 64.

```javascript
function createBoard () {

for (let i = 0;  i < width*width;  i++) {

const square = document.createElement(‘div’);
grid.appendChild(square);
	}
}
```

Next we created another const called squares and make it an empty array so we can actual work and manipulate it.

```javascript
const squares = []
```

In the for loop, we pass each square into the empty array we created called squares.  We did this by using the array push method on squares which adds a new item to the array.

```javascript
const grid = document.querySelector(‘.grid’)
const width = 8
const squares = []

function createBoard () {
for (let i = 0; i < width*width; i++) {

const square = document.createElement(‘div’);
grid.appendChild(square);
squares.push(square);
	}
}
```

Finally call (or invoke) the function.  To make sure it works, inspect the page and see all 64, 70px-squares that will represent the candy pieces.

```javascript
createBoard()
})
```


##Creating the Candy Colors

To create the individual candy colors we create a constant array we called candyColors. In the case of building my Animal Crossing themed candy crush game, I change the color entries by writing the location of each image I created.  You can see my code on my [github](www.github.com/courtneypure) for further reference.

```javascript
const candyColors = [
‘red’,
‘yellow’,
‘orange’,
‘purple’,
‘green’,
‘blue’
]
```

To make the colors random we create a variable using let. The Math.random function is used to get a random color, and the Math.floor is used to get the nearest whole number.  Math.random creates a number between 0 to 1. When we multiply that with the candyColors length, which is 5, we will get a whole number using Math.floor. Since javascript starts at zero we will get a number from 0 - 5. For example candyColors[2] will give us orange, candyColors[0] will give us red and so on.

```javascript
const grid = document.querySelector(‘.grid’)
const width = 8
const squares = []

const candyColors = [
‘red’,
‘yellow’,
‘orange’,
‘purple’,
‘green’,
‘blue’
]

function createBoard () {
for (let i = 0; i < width*width; i++) {

const square = document.createElement(‘div’);
let randomColor = Math.floor(Math.random() * candyColors.length)
grid.appendChild(square);
squares.push(square);
	}
}
```

Lastly we passed the random color to the square with square.style.backgroundColor object and set it equal to candyColors[randomColor];  The style object will assign a square to a random color from the array of colors we stated above.  Note that backgroundColor is camelcase as compared to the CSS which is styled, background-color.

The final script for this part should look like this

```javascript
const grid = document.querySelector(‘.grid’)
const width = 8
const squares = []

const candyColors = [
‘red’,
‘yellow’,
‘orange’,
‘purple’,
‘green’,
‘blue’
]

function createBoard () {
for (let i = 0; i < width*width; i++) {

const square = document.createElement(‘div’);
let randomColor = Math.floor(Math.random() * candyColors.length);
square.style.backgroundColor = candyColors[randomColor];
grid.appendChild(square);
squares.push(square);
	}
}
```


And with this final step we have completed the board and generated randomized candies!  This section is the first 8-9 minutes of the 30 minute video and it covers a lot.  Hence why I wanted to dive deeper and break it down.

To recap in this exercise we learned:

* [EventListener](https://developer.mozilla.org/en-US/docs/Web/API/EventListener)

* [querySelector method](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelector)

* [for loop iterative statement](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Loops_and_iteration)

* [createElement method](https://developer.mozilla.org/en-US/docs/Web/API/Document/createElement)

* [appendChild method](https://developer.mozilla.org/en-US/docs/Web/API/Node/appendChild)

* [push method](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/push)

* [Math.random() function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/random)

* [Math.floor () function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/floor)

Each function and method above is linked to their respective MDN web doc pages.  This concludes the first part in this series of Breaking Down [Ania Kabow’s Candy Crush video](https://www.youtube.com/watch?v=XD5sZWxwJUk).

If there are any errors in my syntax or grammar please shoot me a comment or message to let me know!  This is my first technical blog post so I want to make sure I'm sharing the best information possible.
