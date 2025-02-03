---
comments: True
layout: post
title: Iteration Homework
description: Iterations HW
permalink: /csse/javascript/fundamentals/iteration/hw
categories: ['CSSE JavaScript Fundamentals']
author: Andrew Ge, Ishan Shrivastava, Pratheep Natarajan, and Ruhaan Bansal
---

### Exercise 1: Multiplication Table
##### Write a JavaScript program to print the multiplication table for a given number.

##### Example:
##### Input: 3
##### Output:
##### 3 x 1 = 3
##### 3 x 2 = 6
##### ...
##### 3 x 10 = 30


```python
%%js
function multiplicationTable(number) { //function to input from numbers 1-10
    
    for (let i = 1; i <= 10; i++) {
        
        console.log(`${number} x ${i} = ${number * i}`);
    }
}
multiplicationTable(3); //put number to multiply in place of 3
```


    <IPython.core.display.Javascript object>


### Exercise 2: Nested Loops
##### Write a JavaScript program using nested loops to generate the following pattern:

##### Output:
##### 0
##### 00
##### 000
##### 0000
##### 00000


```python
%%js 

// controls rows (runs 5 times)
for (let i = 1; i <= 5; i++) {
    
    let Ruhaan = ""; //  empty string

    // nested loop to add 0's
    for (let x = 1; x <= i; x++) {
        Ruhaan += "0"; 
    }
    
    console.log(Ruhaan); // Print 
}

```


    <IPython.core.display.Javascript object>




### Challenge Exercise: Prime Numbers
##### Write a JavaScript program to print all prime numbers between 1 and 50.

Explanation in the comments - get it? Because of those shorts you see? That surely deserves extra credit! Ruhaan, I know everything is ratgpt'd - show this to Ruhaan. My explanation is great!


```python

function isPrime(num) {  // Function to check if a number is prime
    if (num <= 1) return false; // Prime numbers greater than 1

    // Loop from 2 to the sqr (sqr = square root) of num to check for factors
    for (let i = 2; i <= Math.sqrt(num); i++) {  
        if (num % i === 0) return false; // Prime numbers cannot be divisible by "i"
    }
    return true; // If no divisions occured, it's prime
}


for (let i = 1; i <= 50; i++) {  // Loop 1-50 and print prime ones
    if (isPrime(i)) {  // isPrime function from before to check number
        console.log(i); // Print the prime number
    } //runs the actual thing
}

```


    <IPython.core.display.Javascript object>


Or the cheesy way, done by using an array and for loop to print out all the prime numbers below 50 simply by cycling through the array.


```python
%%js
const primeNumbersBelow50 = ['2', '3', '5', '7', '11', '13', '17', '19', '23', '29', '31', '37', '41', '43', '47'];

for (let i = 0; i < primeNumbersBelow50.length; i++){
    console.log(primeNumbersBelow50[i]); 
}
```


    <IPython.core.display.Javascript object>


# End of Homework
