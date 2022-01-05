# JavaScript Kata

## Menu

## Content

### 1. Array.diff JavaScript Translation

#### link

[https://www.codewars.com/kata/523f5d21c841566fde000009](https://www.codewars.com/kata/523f5d21c841566fde000009)

#### description

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

#### description

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

### 4. A square of squares

#### description

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

#### description
Return the number (count) of vowels in the given string.

We will consider `a`, `e`, `i`, `o`, `u` as vowels for this Kata (but not `y`).

The input string will only consist of lower case letters and/or spaces.

#### solution
```js
function getCount(str) {
    const regex=/[aeiou]/g;
    const matches=str.match(regex)
    const vowelsCount = matches?matches.length:0;
    return vowelsCount;
}
```

#### the better solution
```js
function getCount(str){
    return (str.match(/[aeiou]/ig)||[]).length;
}
```
---

### 6. Playing with digits

#### description

Some numbers have funny properties. For example:
```plain
89 --> 8¹ + 9² = 89 * 1

695 --> 6² + 9³ + 5⁴= 1390 = 695 * 2

46288 --> 4³ + 6⁴+ 2⁵ + 8⁶ + 8⁷ = 2360688 = 46288 * 51
```

Given a positive integer n written as abcd... (a, b, c, d... being digits) and a positive integer p

we want to find a positive integer `k`, if it exists, such as the sum of the digits of `n` taken to the successive powers of `p` is equal to `k * n`.
In other words:

> Is there an integer k such as : (a ^ p + b ^ (p+1) + c ^(p+2) + d ^ (p+3) + ...) = n * k

If it is the case we will return `k`, if not return `-1`.

Note: `n` and `p` will always be given as strictly positive integers.
```js
digPow(89, 1) should return 1 since 8¹ + 9² = 89 = 89 * 1
digPow(92, 1) should return -1 since there is no k such as 9¹ + 2² equals 92 * k
digPow(695, 2) should return 2 since 6² + 9³ + 5⁴= 1390 = 695 * 2
digPow(46288, 3) should return 51 since 4³ + 6⁴+ 2⁵ + 8⁶ + 8⁷ = 2360688 = 46288 * 51
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

#### description

Write a function that takes an integer as input, and returns the number of bits that are equal to one in the binary representation of that number. You can guarantee that input is non-negative.

##### Example
The binary representation of `1234` is `10011010010`, so the function should return `5` in this case

#### solution
```js
const countBits = function (n) {
    const res=n.toString(2);
    console.log(res)
    return res.split('').reduce((acc, curr) => (curr*1) ? acc + 1 : acc, 0)
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

#### description
Given two arrays `a` and `b` write a function `comp(a, b)` (or `compSame(a, b)` ) that checks whether the two arrays have the "same" elements, with the same multiplicities (the multiplicity of a member is the number of times it appears). "Same" means, here, that the elements in `b` are the elements in `a` squared, regardless of the order.

##### examples

**Valid arrays**
```js
a = [121, 144, 19, 161, 19, 144, 19, 11]  
b = [121, 14641, 20736, 361, 25921, 361, 20736, 361]
```

`comp(a, b)` returns true because in `b` 121 is the square of 11, 14641 is the square of 121, 20736 the square of 144, 361 the square of 19, 25921 the square of 161, and so on. It gets obvious if we write `b`'s elements in terms of squares:

```js
a = [121, 144, 19, 161, 19, 144, 19, 11] 
b = [11*11, 121*121, 144*144, 19*19, 161*161, 19*19, 144*144, 19*19]
```

**Invalid arrays**
If, for example, we change the first number to something else, `comp` is not returning true anymore:
```js
a = [121, 144, 19, 161, 19, 144, 19, 11]  
b = [132, 14641, 20736, 361, 25921, 361, 20736, 361]
```
`comp(a,b)` returns `false` because in `b` 132 is not the square of any number of `a`.

```js
a = [121, 144, 19, 161, 19, 144, 19, 11]  
b = [121, 14641, 20736, 36100, 25921, 361, 20736, 361]
```
`comp(a,b)` returns `false` because in `b` 36100 is not the square of any number of `a`.

**Remarks**
`a` or `b` might be `[] or {}` (all languages except R, Shell).
`a` or `b` might be `nil` or `null` or `None` or `nothing` (except in C++, Crystal, D, Dart, Elixir, Fortran, F#, Haskell, Nim, OCaml, Pascal, Perl, PowerShell, Prolog, PureScript, R, Racket, Rust, Shell, Swift).
If `a` or `b` are `nil` (or `null` or `None`, depending on the language), the problem doesn't make sense so return false.

**Note for C**
The two arrays have the same size `(> 0)` given as parameter in function `comp`.


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
    let i = 0, length = aMap.length;
    for (; i < length; i++) {
        if (array2.length === 0) {
            return false;
        }
        const pos = array2.indexOf(aMap[i]);
        if (pos < 0) {
            return false
        }
        else {
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