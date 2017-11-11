# Why this guide?

A lot of self-taught programmers or bootcamp graduates are not as strong (myself included) in algorithm as a CS graduate. I hope this guide will be found by many to be a helpful supplement for those who has little former knowledge of algorithm complexities, including myself.

If you find a typo, conceptual error, or think you could reword some phrases better, feel free to submit a pull request or email me at letsmailiggy@gmail.com.

# Who is it for?
I originally intend this guide for bootcamp graduate job-seekers and self-taught developers, but everyone will benefit (even a little)

## Computing Efficiency

Computers are not magic *(although it still feels like it sometimes)*. They have limitations. It is best practice to always keep in mind whenever you create an algorithm to optimize their runtime and memory usage: "how can I use the least memory and make it run as fast as possible?". If a function takes up 100ATU (Arbitrary Time Unit) and 100 AMU (Arbitrary Memory Unit) for a user to execute it, it may not be a big deal. However, if your web has 10,000 users who are executing 10 requests per second, imagine how much more performant it will be if we can reduce the time and space cost even by 10%.

When I was attending bootcamp, I started hearing about **big-O** notation. I had no idea what it was but apparently it is a big deal.

## Big-O Examples

**Big-O** notation is generally used to estimate time (amount of computations/ how fast) and space (amount of memory used) complexity of an algorithm. **Big-O** measures worst-case scenario.

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

```
//example3
function logLastElement(arr){
  console.log(arr[arr.length-1]);
}
```

**Big-O** above is **O(1)** because it does not loop.

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

**Big-O** above is **O(n)** because although there are two for-loops, they is not nested.

## Estimating Big-O

The best way to estimate **Big-O** values is to analyze it line-per-line. Over time, I can just see chunks of code and estimate **Big-O** values. The most important parameters are time and space units.

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

### Estimating Time and Space Unit in a Function

Going back to first example:

```
function logArray(arr){
  for(var i = 0; i < arr.length; i++){
    console.log(arr[i]);  
  }
}
```

If we break it down line by line, we will find:

-WIP-
