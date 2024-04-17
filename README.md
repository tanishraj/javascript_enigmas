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

### Answer:

`true`. `==` operator in javascript only compares the values and not the type hence it will log `true`.

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

### Answer:

`start`
`middle`
`1`
`end`
`success`

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

## Contributing

Pull requests are welcome. If you want to add any output based questions that you want to share with others, feel free to do so.

## License

[MIT](https://choosealicense.com/licenses/mit/)
