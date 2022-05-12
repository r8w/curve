---
layout: post
title: "Staircase"
tags: [hackerrank, competitive coding, solution, javascript, level=easy]
comments: true
---

Figuring out how to solve [Staircase](https://www.hackerrank.com/challenges/staircase/problem?isFullScreen=true&h_r=next-challenge&h_v=zen) problem on Hackerrank!

The only reason I'm writing this post is that I was unable to figure out the solution. It felt embarrassing, so here I come venting.

```
        #
       ##
      ###
     ####
```

> __*Its base and height are both equal to n . It is drawn using # symbols and spaces. The last line is not preceded by any spaces.*__

That's what we've to print out, so let's understand the bits and pieces, and do it.

As the staircase is made up of __`"#"`__ and *__spaces__*, it's basically a square board with visible __`"#"`__ and invisible spaces. I think I just repeated myself!

As of now I'm thinking of two ways to solve this problem.

## First Approach

So, suppose we are asked to make a staircase of size 8, what we can do is -

- Create an array with eight items, and these items are *spaces*.

```js
var board = Array(8).fill(' ');
```

we get -

```
> [ ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ' ]
```
Now,

- Assign __`"#"`__ to the `last index` of __`board`__ which is `length - 1`. In our case, it's __`7`__ --- *eighth element*.

```js
base[7] = "#"
```

![]({{site.baseurl}}/images/staircase.png){: .center-image}


- Now, we can join the elements and print it.

![]({{site.baseurl}}/images/staircase-base.png){: .center-image}

```js
var board = Array(8).fill(' ');
board[7] = '#';
board.join('');
```
*which gives ---*
```
'       #'
```

Similarly, we can assign "#" to the __7th element__ of our __`board`__.

![]({{site.baseurl}}/images/staircase-step.png){: .center-image}

and assign __"#"__ to --

```js
board[6] = '#';
board.join('');
// '      ##'

board[5] = '#';
board.join('');
// '     ###'
```

As now it's clear how we are assigning the value to our board, it' time for our first solution ---

```js
function stairCase(n) {
  var board = Array(n).fill(' ');
  var height = board.length - 1;

  for (var i = height; i >= 0; i--) {
    board[i] = "#";
    console.log(board.join(''));
  }
}

stairCase(8);

       #
      ##
     ###
    ####
   #####
  ######
 #######
########
```
If you get rid of the `join()`, you'll see -

```
[ ' ', ' ', ' ', ' ', ' ', ' ', ' ', '#' ]
[ ' ', ' ', ' ', ' ', ' ', ' ', '#', '#' ]
[ ' ', ' ', ' ', ' ', ' ', '#', '#', '#' ]
[ ' ', ' ', ' ', ' ', '#', '#', '#', '#' ]
[ ' ', ' ', ' ', '#', '#', '#', '#', '#' ]
[ ' ', ' ', '#', '#', '#', '#', '#', '#' ]
[ ' ', '#', '#', '#', '#', '#', '#', '#' ]
[ '#', '#', '#', '#', '#', '#', '#', '#' ]
```

---

## Second Approach

In this method, we'll manipulate string.

```js
function stairCase(n) {
  var height = n;
  var index = height - 1;

  for (var i = 0; i < height; i++) {
    var str = "";
    for (var j = 0; j < height; j++) {
      if ((i + j) >= index) {
        str += "#";
      } else {
        str += "0";
      }
    }
    console.log(str);
  }
}

stairCase(4);
````

This method seem tricky, but once we understand the flow of loop, we can recognize the pattern easily. Check out the visualization [here](https://pythontutor.com/javascript.html#code=function%20stairCase%28n%29%20%7B%0A%20%20var%20height%20%3D%20n%3B%0A%20%20var%20index%20%3D%20height%20-%201%3B%0A%0A%20%20for%20%28var%20i%20%3D%200%3B%20i%20%3C%20n%3B%20i%2B%2B%29%20%7B%0A%20%20%20%20var%20str%20%3D%20%22%22%3B%0A%20%20%20%20for%20%28var%20j%20%3D%200%3B%20j%20%3C%20n%3B%20j%2B%2B%29%20%7B%0A%20%20%20%20%20%20if%20%28%28i%20%2B%20j%29%20%3E%3D%20index%29%20%7B%0A%20%20%20%20%20%20%20%20str%20%2B%3D%20%22%23%22%3B%0A%20%20%20%20%20%20%7D%20else%20%7B%0A%20%20%20%20%20%20%20%20str%20%2B%3D%20%220%22%3B%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%20%20%20%20console.log%28str%29%3B%0A%20%20%7D%0A%7D%0A%0AstairCase%284%29%3B&curInstr=0&heapPrimitives=nevernest&mode=display&origin=opt-frontend.js&py=js&rawInputLstJSON=%5B%5D).

__Test Case__ --- It's only for the loop which creates our string.

- Staircase of size 4.

```
First Loop -

i + j | >= | 3 (size - 1) | str
----------------------------
0 + 0 | >= | False        | " "
0 + 1 | >= | False        | " "
0 + 2 | >= | False        | " "
0 + 3 | >= | True         | "#"

output = "   #"
--------------------------------

Second Loop -

i + j | >= | 3 (size - 1) | str
----------------------------
1 + 0 | >= | False        | " "
1 + 1 | >= | False        | " "
1 + 2 | >= | True         | "#"
1 + 3 | >= | True         | "#"

output = "  ##"
```


## Bonus

This one creates a triangle!

```js
function star(n) {
  var arr = Array(n-1).fill('');

  for (var i = arr.length; i >= 0; i--) {
    arr[i] = " #";
    console.log(arr.join('  '))
  }
}

star(10)
```
