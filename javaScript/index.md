# JavaScript Kata

## Menu

## Content

### 1. Array.diff JavaScript Translation

#### link

[https://www.codewars.com/kata/523f5d21c841566fde000009](https://www.codewars.com/kata/523f5d21c841566fde000009)

#### instructions

Your goal in this kata is to implement a difference function, which subtracts one list from another and returns the result.

It should remove all values from `list a` , which are present in `list b` keeping their order.

```js
arrayDiff([1, 2], [1]) == [2];
```

If a value is present in `b` , all of its occurrences must be removed from the other:

```js
arrayDiff([1, 2, 2, 2, 3], [2]) == [1, 3];
```

#### solution

```js
function arrayDiff(a, b) {
  return a.reduce((acc, curr) => {
    return !b.includes(curr) ? [...acc, curr] : acc;
  }, []);
}
```

---

### 2. Sum of Digits / Digital Root

#### link

[https://www.codewars.com/kata/541c8630095125aba6000c00/train/javascript](https://www.codewars.com/kata/541c8630095125aba6000c00/train/javascript)

#### descriptions

Digital root is the recursive sum of all the digits in a number.

Given `n` , take the sum of the digits of `n` . If that value has more than one digit, continue reducing in this way until a single-digit number is produced. The input will be a non-negative integer.

##### Examples

```plains
    16  -->  1 + 6 = 7
   942  -->  9 + 4 + 2 = 15  -->  1 + 5 = 6
132189  -->  1 + 3 + 2 + 1 + 8 + 9 = 24  -->  2 + 4 = 6
493193  -->  4 + 9 + 3 + 1 + 9 + 3 = 29  -->  2 + 9 = 11  -->  1 + 1 = 2
```

#### solution

```js
function digital_root(n) {
  let sum = 0;
  let curr = n;
  do {
    sum += curr % 10;
    curr = Math.floor(curr / 10);
  } while (curr !== 0);
  return sum >= 10 ? digital_root(sum) : sum;
}
```

#### the better solutions

```js
function digital_root(n) {
  return ((n - 1) % 9) + 1;
}
```

---

### 3. Who likes it?

#### link

[https://www.codewars.com/kata/5266876b8f4bf2da9b000362](https://www.codewars.com/kata/5266876b8f4bf2da9b000362)

#### instructions

You probably know the "like" system from Facebook and other pages. People can "like" blog posts, pictures or other items. We want to create the text that should be displayed next to such an item.

Implement the function which takes an array containing the names of people that like an item. It must return the display text as shown in the examples:

```plain
[]                                -->  "no one likes this"
["Peter"]                         -->  "Peter likes this"
["Jacob", "Alex"]                 -->  "Jacob and Alex like this"
["Max", "John", "Mark"]           -->  "Max, John and Mark like this"
["Alex", "Jacob", "Mark", "Max"]  -->  "Alex, Jacob and 2 others like this"
```

Note: For `4` or more names, the number in `"and 2 others"` simply increases.

#### solution

```js
function likes(names) {
  switch (names.length) {
    case 0:
    case 1:
      return `${names[0] ? names[0] : "no one"} likes this`;
    case 2:
      return `${names.join(" and ")} like this`;
    case 3:
    case 4:
    default:
      const [first, second, ...rest] = names;
      return `${first}, ${second} and ${
        rest.length > 1 ? rest.length + " others" : rest[0]
      } like this`;
  }
}
```

#### a crazy but strong solution

```js
function likes(peopleNames) {
  var feels = new FeelingsParty("like", "this");
  for (var name in peopleNames) feels.addFeeler(new Person(peopleNames[name]));
  return feels.shareTheseFeelings();
}

function Person(name) {
  this.name = name;
}

Person.prototype.getName = function () {
  return this.name;
};

function FeelingsParty(emotion, target) {
  this.emotionalContext = emotion;
  this.emotionalSubject = target;
  this.peopleFeelingThisWay = [];
  this.numPeopleFeelingThisWay = 0;
}

FeelingsParty.prototype.getEmotionalContext = function () {
  return this.type;
};

FeelingsParty.prototype.addFeeler = function (person) {
  this.numPeopleFeelingThisWay++;
  this.peopleFeelingThisWay.push(person);
};

FeelingsParty.prototype.shareTheseFeelings = function () {
  this.findTheRightWords();
  if (this.numPeopleFeelingThisWay == 0)
    return "no one " + this.emotionalContext + " " + this.emotionalSubject;
  if (this.numPeopleFeelingThisWay == 1)
    return (
      "" +
      this.peopleFeelingThisWay[0].getName() +
      " " +
      this.emotionalContext +
      " " +
      this.emotionalSubject
    );
  if (this.numPeopleFeelingThisWay == 2)
    return (
      "" +
      this.peopleFeelingThisWay[0].getName() +
      " and " +
      this.peopleFeelingThisWay[1].getName() +
      " " +
      this.emotionalContext +
      " " +
      this.emotionalSubject
    );
  if (this.numPeopleFeelingThisWay == 3)
    return (
      "" +
      this.peopleFeelingThisWay[0].getName() +
      ", " +
      this.peopleFeelingThisWay[1].getName() +
      " and " +
      this.peopleFeelingThisWay[2].getName() +
      " " +
      this.emotionalContext +
      " " +
      this.emotionalSubject
    );
  return (
    "" +
    this.peopleFeelingThisWay[0].getName() +
    ", " +
    this.peopleFeelingThisWay[1].getName() +
    " and " +
    (this.numPeopleFeelingThisWay - 2) +
    " others " +
    this.emotionalContext +
    " " +
    this.emotionalSubject
  );
};

FeelingsParty.prototype.findTheRightWords = function () {
  if (this.numPeopleFeelingThisWay == 0 || this.numPeopleFeelingThisWay == 1)
    this.emotionalContext += "s";
};
```

---

### 4. You're a square!

#### link

[https://www.codewars.com/kata/54c27a33fb7da0db0100040e](https://www.codewars.com/kata/54c27a33fb7da0db0100040e)

#### instructions

##### A square of squares

You like building blocks. You especially like building blocks that are squares. And what you even like more, is to arrange them into a square of square building blocks!

However, sometimes, you can't arrange them into a square. Instead, you end up with an ordinary rectangle! Those blasted things! If you just had a way to know, whether you're currently working in vain… Wait! That's it! You just have to check if your number of building blocks is a perfect square.

##### Task

Given an integral number, determine if it's a [square number](https://en.wikipedia.org/wiki/Square_number):

> In mathematics, a square number or perfect square is an integer that is the square of an integer; in other words, it is the product of some integer with itself.

The tests will always use some integral number, so don't worry about that in dynamic typed languages.

##### Examples

```plain
-1  =>  false
 0  =>  true
 3  =>  false
 4  =>  true
25  =>  true
26  =>  false
```

#### solution

```js
var isSquare = function (n) {
  return parseInt(Math.sqrt(n)) === Math.sqrt(n);
};
```

#### the better solution

```js
function isSquare(n) {
  return Math.sqrt(n) % 1 === 0;
}
```

---

### 5. Vowel Count

#### link

[https://www.codewars.com/kata/54ff3102c1bad923760001f3](https://www.codewars.com/kata/54ff3102c1bad923760001f3)

#### instructions

Return the number (count) of vowels in the given string.

We will consider `a` , `e` , `i` , `o` , `u` as vowels for this Kata (but not `y` ).

The input string will only consist of lower case letters and/or spaces.

#### solution

```js
function getCount(str) {
  const regex = /[aeiou]/g;
  const matches = str.match(regex);
  const vowelsCount = matches ? matches.length : 0;
  return vowelsCount;
}
```

#### the better solution

```js
function getCount(str) {
  return (str.match(/[aeiou]/gi) || []).length;
}
```

---

### 6. Playing with digits

#### link

[https://www.codewars.com/kata/5552101f47fc5178b1000050](https://www.codewars.com/kata/5552101f47fc5178b1000050)

#### instructions

Some numbers have funny properties. For example:

```plain
89 --> 8¹ + 9² = 89 * 1

695 --> 6² + 9³ + 5⁴= 1390 = 695 * 2

46288 --> 4³ + 6⁴+ 2⁵ + 8⁶ + 8⁷ = 2360688 = 46288 * 51
```

Given a positive integer n written as abcd... (a, b, c, d... being digits) and a positive integer p

we want to find a positive integer `k` , if it exists, such as the sum of the digits of `n` taken to the successive powers of `p` is equal to `k * n` .
In other words:

> Is there an integer k such as : (a ^ p + b ^ (p+1) + c ^(p+2) + d ^ (p+3) + ...) = n \* k

If it is the case we will return `k` , if not return `-1` .

Note: `n` and `p` will always be given as strictly positive integers.

```js
digPow(89, 1) should
return 1 since 8¹ + 9² = 89 = 89 * 1
digPow(92, 1) should
return -1 since there is no k such as 9¹ + 2² equals 92 * k
digPow(695, 2) should
return 2 since 6² + 9³ + 5⁴ = 1390 = 695 * 2
digPow(46288, 3) should
return 51 since 4³ + 6⁴ + 2⁵ + 8⁶ + 8⁷ = 2360688 = 46288 * 51
```

#### solution

```js
function digPow(n, p) {
  const digArr = [];
  let division = n;
  do {
    digArr.push(division % 10);
    division = Math.floor(division / 10);
  } while (division !== 0);

  const powers = digArr.reverse().reduce((acc, curr, index) => {
    return acc + Math.pow(curr, index + p);
  }, 0);

  return powers % n === 0 ? powers / n : -1;
}
```

---

### 7. Bit Counting

#### link

[https://www.codewars.com/kata/526571aae218b8ee490006f4](https://www.codewars.com/kata/526571aae218b8ee490006f4)

#### instructions

Write a function that takes an integer as input, and returns the number of bits that are equal to one in the binary representation of that number. You can guarantee that input is non-negative.

##### Example

The binary representation of `1234` is `10011010010` , so the function should return `5` in this case

#### solution

```js
const countBits = function (n) {
  const res = n.toString(2);
  console.log(res);
  return res.split("").reduce((acc, curr) => (curr * 1 ? acc + 1 : acc), 0);
};
```

#### the better solution

```js
countBits = (n) => n.toString(2).split("0").join("").length;
```

#### warning

You can not use `>>` to calculate.(**Big int** problem)

---

### 8. Are they the "same"?

#### link

[https://www.codewars.com/kata/550498447451fbbd7600041c](https://www.codewars.com/kata/550498447451fbbd7600041c)

#### instructions

Given two arrays `a` and `b` write a function `comp(a, b)` (or `compSame(a, b)` ) that checks whether the two arrays have the "same" elements, with the same multiplicities (the multiplicity of a member is the number of times it appears). "Same" means, here, that the elements in `b` are the elements in `a` squared, regardless of the order.

##### examples

**Valid arrays**

```js
a = [121, 144, 19, 161, 19, 144, 19, 11];
b = [121, 14641, 20736, 361, 25921, 361, 20736, 361];
```

`comp(a, b)` returns true because in `b` 121 is the square of 11, 14641 is the square of 121, 20736 the square of 144, 361 the square of 19, 25921 the square of 161, and so on. It gets obvious if we write `b` 's elements in terms of squares:

```js
a = [121, 144, 19, 161, 19, 144, 19, 11];
b = [
  11 * 11,
  121 * 121,
  144 * 144,
  19 * 19,
  161 * 161,
  19 * 19,
  144 * 144,
  19 * 19,
];
```

**Invalid arrays**
If, for example, we change the first number to something else, `comp` is not returning true anymore:

```js
a = [121, 144, 19, 161, 19, 144, 19, 11];
b = [132, 14641, 20736, 361, 25921, 361, 20736, 361];
```

`comp(a,b)` returns `false` because in `b` 132 is not the square of any number of `a` .

```js
a = [121, 144, 19, 161, 19, 144, 19, 11];
b = [121, 14641, 20736, 36100, 25921, 361, 20736, 361];
```

`comp(a,b)` returns `false` because in `b` 36100 is not the square of any number of `a` .

**Remarks**
`a` or `b` might be `[] or {}` (all languages except R, Shell).
`a` or `b` might be `nil` or `null` or `None` or `nothing` (except in C++, Crystal, D, Dart, Elixir, Fortran, F#, Haskell, Nim, OCaml, Pascal, Perl, PowerShell, Prolog, PureScript, R, Racket, Rust, Shell, Swift).
If `a` or `b` are `nil` (or `null` or `None` , depending on the language), the problem doesn't make sense so return false.

**Note for C**
The two arrays have the same size `(> 0)` given as parameter in function `comp` .

#### tips

`comp([],[])` should return `true`

#### solution

```js
function comp(array1, array2) {
  if (!array1 || !array2) {
    return false;
  }
  if (array1.length === 0 && array2.length === 0) {
    return true;
  }
  if (
    array1.length === 0 ||
    array2.length === 0 ||
    array1.length !== array2.length
  ) {
    return false;
  }
  const aMap = array1.map((i) => i * i);
  let i = 0,
    length = aMap.length;
  for (; i < length; i++) {
    if (array2.length === 0) {
      return false;
    }
    const pos = array2.indexOf(aMap[i]);
    if (pos < 0) {
      return false;
    } else {
      array2.splice(pos, 1);
    }
  }
  return true;
}
```

#### the better solution

```js
const comp = (array1, array2) =>
  Array.isArray(array1) &&
  Array.isArray(array2) &&
  array1.every((item) => {
    const index = array2.indexOf(Math.pow(item, 2));
    return index > -1 ? array2.splice(index, 1) : false;
  });
```

---

### 9. First non-repeating character

#### link

[https://www.codewars.com/kata/52bc74d4ac05d0945d00054e](https://www.codewars.com/kata/52bc74d4ac05d0945d00054e)

#### instructions

Write a function named `first_non_repeating_letter` that takes a string input, and returns the first character that is not repeated anywhere in the string.

For example, if given the input `'stress'` , the function should return `'t'` , since the letter t only occurs once in the string, and occurs first in the string.

As an added challenge, **upper-** and **lowercase** letters are considered the same character, but the function should return the correct case for the initial letter. For example, the input `'sTreSS'` should return `'T'` .

If a string contains all repeating characters, it should return an empty string ( `""` ) or `None` -- see sample tests.

#### solutions

```js
function firstNonRepeatingLetter(s) {
  const str = s.toLowerCase();
  let i = 0,
    length = str.length;
  for (; i < length; i++) {
    const flag = str.indexOf(str[i]) === str.lastIndexOf(str[i]);
    if (flag) {
      return s[i];
    }
  }
  return "";
}
```

---

### 10. Take a Ten Minute Walk

#### link

[https://www.codewars.com/kata/54da539698b8a2ad76000228](https://www.codewars.com/kata/54da539698b8a2ad76000228)

#### instructions

You live in the city of Cartesia where all roads are laid out in a perfect grid. You arrived ten minutes too early to an appointment, so you decided to take the opportunity to go for a short walk. The city provides its citizens with a Walk Generating App on their phones -- everytime you press the button it sends you an array of one-letter strings representing directions to walk (eg. `['n', 's', 'w'¸, 'e']` ). You always walk only a single block for each letter (direction) and you know it takes you one minute to traverse one city block, so create a function that will return true if the walk the app gives you will take you exactly ten minutes (you don't want to be early or late!) and will, of course, return you to your starting point. Return false otherwise.

> Note: you will always receive a valid array containing a random assortment of direction letters ('n', 's', 'e', or 'w' only). It will never give you an empty array (that's not a walk, that's standing still!).

#### solution

```js
function isValidWalk(walk) {
  if (walk && walk.length !== 10) return false;
  let horizontal = 0;
  let vertical = 0;
  let distance = 0;
  const MATCH_DISTANCE = 10;
  walk.forEach((item) => {
    distance++;
    switch (item) {
      case "w":
        horizontal--;
        break;
      case "e":
        horizontal++;
        break;
      case "n":
        vertical++;
        break;
      case "s":
        vertical--;
        break;
    }
  });
  return (
    distance + Math.abs(horizontal) + Math.abs(vertical) === MATCH_DISTANCE
  );
}
```

---

### 11. Delete occurrences of an element if it occurs more than n times

#### link

[https://www.codewars.com/kata/554ca54ffa7d91b236000023](https://www.codewars.com/kata/554ca54ffa7d91b236000023)

#### instructions

##### Enough is enough!

Alice and Bob were on a holiday. Both of them took many pictures of the places they've been, and now they want to show Charlie their entire collection. However, Charlie doesn't like these sessions, since the motive usually repeats. He isn't fond of seeing the Eiffel tower 40 times. He tells them that he will only sit during the session if they show the same motive at most N times. Luckily, Alice and Bob are able to encode the motive as a number. Can you help them to remove numbers such that their list contains each number only up to N times, without changing the order?

##### Task

Given a list lst and a number N, create a new list that contains each number of lst at most N times without reordering. For example if N = 2, and the input is `[1,2,3,1,2,1,2,3]` , you take `[1,2,3,1,2]` , drop the next `[1,2]` since this would lead to 1 and 2 being in the result 3 times, and then take 3, which leads to `[1,2,3,1,2,3]` .

##### Example

```js
deleteNth([1, 1, 1, 1], 2); // return [1,1]
deleteNth([20, 37, 20, 21], 1); // return [20,37,21]
```

#### solution

```js
function deleteNth(arr, n) {
  let countMap = new Map();
  return arr.filter((item) => {
    const count = countMap.get(item) || 0;
    countMap.set(item, count ? count + 1 : 1); // make sure count >= 1
    return count < n; // 'count' changed after got the value of Map.get(item)
  });
}
```

#### the better solution

```js
function deleteNth(a, x) {
  let m = {}; // no using Map()
  return a.filter((v) => (m[v] = m[v] + 1 || 1) <= x);
}
```

---

### 12. PaginationHelper

#### link

[https://www.codewars.com/kata/515bb423de843ea99400000a/train/javascript](https://www.codewars.com/kata/515bb423de843ea99400000a/train/javascript)

#### instructions

For this exercise you will be strengthening your page-fu mastery. You will complete the PaginationHelper class, which is a utility class helpful for querying paging information related to an array.

The class is designed to take in an array of values and an integer indicating how many items will be allowed per each page. The types of values contained within the collection/array are not relevant.

The following are some examples of how this class is used:

```js
var helper = new PaginationHelper(["a", "b", "c", "d", "e", "f"], 4);
helper.pageCount(); //should == 2
helper.itemCount(); //should == 6
helper.pageItemCount(0); //should == 4
helper.pageItemCount(1); // last page - should == 2
helper.pageItemCount(2); // should == -1 since the page is invalid

// pageIndex takes an item index and returns the page that it belongs on
helper.pageIndex(5); //should == 1 (zero based index)
helper.pageIndex(2); //should == 0
helper.pageIndex(20); //should == -1
helper.pageIndex(-10); //should == -1
```

#### solution

```js
// TODO: complete this object/class

// The constructor takes in an array of items and a integer indicating how many
// items fit within a single page
function PaginationHelper(collection, itemsPerPage) {
  this.collection = collection || [];
  this.itemsPerPage = itemsPerPage;
}

// returns the number of items within the entire collection
PaginationHelper.prototype.itemCount = function () {
  return this.collection.length;
};

// returns the number of pages
PaginationHelper.prototype.pageCount = function () {
  return Math.ceil(this.collection.length / this.itemsPerPage);
};

// returns the number of items on the current page. page_index is zero based.
// this method should return -1 for pageIndex values that are out of range
PaginationHelper.prototype.pageItemCount = function (pageIndex) {
  if (this.collection.length === 0) {
    return 0;
  }
  const rest = this.collection.length - this.itemsPerPage * pageIndex;
  if (rest < 0) return -1;
  return rest > this.itemsPerPage ? this.itemsPerPage : rest;
};

// determines what page an item is on. Zero based indexes
// this method should return -1 for itemIndex values that are out of range
PaginationHelper.prototype.pageIndex = function (itemIndex) {
  if (
    itemIndex > this.collection.length ||
    itemIndex < 0 ||
    itemIndex === undefined ||
    this.collection.length === 0
  )
    return -1;
  const perPage = isNaN(this.itemsPerPage)
    ? this.collection.length
    : this.itemsPerPage;
  const indexBase = Math.ceil(itemIndex / perPage);
  if (indexBase === 0) {
    return 0;
  }
  return indexBase - 1;
};
```

---

### 13. Most frequently used words in a text

#### link

[https://www.codewars.com/kata/51e056fe544cf36c410000fb/train/javascript](https://www.codewars.com/kata/51e056fe544cf36c410000fb/train/javascript)

#### instructions

Write a function that, given a string of text (possibly with punctuation and line-breaks), returns an array of the top-3 most occurring words, in descending order of the number of occurrences.

##### Assumptions

- A word is a string of letters (A to Z) optionally containing one or more apostrophes (`'`) in ASCII.
- Apostrophes can appear at the start, middle or end of a word (`'abc`, `abc'`, `'abc'`, `ab'c` are all valid)
- Any other characters (e.g. `#`, `\`, `/` , `.` ...) are not part of a word and should be treated as whitespace.
- Matches should be case-insensitive, and the words in the result should be lowercased.
- Ties may be broken arbitrarily.
- If a text contains fewer than three unique words, then either the top-2 or top-1 words should be returned, or an empty array if a text contains no words.

##### Examples

```python
top_3_words("In a village of La Mancha, the name of which I have no desire to call to
mind, there lived not long since one of those gentlemen that keep a lance
in the lance-rack, an old buckler, a lean hack, and a greyhound for
coursing. An olla of rather more beef than mutton, a salad on most
nights, scraps on Saturdays, lentils on Fridays, and a pigeon or so extra
on Sundays, made away with three-quarters of his income.")
# => ["a", "of", "on"]

top_3_words("e e e e DDD ddd DdD: ddd ddd aa aA Aa, bb cc cC e e e")
# => ["e", "ddd", "aa"]

top_3_words("  //wont won't won't")
# => ["won't", "wont"]
```

##### Bonus points (not really, but just for fun)

1. Avoid creating an array whose memory footprint is roughly as big as the input text.
2. Avoid sorting the entire array of unique words.

#### solution

```js
function topThreeWords(text) {
  const arr = text.toLowerCase().match(/(?!')[a-z']+/gi) || [];
  const map = arr.reduce((map, item) => {
    return map.set(item, (map.get(item) || 0) + 1);
  }, new Map());
  return [...map]
    .sort((a, b) => b[1] - a[1])
    .slice(0, 3)
    .map((i) => i[0].toLowerCase());
}
```

---

### 14. Where my anagrams at?

#### link

[https://www.codewars.com/kata/523a86aa4230ebb5420001e1/train/javascript](https://www.codewars.com/kata/523a86aa4230ebb5420001e1/train/javascript)

#### instructions

What is an anagram? Well, two words are anagrams of each other if they both contain the same letters. For example:

```js
"abba" & ("baab" == true);

"abba" & ("bbaa" == true);

"abba" & ("abbba" == false);

"abba" & ("abca" == false);
```

Write a function that will find all the anagrams of a word from a list. You will be given two inputs a word and an array with words. You should return an array of all the anagrams or an empty array if there are none. For example:

```js
anagrams('abba', ['aabb', 'abcd', 'bbaa', 'dada']) => ['aabb', 'bbaa']

anagrams('racer', ['crazer', 'carer', 'racar', 'caers', 'racer']) => ['carer', 'racer']

anagrams('laser', ['lazing', 'lazy', 'lacer']) => []
```

##### Note for Go

For Go: Empty string slice is expected when there are no anagrams found.

##### solution

```js
function anagrams(word, words) {
  const reversal = word
    .split("")
    .sort((a, b) => a.charCodeAt() - b.charCodeAt())
    .join("");
  const res = [];
  words.forEach((i) => {
    const match = i
      .split("")
      .sort((a, b) => a.charCodeAt() - b.charCodeAt())
      .join("");
    match === reversal && res.push(i);
  });
  return res;
}
```

##### the better solution

```js
function anagrams(a, b) {
  return b.filter((w) => "" + [...a].sort() === "" + [...w].sort());
}
```

---

### 15. Weight for weight

#### instructions

My friend John and I are members of the "Fat to Fit Club (FFC)". John is worried because each month a list with the weights of members is published and each month he is the last on the list which means he is the heaviest.

I am the one who establishes the list so I told him: "Don't worry any more, I will modify the order of the list". It was decided to attribute a "weight" to numbers. The weight of a number will be from now on the sum of its digits.

For example `99` will have "weight" `18` , `100` will have "weight" `1` so in the list `100` will come before `99` .

Given a string with the weights of FFC members in normal order can you give this string ordered by "weights" of these numbers?

##### Example

```plain
"56 65 74 100 99 68 86 180 90" ordered by numbers weights becomes:

"100 180 90 56 65 74 68 86 99"
```

When two numbers have the same "weight", let us class them as if they were strings (alphabetical ordering) and not numbers:

`180` is before `90` since, having the same "weight" (9), it comes before as a string.

All numbers in the list are positive numbers and the list can be empty.

##### Notes

- it may happen that the input string have leading, trailing whitespaces and more than a unique whitespace between two consecutive numbers
- For C: The result is freed.

#### solution

```js
function sumDigit(numStr) {
  let number = parseInt(numStr),
    counter = 0;
  do {
    counter = (number % 10) + counter;
    number = Math.floor(number / 10);
  } while (number !== 0);
  return counter;
}

function orderWeight(string) {
  const numbers = string.split(" ");
  return numbers
    .sort((a, b) => {
      const flag = sumDigit(a) - sumDigit(b);
      const res = flag === 0 ? (a > b ? 1 : -1) : flag;
      return res;
    })
    .join(" ");
}
```

#### the better solution

```js
function orderWeight(strng) {
  const sum = (str) => str.split("").reduce((sum, el) => sum + +el, 0);

  function comp(a, b) {
    let sumA = sum(a);
    let sumB = sum(b);
    return sumA === sumB ? a.localeCompare(b) : sumA - sumB;
  }
  return strng.split(" ").sort(comp).join(" ");
}
```

---

### 16. Range Extraction

#### instructions

A format for expressing an ordered list of integers is to use a comma separated list of either

- individual integers
- or a range of integers denoted by the starting integer separated from the end integer in the range by a dash, '-'. The range includes all integers in the interval including both endpoints. It is not considered a range unless it spans at least 3 numbers. For example `"12,13,15-17"`
  Complete the solution so that it takes a list of integers in increasing order and returns a correctly formatted string in the range format.

##### Example

```js
solution([
  -6, -3, -2, -1, 0, 1, 3, 4, 5, 7, 8, 9, 10, 11, 14, 15, 17, 18, 19, 20,
]);
// returns "-6,-3-1,3-5,7-11,14,15,17-20"
```

#### solution

```js
function handleOutput(raw = [], acc = []) {
  let output = [];
  output = raw.concat(acc.length < 3 ? acc : [`${acc[0]}-${acc.slice(-1)}`]);
  return output;
}

function solution(list) {
  let acc = [],
    output = [],
    index = 0;

  do {
    const curr = list[index];
    const last = acc.length === 0 ? undefined : acc.slice(-1);
    if (last !== undefined && curr - last === 1) {
    } else {
      output = handleOutput(output, acc);
      acc.length = 0;
    }

    acc.push(curr);
    index++;
  } while (index < list.length);

  output = handleOutput(output, acc);
  return output.join(",");
}
```

#### the better solution

```js
function solution(nums) {
  nums = nums.map((v, i) =>
    nums[i - 1] == v - 1 && nums[i + 1] == v + 1 ? "-" : v
  );
  return nums
    .filter((v, i) => v != "-" || nums[i - 1] != "-")
    .join(",")
    .replace(/,-,/g, "-");
}
```

---

### 17. Split Strings

#### link

[https://www.codewars.com/kata/515de9ae9dcfc28eb6000001/train/javascript](https://www.codewars.com/kata/515de9ae9dcfc28eb6000001/train/javascript)

#### instructions

Complete the solution so that it splits the string into pairs of two characters. If the string contains an odd number of characters then it should replace the missing second character of the final pair with an underscore ('\_').

Examples:

```js
solution("abc"); // should return ['ab', 'c_']
solution("abcdef"); // should return ['ab', 'cd', 'ef']
```

#### solutions

```js
function solution(str) {
  const res = [];
  let ind = 0;
  while (ind < str.length) {
    const child = str.slice(ind, (ind += 2));
    res.push(child.length === 1 ? `${child}_` : child);
  }
  return res;
}
```

#### the better solution

```js
function solution(s) {
  return (s + "_").match(/.{2}/g) || [];
}
```

---

### 18. Assemble string

#### link

[https://www.codewars.com/kata/6210fb7aabf047000f3a3ad6](https://www.codewars.com/kata/6210fb7aabf047000f3a3ad6)

#### instructions

##### Task

In this task, you need to restore a string from a list of its copies.

You will receive an array of strings. All of them are supposed to be the same as the original but, unfortunately, they were corrupted which means some of the characters were replaced with asterisks ( `"*"` ).

You have to restore the original string based on non-corrupted information you have. If in some cases it is not possible to determine what the original character was, use `"#"` character as a special marker for that.

If the array is empty, then return an empty string.

##### Examples:

```js
input = ["a*cde", "*bcde", "abc*e"];
result = "abcde";

input = ["a*c**", "**cd*", "a*cd*"];
result = "a#cd#";
```

#### solutions

```js
function assembleString(array) {
  if (array.length === 0) {
    return "";
  } else {
    console.log({
      array,
    });
    const initial = array[0].split("");
    const output = array
      .reduce((acc, curr, index) => {
        const length = curr.length;
        const res = [];
        for (let i = 0; i < length; i++) {
          if (acc[i] === "*") {
            res.push(curr[i]);
          } else {
            res.push(acc[i]);
          }
        }
        return res;
      }, initial)
      .join("")
      .replace(/\*/g, "#");
    return output;
  }
}
```

#### the better solution

```js
function assembleString(array) {
  return !array.length
    ? ""
    : [...array[0]].map((x, i) => {
        let s = array.find((y) => y[i] != "*");
        return !s ? "#" : s[i];
      }).join``;
}
```

---

### 19. Strip Comments

#### link

[https://www.codewars.com/kata/51c8e37cee245da6b40000bd](https://www.codewars.com/kata/51c8e37cee245da6b40000bd)

#### instructions

Complete the solution so that it strips all text that follows any of a set of comment markers passed in. Any whitespace at the end of the line should also be stripped out.

##### Example:

Given an input string of:

```plain
apples, pears # and bananas
grapes
bananas !apples
```

The output expected would be:

```plain
apples, pears
grapes
bananas
```

The code would be called like so:

```js
var result = solution("apples, pears # and bananas\ngrapes\nbananas !apples", [
  "#",
  "!",
]);
// result should == "apples, pears\ngrapes\nbananas"
```

#### solution

```js
function solution(input, markers = []) {
  const strs = input.split("\n");
  return strs
    .map((str) => {
      let _str = str;
      markers.forEach((marker) => {
        const pos = _str.indexOf(marker);
        _str = _str.slice(0, pos === -1 ? _str.length : pos);
      });
      return _str.trim();
    })
    .join("\n");
}
```

#### the better solution

```js
function solution(input, markers = []) {
  return input.replace(new RegExp(`\\s*[${markers.join("|")}].+`, "g"), "");
}
```

---

### 20. Adding Big Numbers

#### link

[https://www.codewars.com/kata/525f4206b73515bffb000b21/train/javascript](https://www.codewars.com/kata/525f4206b73515bffb000b21/train/javascript)

#### instructions

We need to sum big numbers and we require your help.

Write a function that returns the sum of two numbers. The input numbers are strings and the function must return a string.

##### example

```sh
add("123","321"); -> "444"
add("11","99"); -> "110"
```

##### notes

- The input numbers are _big_
- The input is a string of only digits
- The numbers are positives

#### solution

```js
function add(a, b) {
  const arrA = a.split("").reverse();
  const arrB = b.split("").reverse();
  const lengthA = arrA.length;
  const lengthB = arrB.length;
  const rounds = Math.max(lengthA, lengthB);
  const arrRes = [];
  let lastCarry = 0;
  for (let i = 0; i < rounds; i++) {
    let tempA = i < lengthA ? Number(arrA[i]) : 0;
    let tempB = i < lengthB ? Number(arrB[i]) : 0;
    const sum = tempA + tempB + lastCarry;
    lastCarry = Math.floor(sum / 10);
    arrRes.push(sum % 10);
  }
  if (lastCarry) {
    arrRes.push(lastCarry);
  }
  return arrRes.reverse().join("");
}
```

---

### 21. Sort binary tree by levels

#### link

[https://www.codewars.com/kata/52bef5e3588c56132c0003bc/train/javascript](https://www.codewars.com/kata/52bef5e3588c56132c0003bc/train/javascript)

#### instructions

You are given a binary tree:

```js
class Node {
  constructor(value, left = null, right = null) {
    this.value = value;
    this.left = left;
    this.right = right;
  }
}
```

Your task is to return the list with elements from tree sorted by levels, which means the root element goes first, then root children (from left to right) are second and third, and so on.

Return empty array if root is `null`.

Example 1 - following tree:

```
                 2
            8        9
          1  3     4   5
```

Should return following list:

```js
[2, 8, 9, 1, 3, 4, 5];
```

Example 2 - following tree:

```
                 1
            8        4
              3        5
                         7
```

Should return following list:

```js
[1, 8, 4, 3, 5, 7];
```

#### solution

```js
function treeByLevels(tree) {
  const res = [];
  let depth = 0;
  if (tree === null) {
    return res;
  } else {
    (function flatNode(node = tree, dep = depth) {
      if (node === null) {
        return;
      }
      if (node.value !== null) {
        res.push({ value: node.value, depth: dep });
      }
      if (node.left !== null) {
        flatNode(node.left, dep + 1);
      }
      if (node.right !== null) {
        flatNode(node.right, dep + 1);
      }
    })(tree);

    return res.sort((a, b) => a.depth - b.depth).map((i) => i.value);
  }
}
```

#### the better solution

```js
function treeByLevels(rootNode) {
  if (!rootNode) return [];
  const nodes = [rootNode];
  const result = [];
  while (nodes.length > 0) {
    const node = nodes.shift();
    if (node.left) {
      nodes.push(node.left);
    }
    if (node.right) {
      nodes.push(node.right);
    }
    result.push(node.value);
  }
  return result;
}
```

### 22. Summarize ranges

#### link

[https://www.codewars.com/kata/55fb6537544ae06ccc0000dc/train/javascript](https://www.codewars.com/kata/55fb6537544ae06ccc0000dc/train/javascript)

#### instructions

Given a sorted array of numbers, return the summary of its ranges.

#### examples

```js
summaryRanges([1, 2, 3, 4]) === ["1->4"];
summaryRanges([1, 1, 1, 1, 1]) === ["1"];
summaryRanges([0, 1, 2, 5, 6, 9]) === ["0->2", "5->6", "9"];
summaryRanges([0, 1, 2, 3, 3, 3, 4, 5, 6, 7]) === ["0->7"];
summaryRanges([0, 1, 2, 3, 3, 3, 4, 4, 5, 6, 7, 7, 9, 9, 10]) ===
  ["0->7", "9->10"];
summaryRanges([-2, 0, 1, 2, 3, 3, 3, 4, 4, 5, 6, 7, 7, 9, 9, 10, 12]) ===
  ["-2", "0->7", "9->10", "12"];
```

#### solution

```js
function range(arr = []) {
  if ((arr.length === 1, arr[0] === arr[arr.length - 1])) {
    return arr[0].toString();
  } else {
    return [arr[0], arr[arr.length - 1]].join("->");
  }
}

function summaryRanges(nums = []) {
  const result = [];
  let tempArr = [];
  for (let i = 0; i < nums.length; i++) {
    const current = nums[i];
    const next = nums[i + 1];
    tempArr.push(current);
    if (next === undefined || current + 1 < next) {
      result.push(range(tempArr));
      tempArr = [];
    }
  }
  if (tempArr.length) {
    result.push(range(tempArr));
  }
  return result;
}
```

---

### 23. So Many Permutations!

#### link

[https://www.codewars.com/kata/5254ca2719453dcc0b00027d/javascript](https://www.codewars.com/kata/5254ca2719453dcc0b00027d/javascript)

#### instructions

In this kata, your task is to create all permutations of a non-empty input string and remove duplicates, if present.

Create as many "shufflings" as you can!

Examples:

```
With input 'a':
Your function should return: ['a']

With input 'ab':
Your function should return ['ab', 'ba']

With input 'abc':
Your function should return ['abc','acb','bac','bca','cab','cba']

With input 'aabb':
Your function should return ['aabb', 'abab', 'abba', 'baab', 'baba', 'bbaa']
```

Note: The order of the permutations doesn't matter.

Good luck!

#### solutions

```js
function permutations(str) {
  if (str.length === 1) {
    return [str];
  }
  const res = [];
  for (let i = 0; i < str.length; i++) {
    const curr = str[i];
    const restStr = str.slice(0, i) + str.slice(i + 1);
    const remainingPerms = permutations(restStr);
    for (let j = 0; j < remainingPerms.length; j++) {
      const currStr = curr + remainingPerms[j];
      if (res.indexOf(currStr) < 0) res.push(currStr);
    }
  }
  return res;
}
```

---

### 24. Simple Fun #120: Range Collapse Representation

#### instructions

##### Task

A range-collapse representation of an array of integers looks like this: `"1,3-6,8"`, where `3-6` denotes the range from `3-6`, i.e. `[3,4,5,6]`.

Hence `"1,3-6,8"` = `[1,3,4,5,6,8]`. Some other range-collapse representations of `[1,3,4,5,6,8]` include `"1,3-5,6,8", "1,3,4,5,6,8", etc`.

Each range is written in the following format `"a-b"`, where `a < b`, and the whole range must belong to the array in an increasing order.

You are given an array arr. Your task is to find the number of different range-collapse representations of the given array.

Example
For `arr = [1,3,4,5,6,8]`, the result should be `8`.

`"1,3-4,5,6,8"  "1,3-4,5-6,8"  "1,3-5,6,8"  "1,3-6,8"  "1,3,4-5,6,8"  "1,3,4-6,8"  "1,3,4,5-6,8"  "1,3,4,5,6,8"`

Input/OutPut
`[input]` integer array `arr`
sorted array of different positive integers.

`[output]` an integer
the number of different range-collapse representations of the given array.

#### solutions

```js
function factorial(n) {
  if (n <= 1) {
    return 1;
  }
  return n * factorial(n - 1);
}

function getCombination(m, n) {
  return factorial(n) / (factorial(n - m) * factorial(m));
}

function getRangeResult(arr = []) {
  if (arr.length === 1) {
    return 1;
  } else {
    const gap = arr[arr.length - 1] - arr[0];
    let count = 0;
    for (let i = 0; i <= gap; i++) {
      count += getCombination(i, gap);
    }
    return count;
  }
}

// A range string `1-5` can be considered as `1-2-3-4-5` connected with five `-` symbol
// Since there are 4 gaps between two numbers in range string `1,2,3,4,5`
// The challenge could transform into a combination problem: *How many combinations are there to place a hyphen between two numbers?*
// The answer is: `Sum( C(0,n), C(1,n), ... , C(n,n) )`
// Finally, don't forget to multiply all the results of range

function descriptions(arr = []) {
  if (arr.length < 1) {
    return 0;
  }
  const result = [];
  // build the ranges
  let tempArr = [];
  for (let i = 0; i < arr.length; i++) {
    const current = arr[i];
    const next = arr[i + 1];
    tempArr.push(current);
    if (next === undefined || current + 1 < next) {
      result.push(getRangeResult(tempArr));
      tempArr = [];
    }
  }
  if (tempArr.length) {
    result.push(getRangeResult(tempArr));
  }
  // end of building the ranges
  const res = result.reduce((pre, next) => {
    return pre * next;
  }, 1);
  return res;
}
```

#### the better solutions

```js
// key 1: `Sum( C(0,n), C(1,n), ... , C(n,n) ) === 2 ^ n`,
// key 2: `res_1 * res_2 * ... * res_n = 2 ^ (res_1 + res_2 + ... + res_n) 
// key 3: What you need is to calculate how many gaps between all numbers are in the range
// key 4: the answer is `2 ^ gaps`
const descriptions = array) =>
  2 ** array.reduce((perv, curr, i) => prev + Number(array[i + 1] - curr === 1), 0);
```

---

### 25. So Many Permutations!

#### link

[https://www.codewars.com/kata/5828b9455421a4a4e8000007/train/javascript](https://www.codewars.com/kata/5828b9455421a4a4e8000007/train/javascript)

#### instructions

Given a certain number, how many multiples of three could you obtain with its digits?

Suposse that you have the number 362. The numbers that can be generated from it are:

```
362 ----> 3, 6, 2, 36, 63, 62, 26, 32, 23, 236, 263, 326, 362, 623, 632 
```

But only:

`3, 6, 36, 63` are multiple of three.

We need a function that can receive a number ann may output in the following order:

- the amount of multiples

- the maximum multiple

Let's see a case the number has a the digit 0 and repeated digits:

```
6063 ----> 0, 3, 6, 30, 36, 60, 63, 66, 306, 360, 366, 603, 606, 630, 636, 660, 663, 3066, 3606, 3660, 6036, 6063, 6306, 6360, 6603, 6630
```
In this case the multiples of three will be all except 0

```
6063 ----> 3, 6, 30, 36, 60, 63, 66, 306, 360, 366, 603, 606, 630, 636, 660, 663, 3066, 3606, 3660, 6036, 6063, 6306, 6360, 6603, 6630
```

The cases above for the function:

```
find_mult_3(362) == [4, 63]

find_mult_3(6063) == [25, 6630]
```

In Javascript `findMult_3()`. The function will receive only positive integers (num > 0), and you don't have to worry for validating the entries.

Features of the random tests:

```
Number of test = 100
1000 ≤ num ≤ 100000000
```
Enjoy it!!


#### solutions

```js
function getNums(number = 0) {
  return number.toString().split('').map((numStr) => parseInt(numStr, 10));
}

function getCombinations(arr = []) {
  const result = [];
  function generateCombo(prefix, remaining) {
    if (prefix !== '') {
      const res = parseInt(prefix, 10)
      if (result.indexOf(res) < 0) {
        result.push(res);
      }
    }
    for (let i = 0; i < remaining.length; i++) {
      generateCombo(prefix + remaining[i], remaining.slice(0, i).concat(remaining.slice(i + 1)));
    }
  }
  generateCombo('', arr.map(String));
  return result.sort((a, b) => a - b);
}

function canMod3(numbers) {
  const nums = numbers.toString().split('').map((numStr) => parseInt(numStr, 10));
  const res = nums.reduce((pre, curr) => pre + curr, 0);
  if (res === 0) {
    return false;
  }
  return res % 3 === 0;
}

function findMult_3(num) {
  const result = getCombinations(getNums(num)).filter((i) => canMod3(i));
  const length = result.length;
  return [length, result[length - 1]]
}
```

#### the better solutions

```js
function* f(s,r=''){
  yield +r
  for (let i=0;i<s.length;i++){
    yield* f(s.slice(0,i)+s.slice(i+1),r+s[i])
  }
}

function findMult_3(n){
  let s = new Set()
  for (let p of f(n+'')){
    if (p && p%3===0) s.add(p)
  }
  return [s.size,Math.max(...s)]
}
```

---

### 26. The latest clock

#### link
[https://www.codewars.com/kata/58925dcb71f43f30cd00005f/train/javascript](https://www.codewars.com/kata/58925dcb71f43f30cd00005f/train/javascript)

#### instructions

Write a function which receives 4 digits and returns the latest time of day that can be built with those digits.

The time should be in `HH:MM` format.

Examples:
```
digits: 1, 9, 8, 3 => result: "19:38"
digits: 9, 1, 2, 5 => result: "21:59" ("19:25" is also a valid time, but 21:59 is later)
```

Notes
- Result should be a valid 24-hour time, between `00:00` and `23:59`.
- Only inputs which have valid answers are tested.

#### solutions

```js
function permutations(str) {
    if (str.length === 1) {
        return [str];
    }
    const res = [];
    for (let i = 0; i < str.length; i++) {
        const curr = str[i];
        const restStr = str.slice(0, i) + str.slice(i + 1);
        const remainingPerms = permutations(restStr);
        for (let j = 0; j < remainingPerms.length; j++) {
            const currStr = curr + remainingPerms[j];
            if (res.indexOf(currStr) < 0) res.push(currStr);
        }
    }
    return res;
}

function latestClock(a, b, c, d) {
    const [clock] = permutations(`${a}${b}${c}${d}`).sort((a, b) => parseInt(b, 10) - parseInt(a, 10)).filter((str) => {
        const [hour1, hour2, minite1] = str.split('').map((i) => parseInt(i, 10))
        if (hour1 > 2) {
            return false
        }
        if (hour1 === 2 && hour2 > 3) {
            return false
        }
        if (minite1 > 5) {
            return false
        }
        return true
    })
    return `${clock[0]}${clock[1]}:${clock[2]}${clock[3]}`
}
```

#### the better solutions

```js

// smart but not clean XD

function latestClock(a, b, c, d) {
  const times = [
    `${a}${b}:${c}${d}`,
    `${a}${b}:${d}${c}`,
    `${a}${c}:${b}${d}`,
    `${a}${c}:${d}${b}`,
    `${a}${d}:${b}${c}`,
    `${a}${d}:${c}${b}`,
    `${b}${a}:${c}${d}`,
    `${b}${a}:${d}${c}`,
    `${b}${c}:${a}${d}`,
    `${b}${c}:${d}${a}`,
    `${b}${d}:${a}${c}`,
    `${b}${d}:${c}${a}`,
    `${c}${a}:${b}${d}`,
    `${c}${a}:${d}${b}`,
    `${c}${b}:${a}${d}`,
    `${c}${b}:${d}${a}`,
    `${c}${d}:${a}${b}`,
    `${c}${d}:${b}${a}`,
    `${d}${a}:${b}${c}`,
    `${d}${a}:${c}${b}`,
    `${d}${b}:${a}${c}`,
    `${d}${b}:${c}${a}`,
    `${d}${c}:${a}${b}`,
    `${d}${c}:${b}${a}`,
  ];
  const time = times.filter(el => {
    const test = el.split(":")
    if (test[0] >= 24) return false
    if (test[1] >= 60) return false
    return true
  })
  time.sort((a, b) =>  (b.split(":")[0] - a.split(":")[0] || b.split(":")[1] - a.split(":")[1]))
  return time[0]
}

```
---
### 27. Text align justify

#### link
[https://www.codewars.com/kata/text-align-justify/train/javascript](https://www.codewars.com/kata/text-align-justify/train/javascript)

#### instructions

Your task in this Kata is to emulate text justification in monospace font. You will be given a single-lined text and the expected justification width. The longest word will never be greater than this width.

Here are the rules:

- Use spaces to fill in the gaps between words.
- Each line should contain as many words as possible.
- Use '\n' to separate lines.
- Gap between words can't differ by more than one space.
- Lines should end with a word not a space.
- '\n' is not included in the length of a line.
- Large gaps go first, then smaller ones ('Lorem--ipsum--dolor--sit-amet,' (2, 2, 2, 1 spaces)).
- Last line should not be justified, use only one space between words.
- Last line should not contain '\n'
- Strings with one word do not need gaps ('somelongword\n').

Example with width=30:

```
Lorem  ipsum  dolor  sit amet,
consectetur  adipiscing  elit.
Vestibulum    sagittis   dolor
mauris,  at  elementum  ligula
tempor  eget.  In quis rhoncus
nunc,  at  aliquet orci. Fusce
at   dolor   sit   amet  felis
suscipit   tristique.   Nam  a
imperdiet   tellus.  Nulla  eu
vestibulum    urna.    Vivamus
tincidunt  suscipit  enim, nec
ultrices   nisi  volutpat  ac.
Maecenas   sit   amet  lacinia
arcu,  non dictum justo. Donec
sed  quam  vel  risus faucibus
euismod.  Suspendisse  rhoncus
rhoncus  felis  at  fermentum.
Donec lorem magna, ultricies a
nunc    sit    amet,   blandit
fringilla  nunc. In vestibulum
velit    ac    felis   rhoncus
pellentesque. Mauris at tellus
enim.  Aliquam eleifend tempus
dapibus. Pellentesque commodo,
nisi    sit   amet   hendrerit
fringilla,   ante  odio  porta
lacus,   ut   elementum  justo
nulla et dolor.
```

Also you can always take a look at how justification works in your text editor or directly in HTML (css: text-align: justify).

Have fun :)

#### solution

```javascript

function justify(text = "", width) {
  const arr = text.split(" ") || [];
  let result = "";
  let prevLinesArr = [];
  let prevTotal = 0;


  for (let i = 0; i < arr.length; i++) {
    const currItem = arr[i]
    const currWordLength = currItem.length;

    if (prevTotal + currWordLength + prevLinesArr.length > width) {
      result += `${alignSingleLine(prevLinesArr, width, prevTotal)}\n`;
      prevLinesArr = [currItem]
      prevTotal = currItem.length
    } else {
      prevLinesArr.push(arr[i])
      prevTotal += currWordLength
    }
  }
  if (prevLinesArr.length) {
    result += `${prevLinesArr.join(' ')}`;
  }

  return result;
}

function alignSingleLine(arr, width = 0, total = 0) {
  const gapCount = arr.length - 1;
  if (total === 0 || gapCount === 0) {
    return arr[0].toString();
  }
  if (total + gapCount > width) {
    return "";
  }

  const baseGap = Math.floor((width - total) / gapCount);
  const remainGaps = (width - total) % gapCount;

  const gapArr = Array(gapCount).fill(baseGap);

  for (
    let i = 0, remainGapsCount = remainGaps;
    i < gapArr.length;
    i++, remainGapsCount--
  ) {
    if (remainGapsCount === 0) {
      break;
    }
    gapArr[i] = gapArr[i] + 1;
  }
  let result = ""
  arr.forEach((item, index) => {
    if (index === arr.length - 1) {
      result += item.toString()
    }
    else {
      const gapStr = ' '.repeat(gapArr[index])
      result += (item + gapStr)
    }
  })
  return result
}

```

#### the better solutions

```javascript
/**
 * @param {String} str - inital string
 * @param {Number} len - line length
 */
function justify(str, len) {
  var words = str.split(' ');
  var lines = [];
  var lastLine = words.reduce(function(line, word) {
    if (line) {
      if (line.length + word.length + 1 <= len)
        return line + ' ' + word;
      lines.push(line);
    }
    return word;
  });
  lines = lines.map(function(line) {
    if (line.indexOf(' ') >= 0)
      for (var lineLen = line.length; lineLen < len; )
        line = line.replace(/ +/g, function(spaces) {
          return spaces + (lineLen++ < len ? ' ' : '');
        });
    return line;
  });
  lastLine && lines.push(lastLine);
  return lines.join('\n');
}
```
---

### 28. Codewars style ranking system

#### instructions

##### description

Write a class called User that is used to calculate the amount that a user will progress through a ranking system similar to the one Codewars uses.

Business Rules:
- A user starts at rank -8 and can progress all the way to 8.
- There is no 0 (zero) rank. The next rank after -1 is 1.
- Users will complete activities. These activities also have ranks.
- Each time the user completes a ranked activity the users rank progress is updated based off of the activity's rank
- The progress earned from the completed activity is relative to what the user's current rank is compared to the rank of the activity
- A user's rank progress starts off at zero, each time the progress reaches 100 the user's rank is upgraded to the next level
- Any remaining progress earned while in the previous rank will be applied towards the next rank's progress (we don't throw any progress away). The exception is if there is no other - rank left to progress towards (Once you reach rank 8 there is no more progression).
- A user cannot progress beyond rank 8.
- The only acceptable range of rank values is -8,-7,-6,-5,-4,-3,-2,-1,1,2,3,4,5,6,7,8. Any other value should raise an error.

The progress is scored like so:

- Completing an activity that is ranked the same as that of the user's will be worth 3 points
- Completing an activity that is ranked one ranking lower than the user's will be worth 1 point
- Any activities completed that are ranking 2 levels or more lower than the user's ranking will be ignored
- Completing an activity ranked higher than the current user's rank will accelerate the rank progression. The greater the difference between rankings the more the progression will beincreased. The formula is `10 * d * d` where `d` equals the difference in ranking between the activity and the user.

Logic Examples:

- If a user ranked -8 completes an activity ranked -7 they will receive 10 progress
- If a user ranked -8 completes an activity ranked -6 they will receive 40 progress
- If a user ranked -8 completes an activity ranked -5 they will receive 90 progress
- If a user ranked -8 completes an activity ranked -4 they will receive 160 progress, resulting in the user being upgraded to rank -7 and having earned 60 progress towards their next rank
- If a user ranked -1 completes an activity ranked 1 they will receive 10 progress (remember, zero rank is ignored)

Code Usage Examples:

```javascript
var user = new User()
user.rank // => -8
user.progress // => 0
user.incProgress(-7)
user.progress // => 10
user.incProgress(-5) // will add 90 progress
user.progress # => 0 // progress is now zero
user.rank # => -7 // rank was upgraded to -7
```

##### note
Codewars no longer uses this algorithm for its own ranking system. It uses a pure Math based solution that gives consistent results no matter what order a set of ranked activities are completed at.

#### solution

```javascript
class User {
    constructor() {
        this.rankLevel = [-8, -7, -6, -5, -4, -3, -2, -1, 1, 2, 3, 4, 5, 6, 7, 8];
        this.rankPos = 0;
        this.progress = 0;
        this.rank = this.rankLevel[this.rankPos];
    }

    rankUp(pos = 0) {
        const maxPos = this.rankLevel.length - 1;
        if ((this.rankPos + pos) >= maxPos) {
            this.rankPos = maxPos;
            this.progress = 0;
        }
        else {
            this.rankPos += pos;
        }
        this.rank = this.rankLevel[this.rankPos];
    }

    incProgress(level) {
        const levelPos = this.rankLevel.indexOf(level);
        const variance = levelPos - this.rankPos;
        if (levelPos === -1 || variance <= -2) {
            throw Error()
        }
        else if (variance === -1) {
            this.addProgress(1);
        }
        else if (variance === 0) {
            this.addProgress(3);
        }
        else if (variance > 0) {
            this.addProgress(10 * variance * variance);
        }
    }

    addProgress(count) {
        const nextProgress = this.progress + count;
        const levels = Math.floor(nextProgress / 100);
        this.progress = nextProgress % 100;
        this.rankUp(levels);
    }
}
```

#### the better solutions

```javascript
class User{
  constructor(){
    this.RANK = [-8,-7,-6,-5,-4,-3,-2,-1,1,2,3,4,5,6,7,8];
    this.pos=0;
    this.rank = this.RANK[this.pos];
    this.progress = 0;
  }
  incProgress(taskRank){
    taskRank = this.RANK.indexOf(taskRank);
    if(taskRank < 0) throw ("error");
    let diff = taskRank - this.pos;
    
         if(diff ==  0) this.progress+=3;
    else if(diff >   0) this.progress += diff*diff*10;
    else if(diff == -1) this.progress += 1;
    // new rank & progress
    this.pos += Math.floor(this.progress/100);
    this.progress = this.progress%100;
    if(this.pos >= 15) {this.pos = 15; this.progress = 0;}
    this.rank = this.RANK[this.pos];
  } 
}
```
---
