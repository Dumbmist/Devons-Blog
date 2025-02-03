---
layout: post
title: Nested Conditionals, Homework
description: Homework for nested conditionals
type: issues
comments: True
---

### Homework Objectives

You and your friend want to do different things at the amusement park. To decide, you do a coin flip. Heads means that you get to choose where to go and tails means that your friend gets to choose. If you go on a ride, be sure to check if you are the right height and have enough tickets, and if you go to a food stand, make sure that you have enough money and that the food is in stock. Be creative, and make sure to use nested conditionals!

### Instructions

1) Create a JavaScript file (Ex. insertName.js)

2) Plan out what you will be doing and make variables for the necessary things. There will be a coin flip, so make a variable for that. If there are rides, make a value for the amount of tickets the person has and what height they are. If they go to a food stand, you can make a variable for the amount of money that you have and if the food is in stock.

3) Use Math.random() for the coin flip. This generates a number between 0 and 1, so then you multiply this value by 2 and put it inside Math.floor() to round down and get either 0 or 1. Make this the coin flip variable.

4) Use an if statement to check what the result of the coin flip was and use console.log to print out a statement to see who won or lost the coin flip. Along with that, print out where they are going next.

5) Use more if statements inside of if statements to check if the person can do what they want to do. (Are they tall enough, do they have enough money, etc.)

6) After all the checks, print out a result of what happened. If you get stuck, you can look at the examples in the popcorn hacks. Please don't copy and paste, though! 



```python
%%js

let coinFlip = Math.floor(Math.random() * 2);
let tickets = Math.floor(Math.random() * 10) + 1;
let height = Math.floor(Math.random() * 40) + 50;
let money = Math.floor(Math.random() * 20) + 5;
let foodInStock = Math.random() > 0.5;

console.log("Coin flip result:", coinFlip === 0 ? "Heads" : "Tails");

if (coinFlip === 0) {
    console.log("Going to the roller coaster!");

    if (height >= 54) {
        if (tickets >= 3) {
            tickets -= 3;
            console.log("You are tall enough and have enough tickets! Maybe enjoy the ride! Hope you don't hit your head!");
        } else {
            console.log("You are tall enough, but you don’t have enough tickets. Go spend more money for me!");
        }
    } else {
        console.log("You are not tall enough to ride. That growthspurt is coming soon");
    }
} else {
    console.log("Going to the food stand! A man's gotta eat!");

    if (foodInStock) {
        if (money >= 10) {
            money -= 10;
            console.log("Food is in stock and you have enough money. Enjoy your meal and the mystery meat!");
        } else {
            console.log("Food is available, but you don't have enough money. Spend more money please!");
        }
    } else {
        console.log("Sorry, the food is out of stock. Someone ate all the food, definitely not buisness problems.");
    }
}

console.log(`Remaining Tickets: ${tickets}, Height: ${height} inches, Money Left: $${money}`);

```


    <IPython.core.display.Javascript object>

