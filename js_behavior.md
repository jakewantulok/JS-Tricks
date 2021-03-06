# JS Behavior

## Adding Strings & Numbers

JavaScript isn't the most reliable when it comes to some operations. 

### Example

`"11" +  11`

We would hope that this equals to `22`, but this is not the case. 

`Result: "1111"`

Instead of performing an numeric operation, JS will disregard the different data types of these two operands, and treats this as a concatenation of two strings.

Interesting enough, we do not see this issue when we subtract.

`"11" - 11`

As you can see we get exactly what we need.

`Result: 0`

### One Solution: Subtract first

You can subtract `1` from the string `"11"` and add `1` to retain its value.

`Result: 11` It's no longer a string!

So...

```js
"11" - 1 + 1 + 11

= 22
```

One thing to note, however, you must subtract by `1` before adding by `1` or else you will once again concatenate operands and create another issue rather than solving one.

### Better Solution: Unary Operator

We can take this idea one step further and simplify this.

```js
+"11"

// Result
> 11

+"11" + 11

// Result
> 22
```

## Converting to a String

Because of how JavaScript concatenates an integer with a string, you can utilize this opportunity to quickly convert a integer *as* a string if you needed to.

### Example

`1`

### Solution 

```js
1 + ""

"1" // Now it's a string!
```

## Decimals

JavaScript isn't good with decimals either. 

`150.90 * 6`

You would hope the answer would come to `905.40`.
However...

Result: `905.4000000000001`

### Solution: Whole Numbers

Convert the number to a whole number and convert it back to its true output.

```js
150.9 * 100 * 6 /100

905.4 // result
```

## Objects

In JavaScript, `null` is considered as an object. So using `typeof` can be tricky.

```js
var test = null;
console.log(typeof test === "object");

> true
```

This is a safer way to check!

```js
console.log((typeof nullObj === null) && (typeof test === "object"));
> false
```

## Functions

```js
function test1()
{
  return {
      bar: "hello"
  };
}

function test2()
{
  return
  {
      bar: "hello"
  };
}

console.log(test1());
> Object { bar: "hello" };

console.log(test2());
> undefined // or might throw an error
```

What's going on? Well, when `test2()` is ran after `test1()` a semicolon is added between return and the object.

```js
function test2()
{
  return; /* <--- this will add a semicolon!
  {
      bar: "hello"
  };
}
```

The bracket has been ignored so a semicolon was added right after `return` in `test2()`, making the rest of the code unreachable. A good way to avoid this is wrapping everything in parenthesis `()` for our `return`. Also, staying consistent is key.

```js
function test1()
{
  return ({
      bar: "hello"
  });
}

function test2()
{
  return (
  { // even if it differs, it will still work
      bar: "hello"
  });
}

console.log(test1());
> Object { bar: "hello" };

console.log(test2());
> Object { bar: "hello" };
```