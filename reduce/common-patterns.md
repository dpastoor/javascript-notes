```JavaScript
var data = [1, 2, 3];
var doubled = data.reduce(function(acc, value) {
  acc.push(value * 2);

  return acc;
}, []);


var doubleMapped = data.map(function(item) {
  return item * 2;
});
```

```JavaScript
var data2 = [1, 2, 3, 4, 5, 6];
var evens = data2.reduce(function(acc, value) {
  if (value % 2 === 0) {
    acc.push(value);
  }

  return acc;
}, []);

var evenFiltered = data2.filter(function(item) {
  return (item % 2 === 0);
});
```

Why use reduce when you can elegantly compose these array-method based functions
that are more concise and easy to read?

```JavaScript
var filterMapped = data2.filter(function(value) {
  return value % 2 === 0;
}).map(function(value) {
  return value * 2;
});
```

I still want you to be thinking in terms of reduction. I still want you to realize that _what you've really done is reduce this array into another array._ But keeping your code simple and concise and readable is really important, and I encourage that.

And, what if you have big data?

```JavaScript
var bigData = [];
for (var i = 0; i < 1000000; i++) {
  bigData[i] = i;
}
```

```JavaScript
console.time('bigData');

var filterMappedBigData = bigData.filter(function(value) {
  return value % 2 === 0;
}).map(function(value) {
  return value * 2;
});
console.timeEnd('bigData'); // --> 97 milliseconds

console.time('bigDataReduce');
var reducedBigData = bigData.reduce(function(acc, value) {
  if (value % 2 === 0) {
    acc.push(value * 2);
  }
  return acc;
}, []);
console.timeEnd('bigDataReduce'); // --> 50 milliseconds
```

Wow, look at that. This one took 97 milliseconds, this one took 50. Why is that? Well, that's because when you're composing, you're mapping your filter, first the filter's going to iterate through one million items, and it's going to return 500,000 items. Then your map needs to be applied to each of those 500,000 items.

Contrast that to the reduce approach where we're filtering and mapping all in one step. We only need to iterate over those million items once and then we're done. I'm not saying that you should always be doing this, but I am saying that for complex chains like especially if you're doing things like filter this and then map to that and then like sort this and da da da.

If you're dealing with a lot of information, then it can be very helpful to be aware of the way reduce can give you a huge performance boost by allowing you to merge all these operations together so you're not constantly iterating over the same dataset.
