What we want to do now that we have this list of votes is we want to turn this into an object that gives us the number of votes for each framework that was named. Well, you should think to yourself, "I've got an array, and I want to turn that array into an object. Hey, this is a job for Reduce."

```JavaScript
var votes = [
  "angular",
  "angular",
  "react",
  "react",
  "react",
  "angular",
  "ember",
  "react",
  "vanilla"
];
```

Remember the reduce pattern - we need 2 things:

* accumulator - initialValue
* reducer - reducer function that will take the accumulator (tally) and each value of the array passed in (vote)



```JavaScript
var initialValue = {};
var reducer = function(tally, vote) {
  if (!tally[vote]) {
    tally[vote] = 1;
  } else {
    tally[vote] = tally[vote] + 1;
  }

  return tally;
};

var result = votes.reduce(reducer, initialValue);

console.log(result); // --> { angular: 3, react: 4, ember: 1, vanilla: 1 }
```

We're going to say if the tally does not have a key with the same name as that vote, then we're going to create one. We're going to set its value equal to one. However, if the tally already has a value for that particular vote, we're just going to increment it. Then, because this is a reducer, it's very important that you remember to return your accumulator.

The result of our informal poll is going to be votes.reduce. It's going to take our reducer, and it's going to take our initial value. Now let's just step through and make sure we understand exactly what's going on here. We've got our votes. We're going to reduce it using this reducer.

This reducer's going to take the accumulator and it's going to take the first item in the array. The vote here is going to be Angular, and the tally is going to be this empty object. It's going to say, "Hey, does tally.angular exist? No? Great. Tally.angular now equals one. Return tally."

It's going to get called again. Vote is Angular again, and tally is the return value from the previous iteration. It's an object with one key, Angular, whose value is one. Now when we get to our logic we're going to see it does exist, so we're going to increment that. Now we're returning an object whose key is Angular and whose value is two.

We get to the third item here, React. We'll vote as React. Tally is this list of Angular is two. We're going to create a new key, and we're going to say, "Tally.react is equals one." When we return that, it's an object. It's got two keys, Angular whose value is two, and React, whose value is one and so on and so forth.

We're going to step through every item here, and we're going to integrate each of those items one at a time into our running tally. Because this is reduced this whole thing evaluates to the value that gets returned from the very last call of the Reduce function.

When we run this, we see we had three votes for Angular, four votes for React, one vote for Amber, and one vote for no framework.
