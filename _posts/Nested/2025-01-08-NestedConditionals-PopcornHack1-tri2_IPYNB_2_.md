---
layout: post
title: Nested Conditionals, Popcorn Hack One
description: First popcorn hack for nested conditonals
type: issues
comments: True
---

### Popcorn Hack 1

This code has the option to let the player go on a ride of their choosing, and either lets them go on the ride or does not let them go on the ride based on their amount of tickets that they have. Try adding some code that makes it so that the code also takes into account the height of the person trying to ride the ride and have it be another constraint that determines whether or not the person goes on a ride.


```python
%%html
<!-- HTML output div -->
<div id="message"></div>  
<script>
    function runWhenDOMLoaded() {
        let ticketAmount = 60; // Makes the ticket amount be 60, make another variable for height
        let ride = "Ferris Wheel"; // sets the ride that the person wants to ride on

        const messageElement = document.getElementById("message");

        function displayMessage(message) {
            console.log(message); // Log to console
            messageElement.textContent = message; // Display on the webpage
        }

        function enoughTickets(a) {//Add another parameter for height (use a comma and then a letter or word), maybe change the name of the parameter
            if (ticketAmount >= a) {
                displayMessage("You have enough tickets! Yay! :D");//make another if else statement inside of this to check for height
            } else {
                displayMessage("You don't have enough tickets... :(");
            }
        }

        if (ride === "Roller Coaster") {
            enoughTickets(60); //Nests the function and the conditionals
        } else if (ride === "Ferris Wheel") {
            enoughTickets(40);
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
        let ticketAmount = 60; // Makes the ticket amount be 60, make another variable for height
        let ride = "Ferris Wheel"; // sets the ride that the person wants to ride on

        const messageElement = document.getElementById("message");

        function displayMessage(message) {
            console.log(message); // Log to console
            messageElement.textContent = message; // Display on the webpage
        }

        function enoughTickets(a) {//Add another parameter for height (use a comma and then a letter or word), maybe change the name of the parameter
            if (ticketAmount >= a) {
                displayMessage("You have enough tickets! Yay! :D");//make another if else statement inside of this to check for height
            } else {
                displayMessage("You don't have enough tickets... :(");
            }
        }

        if (ride === "Roller Coaster") {
            enoughTickets(60); //Nests the function and the conditionals
        } else if (ride === "Ferris Wheel") {
            enoughTickets(40);
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
My code is below - your code with the edits. I added comments for explanation since elise said so. Bye!
```


```python
%%html
<!-- HTML output div -->
<div id="message"></div>
<script>
    function runWhenDOMLoaded() {
        let ticketAmount = 60; // Ticket amount
        let ride = "Ferris Wheel"; // Chosen ride
        let height = 85; // Height of the rider in inches

        const messageElement = document.getElementById("message");

        function displayMessage(message) {
            console.log(message); // Log to console
            messageElement.textContent = message; // Display on the webpage
        }

        function enoughTickets(ticketCost, riderHeight) {
            if (ticketAmount >= ticketCost) {
                if (riderHeight > 80) { // Too tall to ride
                    displayMessage("Sorry, you're too tall to go on this ride. Youre going to hit your head endlessly like andrew. :(");
                } else {
                    displayMessage("You have enough tickets! Enjoy the ride! :D");
                }
            } else {
                displayMessage("You don't have enough tickets... :(");
            }
        }

        if (ride === "Roller Coaster") {
            enoughTickets(60, height);
        } else if (ride === "Ferris Wheel") {
            enoughTickets(40, height);
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
        let ticketAmount = 60; // Ticket amount
        let ride = "Ferris Wheel"; // Chosen ride
        let height = 85; // Height of the rider in inches

        const messageElement = document.getElementById("message");

        function displayMessage(message) {
            console.log(message); // Log to console
            messageElement.textContent = message; // Display on the webpage
        }

        function enoughTickets(ticketCost, riderHeight) {
            if (ticketAmount >= ticketCost) {
                if (riderHeight > 80) { // Too tall to ride
                    displayMessage("Sorry, you're too tall to go on this ride. Youre going to hit your head endlessly like andrew. :(");
                } else {
                    displayMessage("You have enough tickets! Enjoy the ride! :D");
                }
            } else {
                displayMessage("You don't have enough tickets... :(");
            }
        }

        if (ride === "Roller Coaster") {
            enoughTickets(60, height);
        } else if (ride === "Ferris Wheel") {
            enoughTickets(40, height);
        }    
    }

    // Ensure the function runs only after the page loads
    if (document.readyState === "loading") {
        document.addEventListener("DOMContentLoaded", runWhenDOMLoaded);
    } else {
        runWhenDOMLoaded();
    }
</script>


