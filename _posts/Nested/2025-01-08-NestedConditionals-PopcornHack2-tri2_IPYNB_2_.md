---
layout: post
title: Nested Conditionals, Popcorn Hack Two
description: Second popcorn hack for nested conditionals
type: issues
comments: True
---

### Popcorn Hack 2

This code uses boolean to check if a person has the unlimited amusement food card. If they do, then they are allowed to buy any food that they want for free. Add code for another type of food and take into account whether or not the food is in stock.


```python
%%html
<!-- HTML output div -->
<div id="message"></div>
<script>
    function runWhenDOMLoaded() {
        let foodCard = true;
        let money = 1;
        let foodChoice = "cotton candy";
        //You probably want to add some boolean variables here to check if the food is in stock or not... 
        //Make sure to add another food! Get creative!

        const messageElement = document.getElementById("message");

        function displayMessage(message) {
            console.log(message); // Log to console
            messageElement.textContent = message; // Display on the webpage
        }

        if (foodCard === true) {
            if (foodChoice === "popcorn") {//Checks the food choice
                    displayMessage("Yum! The popcorn is tasty!");
            } else if (foodChoice === "cotton candy") {
                    displayMessage("Yum! The cotton candy is tasty!");
            }//Use the previous code as examples to help make another food! 
            // Also, make sure to add more nested conditionals inside the if statements above to check if the food is in stock
        } else {
            if (foodChoice === "popcorn") {
                if (money >= 8) { // checks if you have enough money to buy
                    //Add another if statement to check if the food is in stock!
                    displayMessage("Yay! You can buy the popcorn!");
                } else {
                    displayMessage("Oh... you can't buy the popcorn.");
                }
            } else if (foodChoice === "cotton candy") {
                if (money >= 5) {
                    //Add another if statement to check if the food is in stock!
                    displayMessage("Yay! You can buy the cotton candy!");
                } else {
                    displayMessage("Oh... you can't buy the cotton candy.");
                }//Add the other food and make sure to check if it is in stock!
            }
        }
    }

    // Ensure the function runs only after the page loads
    if (document.readyState === "loading") {
        document.addEventListener("DOMContentLoaded", runWhenDOMLoaded);
    } else {
        runWhenDOMLoaded();
    }
</script>

```


<!-- HTML output div -->
<div id="message"></div>
<script>
    function runWhenDOMLoaded() {
        let foodCard = true;
        let money = 1;
        let foodChoice = "cotton candy";
        //You probably want to add some boolean variables here to check if the food is in stock or not... 
        //Make sure to add another food! Get creative!

        const messageElement = document.getElementById("message");

        function displayMessage(message) {
            console.log(message); // Log to console
            messageElement.textContent = message; // Display on the webpage
        }

        if (foodCard === true) {
            if (foodChoice === "popcorn") {//Checks the food choice
                    displayMessage("Yum! The popcorn is tasty!");
            } else if (foodChoice === "cotton candy") {
                    displayMessage("Yum! The cotton candy is tasty!");
            }//Use the previous code as examples to help make another food! 
            // Also, make sure to add more nested conditionals inside the if statements above to check if the food is in stock
        } else {
            if (foodChoice === "popcorn") {
                if (money >= 8) { // checks if you have enough money to buy
                    //Add another if statement to check if the food is in stock!
                    displayMessage("Yay! You can buy the popcorn!");
                } else {
                    displayMessage("Oh... you can't buy the popcorn.");
                }
            } else if (foodChoice === "cotton candy") {
                if (money >= 5) {
                    //Add another if statement to check if the food is in stock!
                    displayMessage("Yay! You can buy the cotton candy!");
                } else {
                    displayMessage("Oh... you can't buy the cotton candy.");
                }//Add the other food and make sure to check if it is in stock!
            }
        }
    }

    // Ensure the function runs only after the page loads
    if (document.readyState === "loading") {
        document.addEventListener("DOMContentLoaded", runWhenDOMLoaded);
    } else {
        runWhenDOMLoaded();
    }
</script>




```python
My code is below - your code with the edits. I added comments for explanation since elise said so.
```


