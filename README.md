# Why this guide?

A lot of self-taught programmers or bootcamp graduates are not as strong (myself included) in algorithm as an average CS graduate. I hope this guide will be found by many to be a helpful supplement, including myself.

If you find any error, feel free to submit a request or email me at letsmailiggy@gmail.com.

# Who is this for?
I originally intend this guide for bootcamp graduate job-seekers and self-taught developers, but my hope is that everyone will benefit from this.

## Efficiency

Computers are not magic *(although it feels like it at times)*. They have limitations. It is best practice to always keep in mind whenever you create an algorithm to optimize their runtime and memory usage: "how can I use the least memory and make it run as fast as possible?". If a function takes up 100ATU (Arbitrary Time Unit) and 100 AMU (Arbitrary Memory Unit) for it to execute once, it may not be a big deal. However, if your application has 10,000 users who are executing that request per second, imagine how much more performant it will be if we can reduce the time and space cost even by 10%.

When I was attending bootcamp, I started hearing about **Big-O** notation. I had no idea what it was but apparently it is a big deal.

## The Big-O

Big-O notation is generally used to estimate time (amount of computations/ how fast) and space (amount of memory used) complexity of an algorithm. Big-O measures worst-case scenario.

### Time and Space Units

**Time Unit**

The following are equal one "time unit":
- Mathematical equation (`1+2`, `i++`)
- Printing or returning something (`console.log('hello')`, `return 10`)
- Instantiating new variable (`let foo = 'bar';`, `const bar = baz`)
- Accessing an item in an Array  (`arr[i]`)
- Boolean comparison (`hello !== true`)

Anytime you execute something similar to the list above, you can assume it costs one time unit.

**Space Unit**

The following are roughly equal one "space unit":

- Creating a single variable, empty array, or object (`var i = 1`, `let obj = {}`, `const arr = []`)
- Adding a *new* key-value pair into a hashtable or array (`obj[bar] = 'baz';`, `arr.push(10)`)

Whenever you create a single variable/ instantiate a blank array or object, you take up a space somewhere in the memory that costs one space unit.

### Time complexities

Most of this guide I will be talking about time complexity (runtime). At the end, I will briefly talk about space complexity (memory).

I find myself understanding Big-O best when I see examples, so here goes:


```
//example1
function logArray(arr){
  for(var i = 0; i < arr.length; i++){
    console.log(arr[i]);  
  }
}
```

The function above has a Big-O complexity of O(n) because it iterates through every single array element **once**.

Let's inspect them line-by-line:

1. `var i = 0;` does one operation
2. `i < (arr.length)` does two operations (the comparison, `<`, plus `arr.length`)
3. `console.log(arr[i])` does two operations: one for `console.log` and another one to look up an array value `arr[i]`.

Since we are dealing with a `for` loop, the amount of operations will increase as the array input gets larger. If array contains 10 elements, it will loop 10 times. The calculations becomes:

`1 + 10 * 4 = 41 operations.`

If the array contains 1,000,000 elements, it will loop a million times, and so on. Big-O values will always depend, linearly, on the array size. Hence it is **O(n)**.


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

The Big-O above is O(n<sup>2</sup>) because it contains a `for` loop inside a `for` loop (one nested loop).

A good rule of thumb is, whenever you see a loop inside loop, Big-O will probably be n polynomial, whereas the polynomial is the amount of nested loops. So if it were:

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

If you guessed O(n<sup>4</sup>), you're right. If you ever find yourself nesting 3 levels deep or more, then you are probably a horrible human being. I would highly **discourage** any nesting deeper than 2 levels deep.

```
//example3
function logLastElement(arr){
  console.log(arr[arr.length-1]);
}
```

Big-O above is O(1) because it does not loop.

1. `console.log()` counts as one operation.
2. `arr[arr.length - 1]` counts as three operations: one for `arr.length`, one for `- 1` operation, and one for `arr[...]`.

Keep in mind that we don't say O(4) but O(1). Another rule of thumb in Big-O calculation is that we **always drop the constant coefficients to 1**. The important picture here is that regardless how big the array is, it does not make it slower to execute the function. We can have an array size of 10 or 1,000,000, but all the function does is to print out the last array element.


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

Recall that although we are looping the array twice, the loops are not nested. O(2n) becomes O(n). **Nested loops multiply while un-nested loops add**.

Not all loops have n value. Some loops have constant values. For example:

```
//example5
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

The function above loops the array 10 times regardless array size of 1,000,000 or 100. Since it is only looping 10 times and does not depend on array size, it is not O(n) but O(1).

```
//example6
function logNestedArrayAndMore(arr){
  var k = 0;
  for(var i = 0; i < arr.length; i++){
    for(var j = arr.length - 1; j >= 0; j--){
      console.log("i element is: " + arr[i] + " j element is: " + arr[j]);
    }  
  }
  while(k < arr.length){
    console.log("Meanwhile k element is: " + arr[k]);
    k++;
  }
}
```

The function above can be said to have O(n<sup>2</sup>). There is a nested loop (O(n<sup>2</sup>)) and a regular loop (O(n)), making O(n<sup>2</sup> + n). The last rule of thumb is, we only care about the most significant portion and we can drop everything else. Think about this: if we have a million array (n = 1,000,000) and we have O(n<sup>2</sup> + n), the n portion accounts for less than 0.00001% of total operations. Since it is insignificant when n is large, we can safely drop it.

#### Order of magnitudes

Not an exhaustive list, but the order of Big-O notation from small to largest:

- O(1)
- O(lg n)
- O(n)
- O(n lg n)
- O(n<sup>2</sup>)
- O(n<sup>3</sup>)
- O(c<sup>n</sup>)

*Note the last list, O(c<sup>n</sup>) is true when c > 1.*

#### End Goal

Over time, you will learn to approximate Big-O values just by sectioning and comparing them based on magnitude.

For example, looking at the palindrome code below ([source](https://stackoverflow.com/questions/22111507/how-to-write-palindrome-in-javascript))

```
function palindrome(str) {
    var len = str.length;  //=> This line is O(1)
    for ( var i = 0; i < Math.floor(len/2); i++ ) { //=> this for loop is O(n)
        if (str[i] !== str[len - 1 - i]) {
            return false;
        }
    }
    return true;
}
```

The first section, `var len = str.length` is constant. The second section, the for loop is dependent on string length (even though it has `Math.floor(len/2)`, if we have a string 1,000,000 characters long, it will be proportionally large), therefore it has Big-O of O(n). The largest section is O(n). Therefore the function can be said to be O(n) overall.

The goal of knowing Big-O is to create codes with the lowest Big-O value as possible. Avoid nesting too many loops.  

### Space Complexities

We went over time complexities. Another important consideration when measuring Big-O is how much space it is taking when running a program.

The idea behind space complexity is similar to time complexity. For example:

```
function sumItUp(arr){
  var total = 0;
  for(var i = 0; i < arr.length; i++){
    total+= arr[i]
  }
  return total;
}
```

The first line, `var total = 0` takes up only one memory space (regardless the input size). However, since the for loop depends on the size of the array, the Big-O is O(n).
