# New Set Proposal

Set is a data structure from the ADT (Abstract Data Types) group. It is also a data group referred to from mathematical paradigms and refers to the set. 

## Overview

Just like in mathematics, they are arranged unordered or unindexed. Each element is unique. In mathematics, they are arranged in the form of {1,2,3}. In programming, an array-based set is usually used in the form of [1,2,3].

When an empty Set returns in mathematics 0, in programming it usually returns false.

The set can be changed. Addition and removal can be made. With frozen set (e.g. Python), modification cannot be done.

In JavaScript, Set can contain values and reference data types of any type. If an Array can contain different reference types, Set can contain them.

In many programming languages, we can't contain references in Array. Pascal and Perl are examples of languages that best use the Set feature.

## Motivation
JavaScript does not have the same features as the Set defined in Mathematics. We can accomplish these tasks by writing longer codes, but from a performance and implementation perspective, we need to put in more effort. It is necessary for there to be default Set methods in JavaScript, just like in other languages, so that we can save time without using external libraries.

### Set.prototype.union
To create a new Set by combining two Sets, we must follow the following path;

`X ∪ Y = { x | x ∈ X or x ∈ Y}`

![union](https://res.cloudinary.com/duxhkuady/image/upload/v1531746857/ArraySet/union.png)

#### python
```py
A = {1, 2, 3, 4}
B = {2, 3}
C = {3, 4, 5, 6}

print('A U B =', A.union(B))
print('B U C =', B.union(C))

print('A U B U C =', A.union(B, C))

print('A.union() = ', A.union())
```

```py
A U B = {1, 2, 3, 4}
B U C = {2, 3, 4, 5, 6}
A U B U C = {1, 2, 3, 4, 5, 6}
A.union() =  {1, 2, 3, 4}
```

#### js old:
```js
var setA = new Set([1, 2, 3, 4]),
    setB = new Set([2, 3]),
    setC = new Set([3, 4, 5, 6]);
    
function union(setA, setB) {
    var _union = new Set(setA);
    for (var elem of setB) {
        _union.add(elem);
    }
    return _union;
}
```
```js
union(setA, setC);
```
We need to utilize helper libraries like Lodash, Underscore, etc.

We can combine two sets of data theoretically as follows;

#### js new:

**variant 1:**
```js
var setA = new Set([1, 2, 3, 4]),
    setB = new Set([2, 3]),
    setC = new Set([3, 4, 5, 6]);
    
var union = setA.union(setC);
```

**variant 2:**
```js
var setA = new Set([1, 2, 3, 4]),
    setB = new Set([2, 3]),
    setC = new Set([3, 4, 5, 6]);
    
var unionPrototype = Set.prototype.union(setA, setC);
console.log(unionPrototype);
```

### Set.prototype.difference
*Relative Complement:

The difference between two Sets can be expressed as follows;
`X - Y = { x | x ∈ X and x ∉ Y}`

![difference](https://res.cloudinary.com/duxhkuady/image/upload/v1531749343/ArraySet/difference.png)


#### python:
```py
A = {1, 2, 3, 4}
B = {3, 4, 5, 6}

# Equivalent to A-B
print(A.difference(B))
```

#### js old:
```js
var setA = new Set([1, 2, 3, 4]),
    setC = new Set([3, 4, 5, 6]);
    
function difference(setA, setB) {
    var _difference = new Set(setA);
    for (var elem of setB) {
        _difference.delete(elem);
    }
    return _difference;
}
```
```js
difference(setA, setC);
```

#### js new:
```js
var setA = new Set([1, 2, 3, 4]),
    setC = new Set([3, 4, 5, 6]);
    
setA.difference(setC);
```

### Set.prototype.common
We can express the intersection of two Sets as follows.
`X ∩ Y = { x | x ∈ X and x ∈ Y}`

#### python:
```py
A = {2, 3, 5, 4}
B = {2, 5, 100}
C = {2, 3, 8, 9, 10}

print(B.intersection(A))
print(B.intersection(C))
print(A.intersection(C))
print(C.intersection(A, B))
```

#### js old:
```js
var setA = new Set([1, 2, 3, 4]),
    setB = new Set([2, 3]),
    setC = new Set([3, 4, 5, 6]);
    
function common(setA, setB) {
    var _common = new Set();
    for (var elem of setB) {
        if (setA.has(elem)) {
            _common.add(elem);
        }
    }
    return _common;
}
```
```js
common(setA, setC);
```

#### js new:
```js
var setA = new Set([1, 2, 3, 4]),
    setB = new Set([2, 3]),
    setC = new Set([3, 4, 5, 6]);
    
var common = Set.prototype.common(setA, setC);
