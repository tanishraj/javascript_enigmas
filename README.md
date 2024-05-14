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

### Question 13:

What will be the output for below javascript code?

```javascript
let x = [0, 1, [2]];
x[2][0] = 3;
console.log(x);
```

### Output:

`[0, 1, [3]]`

### Explanation:

- The variable x was initialized with the array [0, 1, [2]].

- The expression `x[2][0]` accessed the nested array `[2]` inside `x`, which is located at index `2`. Then, it accessed the element at index `0` of that nested array, which was `2`.

- The assignment `x[2][0] = 3` replaced the value `2` with `3` inside the nested array.

- After the modification, the nested array became `[3]`, and the overall `x` array became `[0, 1, [3]]`.

- Finally, `console.log(x)` printed the updated value of `x`, which is `[0, 1, [3]]`.

##

### Question 14:

What will be the output for below javascript code?

```javascript
(function () {
  var a = (b = 3);
})();

console.log("a defined? " + (typeof a !== undefined));
console.log("b defined? " + (typeof b !== undefined));
console.log("b value is ", b);
console.log("a value is ", a);
```

### Output:

`a defined? true`

`b defined? true`

`b value is 3`

`ReferenceError: a is not defined`

### Explanation:

Since both the `a` and `b` is defined inside the functional scope most of the developer would expect both `a` and `b` to be undefined outside of the function scope.

Most of the developers think, that `var a = b = 3` is equivalent to `var b = 3; var a = b;`. But thats not how javascript treats this statement. Instead, javascript treats this code as `b = 3; var a = b;`

So, `b` is defined without `var` keyword so it will be accessible outside of the functional scope as it will be treated as a global variable but `a` is defined with `var` keyword it can not be accessed outside of the functional scope. and hence it will be `Reference Error`.

##

### Question 15:

What will be the output for below javascript code?

```javascript
var myObject = {
  foo: "bar",
  func: function () {
    var self = this;
    console.log("outer func:  this.foo = " + this.foo);
    console.log("outer func:  self.foo = " + self.foo);
    (function () {
      console.log("inner func:  this.foo = " + this.foo);
      console.log("inner func:  self.foo = " + self.foo);
    })();
  }
};
myObject.func();
```

### Output:

`outer func:  this.foo = bar`

`outer func:  self.foo = bar`

`inner func:  this.foo = undefined`

`inner func:  self.foo = bar`

### Explanation:

In the outer function, both `this` and `self` refer to `myObject` and therefore both can properly reference and access `foo`.

In the inner function, though, this no longer refers to `myObject`. As a result, `this.foo` is `undefined` in the inner function, whereas the reference to the local variable `self` remains in scope and is accessible there.

##

### Question 16:

What will be the output for below javascript code?

```javascript
function foo1() {
  return {
    bar: "hello"
  };
}

function foo2() {
  return;
  {
    bar: "hello";
  }
}

console.log("foo1 returns:");
console.log(foo1());
console.log("foo2 returns:");
console.log(foo2());
```

### Output:

`foo1 returns:`

`Object {bar: "hello"}`

`foo2 returns:`

`undefined`

### Explanation:

In JavaScript, the automatic semicolon insertion (ASI) mechanism interprets the line break after return as the end of the statement, effectively treating it as `return;`. This means that the function returns undefined and the subsequent object literal is never reached.

When the return statement is encountered in the `foo1()` function, the function immediately returns the `{ bar: "hello" }`. but in 'foo2()' `return` statement will be converted to `return;`, hence will return `undefined`.

##

### Question 17:

What will be the output for below javascript code?

```javascript
console.log(Boolean([]));
console.log(Boolean({}));
console.log(Boolean(""));
console.log(Boolean(0));
```

### Output:

`true`

`true`

`false`

`false`

### Explanation:

1 - An empty array `[]` is considered a `truthy` value in JavaScript. When the Boolean function is called with an array, it returns true because arrays are considered non-empty objects.

2 - An empty object `{}` is also considered a `truthy` value in JavaScript. When the Boolean function is called with an object, it returns true because objects are non-empty.

3 - An empty string `""` is considered a `falsy` value in JavaScript. When the Boolean function is called with an empty string, it returns false.

4 - The number `0` is considered a `falsy` value in JavaScript. When the Boolean function is called with 0, it returns false.

##

### Question 18:

What will be the output for below javascript code?

```javascript
function left() {
  return console.log("left");
}

function right() {
  return console.log("right");
}

left() || right();
```

### Output:

`left`
`right`

### Explanation:

In this code, you have two functions, `left()` and `right()`, that simply log the strings `left` and `right` to the console, respectively. Then, you have the expression `left() || right();`.

The logical `OR operator (||)` in JavaScript works in the following way:

1 - It evaluates the operand on the left side, in this case, `left()`.

