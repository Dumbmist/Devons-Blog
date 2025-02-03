---
layout: post
title: Homework
description: Homework for classes and methods lessons.
type: issues
comments: True
---

## Homework 

# JavaScript Classes and Methods - Interactive Homework
In this notebook, you will learn about classes and methods in JavaScript. After the lesson, complete the tasks by editing the code cells.

### What are Classes and Methods?
- **Class**: A blueprint for creating objects with properties and methods.
- **Method**: A function inside a class that defines an object's behavior.



## Example: Class for food

Below is an example of a JavaScript class for creating different foods. The class has:
1. A **constructor** to initialize properties (brand and model).
2. Two **methods** (`displayInfo` and `start`) to define behaviors.



```python
%%js
// Example: A Class for Cars
class Car {
  constructor(brand, model) {
    this.brand = brand; // Property
    this.model = model; // Property
  }

  displayInfo() {
    console.log(`This car is a ${this.brand} ${this.model}.`);
  }

  start() {
    console.log(`${this.brand} ${this.model} is starting...`);
  }
}

// Create an instance of the class
const myCar = new Car("Tesla", "Model S");
myCar.displayInfo();
myCar.start();

```


    <IPython.core.display.Javascript object>


# What to Do
I want you to look through the code and complete the missing pieces and write new code lines to make the game funtion.
this is basically a `gambling simulator` but with food.
I have porvided "hints" in the code.
### if you want a challenge dont read the <span style="color: green;">GREEN</span>
the green next to code it the real hint if you look at the // above there is description of what you need to do
starting from a little above the bottom at the fill in the blank or top is the easiest the `middle is the hardest`.
## Grab item
I want you to Create a grab item function that will reference the class to randomly pick a food item
12:21



```python
%%js
class FridgeGame {
    constructor() {
      // Array of items in the fridge with their scores
      this.fridgeItems = [
        { name: "Piece of pizza", score: 10 },
        { name: "Half-empty soda can", score: 4 },
        { name: "Old sandwich", score: 3 },
        { name: "Fresh apple", score: 7 },
        { name: "Stale muffin", score: 5 },
        { name: "Block of cheese", score: 8 },
        { name: "Bag of carrots", score: 6 },
        { name: "Yogurt", score: 9 },
        { name: "Expired milk", score: 2 },
        { name: "Leftover spaghetti", score: 8 }
      ];
    }
  
    // Method to pick a random item from the fridge
    grabItem() {
      const randomIndex = Math.floor(Math.random() * this.fridgeItems.length);
      return this.fridgeItems[randomIndex];
    }
  
    // Method to classify the find based on its score
    classifyFind(score) {
      if (score >= 8) {
        return "Great, Just great! A maybe tasty find!";
      } else if (score >= 5) {
        return "Eh, could be better.";
      } else {
        return "Skibidi! That's a bad one!";
      }
    }
  
    // Reference method to start the game
    play() {
      console.log("Welcome to the Fridge Game!");
      const item = this.grabItem();
      console.log(`You found: ${item.name}`);
      
      // Get feedback based on the item's score
      const feedback = this.classifyFind(item.score);
      console.log(`It is ${feedback} Score: ${item.score}`);
    }
  }
  
  // Create an instance of the game
  const fridgeGame = new FridgeGame();
  
  // Start the game by calling the play method
  fridgeGame.play();
  

```


    <IPython.core.display.Javascript object>

