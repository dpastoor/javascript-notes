

## Forgetting to pass the initial value of accumulator

If you forget to pass in initial value for the accumulator, javascript tries
to help and takes the first value of the array as your initial accumulator value,
however this is really only good for scenarios where you are doing things
like adding up numbers


```JavaScript
var data = ["vote1", "vote2", "vote1", "vote2"];
function reducer(accumulator, value) {
  if (accumulator[value]) {
    accumulator[value] = accumulator[value] + 1;
  } else {
    accumulator[value] = 1;
  }

  return accumulator;
}

var tally = data.reduce(reducer);

console.log(tally); // --> vote1
```

The accumulator was just vote one. Because when we didn't specify an initial value, it assumed that this is our initial value. Strings are primitives. They can't have properties, and so this always resolves to false. What's going to happen is that that initial value is just going to get returned every time.

Bugs like this can happen. They're incredibly hard to understand or figure out what the hell's happening. It's not like it's throwing an exception. It's not like it's returning undefined. It's returning a value. It's just, where the hell did that come from?

#### Must also pass in an initial value of {}

```JavaScript
var tallyCorrected = data.reduce(reducer, {})
console.log(tallyCorrected) // --> { vote1: 2, vote2: 2 }
```

## forgetting to return accumulator

INCORRECT VERSION OF FUNCTION ABOVE

```JavaScript
var data = ["vote1", "vote2", "vote1", "vote2"];
function reducer(accumulator, value) {
  if (accumulator[value]) {
    accumulator[value] = accumulator[value] + 1;
  } else {
    accumulator[value] = 1;
  }
  // forget to
  //return accumulator;
}
```

Well, this is actually the second time it runs, because the first time it ran it never returned a new accumulator. Accumulator became null the second time this ran, and you're going to get that kind of an error.

Two takeaways here. Number one, always pass in an initial value for your accumulator. Never rely on the fact that it'll automatically work when you're summing numbers, because the bugs you're going to find are really quite magnificent. Number two, always double check and make sure that you're actually returning the accumulator.
