# Python Treasure Hunt

This is a tutorial on building a MineSweeper-like game called Sonar Treasure Hunt. Rather than playing it in a GUI with a point and click interface, we'll be doing it in the console.

Programming text-based games is a relatively common part of coding interviews. It tests a number of basic coding skills and the console is the great equalizer.

We'll be using a slide-based deck in the workshop, but keep this window open as it will correlate with the slides and give you more details than the slides.

## Slide 01: Opening Slide

This shows as you're all filing in. Please get online and go to https://REPL.it and the bit.ly link goes to this github repository. We'll be using this as our online coding environment for Python.

## Slide 02: Welcome

The exercise we're doing, "Sonar Treasure Hunt" is by Al Sweigart, from his book "[Invent Your Own Computer Games with Python - 4th Edition](https://inventwithpython.com/invent4thed)." It is used with permission thanks to his Creative Commons licensing on all his books. This presentation borrows liberally from his code and text.

![Invent Your Own Computer Games cover](images/ivnewgames.jpg)



We are using **Chapter 13** of the book, so if you're a beginner with Python, this workshop isn't for you. We'll deal with middle school math (Cartesian coordinates and the Pythagorean Theorem), data structures (which are variables that hold other variables), and Python methods for manipulating strings and data structures.

Here's a working version (just copying Al Sweigart's final code): [play the game](https://repl.it/repls/PrevailingEasygoingAdministrators)



## Slide 03: Repl.it

Please go to [repl.it](https://repl.it) and click the "+new repl" button.

![repl.it homepage](images/replit00.jpg)

Select Python.

![selection widget](images/replit01.jpg)

Then click the "Create repl" button. The result will be a Python programming environment and runtime. We're ready to start coding.

## Slide 4: Demo 1

We'll be creating a Sonar Treasure Hunt game. The game will draw our oceanscape and hide treasure chests in it. 

When we put a sonar device down, it will tell us  the distance to nearby treasure chests, but not the direction.

## Slide 5: Demo 2

If we put down multiple devices, the combined data can help us triangulate the position of a treasure chest.

## Slide 6: Cartesian Coordinates 1

Let's get the math out of the way. Cartesian Coordinates are a point's place on a grid. A flat, or two-dimensional grid will have two axes: the x-axis that goes left to right, and the y-axis that goes up and down. If you've done Scratch, you're probably pretty familiar with this.

Where the two axes cross is the coordinate 0,0.

## Slide 7: Cartesian Coordinates 2

If you move away from the the center, the numbers change to measure how many units away.

This second dot is at 3,4, We say it in that order, because we usually say X first, then Y.

## Slide X: The Pythagorean theorem

If we add a third dot at 0,4, we have a triangle. Not only do we have a triangle, but we have a "right triangle." That's a triangle where one of the angles is a 90, degree angle, or a quarter of a circle. 

The straight lines that meet to form that crisp right angle are the base and height. The third longer line that connects their ends is called the hypotenuse.

Way back in Ancient Greece, a mathematician named Pythagoras figured out something cool. If you took the lengths of all the lines and multiplied them by themselves to get their squares, the base's square plus the height's square would always equal the hypotenuse's square. 

Which means if you know the base and the height, you don't need to take a ruler and measure the hypotenuse. You could *derive* it mathematically.

## Slide 8: Lists

Lists are variables that can hold multiple other variables, including other lists.

```python
x = [] # empty list
y = [ "potato" , 78 , "hut" , "hike" ]
z = [ [ 1 , 2 ] , ["apple" , "orange"] ]
```

Lists start counting at 0. 

`y[0]`'s value is "potato".

`z[1][0]`'s value is "apple".

## Slide 9: Let's get programming

First we're going to import the modules from the SPL (Standard Python Library) that we'll need.

We've got `random` for generating random numbers (which we'll need almost right away), math for doing more advanced math to figure out how far away our sonars are from our treasure chests, and sys for a system operation to end the program when all is said and done.

Then we have our first function. It's going to create the ocean for our game board.

It's going to create a board 60 characters wide by 15 high. Let's look at the code

```python
# Sonar Treasure Hunt

import random
import sys
import math

def getNewBoard():
    # Create a new 60x15 board data structure.
    board = []
    for x in range(60): # The main list is a list of 60 lists.
        board.append([])
        for y in range(15): 
            # Each list in the main list has 15 single-character strings.
            # Use different characters for the ocean to make it more readable.
            if random.randint(0, 1) == 0:
                board[x].append('~')
            else:
                board[x].append('`')
    return board
```

The board data structure is a list of lists of strings. The first list represents the x-coordinate. Since the game’s board is 60 characters across, this first list needs to contain 60 lists. After we create the `board` list, we create a for loop that will append 60 blank lists to it.

But board is more than just a list of 60 blank lists. Each of the 60 lists represents an x-coordinate of the game board. There are 15 rows in the board, so each of these 60 lists must contain 15 strings. Within that is another for loop that adds 15 single-character strings that represent the ocean.

The ocean will be a bunch of randomly chosen '~' and '\`' strings. The tilde (~) and backtick (\`) characters—located next to the 1 key on your keyboard—will be used for the ocean waves. To determine which character to use, we apply this logic: if the return value of random.randint() is 0, add the '~' string; otherwise, add the '\`' string. This will give the ocean a random, choppy look.