2 - If the left operand is `truthy`, it returns the value of the left operand.

3 - If the left operand is `falsy`, it evaluates the right operand, in this case, `right()`.

4 - If the right operand is evaluated, it returns the value of the right operand.

#### In this specific case, when left() || right(); is executed, the following happens:

1 - `left()` is called, which logs `left` to the console.

2 - The `console.log("left");` statement itself returns undefined, which is a `falsy` value.

3 - Since the left operand `left()` is `falsy`, the logical OR operator evaluates the right operand `right()`.

4 - `right()` is called, which logs `right` to the console.

5 - The `console.log("right");` statement also returns undefined, which is a `falsy` value.

6 - Since both operands are `falsy`, the expression `left() || right();` evaluates to the value of the right operand, which is `undefined`.

Therefore, the output of this code will be:

`left` `right`

##

### Question 19:

What will be the output for below javascript code?

```javascript
function counter() {
  let count = 0;
  return () => count++;
}

let c = counter();
console.log(c());
console.log(c());
console.log(c());
```

### Output:

`0` `1` `2`

### Explanation:

The code defines a function `counter` that returns another `function`. The returned function is a closure that has access to the count variable defined inside the `counter` function.

1 - The `counter` function is defined.

2 - Inside `counter`, a variable count is declared and initialized to `0`.

3 - The counter function returns an anonymous arrow `function () => count++`.

- This anonymous function has access to the count variable through closure.
- It increments the count variable and returns its value before incrementing.

4 - The counter function is called, and its returned anonymous function is assigned to the variable c.

5 - `console.log(c());` is executed three times:

- The first time, it logs 0 and increments count to 1.
- The second time, it logs 1 and increments count to 2.
- The third time, it logs 2 and increments count to 3.

This behavior is possible because the anonymous function returned by counter has access to the count variable through closure. Each time the anonymous function is called, it increments and returns the count variable, which is preserved in the closure.

Closures allow functions to have private variables and maintain state across multiple function calls. In this example, the counter function creates a new private count variable each time it is called, and the returned anonymous function has access to that private variable through the closure.

##

### Question 20:

What will be the output for below javascript code?

```javascript
const greeting = "hello";
greeting.length = 10;
console.log(greeting.length);
console.log(greeting);
```

### Output:

`5` `hello`

### Explanation:

In JavaScript, strings are immutable, which means their values cannot be changed once they are created. The program demonstrates this behavior by attempting to modify the length property of a string.

1 - The program declares a constant variable greeting and assigns it the string value "hello".

2 - It then attempts to change the length property of the greeting string by assigning it the value 10 using greeting.length = 10;.

3 - However, this assignment operation has no effect because strings in JavaScript are immutable. The length property of a string is a read-only property that reflects the actual number of characters in the string.

4 - The program then logs the length property of the greeting string using console.log(greeting.length);. Since the previous attempt to modify the length property failed, the output is still 5, which is the original length of the "hello" string.

5 - Finally, the program logs the actual value of the greeting string using console.log(greeting);. As expected, the output is "hello", which is the original string value assigned to greeting.

#### Key Points:

- Strings in JavaScript are immutable, meaning their values cannot be changed after they are created.
- The length property of a string is read-only and reflects the actual number of characters in the string.
- Attempting to modify the length property of a string has no effect, as it is a derived property based on the string's content.

##

### Question 21:

What will be the output for below javascript code?

```javascript
(function () {
  console.log(1);
  setTimeout(function () {
    console.log(2);
  }, 1000);
  setTimeout(function () {
    console.log(3);
  }, 0);
  console.log(4);
})();
```

### Output:

`1` `4` `3` `2`

### Explanation:

- `1` and `4` are displayed first since they are logged by simple calls to `console.log()` without any delay

- `2` is displayed after `3` because `2` is being logged after a delay of `1000 msecs` (i.e., 1 second) whereas 3 is being logged after a delay of `0` msecs.

OK, fine. But if `3` is being logged after a delay of 0 msecs, doesn’t that mean that it is being logged right away? And, if so, shouldn’t it be logged before `4`, since `4` is being logged by a later line of code?

The answer has to do with properly understanding `JavaScript events` and `timing`.

The browser has an event loop which checks the event queue and processes pending events. For example, if an event happens in the background (e.g., a script onload event) while the browser is busy (e.g., processing an onclick), the event gets appended to the queue. When the `onclick` handler is complete, the queue is checked and the event is then handled (e.g., the onload script is executed).

Similarly, `setTimeout()` also puts execution of its referenced function into the event queue if the browser is busy.

When a value of zero is passed as the second argument to `setTimeout()`, it attempts to execute the specified function “as soon as possible”. Specifically, execution of the function is placed on the event queue to occur on the next timer tick. Note, though, that this is not immediate; the function is not executed until the next tick. That’s why in the above example, the call to `console.log(4)` occurs before the call to `console.log(3)` (since the call to `console.log(3)` is invoked via `setTimeout`, so it is slightly delayed).