```python
%%html
<!-- HTML output div -->
<div id="message"></div>
<script>
    function runWhenDOMLoaded() {
        let foodCard = true;
        let money = 1;
        let foodChoice = "hot dog"; // New food option 
        let popcornInStock = true;
        let cottonCandyInStock = false;
        let hotDogInStock = true; // New stock variable for hot dog

        const messageElement = document.getElementById("message");

        function displayMessage(message) {
            console.log(message); // Log to console
            messageElement.textContent = message; // Display on the webpage
        }

        if (foodCard === true) {
            if (foodChoice === "popcorn") {
                if (popcornInStock) {
                    displayMessage("Yummy in my tummy! The popcorn is tasty and stale!");
                } else {
                    displayMessage("Sorry, the popcorn is out of stock. Andrew ate the food.");
                }
            } else if (foodChoice === "cotton candy") {
                if (cottonCandyInStock) {
                    displayMessage("Yummy! The cotton candy is tasty!");
                } else {
                    displayMessage("Sorry, the cotton candy is out of stock. You ate all of it.");
                }
            } else if (foodChoice === "hot dog") { // New food option
                if (hotDogInStock) {
                    displayMessage("Glizzy with glitter! The hot dog is delicious!");
                } else {
                    displayMessage("Sorry, the hot dog is out of stock. more points for my grade is needed");
                }
            }
        } else {
            if (foodChoice === "popcorn") {
                if (money >= 8) {
                    if (popcornInStock) {
                        displayMessage("Yay! You can buy the popcorn!");
                    } else {
                        displayMessage("Sorry, the popcorn is out of stock.");
                    }
                } else {
                    displayMessage("Oh... you can't buy the popcorn.");
                }
            } else if (foodChoice === "cotton candy") {
                if (money >= 5) {
                    if (cottonCandyInStock) {
                        displayMessage("Yay! You can buy the cotton candy!");
                    } else {
                        displayMessage("Sorry, the cotton candy is out of stock.");
                    }
                } else {
                    displayMessage("Oh... you can't buy the cotton candy.");
                }
            } else if (foodChoice === "hot dog") { // New food buying logic
                if (money >= 6) {
                    if (hotDogInStock) {
                        displayMessage("Yay! You can buy the hot dog!");
                    } else {
                        displayMessage("Sorry, the hot dog is out of stock.");
                    }
                } else {
                    displayMessage("Oh... you can't buy the hot dog.");
                }
            }
        }
    }

    // Ensure the function runs only after the page loads
    if (document.readyState === "loading") {
        document.addEventListener("DOMContentLoaded", runWhenDOMLoaded);
    } else {
        runWhenDOMLoaded();
    }
</script>

```


<!-- HTML output div -->
<div id="message"></div>
<script>
    function runWhenDOMLoaded() {
        let foodCard = true;
        let money = 1;
        let foodChoice = "hot dog"; // New food option 
        let popcornInStock = true;
        let cottonCandyInStock = false;
        let hotDogInStock = true; // New stock variable for hot dog

        const messageElement = document.getElementById("message");

        function displayMessage(message) {
            console.log(message); // Log to console
            messageElement.textContent = message; // Display on the webpage
        }

        if (foodCard === true) {
            if (foodChoice === "popcorn") {
                if (popcornInStock) {
                    displayMessage("Yummy in my tummy! The popcorn is tasty and stale!");
                } else {
                    displayMessage("Sorry, the popcorn is out of stock. Andrew ate the food.");
                }
            } else if (foodChoice === "cotton candy") {
                if (cottonCandyInStock) {
                    displayMessage("Yummy! The cotton candy is tasty!");
                } else {
                    displayMessage("Sorry, the cotton candy is out of stock. You ate all of it.");
                }
            } else if (foodChoice === "hot dog") { // New food option
                if (hotDogInStock) {
                    displayMessage("Glizzy with glitter! The hot dog is delicious!");
                } else {
                    displayMessage("Sorry, the hot dog is out of stock. more points for my grade is needed");
                }
            }
        } else {
            if (foodChoice === "popcorn") {
                if (money >= 8) {
                    if (popcornInStock) {
                        displayMessage("Yay! You can buy the popcorn!");
                    } else {
                        displayMessage("Sorry, the popcorn is out of stock.");
                    }
                } else {
                    displayMessage("Oh... you can't buy the popcorn.");
                }
            } else if (foodChoice === "cotton candy") {
                if (money >= 5) {
                    if (cottonCandyInStock) {
                        displayMessage("Yay! You can buy the cotton candy!");
                    } else {
                        displayMessage("Sorry, the cotton candy is out of stock.");
                    }
                } else {
                    displayMessage("Oh... you can't buy the cotton candy.");
                }
            } else if (foodChoice === "hot dog") { // New food buying logic
                if (money >= 6) {
                    if (hotDogInStock) {
                        displayMessage("Yay! You can buy the hot dog!");
                    } else {
                        displayMessage("Sorry, the hot dog is out of stock.");
                    }
                } else {
                    displayMessage("Oh... you can't buy the hot dog.");
                }
            }
        }
    }

    // Ensure the function runs only after the page loads
    if (document.readyState === "loading") {
        document.addEventListener("DOMContentLoaded", runWhenDOMLoaded);
    } else {
        runWhenDOMLoaded();
    }
</script>




```python

```
