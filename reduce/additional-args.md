Sometimes we need to turn arrays into new values in ways that can't be done purely by passing an accumulator along with no knowledge about its context. Learn how to reduce an array of numbers into its mathematical mean in a single reduce step by using the optional index and array reducer arguments.



We know that it's possible to reduce an array into another value by writing a reduce function. The reduce function has a signature that looks like this, it takes an accumulator, and it takes a value, and it returns some integration of that accumulator and that value to act as a new accumulator.

```JavaScript
function reducer(accumulator, value, index, array) {
  var intermediaryValue = accumulator + value;

  if (index === array.length - 1) {
    return intermediaryValue / array.length;
  }

  return intermediaryValue;
}

var data = [1, 2, 3, 3, 4, 5, 3, 1];
var mean = data.reduce(reducer, 0);

console.log(mean);
```

What does this let us do? This lets us say, "Look, let's compute our intermediary value for our accumulator and if this is the very last item, if this is the last time this is being fired, then we're going to know that that's the case because index is going to be equal to array.length minus one.

If index equals array.length minus one, instead of merely returning the intermediary value the way we do when we sum it up, we're going to return intermediary value divided by array.length. Otherwise, if this is not the very last time this fires, go ahead and just return the intermediary value directly.

You can see when this runs, it's going to run here. The accumulator's going to be 1, then the accumulator's going to be 3, then it's going to be 6, then it's going to be 9, then it's going to be 13. We're going to add this up until it gets to the very last step.

Now in this instance, we have an array whose length is 8. So the very last time it fires, value is going to be 1, the accumulator is going to be 1+2+3+3 is 13, 18, 21. The index is going to be 7, right, because it's the last item in our length of 8 array with a 0 index and the array is the array itself. What's going to happen is that 1 is going to added to our accumulator to give us our total of 22.

This then is going to evaluate to true, so instead of returning the sum directly we're going to go ahead and we're going to compute the mean right here inside of our reducer. The big difference here, this is going to get us the exact same value but now, instead of reducing the array into a sum and then computing the mean, we've gone ahead and we've directly reduced the array into a mean.

This is all one pure function. If you're writing unit tests you can test this. You can pass in an accumulator, and a value, and some index and some array, and you can write test to make sure that this behaves the way you would expect when you pass in, for instance, an array of length 1 and whatever.

Given that it's a pure function, this is a rule that tells you how to take some array of numbers and reduce it into a mean.
