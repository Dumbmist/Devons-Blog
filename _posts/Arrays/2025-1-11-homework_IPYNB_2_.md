---

---

# Lesson 1 Homework


```python
%%js
//We have an array made for you, but something's off...
let desserts = ["lemon merangue","advaits amazing apple pie","ice cream","chocolate cake","key lime pie","pratheeps purple pie"];

//We need to get rid of the elements labeled delete1 and delete2!
desserts.pop(); //which command gets rid of the last element in the array?
desserts.splice(0, 1); //which command will delete the delete1 element and how do you use it??

//now that that's done... a lemon isn't a dessert unless you're weird... maybe change it to a lemon-themed dessert?
desserts[0] = "lemon merangue lolipop with lemon compote and lovely lemon glaze, topped with abraham lincolns lemon frosting";

//hint for the previous 2 fill-in-the-blanks: the indexing starts at 0

//okay okay, you've proven your skills... now all that's left is to print the list!
console.log(desserts);

```


    <IPython.core.display.Javascript object>


# Lesson 2 Homework - Part 1


```python
%%js
//I want you to create a list of whatever you'd like (integers or strings, it really doesn't matter) and have a repeating element in it.
let menialTaskofHomework = ["Skibidi", "Toilet", "Fanum", "Tax", "Ohio", "Sigma", "Ohio"]; // "Ohio" is repeated

//Ok, now I know this is about arrays, but could you make a for loop to iterate through each element and print the index of them?
for (let i = 0; i < menialTaskofHomework.length; i++) {
    console.log(`Index ${i}: ${menialTaskofHomework[i]}`);
}

//Wait! You remember that repeating element I made you put in your list? Create a separate command outside of the loop to print the index of the last occurring repeated value.
console.log("Last index of 'Ohio':", menialTaskofHomework.lastIndexOf("Ohio"));

```


    <IPython.core.display.Javascript object>


# Lesson 2 Homework - Part 2


```python
%%js
//This is the fairly simple final problem of arrays!

//Create a list here that includes whatever you'd like once again.
let middleTablePeeps = ["Andrew", "Devon", "PPratheep", "Ishaanti om", "Ruhaan", "Evan da Goat"];

//Now, print the length of your list!
console.log("List Length:", middleTablePeeps.length);

//Finally, create a variable to check if a value in your list is included in the list and print that variable you created (it should output true or false)
let isIncluded = middleTablePeeps.includes("Ruhaan");
console.log("Is 'Ruhaan' in the list?", isIncluded);

```


    <IPython.core.display.Javascript object>


You're done with your homework!!
