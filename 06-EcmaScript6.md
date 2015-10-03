# JavaScript.next
## JavaScript History
* JavaScript is a front-end scripting language developed by Netscape for dynamic content
  * Lightweight, but with limited capabilities
  * Can be used as object-oriented language
  * Embedded in your HTML page
  * Interpreted by the Web browser
* Client-side, mobile and desktop technology
* Simple and flexible
* Powerful to manipulate the DOM

## Using JavaScript.next
* There are a few ways to use JavaScript.next today
  * Enable tags in Chrome and Firefox
  * Compile to JavaScript 5 using Traceur or Babel
  
```javascript
var babel = require('gulp-babel');

gulp.task('build', function() {
  return gulp.src('src/**/*.js')
    .pipe(babel())
    .pipe(gulp.dest('dist'));
});
```

* ES6 introduces new ways to declare variables:
  * ```let``` – creates a scope variable
  * ```const``` – creates a constant variable
* ES6 supports templated strings

```javascript
let people = [new Person('Lionel', 'Nguyen')];
for(let person of people){
   log(`Fullname: ${person.fname} ${person.lname}`);
}
```

* ES6 adds a new feature (rule) to the way of defining properties:

```javascript
let name = 'Lionel Nguyen',
    age = 25;
let person = {
  name,
  age
};
```

* Destructuring assignments allow to set values to objects in an easier way:

```javascript
let [a,b] = [1,2]; //a = 1, b = 2
let [x, , y] = [1, 2, 3] // x = 1, y = 3
let [first, second, ...rest] = people;
let person = {
  name: 'Doncho Minkov',
  address: {
    city: 'Sofia',
    street: 'Aleksander Malinov'
  }
};

let {name, address: {city}} = person;
```

## For-of loop
* The for-of loop iterates over the values
  * Of an array

```javascript
let sum = 0;
for(let number of [1, 2, 3]) {
  sum += number;
}
```

  * Of An iteratable object
  
```javascript
function* generator(maxValue) {
  for(let i = 0; i < maxValue; ++i){
    yield i;
  }
}
let iter = generator(10);
for(let val of iter()) {
  console.log(val);
}
```

## Classes and Inheritance in ES6
* ES6 introduces classes and a way to create classical OOP

```javascript
class Person extends Mammal {
  constructor(fname, lname, age) {
    super(age);
    this._fname = fname;
    this._lname = lname;
  }
  get fullname() {
    //getter property of fullname
  }
  set fullname(newFullName) {
    //setter property of fullname
  }
  // more class members…
}
```

## Arrow Functions
* Also called Lambda expressions

```javascript
numbers.sort((a, b) => b – a);
```

* Arrow functions easify the creation of functions:

```javascript
var fullnames2 = people.filter(p => p.age >= 18).map(p => p.fullname);
```

## ES6 supports modules
* ES6 supports modules
  * A way to write JavaScript in different files
    * Each file has its own scope (not the global)
    * Each file decides what to export from its module
  * Export the objects you want from a module:
  
```javascript
export { Person, Mammal };
```

  * To use the module in another file:
  
```javascript
import { Person, Mammal } from './person';
```