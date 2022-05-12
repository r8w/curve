---
layout: post
title: "Diagonal Matrix Difference"
tags: [hackerrank, competitive coding, solution, javascript, matrix, level=easy]
comments: true
---

Let's understand a part of Matrix by solving [Diagonal Difference](https://www.hackerrank.com/challenges/diagonal-difference/submissions/code/269194423). I'm not going to brief explain the concept, but at the end of this post, you won't be confused regarding how the looping through matrices work.

First, a __*Matrix*__ is a rectangular array of numbers arranged in rows and columns, and a __*Diagonal*__ is a straight line that joins two opposite corners of a square, rectangle, or other straight-sided shape.

If the word *matrix* bothers you, think of it as an array whose elements are arrays itself with *n* equal number of elements in each array.

__For example__

```js
var matrix = [[1,2,3], [4,5,6], [7,8,0]];
```

In problem statements, it's given as -

```
1  2  3
4  5  6
7  8  9
````

Now, we have to find the difference of its diagonals' sum.

```
[1]  2  [3]
 4  [5]  6
[7]  8  [9]
````

which is -

```js
var diagonalOne = 1 + 5 + 9;
var diagonalTwo = 3 + 5 + 7;
var difference = diagonalTwo - diagonalOne;
````

Before that, let's jump to the *rows* and *columns* of our matrix.

![]({{site.baseurl}}/images/matrix.png){: .center-image}

Here, we have three rows and three columns.

```js
var matrix = [[1,2,3], [4,5,6], [7,8,9]];
var matrixLength = matrix.length; // 3
````


__First Diagonal__ : We find the position of 1, 5, and 9.

- `matrix[0][0]` --->> 1
- `matrix[1][1]` --->> 5
- `matrix[2][2]` --->> 9

__Observation__ --- What we see here is that the __index__ of our `matrix`'s *row* and *column* are __equal__ if we're looking for the values that makes the __left-to-right diagonal__.

```
[i]     [j]      ?
 0  ===  0     True
 0  ===  1     False
 0  ===  2     False

 1  ===  0     False
 1  ===  1     True
 1  ===  2     False

 2  ===  0     False
 2  ===  1     False
 2  ===  2     True
```

__Second Diagonal__ : We find the position of 3, 5, and 7.

- `matrix[0][2]` ---> 3
- `matrix[1][1]` ---> 5
- `matrix[2][0]` ---> 7

__Observation__ --- Here, we see that when the __sum__ of __index__ of the matrix's __`row[i]`__ and __`column[j]`__ is equal to __`matrixLength - 1`__, it gives us the values for our __right-to-left diagonal__.

```
[i]   [j]       matrixLength - 1    ?
 0  +  0   ===       2            False
 0  +  1   ===       2            False
 0  +  2   ===       2            True

 1  +  0   ===       2            False
 1  +  1   ===       2            True
 1  +  2   ===       2            False

 2  +  0   ===       2            True
 2  +  1   ===       2            False
 2  +  2   ===       2            False
```

Now that we've figured the logic, we can proceed to solve the problem -

```js
function diagonalDifference(arr) {
    var sum = 0; // first diagonal
    var _sum = 0; // second diagonal
    var a = arr.length; // length of matrix

    for (var i = 0; i < a; i++) {
        for (var j = 0; j < a; j++) {
            if (arr[i] === arr[j]) {
                sum += arr[i][j]
            }
            if ((i + j) === (a - 1)) {
                _sum += arr[i][j]
            }
        }
    }
    return Math.abs(sum - _sum); // get rid of plus/minus
}

var array = [[10,2,3], [4,5,6], [7,8,9]];

console.log(diagonalDifference(array));
```
That's it!

---


__Links__

- [Introduction to Matrices](https://courses.lumenlearning.com/boundless-algebra/chapter/introduction-to-matrices/)
