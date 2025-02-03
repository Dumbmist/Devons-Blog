---
layout: post
title: Boolean Popcorn Hacks
description: Popcorn Hacks
categories: ['Foundation']
courses: {'csse': {'week': 1}, 'csp': {'week': 1}, 'csa': {'week': 1}}
comments: True
sticky_rank: 1
---

# Popcorn Hacks

# Exercise 1

Create a variable that holds a true or false value. Print a message that says "This is true!" if the value is true and "This is false!" if the value is false.


```python
%%js 

let Shayan = false;  // Change this to false to test the other case

if (Shayan === "true") {
    console.log("THis is true")
} else {
    console.log("THis is false. No durrr cuz you put false.")
}
```


    <IPython.core.display.Javascript object>


# Exercise 2

Write a program that checks if both conditions are true: the weather is nice (true) and it’s a weekend (true). Print "Go outside!" if both are true, and "Stay inside!" otherwise.


```python
%%js 

let isNiceWeather = false;  // Change to false to test the other case

if (isNiceWeather === true) {
    console.log("Go outside Shayan")
} else {
    console.log("The weather outside is frightful, but the fire is so delightful if we have no place to go let it snow let it snow. Stay inside")
}

let isWeekend = false;  // Change to false to test the other case

if (isWeekend === true) {
    console.log("No more school work")
} else {
    console.log("Go do your homework beta")
}


```


    <IPython.core.display.Javascript object>


# Exercise 3

Write a program that prints "Time to go to the beach!" if it's either sunny or the weekend. Use the OR (||) operator.


```python
%%js 

let isSunny = true;  // Change to false to test the other case
let isWeekend = false;  // Change to true to test the other case

if (isSunny === true) {
    console.log("Time to go to the beach")
} else {
    console.log("Stay inside")
}

if (isWeekend === true) {
    console.log("Time to go to the beach")
} else {
    console.log("Stay inside")
}

```


    <IPython.core.display.Javascript object>


# Exercise 4

Write a program that prints "Not sunny today" if isSunny is false, and "It's sunny!" if isSunny is true. Use the NOT (!) operator to invert the value of isSunny.


```python
%%js 

let isSunny = false;  // Change to true to test the other case

if (isSunny === true) {
    console.log("It's sunny")
} else {
    console.log("Not sunny today")
}
```


    <IPython.core.display.Javascript object>


# Exercise 5

Create a program that checks if a user is both logged in (true) and has admin rights (true). Print "Access granted!" if both are true, and "Access denied!" if either is false.


```python
%%js 

let isLoggedIn = true;  // Change to false to test the other case
let isAdmin = true;     // Change to false to test the other case

if (isLoggedIn && isAdmin) {
    console.log("Access granted!");
} else {
    console.log("Access denied!");
}

```


    <IPython.core.display.Javascript object>


# Exercise 6

Use a ternary operator to decide whether a user is allowed access based on their age. If the age is 18 or above, print "You are allowed access." If below 18, print "Sorry, you are too young."


```python
%%js

let age = 16;  // Change this value to test different cases

let accessMessage = age >= 18 ? "You are allowed access." : "Sorry, you are too young. Go get older";

console.log(accessMessage); 


```

# Exercise 7

Write a program that checks if a user is both a VIP (true) and has a VIP ticket (true). If both conditions are true, print "VIP Access granted!" Otherwise, print "Access denied!"


```python
%%js 

let isVIP = true;        // Change to false to test the other case
let hasVIPticket = false; // Change to true to test the other case

if (isVIP && hasVIPticket) {
    console.log("VIP Access granted!");
} else {
    console.log("Access denied!");
}

```


    <IPython.core.display.Javascript object>

