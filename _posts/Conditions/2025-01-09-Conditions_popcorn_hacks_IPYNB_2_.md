---
layout: post
title: Popcorn Hacks, Conditionals
description: First popcorn hack for  conditonals
type: issues
comments: True
permalink: /csse/javascript/fundamentals/conditionals/popcorn
---

# Popcorn Hacks!
You're at the mall with your friends, and head into the Build-A-Bear store. Use conditionals to decide what kind of bear you want with different accessories! The employee comes up to you and explains the steps. She states...

"Choose Me: Pick that special furry friend — from a silly superhero to a sporty mascot and a cheerleading bunny to a snuggly teddy bear.
Hear Me: Add a special sound effect to your furry friend.
Stuff Me: Customize your creation with sounds, scents, stuffing and, of course, our iconic special heart that holds your love and wishes.
Hug Me: Give your furry friend its first hug to make sure it’s stuffed just right.
Dress Me: Turn up the fun with outfits and extras!
Name Me: It’s official once your creation has a birth certificate of its bear-y own!"

### Hack 1: Simple If-Statement
Create a variable based on what kind of stuffed animal you want.


```python
%%js
let bearType = "monkey"; //Choose what kind of bear you want: Teddy or Unicorn (Example: let bearType = "Teddyy")

if (bearType === "monkey") { //Put the same bear type from above into this line
    console.log("You picked a snuggly monkey bear!");
}
```


    <IPython.core.display.Javascript object>


### Hack 2: If-Else Statement
Add a sound to the bear based on the type chosen.


```python
%%js
let bearType = "monkey"; //Put the same bear type as before.

if (bearType ==="monkey") {
    console.log("Your monkey snores...");
} else {
    console.log("Your Unicorn neighs loud... and fell off into extinction")
}

```


    <IPython.core.display.Javascript object>


### Hack 3: Else-If Statement
Choose the stuffing type using an If-Else-If statement


```python
%%js
let stuffingType = "rocks"; //Choose a stuffing: Fluffy, Firm, or Squishy

if (stuffingType === "Fluffy") {
    console.log("Your bear will be extra soft and fluffy!");
} else if (stuffingType === "rocks") {
    console.log ("Your bear will have a firm, sturdy feel and hurt when dropped on your head");
} else {
    console.log("Your bear will be nice and squishy!");
}
```


    <IPython.core.display.Javascript object>


### Hack 4: Switch Statement
Use a switch statement to pick a bear outfit


```python
%%js
let bearOutfit = "monkey"; // Choose an outfit: "Superhero", "Cheerleader", "Pirate", "Princess"

switch (bearOutfit) {
    case "Superhero":
        console.log("Your bear is ready to save the day in a Superhero costume!");
        break;
    case "Cheerleader":
        console.log("Your bear will cheer with its Cheerleader outfit!");
        break;
    case "Pirate":
        console.log("Ahoy! Your bear is ready to sail in a Pirate costume!");
        break;
    case "monkey":
        console.log("Ooh ooh ahh ahh. I want large bananas. Tickle my monkey feet tarzan.");
        break;
    default:
        console.log("Your bear is ready for a royal adventure in a Princess outfit!");
}

```


    <IPython.core.display.Javascript object>


### Hack 5: Complete Build-A-Bear Experience
Combine all conditionals to create new types of bears, stuffings, and outfits in a single code cell!


```python
%%js
let bearType = "monkey"; //Make a type of bear!
let stuffingType = "rocks"; //Choose a type of stuffing!
let bearOutfit = "diddy monkey"; //Create your own outfit!

// Step 1: Choose Me
if (bearType === "monkey") { //Choose a bear type
    console.log("You have selected the skinless monkey. It is just fake skin in a monkey shape."); //Create a console message for the specified bear type
} else if (bearType === "Diddy") {
    console.log("You have chosen the diddy bear.");
} else {
    console.log("You have selected the generic teddy bear, a bit... boring");
}

//Repeat these steps. When finished, you should be able to choose your own type of bear, stuffing, and outfit within a single code cell. Be creative and have fun!!!
// Step 2: Hear Me
if (bearType === "skibidi toilet") {
    console.log("You have selected the skibidi toilet bear. Your child may get brainrot.");
} else {
    console.log("You have selected Yasna cuz she taught this stuff. You need to get off block blast.");
}

// Step 3: Stuff Me
if (stuffingType === "rocks") {
    console.log("Have fun with your rock stuffed bears. They may tickle a bit.");
} else if (stuffingType === "Popcorn") {
    console.log("You can eat your stuffing or crush it up to have a limp bear");
} else {
    console.log("You have been given fluffy stuffing, it is fluffy and nice for your (lame) awesome person.");
}

// Step 4: Dress Me
switch (bearOutfit) {
    case "diddy monkey":
        console.log("your bear holds baby oil and has a smaller bear friend to have playdates with.");
        break;
    case "generic school boy":
        console.log("You got baggy pants and a hoodie, plus you act tuff but aren't (cough cough...person)");
        break;
    case "Rachit":
        console.log("you have glasses and need to be nerdy as well as a chill guy");
        break;
    default:
        console.log("You have chosen no outfit, a shame because of the many amazing choices.");
}

```


    <IPython.core.display.Javascript object>

