# Objects

## Literal

```js
var cat = { 
    name: "Fluffly", 
    color: "White",
    speak: function() { console.log("Meow") }
}
```

## Constructor Functions

```js
function Cat(name, color) {
    this.name = name;
    this.color = color;
}

var cat = new Cat("Fluffy", "White");
```

## Object Create

- Enumerable: Displays the property in object iterators and affects Json serialization
- Writable: Sets if the property will be editable or not
- Configurable: Sets if we can change the property configurations. Once it's true, it can never be turned off.

```js
var cat = Object.create(Object.prototype, {
    name: {
        value: 'Fluffy',
        enumerable: true,
        writable: true,
        configurable: true
    },
    color: {
        value: 'White',
        enumerable: true,
        writable: true,
        configurable: true
    }
})
```

## ES6 Classes

```js
class Cat {
    constructor(name, color) {
        this.name = name;
        this.color = color;
    }

    speak() {
        console.log('Meow');
    }
}

var cat = new Cat('Fluffy', 'White');
```

# Usaful Operators

- Shows property configuration: 
`Object.getOwnPropertyDescriptior(cat, 'name');`

- Sets Object Property:
`Object.defineProperty(cat, 'name', {writable: true})`

- Freezes a Object:
`Object.freeze(cat.name)`

- Check what Class a object belongs: `cat instanceof animal`

# Getters and Setters

```js
Object.defineProperty(cat, 'fullname', {
    get: function() {
        return this.name.first + ' ' + this.name.last;
    },
    set: function(value) {
        var nameParts = value.split(' ');
        this.name.first = nameParts[0];
        this.name.last = nameParts[1];
    }
})
```

# Inheritance

## Prototype Introdution

```js
Object.defineProperty(Array.prototype, 'last', {
    get: function() {
        return this[this.length - 1]
    }
})

var arr = [1, 2, 3];
console.log(arr.last); // 3
```

## Prototypal Inheritance

```js
function Animal(voice) {
    this.voice = voice || 'grunt';
}
Animal.prototype.speak = function() {
    console.log(this.voice);
}

function Cat(name, color) {
    Animal.call(this, 'Meow');
    this.name = name;
    this.color = color;
}
Cat.prototype = Object.create(Animal.prototype);
Cat.prototytpe.constructor = Cat;
Cat.prototype.age = 4;

var fluffy = new Cat('Fluffy', 'White');
console.log(fluffy.age); // 4
fluffy.speak(); // Grunt
console.log(fluffy.hasOwnProperty('age')); // False
```

## ES6 Class Inheritance

```js
class Animal {
    constructor(voice){
        this.voice = voice || 'grunt'
    }

    speak() {
        console.log(this.voice);
    }
}

class Cat extends Animal {
    constructor(name, color){
        super('Meow');
        this.name = name;
        this.color = color;
    }
}

var fluffy = new Cat('Fluffy', 'White');
```