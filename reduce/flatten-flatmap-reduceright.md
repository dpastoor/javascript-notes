```JavaScript
var data = [[1, 2, 3], [4, 5, 6], [7, 8, 9]];
var flattenedData = data.reduce(function(acc, value) {
  return acc.concat(value);
}, []);
```


You can't take some bunch of really complex objects and just reduce that down to an array of just the things you care about. That kind of thing only works in examples in tutorial videos. How could you do something like that with more complex data?

I'd like to introduce you to my next pattern here. Instead of flattening a list of lists, what we're going to do is take a list of complex objects, in this case it's a list of movies. Christopher Nolan's Batman movies.

What we're going to do is we're going to reduce this list of objects into a single list of the stars that appeared in these movies. We want to make sure among other things that only include each star once. We don't want to see Christian Bale showing up three times.

How can we do this with a single reduce operation? Well, this kind of operation has a special name. This is called a flat map. If that sounds familiar, it might be because at your local meetup you might have heard some functional programmers talking about monads and flat maps and the rest of us have no idea what they're talking about, right?

**A flat map takes a list of values here, where those values are potentially complex objects, and it turns each of those values into an array, somehow.**

```JavaScript
var input = [
  {
    title: "Batman Begins",
    year: 2005,
    cast: [
      "Christian Bale",
      "Michael Caine",
      "Liam Neeson",
      "Katie Holmes",
      "Gary Oldman",
      "Cillian Murphy"
    ]
  },
  {
    title: "The Dark Knight",
    year: 2008,
    cast: [
      "Christian Bale",
      "Heath Ledger",
      "Aaron Eckhart",
      "Michael Caine",
      "Maggie Gyllenhal",
      "Gary Oldman",
      "Morgan Freeman"
    ]
  },
  {
    title: "The Dark Knight Rises",
    year: 2012,
    cast: [
      "Christian Bale",
      "Gary Oldman",
      "Tom Hardy",
      "Joseph Gordon-Levitt",
      "Anne Hathaway",
      "Marion Cotillard",
      "Morgan Freeman",
      "Michael Caine"
    ]
  }
];

var stars = input.reduce(function(acc, value) {
  value.cast.forEach(function(star) {
    if (acc.indexOf(star) === -1) {
      acc.push(star);
    }
  });

  return acc;
}, []);
```


```JavaScript

var data = [1, 2, 3, 4, "5"];
var sum = data.reduceRight(function(acc, value, index) {
  console.log(index);
  return acc + value;
}, 0);

console.log(sum);
```

What is this going to resolve to? Anybody want to take a guess? If you guessed 15, you're wrong. Resolved to 105, because in JavaScript a number plus a string is actually a string concatenation operation.

Our accumulator starts at zero. We add 1, then we add 2 to that, then we add 3 to that, then we add 4 to that and we're at 10. We add the string 5 to 10 and that gives us 105. As you can see, our index started at zero, then one, then two, then three, then four.
But maybe it's really important to you. Maybe this isn't a bug. Maybe you really, you have this string five and you really need to start with this. You want to reduce this array so that it starts here and then works its way down. When you do a for loop you can count down instead of counting up. You want to be able to do that for reduce.

Is there some way to do that? Sure. Instead of calling array.reduce, call array.reduce right. Now you can see we're counting down from index four to three to two to one to zero. Our final output is what happens when you append the string zero to the string five to the string four to the string three to the string two to one.
