Now in order to use reduce, you need two things. The first thing you need is a reducer, and the second thing you need
is the initial value of the accumulator.

 Let's say we have a list of numbers and we want to add them all up. This is the classic example of reduce. Our reducer looks like this.

It takes two arguments:
* The first argument is called the accumulator.
* The second argument is the item in the array that you're going to be integrating into the accumulator.

What you're going to do is you're going to return a new accumulator.

Because we're summing up an array, we're going to return the previous accumulator. This is what got returned the last time this function was called. We're just going to add that to the current item.

If the accumulator here is _always the previously returned accumulator value_, then the very first time this runs, we need to provide:

* some sort of a specific value so that it knows what to start with, since it never worked. It never fired before.
* The second thing we need is the initial value. For now let's just call that zero.

```JavaScript
var initialValue = 0;
var data = [15, 3, 20];

var reducer = function(accumulator, item) {
  return accumulator + item;
};

var total = data.reduce(reducer, initialValue);

console.log("The sum is", total);
```

The initial value is zero. That's the initial value of the accumulator the one time this runs. The only item in this array is the number 15, so this is going to fire once, and it's going to return 0 plus 15. The total we should expect to see is 15, and we do.

The first time it fires, the accumulator value is 0, and the item is 15. It returns 15. The second time it fires, the accumulator value is 15, because that's what got returned the last time. The item is 3, so the total value here is 18. Finally, it's going to fire a third time, so the accumulator value is 18, and the item value is 20, and so that's going to return 38.

Now the way this always works, the reduce expression here, this whole thing is an expression. That means is evaluates to a specific value. Array.reduce always evaluates to the final value of the accumulator, so this whole thing is just going to be 38.
