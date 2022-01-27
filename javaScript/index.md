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
arrayDiff([1, 2], [1]) == [2]
```

If a value is present in `b` , all of its occurrences must be removed from the other:

```js
arrayDiff([1, 2, 2, 2, 3], [2]) == [1, 3]
```

#### solution

```js
function arrayDiff(a, b) {
    return a.reduce((acc, curr) => {
        return !b.includes(curr) ? [...acc, curr] : acc
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
    } while (curr !== 0)
    return sum >= 10 ? digital_root(sum) : sum;
}
```

#### the better solutions

```js
function digital_root(n) {
    return (n - 1) % 9 + 1;
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
            return `${names[0] ? names[0] : 'no one'} likes this`;
        case 2:
            return `${names.join(' and ')} like this`;
        case 3:
        case 4:
        default:
            const [first, second, ...rest] = names;
            return `${first}, ${second} and ${rest.length > 1 ? rest.length + ' others' : rest[0]} like this`;
    }
}
```

#### a crazy but strong solution

```js
function likes(peopleNames) {
    var feels = new FeelingsParty('like', 'this');
    for (var name in peopleNames) feels.addFeeler(new Person(peopleNames[name]));
    return feels.shareTheseFeelings();
}

function Person(name) {
    this.name = name;
}

Person.prototype.getName = function() {
    return this.name;
}

function FeelingsParty(emotion, target) {
    this.emotionalContext = emotion;
    this.emotionalSubject = target;
    this.peopleFeelingThisWay = [];
    this.numPeopleFeelingThisWay = 0;
}

FeelingsParty.prototype.getEmotionalContext = function() {
    return this.type;
}

FeelingsParty.prototype.addFeeler = function(person) {
    this.numPeopleFeelingThisWay++;
    this.peopleFeelingThisWay.push(person);
}

FeelingsParty.prototype.shareTheseFeelings = function() {
    this.findTheRightWords();
    if (this.numPeopleFeelingThisWay == 0) return 'no one ' + this.emotionalContext + ' ' + this.emotionalSubject;
    if (this.numPeopleFeelingThisWay == 1) return '' + this.peopleFeelingThisWay[0].getName() + ' ' + this.emotionalContext + ' ' + this.emotionalSubject;
    if (this.numPeopleFeelingThisWay == 2) return '' + this.peopleFeelingThisWay[0].getName() + ' and ' + this.peopleFeelingThisWay[1].getName() + ' ' + this.emotionalContext + ' ' + this.emotionalSubject;
    if (this.numPeopleFeelingThisWay == 3) return '' + this.peopleFeelingThisWay[0].getName() + ', ' + this.peopleFeelingThisWay[1].getName() + ' and ' + this.peopleFeelingThisWay[2].getName() + ' ' + this.emotionalContext + ' ' + this.emotionalSubject;
    return '' + this.peopleFeelingThisWay[0].getName() + ', ' + this.peopleFeelingThisWay[1].getName() + ' and ' + (this.numPeopleFeelingThisWay - 2) + ' others ' + this.emotionalContext + ' ' + this.emotionalSubject;
}

