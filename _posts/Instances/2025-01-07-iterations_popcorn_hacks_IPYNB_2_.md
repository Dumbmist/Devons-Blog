---
comments: True
layout: post
title: Iteration Popcorn Hacks
description: Iterations Popcorn Hacks
permalink: /csse/javascript/fundamentals/iteration/Popcorn_Hacks
categories: ['CSSE JavaScript Fundamentals']
author: Andrew Ge, Ishan Shrivastava, Pratheep Natarajan, and Ruhaan Bansal
---

# Popcorn Hacks on Iterations in JavaScript

##### Instructions:
##### Complete the exercises below in JavaScript.
##### You can run and test your code in a JavaScript environment.

### Exercise 1: Counting with a For Loop
##### Write a JavaScript for loop that prints all numbers from 1 to 10.

##### Example:
##### Output:
##### 1
##### 2
##### 3
##### ...
##### 9 
##### 10 


```python
%%js
for (let count = 1; count < 11; count++) {
    console.log(count);
}
```


    <IPython.core.display.Javascript object>


### Exercise 2: Sum of Numbers
##### Write a for loop in JavaScript to calculate the sum of all numbers from 1 to n using a loop.

##### Example:
##### Input: 5
##### Output: 15 (because 1 + 2 + 3 + 4 + 5 = 15)



```python
%%js
let n = 5; 
let sum = 0;

for (let i = 1; i <= n; i++) {
  sum += i;
}

console.log(sum); 

```


    <IPython.core.display.Javascript object>


### Exercise 3: Looping through Arrays
##### Write a JavaScript program to iterate through an array of names and print each name.


```python
%%js
const colors = ['bandrew','boohan','brattheep','bortenson','black', 'racksht j', 'hangry geey'];

for (let i = 0; i < colors.length; i++){
    console.log(colors[i]); 
}
```


```python
%%js
const colors = ['bandrew','boohan','brattheep','bortenson','black', 'backsht j', 'hangry geey'];

for (let color of colors) { 
    console.log(color); 
}
```


    <IPython.core.display.Javascript object>

