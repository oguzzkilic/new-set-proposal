# New Set Proposal

Set, ADT (Abstract Data Types) grubundan bir veri yapısıdır. Aynı zamanda matematik paradigmalarından referans alınan bir veri grubudur ve kümeyi referans alır.

## Overview

Tıpkı matematikte olduğu gibi **unorder** veya **unindex** olarak dizilirler. Her eleman **benzersizdir**.

Matematikte **{1,2,3}** şeklinde dizilirler. Programlamada array tabanlı **set** çoğu zaman **[1,2,3]** şeklinde kullanılmaktadır.

Küme, bir kadın çantasına benzer. İçinde ne olduğu bellidir ancak hangi sırayla yerleştirildiği belli değildir. İnsan, hayvan, telefon numaraları veya kategoriler birer set elemanı olabilir. Kesiştiği noktalar ve ayrıştığı noktalar olabilir.

İçi boş olan **Set** matematikte **0** döndürürken, programlamada genellikle **false** döndürür.

Set değişebilir. Ekleme ve silme yapılabilir. **Frozen** olan set ile (örn: Python) değiştirme işlemi yapılamaz.

JavaScript'de **Set** her türde değer ve referans veri tipini içerisinde barındırabilir. Bir **Array** kendisi gibi farklı referans tiplerini içerisinde barındırabiliyorsa **Set**'de barındırabilir.

Bir çok programlama dilinde **Array** içerisinde referans barındıramayız. **Set** özelliğini en iyi kullanan programalama dillerinden **Pascal** ve **Perl** örnek olarak gösterilebilir.

## Motivasyon
JavaScript'te yer alan **Set** Matematikte tanımlanan **Set** ile aynı özellikleri barındırmamaktadır. Daha uzun kodlar yazarak bu işlemleri gerçekleştirebiliyoruz. Performans ve implementasyon açısından bakıldığında daha fazla efor sarfetmemiz gerekiyor. Farklı dillerde varsayılan Set metodlarının JavaScript'te de olması gerekliliktir. Harici kütüphaneler kullanmadan daha efektif bir şekilde zamandan tasarruf edilebilir.

### Set.prototype.union
İki Set'i birleştirerek yeni bir Set oluşturmak için aşağıdaki gibi bir yol izlememiz gerekmektedir;

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
ya da Lodash, Underscore gibi yardımcı kütüphaneler kullanmak zorundayız.

Varsayımsal olarak iki Set verisini aşağıdaki gibi birleştirebiliriz;

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

İki **Set** arasındaki farkı şu şekilde ifade ederiz;
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
İki **Set**'in kesişimini şu şekilde ifade ederiz,
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
