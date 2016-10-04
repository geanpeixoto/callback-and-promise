# callbacks & promises

## revisão

#### types

```javascript
var int = 10; // number

var string = 'my string'; // string

// named function
function myFunction() {
  console.log('my-function');
}

var myFunction2 = myFunction; // function

 // anonymous function
var myFunction3 = function() {
  console.log('another-function');
};

myFunction(); // console: "my-function"
myFunction2(); // console: "my-function"
myFunction3(); // console: "another-function"
```

#### closures

```javascript
var number = 10;
function myFunction() {
  var inner = 'inner';
  console.log(number++, string);
}
myFunction(); // console: 10, undefined
var string = "my string";
myFunction(); // console: 11, "my string"
console.log(inner); // ReferenceError: inner is not def
```

#### async functions

```javascript
var input = 'my-input'
setTimeout(function() {
  console.log(input);
}, Math.trunc(Math.random()*1000));
```

```javascript
setTimeout(function() {
  console.log('inner', value);
}, 0);
console.log('out', value);
var value = 0;

// O que aparecerá no console primeiro?
// Qual o valor que [[value]] assumirá?
```

## callbacks

```javascript
/**
 * Irá executar o [[callback]] após 1 segundo
 * @param {Function} callback método que será executado
 */
var i = 0;
function asyncMethod(input, callback) {
  setTimeout(function() {
    callback([i++].concat(input));
  }, 1000);
}

asyncMethod('input', function(input1) {
  console.log(input1); // console: [0, 'input']
});
```

```javascript
asyncMethod('input', function(i) {
  console.log(i); // console: [0, 'input']
  asyncMethod(i, function(input2) {
    console.log(input2); // console: [1, 0, 'input']
    asyncMethod(input2, function(input3) {
      console.log(input3); // console: [2, 1, 0, 'input']
      asyncMethod(input3, function(input4) {
        console.log(input4); // console: [3, 2, 1, 0, 'input']
        asyncMethod(i, function(r) {
          console.log(r); // console: [4, 0, 'input']
        });
      });
    });
  });
});
```

## promises
