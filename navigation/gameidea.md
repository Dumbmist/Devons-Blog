---
layout: post
title: GameIdea
course: gameidea
menu: nav/home.html
---

### My CSSE Journey PT.1

##### By: Devon Mistry
---

### 1) My Take-aways

This is not going to be some flowery essay or some detailed response because this is CSSE, and what do we do "code, code, code". So here are my main 5 takeaways:
-  1) Both the difficulty of and how to set up a blog, connect a github repository to vscode, and the steps along the way to make everything function. 
    - This occured within the first few weeks of school and was very, very hard  - even with the detailed path given to us ( almost as hard as getting a 1 in this class, ha ha ha...)
- 2) How to "code" in markdown, all of the functions in markdown, and how to apply it to a real life example (our blogs)
    - Code below
- 3) How to create a collaborative github repository, how to make a pull request, what gitpull is, and the difficulties of merging files/ multiple people working on one file.
    - Through the lesson group project I collaborated with my teamates and learned how to perform the actions above.
- 4) These lessons, both from my own and the other classmates information, I learned many the fundamentals and basics of code - from for loops to arrays - and these helped me (along with prior knowledge) helped with my RPG game and it's creation
- 5) The rpg game was like an accumulation of all the knowledge I had learned throughout the unit but applying it to an object based game. The clear object combined with the knowledge I had learned to produce a product that both went beyond and delivered on the planning guide.
- #### Honorable Mention: Snake Game
    - This was definitely the most fun I had the entire unit, I was deeply invested in creating new code to produce a product that I was happy with and was fun to play (both in difficulty and gamefunctions).
    - This allowed me to win the style compitions, due to my additions of a maze that randomely generates each round, a golden apple that gives the snake a speed boost, a color changing snake, and more.

Function | "#" | "<br>" | "-" | "|" |
Purpose  | changes the text size and makes it bold - more #'s and the smaller the big text gets| line break | bullet points | create a table - like this one |


### 2) RPG Game Tinkers

In the Rpg game there was many adaptations of the code that I made, I will mention the most prominent and importnant ones - but the small details and code in my mind are the most important, maybe thats why without them the code can't function.
- Keys
    - I created an item file with an inventory and data file to go along with this. This allowed me to produce an item which the player can pick up by pressing the e key and it will be added to their inventory, both in local storage and in game
- Keyslot
    - This was my endgame feature. The idea behind in was that the player would insert a key into it and that would both remove a key from the players inventory and fill the keyslot. Once all keyslots were filled the game would end. This was the hardest part of the rpg game by far as the coding took so many intricate details, additional code, checks, debugging, and more. But I really wanted it to work and after a whole weekend of work nonstop I finally figured it out. Only to have bugs to fix.
- Victory Screen
    - The victory screen itself is nothing fancy, a black background with white text, but this was to polish up the game and make it so that the game felt complete and had an objective. Rather than filling the keyslots and sitting there with a complete game and nothing to do. This provided a final step for completion that both allowed for playing again and the work in progress minigame buttons.
- Honorable mentions: 
    - movement fixes
    - work in progress background collision/interactability
    - the pick up function itself (with the e key)

    
### 3) Break Down of Tinkers

<div class="image-gallery"> 
    <img src="https://i.imgur.com/aKZFrTm.jpeg" alt="Chart">
</div>

#### First breakdown: Keys (Using comments)

``` javascript
function updateInventory() {
    const inventory = document.getElementById("inventory"); // Get the inventory element from the HTML
    if (!inventory) return; // Exit if the inventory element doesn't exist (prevents errors)

    inventory.innerHTML = ""; // Clears old inventory items before updating

    inventoryItems.forEach(item => {
        const slot = document.createElement("div"); // Create a new inventory slot for each item
        slot.className = "inventory-slot"; // Assign a class for styling

        const img = document.createElement("img"); // Create an image element to represent the item
        img.src = imagePath + itemImages[item] || imagePath + "/assets/images/default.png"; // Set item image, with a default fallback
        img.alt = item; // Set alternative text for accessibility
        img.style.width = "40px"; // Set the image width
        img.style.height = "40px"; // Set the image height

        slot.appendChild(img); // Add the image to the inventory slot
        inventory.appendChild(slot); // Add the slot to the inventory display
    });
}
```
<br>

``` javascript
export function addItemToInventory(itemName) { //exported so it can be used in other code files
    if (inventoryItems.length < 8) { // Limit inventory slots at 8
        inventoryItems.push(itemName);
        localStorage.setItem("inventoryItems", JSON.stringify(inventoryItems)); //local storage to showcase how many items the player has
    } else {
        alert("Inventory full! NO MORE KEYS"); //when there are 8 items
    }
    updateInventory();
}
```
<br>

