# Why this guide?

A lot of self-taught programmers or bootcamp graduates are not as strong (myself included) in algorithm as a CS graduate. I hope this guide will be found by many to be a helpful supplement for those who has little former knowledge of algorithm complexities, including myself.

If you find a typo, conceptual error, or think you could reword some phrases better, feel free to submit a pull request or email me at letsmailiggy@gmail.com. If you have additional content ideas, please feel free to discuss it with me.

# Who is it for?
I originally intend this guide for bootcamp graduate job-seekers and self-taught developers, but I hope everyone will benefit from this (even a little).

## Efficiency

Computers are not magic *(although it still feels like it sometimes)*. They have limitations. It is best practice to always keep in mind whenever you create an algorithm to optimize their runtime and memory usage: "how can I use the least memory and make it run as fast as possible?". If a function takes up 100ATU (Arbitrary Time Unit) and 100 AMU (Arbitrary Memory Unit) for a user to execute it, it may not be a big deal. However, if your web has 10,000 users who are executing 10 requests per second, imagine how much more performant it will be if we can reduce the time and space cost even by 10%.

When I was attending bootcamp, I started hearing about **big-O** notation. I had no idea what it was but apparently it is a big deal.

## Big-O Examples

**Big-O** notation is generally used to estimate time (amount of computations/ how fast) and space (amount of memory used) complexity of an algorithm. **Big-O** measures worst-case scenario.

### Time and Space Units

**Time Unit**

The following are equal one "time unit":
- Mathematical equation (`1+2`, `i++`)
- Printing or returning something (`console.log('hello')`, `return 10`)
- Instantiating new variable (`let foo = 'bar';`, `const bar = baz`)
- Accessing an item in an Array  (`arr[i]`)
- Boolean comparison (`hello !== true`)

Essentially, anytime you are executing something other than a function, you can assume it costs one time unit.

**Space Unit**

The following are roughly equal one "space unit":

- Creating a single variable, empty array, or object (`var i = 1`, `let obj = {}`, `const arr = []`)
- Adding a *new* key-value pair into a hashtable or array (`obj[bar] = 'baz';`, `arr.push(10)`)

Essentially, when you are creating a single variable/ instantiating a blank array or object, you are taking up a space somewhere in the memory that costs a space unit.

### Some examples

I find myself understanding **Big-O** best when I see examples.

```
//example1
function logArray(arr){
  for(var i = 0; i < arr.length; i++){
    console.log(arr[i]);  
  }
}
```

The function above has a **Big-O** complexity of **O(n)** because it iterates through every single array element **once**.

Let's inspect them line-by-line:

1. `var i = 0;` contains one operation
2. `i < (arr.length)` contains two operations (the comparison, `<`, plus `arr.length`)
3. `console.log(arr[i])` contains two operations: one for `console.log` and another one to look up an array value `arr[i]`.

Since we are dealing with `for` loop, the amount of operations will increase as the array input gets larger. If array contains 10 elements, it will loop 10 times. The calculations becomes:

`1 + 10 * 4 = 41 operations.`

If the array contains 1,000,000 elements, it will loop a million times, and so on. **Big-O** values will always depend, linearly, on the array size. Hence it is **O(n)**.


```
//example2
function logNestedArray(arr){
  for(var i = 0; i < arr.length; i++){
    for(var j = i; j < arr.length; j++){
      console.log(arr[i] + arr[j])
    }
  }
}
```

The **Big-O** above is **O(n^2)** because it contains a `for` loop inside a `for` loop (one nested loop).

A good rule of thumb is, whenever you see a loop inside loop, **Big-O** will probably be n polynomial, whereas the polynomial is the amount of nested loops. So if it were to be like:

```
for (var i = 0; i < arr.length; i++){
  for (var j = 0; j < arr.length; j++){
    for (var k = 0; k < arr.length; k++){
      for(var l = 0; l < arr.length; l++){
        //do something
      }
    }  
  }
}
```

If you guessed **O(n^4)**, you're right. If you ever find yourself nesting 3 levels deep or more, then you are probably a horrible human being. I would highly **discourage** any nesting deeper than 2 levels deep.

```
//example3
function logLastElement(arr){
  console.log(arr[arr.length-1]);
}
```

**Big-O** above is **O(1)** because it does not loop.

1. `console.log()` counts as one operation.
2. `arr[arr.length - 1]` counts as three operations: one for `arr.length`, one for `- 1` operation, and one for `arr[...]`.

Keep in mind that we don't say **O(4)** but **O(1)**. Another rule of thumb in **Big-O** calculation is we **always drop the constant coefficients to 1**. The important picture here is that regardless how big the array is, it does not make it slower to execute the function. We can have an array size of 10 or 1,000,000, but all the function does is to print out the last array element.


```
//example4
function logArrayTwice(arr){
  for(var i = 0; i < arr.length; i++){
    console.log(arr[i]);
  }
  for(var j = arr.length - 1; j >= 0; j--){
    console.log(arr[j]);
  }
}
```

Recall that although we are looping the array twice, the loops are not nested. **O(2n)** becomes **O(n)**. **Nested loops multiply while un-nested loops add**.

Not all loops have **n** value. Some loops have constant values. For example:

```
function logArrayTenTimes(arr){
  var i = 0;
  if(arr.length >= 10){
    while(i < 10){
      console.log(arr[i]);
      i++;
    }
  }
}
```

The function above loops the array 10 times regardless array size of 1,000,000 or 100. Since it is only looping 10 times and does not depend on array size, it is not **O(n)** but **O(1)**.

### Chunking

Over time, you will learn to approximate **Big-O** values just by looking at them. In reality, people usually only care for the highest value, not the small ones. For example, if you estimate a **Big-O** of **O(2n^2 + 8n + 5)**, you can look at it as **O(n^2)**. First, we remove smaller variables: **8n** and **5**, leaving us with **O(2n^2)**. After dropping the coefficient, we get only **O(n^2)** left. We would say that such function has a **Big-O** of **O(n^2)**.

The goal of knowing Big-O is to create codes with the lowest Big-O value as possible. Avoid nesting too many loops.  
