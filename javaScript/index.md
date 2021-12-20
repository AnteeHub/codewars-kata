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


