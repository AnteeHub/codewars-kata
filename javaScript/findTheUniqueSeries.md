# Find The Unique Series in JavaScript Kata

## Menu
1. [Find the unique number](#1-find-the-unique-number)
2. [Find the unique string](#2-find-the-unique-string)
3. [Find the unique](#3-find-the-unique)

## Content


### 1. Find the unique number

#### link
[https://www.codewars.com/kata/585d7d5adb20cf33cb000235](https://www.codewars.com/kata/585d7d5adb20cf33cb000235)

#### instructions
There is an array with some numbers. All numbers are equal except for one. Try to find it!
```js
findUniq([ 1, 1, 1, 2, 1, 1 ]) === 2
findUniq([ 0, 0, 0.55, 0, 0 ]) === 0.55
```
It’s guaranteed that array contains at least 3 numbers.

The tests contain some very huge arrays, so think about performance.

#### solution
```js
function findUniq(arr) {
    return arr.find(i => {
        return arr.indexOf(i) === arr.lastIndexOf(i)
    })
}
```
---
### 2. Find the unique string

#### link
[https://www.codewars.com/kata/585d8c8a28bc7403ea0000c3/javascript](https://www.codewars.com/kata/585d8c8a28bc7403ea0000c3/javascript)

#### instructions
There is an array of strings. All strings contains similar letters except one. Try to find it!

```js
findUniq([ 'Aa', 'aaa', 'aaaaa', 'BbBb', 'Aaaa', 'AaAaAa', 'a' ]) === 'BbBb'
findUniq([ 'abc', 'acb', 'bac', 'foo', 'bca', 'cab', 'cba' ]) === 'foo'
```

Strings may contain spaces. Spaces is not significant, only non-spaces symbols matters. E.g. string that contains only spaces is like empty string.

It’s guaranteed that array contains more than 3 strings.

#### solution
```js
function findUniq(arr) {
    const processArr = arr.map((str) => {
        return [...new Set(str.toLowerCase().split(''))].sort().join('')
    })
    const res = processArr.find((item) => {
        return processArr.indexOf(item) === processArr.lastIndexOf(item)
    })
    const index = processArr.indexOf(res);
    return arr[index]
}
```
---

### 3. Find The Unique

#### link
[https://www.codewars.com/kata/5862e0db4f7ab47bed0000e5](https://www.codewars.com/kata/5862e0db4f7ab47bed0000e5)

#### instructions

There is an array. All elements are the same except for one. Try to find it!
```js
findUniq([ 1, 1, 1, 2, 1, 1 ]) === 2
findUniq([ 4, 4, 'foo', 4 ]) === 'foo'
```
It’s guaranteed that array contains more than 3 elements. Array may contain anything (including `NaN`).

#### solution
```js
function findUniq(arr) {
    const keyMap = new Map()
    arr.forEach((item) => {
        const count = keyMap.get(item);
        keyMap.set(item, count ? count + 1 : 1)
    })
    return [...keyMap].find(([key, count]) => {
        return count === 1
    })[0]; // return [key, count]
}
```
---