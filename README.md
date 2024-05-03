# Javascript Enigmas - Odds of Javascript:

- Contains output based questions for javascript.
- Example explains the odds of javascript.

##

### Question 1:

What will be the output for below javascript code?

```javascript
var a = 10;
var b = "10";
console.log(a == b);
```

### Output:

`true`.

### Explanation:

`==` operator in javascript only compares the values and not the type hence it will log `true`.

##

### Question 2:

What will be the output for below javascript code?

```javascript
console.log("start");

const fn = () =>
  new Promise((resolve, reject) => {
    console.log(1);
    resolve("success");
  });

console.log("middle");

fn().then((res) => {
  console.log(res);
});

console.log("end");
```

### Output:

`start`
`middle`
`1`
`end`
`success`

### Explanation:

Since Javascript is a single threaded language, it can process only one statement at a time. Also we know that Promises are async code that will be kept aside in the task queue to be executed later until the main thread / synchronous code is executed.

Now you might think that `fn()` is executed then the Promise will be push the callback queue but here is a catch, Promise does not go to the callback queue, its the `then()` function which is a special kind of callback function that receives the resolved value.

So when we call `fn()` it creates a new Promise object and also takes a executor function and finds out that there is a `console.log()` which is synchronous code, so it will be executed right away and then `resolve()` will provide the value for it's `then()` method to use the value as response.

So, below are the order the output will be printed...

1. Log "start"
2. Function declared
3. Log "middle"
4. Calling function fn(): will log "1" and resolve "success" as a value which will be executed later once the main thread is executed.
5. Log "end"
6. Main thread is completed, now promise value will be printed "success"

##

### Question 3:

What will be the output for below javascript code?

```javascript
const a = [{ name: "John" }, { name: "Jane" }];

const b = [...a];

b[0] = { name: "Oliver" };
b[1].age = 30;

console.log(a);
console.log(b);
```

### Output:

a = `[ { name: 'John' }, { name: 'Jane', age: 30 } ]`

b = `[ { name: 'Oliver' }, { name: 'Jane', age: 30 } ]`

### Explanation:

1. `const a = [{name: "John"}, {name: "Jane"}]` - Creates a variable `a` with an array that contains 2 objects.
2. `const b = [...a];` - Creates a shallow copy of `a`, where reference of objects is being copied to variable `b`.
3. `b[0] = {name: "Oliver"}` - Replacing the first object in variable `b` with a brand new object, without affecting the variable `a`.
4. `b[1].age = 30;` - Now updating the second object inside variable `b` which is the reference of second object in variable `a`, will update the values in both `a` and `b` as they both are referencing to the same object.

##

### Question 4:

What will be the output for below javascript code?

```javascript
var x = 5;
var y = 2;
console.log(x ** y);
```

### Output:

`25`

### Explanation:

The `**` operator is used for exponentiation in JavaScript. which is equal to `Math.pow(5,2)`. `**` is called exponential operator.

##

### Question 5:

What will be the output for below javascript code?

```javascript
function getTotal(...args) {
  console.log(typeof args);
}

getTotal(871);
```

### Output:

`object`

### Explanation:

When you use `...args` as a parameter, it creates an array named args within the function that will hold all the arguments passed to the function. So, even though you call `getTotal(871)`, the args array will still contain that single argument `(871)` as an array element. And as `typeof Array` is object.

##

### Question 6:

What will be the output for below javascript code?

```javascript
const a = [1, 2, 3];
const b = a;
a.push(4);

console.log(b.length);
```

### Output:

`4`

### Explanation:

1. `const a = [1, 2, 3];` creates a constant variable named a and assigns an array literal containing the numbers 1, 2, and 3 to it.
2. `const b = a;` creates another constant variable named b and assigns the value of a to it. However, it's important to understand that this is not copying the array elements. Instead, it's creating a new reference (or alias) that points to the same array object in memory. Both a and b now refer to the same array.
3. `a.push(4);` uses the push method to add the number 4 to the end of the array that a (and consequently b) refers to. Since a and b point to the same array, this modification affects both variables.
4. `console.log(b.length);` logs the length of the array using b.length. Because a and b refer to the same modified array, this will print: `4`

##

### Question 7:

What will be the output for below javascript code?

```javascript
const obj = { prop: 10 };
const arr = [obj];
arr[0].prop = 20;

console.log(obj.prop);
```

### Output:

`20`

### Explanation:

1. `const obj = { prop: 10 };` creates a constant object named obj with a single property named prop that has the value 10.
2. `const arr = [obj];` creates a constant array named `arr` and assigns a single element to it. That element is a reference to the obj object you created earlier. It's important to remember that you're not copying the object itself, but rather creating a new reference in the array that points to the same object in memory.
3. `arr[0].prop = 20;` accesses the first element of the arr array (which is the reference to the obj object) and modifies the prop property within that object to have a value of `20`. Because `arr[0]` and obj both refer to the same object, this change is reflected in both.
4. `console.log(obj.prop);` logs the value of the prop property within the obj object. Since you modified the property in step 3, this will print: `20`.

##

### Question 8:

What will be the output for below javascript code?

```javascript
console.log("5" - "3");
console.log("5" - 3);
console.log(5 - "3");
```

### Output:

`2` for all logs.

### Explanation:

In JavaScript, the code console.log("5" - "3"); will output 2. This might seem complex at first, because subtraction typically deals with numbers. However, JavaScript has a behavior where it tries to convert operands (the values used in an operation) to a common type before performing the operation.

In this example, JavaScript attempts to convert both "5" and "3" to numbers before performing the subtraction. Similarly, for all other instances it does the same thing.

##

### Question 9:

What will be the output for below javascript code?

```javascript
function doSomething() {
  return;
  {
    success: true;
  }
}
console.log(doSomething());
```

### Output:

`undefined`

### Explanation:

In JavaScript, the automatic semicolon insertion (ASI) mechanism interprets the line break after return as the end of the statement, effectively treating it as `return;`. This means that the function returns undefined and the subsequent object literal is never reached.

When the return statement is encountered in the `doSomething` function, the function immediately exits and returns `undefined` by default (if no value is explicitly returned). The object literal `{ success: true }` on the next line is never evaluated or returned because the function has already exited.

##

### Question 10:

What will be the output for below javascript code?

```javascript
console.log(false ?? "Some Truthy Value");
console.log(undefined ?? "Some Truthy Value");
console.log(null ?? "Some Truthy Value");
console.log(NaN ?? "Some Truthy Value");
```

### Output:

`false`
`Some Truthy Value`
`Some Truthy Value`
`NaN`

### Explanation:

This is a concept of javascript called, `Nullish coalescing operator ??`. So as per `MDN` definition, The `nullish coalescing (??)` operator is a logical operator that returns its right-hand side operand when its left-hand side operand is `null` or `undefined`, and otherwise returns its left-hand side operand.

So whenever the left operand is either `undefined` or `null` it will return the right operand as an output or else the left operand itself will be returned.

##

### Question 11:

What will be the output for below javascript code?

```javascript
console.log(false || "Some Truthy Value");
console.log(undefined || "Some Truthy Value");
console.log(null || "Some Truthy Value");
console.log(NaN || "Some Truthy Value");
console.log(NaN || NaN || false);
console.log(true || "Some Truthy Value" || false);
```

### Output:

`Some Truthy Value`
`Some Truthy Value`
`Some Truthy Value`
`Some Truthy Value`
`false`
`true`

### Explanation:

The logical `OR operator (||)` evaluates the operands from left to right and returns the first `truthy` value it encounters. If no `truthy` value is found, it returns the last operand. This behaviour is often used for providing default values.

##

### Question 12:

What will be the output for below javascript code?

```javascript
console.log(0.1 + 0.2);
console.log(0.1 + 0.2 == 0.3);
```

### Output:

`0.30000000000000004`
`false`

### Explanation:

`console.log(0.1 + 0.2);` This line performs an addition operation between two decimal numbers, `0.1` and `0.2`. It then logs the result of this operation to the console.

In most programming languages, including JavaScript, floating-point arithmetic operations can sometimes produce unexpected or imprecise results due to the way computers represent and store decimal numbers internally. This is because decimal numbers like `0.1` and `0.2` cannot be represented precisely in binary format.

`console.log(0.1 + 0.2 == 0.3)` This line also performs the addition `0.1 + 0.2`, but it then compares the result with the value `0.3` using the strict equality operator `==`.

Due to the imprecise representation of floating-point numbers mentioned earlier, the result of `0.1 + 0.2` is not exactly equal to `0.3`. Therefore, when you run this line, the output in the console will be `false`.

##

## Contributing

Pull requests are welcome. If you want to add any output based questions that you want to share with others, feel free to do so.

## License

[MIT](https://choosealicense.com/licenses/mit/)