``` javascript
setPlayerItem() { //this code is to change a npc's code ater they have collected two keys
    this.itemsCollected++;
    addItemToInventory("spoon");
    
    if (this.itemsCollected === 2) { //two keys requirement
        const questGiver = GameEnv.gameObjects.find(obj => obj.canvas?.id === 'Questgiver');
        if (questGiver) {
            if (this.keys == 0) {

                questGiver.spriteData.greeting = "Now you have collected the keys, go to one of the rare keyslots and press q to give them the key!";
                console.clear(); 
            } else {
                questGiver.spriteData.greeting = "You already have the key. Use it to escape!"; //scrapped idea that was replaced by keyslot
                this.displayStatus();
            }
        }
    } else {
        this.displayStatus();
    }
}
```
<br>

``` javascript
// This code calls upon the functions ive created in inventory.js to make the basic item/key functions occur.
removePlayerItem(item){
    this.itemsCollected--;
    removeItemFromInventory(item);
}

getPlayerItem() {
    return this.itemsCollected;
}

addKey() {
    this.keys++;
    addItemToInventory("key");
}
```

#### Second breakdown: KeySlot (the final boss)

``` javascript
addKey() { //Handles the add key to the keyslot feature
    if (this.isFilled) { // this.isFilled checks whether or not the keyslot is filled/ has 1 key (initially set to false)
        console.log("KeySlot already filled!");
        return false;
    }
    
    const inventoryItems = JSON.parse(localStorage.getItem("inventoryItems") || "[]");
    const hasKey = inventoryItems.includes("spoon"); //checks to make sure the player has a key in their inventory - bug fix to prevent interaction without a key
    
    if (hasKey) {
        inventoryItems.splice(inventoryItems.indexOf("spoon"), 1); // makes player put in 1 key
        localStorage.setItem("inventoryItems", JSON.stringify(inventoryItems)); // local storage display of key insertion
        removeItemFromInventory("spoon"); //removes key from in-game inventory
        this.isFilled = true; // changes boolean to stimulate filling the keyslot
        console.log("KeySlot filled!");
        return true;
    }
    
    console.log("No key in inventory!"); //else, it returns this
    return false;
} 
```
<br>

``` javascript
checkVictoryCondition() {
    if (GameEnv.victoryAchieved) return; // Stop checking if victory is already achieved to avoid redundant checks.

    // Get all KeySlot objects from the game's list of objects.
    const keyslots = GameEnv.gameObjects.filter(obj => obj instanceof KeySlot); 

    // Count how many of these KeySlot objects are filled.
    const filledKeyslots = keyslots.filter(slot => slot.isFilled).length;

    // Log the number of filled slots to the console for debugging.
    console.log(`Filled keyslots: ${filledKeyslots}/${keyslots.length}`);

    // Check if all keyslots are filled and if there is more than one keyslot.
    if (filledKeyslots === keyslots.length && keyslots.length > 1) {
        GameEnv.victoryAchieved = true; // Mark the game as won.
        GameEnv.paused = true; // Pause the game to stop further actions - bug fix of consitant updates breaking victory screen
        this.showVictoryScreen(); // Display the victory screen.
    }
}
```
<br>

``` javascript
handleKeyDown(event) {
    // Debug - Log the key that was pressed
    console.log(`Key pressed: ${event.key}`);
    
    if (event.key === 'q') { // Check if the 'Q' key was pressed
        console.log("Q key pressed - checking for player collision");
        
        // Check if the player is colliding with a keyslot
        if (this.collidedPlayer) {
            console.log("Player is in range to use key");
            const success = this.addKey(); // Attempt to add a key to the keyslot
            
            if (!success && !this.isFilled) {
                // If adding the key fails and the slot isn't already filled,
                // show a message to the player that they need a key
                this.showMessage("You need a key to unlock this!");
            }
            
            return; // Stop further execution
        } else {
            console.log("No player in range to interact with keyslot");
        }
    }
}
```

#### third breakdown: Victory Screen

