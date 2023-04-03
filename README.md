# Review: Object Iteration

## Learning Goals

- Iterate over an object using the `for...in` statement
- Build a nested object using literal syntax

## Introduction

In the previous lesson, we practiced accessing information in an object by
directly typing in the needed commands. In the next few lessons, we will learn
how to access information programmatically, by writing code that iterates over
an object, finds the desired information and returns it. We'll start by learning
how to iterate over objects.

## Using `for...in` to Iterate over Objects

In an earlier lesson, we learned how to iterate over an array using `for...of`.
JavaScript has a similar statement, `for...in`, that can be used to iterate over
an object. The usage is similar, but while `for...of` iterates through the
_values_ in an array, `for...of` iterates through the _keys_ in an object:

```js
const worldCapitals = {
    USA: "Washington D.C.",
    Brazil: "Brasilia",
    SouthKorea: "Seoul",
    Iceland: "Reykjavik",
    Ghana: "Accra",
    Netherlands: "Amsterdam",
}

for (const country in worldCapitals) {
    console.log(country:)
}
// =>
// USA
// Brazil
// SouthKorea
// Iceland
// Ghana
// Netherlands
```

If we want to access the values instead, we know how to do that as well:

```js
for (const country in worldCapitals) {
  console.log(worldCapitals.country);
}
```

Will this work?...

If you try running the code above, you'll see that JavaScript returns
`undefined` each time through the loop. Why is that?

Recall from the last lesson that one of the times we **can't** use dot notation
is when we're accessing information dynamically, i.e., when the value of the key
is stored in a variable. In the `for...in` loop above, we've created a variable,
`country`, that stores the name of the current key for each iteration through
the object. When the `console.log` is executed, the JavaScript engine tries to
access the value associated with a key with the literal value "country", but
there is no `country` key in our object.

To fix this, we need to use bracket notation in our loop instead:

```js
for (const country in worldCapitals) {
  console.log(worldCapitals[country]);
}
// =>
// "Washington D.C."
// "Brasilia"
// "Seoul"
// "Reykjavik"
// "Accra"
// "Amsterdam"
```

Success!

To review: in the first time through the loop, JavaScript accesses the first
key, `USA`, and stores it in the variable `country`. In the next line, it
_evaluates_ what's inside the square brackets, i.e., it looks for a variable
with the name `country` and substitutes its value in the brackets, which yields
`worldCapitals["USA"]` or "Washington D.C.".

Over the next couple of lessons, we're going to practice iterating through a
complex nested object to access specific pieces of information. Before we start,
let's use literal syntax to build the object. In other words, we'll literally
type out the object we'll use and assign it to a variable. For example, if we
were to use literal syntax to create the `address` object we've seen in earlier
lessons, it would look like this:

```js
const address = {
  street1: {
    line1: '11 Broadway',
    line2: '2nd Floor',
  }
  city: 'New York',
  state: 'NY',
  zipCode: "10004"
}
```

## Build a Nested Object using Literal Syntax

Create a variable called `gameObject` to contain your object:

```js
const gameObject = {};
```

The top level of the object should have two keys: `"home"`, for the home team,
and `"away"`, for the away team. The values of the `"home"` and `"away"` keys
are objects too:

```js
const gameObject = {
  home: {},
  away: {},
};
```

Continue building out the object, following the guidelines below:

- The `home` and `away` objects have the following keys:
  - `"teamName"`
  - `"colors"`
  - `"players"`
- The `teamName` key points to a string of the team name.
- The `colors` key points to an _array_ of strings that are that team's colors.
- The `players` key points to an object of players whose names (as strings) are
  the keys to an object containing their stats. The values for each player's
  names and their stats can be found in the table below. The stats keys should
  be formatted like this:
  - `"number"`
  - `"shoe"`
  - `"points"`
  - `"rebounds"`
  - `"assists"`
  - `"steals"`
  - `"blocks"`
  - `"slamDunks"`

Use the following data to populate your `gameObject` as outlined above.

Home Team:

- Team name: Brooklyn Nets
- Colors: Black, White
- Players:

|      Stat       |     Info      |     Info     |    Info     |     Info      |    Info     |
| :-------------: | :-----------: | :----------: | :---------: | :-----------: | :---------: |
| **Player Name** | Alan Anderson | Reggie Evans | Brook Lopez | Mason Plumlee | Jason Terry |
|   **Number**    |       0       |      30      |     11      |       1       |     31      |
|    **Shoe**     |      16       |      14      |     17      |      19       |     15      |
|   **Points**    |      22       |      12      |     17      |      26       |     19      |
|  **Rebounds**   |      12       |      12      |     19      |      12       |      2      |
|   **Assists**   |      12       |      12      |     10      |       6       |      2      |
|   **Steals**    |       3       |      12      |      3      |       3       |      4      |
|   **Blocks**    |       1       |      12      |      1      |       8       |     11      |
| **Slam Dunks**  |       1       |      7       |     15      |       5       |      1      |

Away Team:

- Team name: Charlotte Hornets
- Colors: Turquoise, Purple
- Players:

|      Stat       |    Info     |      Info      |     Info     |    Info    |      Info       |
| :-------------: | :---------: | :------------: | :----------: | :--------: | :-------------: |
| **Player Name** | Jeff Adrien | Bismak Biyombo | DeSagna Diop | Ben Gordon | Brendan Haywood |
|   **Number**    |      4      |       0        |      2       |     8      |       33        |
|    **Shoe**     |     18      |       16       |      14      |     15     |       15        |
|   **Points**    |     10      |       12       |      24      |     33     |        6        |
|  **Rebounds**   |      1      |       4        |      12      |     3      |       12        |
|   **Assists**   |      1      |       7        |      12      |     2      |       12        |
|   **Steals**    |      2      |       7        |      4       |     1      |       22        |
|   **Blocks**    |      7      |       15       |      5       |     1      |        5        |
| **Slam Dunks**  |      2      |       10       |      5       |     0      |       12        |

Don't worry to much about catching every typo as you go — this lesson has tests
that we will use to verify that you have everything set up properly.

Once you're done building your object, before moving on, we're going to make one
change. In a lab a bit later in this section, we'll be writing a number of
functions to access different pieces of information in our object, so the
functions will need to be able to access it. Rather than storing `gameObject` as
a global variable, let's turn it into a _function_ that contains and returns the
object. When you're done, running `gameObject()` should return the object. If we
want to access one of the properties in our object - say, the name of the home
team - we could do something like this:

```js
const obj = gameObject();
console.log(obj["home"]["teamName"]);
// => "Brooklyn Nets"
```

We could even skip the variable assignment and access the properties of the
object directly off the function call:

```js
console.log(gameObject()["home"]["teamName"]);
```

However, it's often a good idea to save results from functions into variables
because that makes it easier to debug our programs later. One-liners are not
always better!

Once you've converted `gameObject` into a function, run the tests to make sure
everything is correct.

**ADD TESTS TO CHECK THAT OBJECT IS CREATED CORRECTLY**

## Conclusion

We are now almost ready to start building the functions to access information in
our object. Before we get to that, however, let's learn a little about debugging
JavaScript. You may want to leave this lesson open in your text editor because
you'll be using your `gameObject()` function in the next lesson as well.

## Resources

- [MDN: Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)
- [MDN: for...in](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...in)