FeelingsParty.prototype.findTheRightWords = function() {
    if (this.numPeopleFeelingThisWay == 0 || this.numPeopleFeelingThisWay == 1) this.emotionalContext += 's';
}
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
var isSquare = function(n) {
    return parseInt(Math.sqrt(n)) === Math.sqrt(n);
}
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
    const matches = str.match(regex)
    const vowelsCount = matches ? matches.length : 0;
    return vowelsCount;
}
```

#### the better solution

```js
function getCount(str) {
    return (str.match(/[aeiou]/ig) || []).length;
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

> Is there an integer k such as : (a ^ p + b ^ (p+1) + c ^(p+2) + d ^ (p+3) + ...) = n * k

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
        return acc + Math.pow(curr, (index + p));
    }, 0)

    return powers % n === 0 ? powers / n : -1
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
const countBits = function(n) {
    const res = n.toString(2);
    console.log(res)
    return res.split('').reduce((acc, curr) => (curr * 1) ? acc + 1 : acc, 0)
};
```

#### the better solution

```js
countBits = n => n.toString(2).split('0').join('').length;
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
a = [121, 144, 19, 161, 19, 144, 19, 11]
b = [121, 14641, 20736, 361, 25921, 361, 20736, 361]
```

`comp(a, b)` returns true because in `b` 121 is the square of 11, 14641 is the square of 121, 20736 the square of 144, 361 the square of 19, 25921 the square of 161, and so on. It gets obvious if we write `b` 's elements in terms of squares:

```js
a = [121, 144, 19, 161, 19, 144, 19, 11]
b = [11 * 11, 121 * 121, 144 * 144, 19 * 19, 161 * 161, 19 * 19, 144 * 144, 19 * 19]
```

**Invalid arrays**
If, for example, we change the first number to something else, `comp` is not returning true anymore:

```js
a = [121, 144, 19, 161, 19, 144, 19, 11]
b = [132, 14641, 20736, 361, 25921, 361, 20736, 361]
```

`comp(a,b)` returns `false` because in `b` 132 is not the square of any number of `a` .

```js
a = [121, 144, 19, 161, 19, 144, 19, 11]
b = [121, 14641, 20736, 36100, 25921, 361, 20736, 361]
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
        return false
    }
    if (array1.length === 0 && array2.length === 0) {
        return true;
    }
    if (array1.length === 0 || array2.length === 0 || (array1.length !== array2.length)) {
        return false
    }
    const aMap = array1.map((i) => i * i)
    let i = 0,
        length = aMap.length;
    for (; i < length; i++) {
        if (array2.length === 0) {
            return false;
        }
        const pos = array2.indexOf(aMap[i]);
        if (pos < 0) {
            return false
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
    array1.every(item => {
        const index = array2.indexOf(Math.pow(item, 2))
        return index > -1 ? array2.splice(index, 1) : false
    })
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
        const flag = str.indexOf(str[i]) === str.lastIndexOf(str[i])
        if (flag) {
            return s[i]
        }
    }
    return ''
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
    if (walk && walk.length !== 10)
        return false;
    let horizontal = 0;
    let vertical = 0;
    let distance = 0;
    const MATCH_DISTANCE = 10;
    walk.forEach((item) => {
        distance++;
        switch (item) {
            case 'w':
                horizontal--;
                break;
            case 'e':
                horizontal++;
                break;
            case 'n':
                vertical++;
                break;
            case 's':
                vertical--;
                break;
        }
    })
    return distance + Math.abs(horizontal) + Math.abs(vertical) === MATCH_DISTANCE;
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
deleteNth([1, 1, 1, 1], 2) // return [1,1]
deleteNth([20, 37, 20, 21], 1) // return [20,37,21]
```

#### solution

```js
function deleteNth(arr, n) {
    let countMap = new Map();
    return arr.filter((item) => {
        const count = countMap.get(item) || 0;
        countMap.set(item, count ? count + 1 : 1); // make sure count >= 1
        return count < n; // 'count' changed after got the value of Map.get(item)
    })
}
```

#### the better solution

```js
function deleteNth(a, x) {
    let m = {}; // no using Map()
    return a.filter(v => (m[v] = m[v] + 1 || 1) <= x);
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
var helper = new PaginationHelper(['a', 'b', 'c', 'd', 'e', 'f'], 4);
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
}

// returns the number of pages
PaginationHelper.prototype.pageCount = function () {
    return Math.ceil(this.collection.length / this.itemsPerPage);
}

// returns the number of items on the current page. page_index is zero based.
// this method should return -1 for pageIndex values that are out of range
PaginationHelper.prototype.pageItemCount = function (pageIndex) {
    if (this.collection.length === 0) {
        return 0;
    }
    const rest = this.collection.length - (this.itemsPerPage * pageIndex);
    if (rest < 0)
        return -1;
    return rest > this.itemsPerPage ? this.itemsPerPage : rest;
}

// determines what page an item is on. Zero based indexes
// this method should return -1 for itemIndex values that are out of range
PaginationHelper.prototype.pageIndex = function (itemIndex) {
    if (itemIndex > this.collection.length || itemIndex < 0 || itemIndex === undefined || this.collection.length === 0)
        return -1;
    const perPage = isNaN(this.itemsPerPage) ? this.collection.length : this.itemsPerPage;
    const indexBase = Math.ceil(itemIndex / perPage);
    if (indexBase === 0) {
        return 0;
    }
    return indexBase - 1;
}
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
    const arr = text.toLowerCase().match( /(?!')[a-z']+/gi)||[];
    const map = arr.reduce((map, item) => {
        return map.set(item, (map.get(item) || 0) + 1)
    }, new Map())
    return [...map].sort((a, b) => b[1] - a[1]).slice(0,3).map(i => i[0].toLowerCase());
}
```
---



Roman Numerals Encoder

#### instructions

Create a function taking a positive integer as its parameter and returning a string containing the Roman Numeral representation of that integer.

Modern Roman numerals are written by expressing each digit separately starting with the left most digit and skipping any digit with a value of zero. In Roman numerals 1990 is rendered: `1000=M, 900=CM, 90=XC` ; resulting in `MCMXC` . 2008 is written as `2000=MM, 8=VIII` ; or `MMVIII` . 1666 uses each Roman symbol in descending order: `MDCLXVI` .

Example:

```js
solution(1000); // should return 'M'
```

Help:

```plain
Symbol    Value
I          1
V          5
X          10
L          50
C          100
D          500
M          1,000
```

Remember that there can't be more than 3 identical symbols in a row.

More about roman numerals - [http://en.wikipedia.org/wiki/Roman_numerals](http://en.wikipedia.org/wiki/Roman_numerals)

#### solution

```js
function solution(number) {}
```

  转换  	  为罗马数字  	  罗马数字至今  	  仍存在  
1808
1000	M	M	808
500	D	MD	308
100	C	MDC	208
100	C	MDCC	108
100	C	MDCCC	8
5	V	MDCCCV	3
1	I	MDCCCVI	2
1	I	MDCCCVII	1
1	I	MDCCCVIII	0