``` javascript
showVictoryScreen() {
    // Create the victory screen container
    const victoryScreen = document.createElement('div');
    Object.assign(victoryScreen.style, {
        position: 'fixed', // Keeps the victory screen in place
        top: '0',
        left: '0',
        width: '100vw', // Full-screen
        height: '100vh', // Full-screen 
        backgroundColor: 'black', 
        color: 'green', 
        display: 'flex',
        flexDirection: 'column', // Stack elements vertically
        justifyContent: 'center', // Center items vertically
        alignItems: 'center', // Center items horizontally
        zIndex: '1000', // Ensures it appears above other elements
        fontSize: '3rem', // Sets text size
    });

    // Create and style the victory message
    const victoryText = document.createElement('h1');
    victoryText.textContent = 'VICTORY!';
    victoryText.style.marginBottom = '2rem'; // Spacing

    // Create and style description of the victory
    const victoryDesc = document.createElement('p');
    victoryDesc.textContent = 'You have escaped the forest and saved ratGPT from the chest!';

    // Create the restart button
    const restartButton = document.createElement('button');
    Object.assign(restartButton.style, {
        marginTop: '2rem',
        padding: '1rem 2rem',
        fontSize: '1.2rem',
        cursor: 'pointer',
    });
    restartButton.textContent = 'Play Again';
    restartButton.onclick = () => location.reload(); // Reloads the page to restart the game

    // Create the Pong game button - minigame work in progress
    const PongButton = document.createElement('button');
    Object.assign(PongButton.style, {
        marginTop: '2rem',
        padding: '1rem 2rem',
        fontSize: '1.2rem',
        cursor: 'pointer',
    });
    PongButton.textContent = 'Pong Game';
    PongButton.onclick = () => {
        window.location.href = 'pong.html'; // Redirects to the Pong game - not currently functioning
    };

    // Create the Snake game button
    const SnakeButton = document.createElement('button');
    Object.assign(SnakeButton.style, {
        marginTop: '2rem',
        padding: '1rem 2rem',
        fontSize: '1.2rem',
        cursor: 'pointer',
    });
    SnakeButton.textContent = 'Snake Remix';
    SnakeButton.onclick = () => {
        window.location.href = 'snake.html'; // Redirects to the Snake game - not currently functioning
    };

    // Add all elements to the victory screen
    victoryScreen.append(victoryText, victoryDesc, restartButton, PongButton, SnakeButton);
    document.body.appendChild(victoryScreen); // Add the victory screen to the page

    // Clear any existing timeout for victory screen (if applicable)
    clearTimeout(this.victoryScreenTimeout);
};
```
<br>

``` javascript 
update() {
    // Update begins by drawing the object
    this.draw();
    
    // Check for collisions with players
    this.checkAllPlayerCollisions();
    
    if (GameEnv.victoryAchieved) return; // bug fix - prevents the update spam of this.checkVictoryConditon which before would prevent the victory screen from loading

    this.checkVictoryCondition(); // calls on the function to allow this.isFilled to run and to check for it the game is won
    
    // Visual indicator for collision - debugging
    if (GameEnv.debugging && this.collidedPlayer) {
        this.ctx.strokeStyle = 'red';
        this.ctx.lineWidth = 2;
        this.ctx.strokeRect(0, 0, this.canvas.width, this.canvas.height);
    }
```

### 4) Night at the Museum feedback and performance

### 5) Uncharted territory

This will discuss the bullet points that surround point 5

1) Intrest. Evan and West's project was really intresting, considering their impressive game design and role as former members of our lesson group. They are intelligent members and consitantly checked up on what they were doing and how they did some of their stuff to learn and improve my game. Such as movement fixes which Evan taught me why the code was faulty and how to fix it. During N@TM I even left an issue on their blog to both congradulate and help them in the future.
2) This section was already beggining when my mind went off into the whirlwind of possibilities this game could have. Focusing on the minigames as the next steps into CSSE 2 as I have the code for them and just need to set them up in the game, possibly as npcs which direct them to the page instead of just buttons on the victory screen. Additionally, graphics can be cleaned up and the background can be custom made to suit our game needs even better as right now dora is walking on trees.
3) I know I am very far from a complete coder, but I have learned a lot, both in this class and outside which has helped ease me into this class and allow me to succeed by implementing the basics into my code. I know I am good at coming up with game ideas and new ways to improve gameplay, however managing the small niches and debugging is far from my strong suit. Leaving me to sometimes use our trusty friends rachit and chatGPT.
4) This project went really well. Me and Nikhil worked hard together with little procrastination. We solved our issues together and never got caught up on struggling on the same thing. We executed our plans in the planning document and even went beyond to add more features.

---

#### The moment of truth...
The moral dilema of choosing our self-grade! If we give ourselves a hundred, we will seem like know it alls, but we did do everything...

- I would honestly give myself a 4 6/7 or a 5, I believe that I completed everything in the slack message during this jupityr notebook retrospective and was truly invested in my game. I loved spending time creating an actual game, something you think only adults can do and to see it work and be complete with a game objective was pure joy. I covered all 5 bullet points extensively and fully understood everything we learned, and will gladly give more explanation if this wasn't apparent. The 1/7 missing is maybe because I wasn't a full 24 hours ahead with my slack message, but other than that, I met and went above and beyond in all catagories - winning style compitions for the snake game, getting a rare 0.93, and more. 