##

### Question 22:

What will be the output for below javascript code?

```javascript
var arr1 = "john".split("");
var arr2 = arr1.reverse();
var arr3 = "jones".split("");
arr2.push(arr3);
console.log("array 1: length=" + arr1.length + " last=" + arr1.slice(-1));
console.log("array 2: length=" + arr2.length + " last=" + arr2.slice(-1));
```

### Output:

`array 1: length=5 last=j,o,n,e,s`

`array 2: length=5 last=j,o,n,e,s`

### Explanation:

`arr1` and `arr2` are the same (i.e. `['n','h','o','j', ['j','o','n','e','s'] ]`) after the above code is executed for the following reasons:

- Calling an array object’s `reverse()` method doesn’t only return the array in reverse order, it also reverses the order of the array itself (i.e., in this case, `arr1`).

- The `reverse()` method returns a reference to the array itself (i.e., in this case, `arr1`). As a result, `arr2` is simply a reference to (rather than a copy of) `arr1`. Therefore, when anything is done to `arr2` (i.e., when we invoke `arr2.push(arr3);)`, `arr1` will be affected as well since `arr1` and `arr2` are simply references to the same object.

And a couple of side points here that can sometimes trip someone up in answering this question:

- Passing an array to the push() method of another array pushes that entire array as a single element onto the end of the array. As a result, the statement `arr2.push(arr3);` adds `arr3` in its entirety as a single element to the end of `arr2` (i.e., it does not concatenate the two arrays, that’s what the `concat()` method is for).

- Like Python, JavaScript honors negative subscripts in calls to array methods like `slice()` as a way of referencing elements at the end of the array; e.g., a subscript of `-1` indicates the last element in the array, and so on.

##

### Question 23:

What will be the output for below javascript code?

```javascript
console.log(1 + "2" + "2");
console.log(1 + +"2" + "2");
console.log(1 + -"1" + "2");
console.log(+"1" + "1" + "2");
console.log("A" - "B" + "2");
console.log("A" - "B" + 2);
```

### Output:

`122`
`32`
`02`
`112`
`NaN2`
`NaN`

### Explanation:

#### Example 1:

1 + "2" + "2" Outputs: "122" Explanation: The first operation to be performed in 1 + "2". Since one of the operands ("2") is a string, JavaScript assumes it needs to perform string concatenation and therefore converts the type of 1 to "1", 1 + "2" yields "12". Then, "12" + "2" yields "122".

#### Example 2:

1 + +"2" + "2" Outputs: "32" Explanation: Based on order of operations, the first operation to be performed is +"2" (the extra + before the first "2" is treated as a unary operator). Thus, JavaScript converts the type of "2" to numeric and then applies the unary + sign to it (i.e., treats it as a positive number). As a result, the next operation is now 1 + 2 which of course yields 3. But then, we have an operation between a number and a string (i.e., 3 and "2"), so once again JavaScript converts the type of the numeric value to a string and performs string concatenation, yielding "32".

#### Example 3:

1 + -"1" + "2" Outputs: "02" Explanation: The explanation here is identical to the prior example, except the unary operator is - rather than +. So "1" becomes 1, which then becomes -1 when the - is applied, which is then added to 1 yielding 0, which is then converted to a string and concatenated with the final "2" operand, yielding "02".

#### Example 4:

+"1" + "1" + "2" Outputs: "112" Explanation: Although the first "1" operand is typecast to a numeric value based on the unary + operator that precedes it, it is then immediately converted back to a string when it is concatenated with the second "1" operand, which is then concatenated with the final "2" operand, yielding the string "112".

#### Example 5:

"A" - "B" + "2" Outputs: "NaN2" Explanation: Since the - operator can not be applied to strings, and since neither "A" nor "B" can be converted to numeric values, "A" - "B" yields NaN which is then concatenated with the string "2" to yield “NaN2”.

#### Example 6:

"A" - "B" + 2 Outputs: NaN Explanation: As exlained in the previous example, "A" - "B" yields NaN. But any operator applied to NaN with any other numeric operand will still yield NaN.

##

### Question 24:

What will be the output for below javascript code?

```javascript
function getValue1() {
  this.value = 10;
  function printValue() {
    console.log(this.value);
  }

  printValue();
}

function getValue2() {
  this.value = 10;
  var printValue = () => {
    console.log(this.value);
  };

  printValue();
}

var value = 20;
new getValue1();
new getValue2();
```

### Output:

`undefined`
`10`

### Explanation:

The provided JavaScript code demonstrates the concept of this keyword and its behavior in different contexts, specifically within regular functions and arrow functions.

- In the `getValue1` function, `this.value` is assigned the value of `10`. However, inside the nested printValue function, the `this` keyword refers to the global object (window in browsers) because regular functions create their own this binding. When printValue is called, it logs the value of `this.value` from the global context, which is initially undefined (because no such property exists on the global object). Therefore, the output will be `undefined`.

- In the `getValue2` function, this.value is assigned the value of `10`, similar to `getValue1`. However, the `printValue` function is defined as an arrow function. Arrow functions do not create their own this binding. Instead, they inherit the this value from the surrounding lexical scope, which in this case is the `getValue2` function. When `printValue` is called, it logs the value of `this.value` from the `getValue2` function's context, which is `10`.

##

### Question 25:

What will be the output for below javascript code?

```javascript
console.log("0 || 1 = " + (0 || 1));
console.log("1 || 2 = " + (1 || 2));
console.log("0 && 1 = " + (0 && 1));
console.log("1 && 2 = " + (1 && 2));
```

### Output:

`0 || 1 = 1`

`1 || 2 = 1`

`0 && 1 = 0`

`1 && 2 = 2`

### Explanation:

In JavaScript, both `||` and `&&` are logical operators that return the first fully-determined `logical value` when evaluated from left to right.

The or `||` operator. In an expression of the form `X||Y`, `X` is first evaluated and interpreted as a boolean value. If this boolean value is `true`, then `true` `1` is returned and `Y` is not evaluated, since the `or` condition has already been satisfied. If this boolean value is `false`, though, we still don’t know if `X||Y` is true or false until we evaluate `Y`, and interpret it as a boolean value as well.

Accordingly, `0 || 1` evaluates to true `1`, as does `1 || 2`.

The and `&&` operator. In an expression of the form `X&&Y`, `X` is first evaluated and interpreted as a boolean value. If this boolean value is false, then false `0` is returned and `Y` is not evaluated, since the `and` condition has already failed. If this boolean value is `true`, though, we still don’t know if `X&&Y` is true or false until we evaluate `Y`, and interpret it as a boolean value as well.

However, the interesting thing with the `&&` operator is that when an expression is evaluated as `true`, then the expression itself is returned. This is fine, since it counts as `true` in logical expressions, but also can be used to return that value when you care to do so. This explains why, somewhat surprisingly, `1 && 2` returns `2` (whereas you might it expect it to return true or `1`).

##

### Question 26:

What will be the output for below javascript code?

```javascript
console.log(false == "0");
console.log(false === "0");
```

### Output:

`true`
`false`

### Explanation:

In JavaScript, there are two sets of equality operators. The triple-equal operator `===` behaves like any traditional equality operator would: evaluates to true if the two expressions on either of its sides have the same type and the same value. The double-equal operator, however, tries to coerce the values before comparing them. It is therefore generally good practice to use the `===` rather than `==`. The same holds true for `!==` vs `!=`.

##

### Question 27:

What will be the output for below javascript code?

```javascript
var a = {},
  b = { key: "b" },
  c = { key: "c" };

a[b] = 123;
a[c] = 456;

console.log(a[b]);
```

### Output:

`456`

### Explanation:

When setting an object property, JavaScript will implicitly stringify the parameter value. In this case, since `b` and `c` are both objects, they will both be converted to `[object Object]`. As a result, `a[b]` and `a[c]` are both equivalent to `a["[object Object]"]` and can be used interchangeably. Therefore, setting or referencing `a[c]` is precisely the same as setting or referencing `a[b]`.

##

### Question 28:

What will be the output for below javascript code?

```javascript
var a = 2;
a++;
console.log(a);

const d = [1, 2, 3];
d.push(5);
console.log(d);

const b = 2;
b++;
console.log(b);

const c = [2];
c[0]++;
console.log(c);
```

### Output:

`3`

`[1, 2, 3, 5]`

`TypeError: Assignment to constant variable.`

### Explanation:

- The reason why the output is `3` is because the increment operation `a++` is performed before the `console.log(a)` statement. If the increment operator was used before the variable `(++a)`, it would return the incremented value `(3)`.

- Even though `d` is a constant variable, the contents of the array can be modified. The constant nature of d only prevents re-assigning a new value to the variable itself, but it doesn't make the array immutable. Therefore, when you run this code, it will output: `[1, 2, 3, 5]`

- Since `b` is a constant variable, b++ is trying to assign the incremented value to a constant. which is not allowed, since it will throw an error. `TypeError: Assignment to constant variable.`

- And Since, we got an error in our program, 4 set of problem wont be executed. But if you will run that individually then it is going to output `[3]`

##

## Contributing

Pull requests are welcome. If you want to add any output based questions that you want to share with others, feel free to do so.

## License

[MIT](https://choosealicense.com/licenses/mit/)
