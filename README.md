# RPN Interpreter

Basic Reverse Polish Notation Interpreter. 

## What? What is this?

Basically, usual calculators use infix notation to interpret operations, like
`1 + 2`, or `3 * 4`.

Reverse Polish Notation uses postfix notation to interpret operations. This means 
that, the operands comes first, and the operators after, like `1 2 +` or `3 4 *`. 

It simplifies some notations, because the parenthesis becomes almost unnecessary, 
but it's an unusual way to represent calculations. 

The [Wikipedia Page](https://en.wikipedia.org/wiki/Reverse_Polish_notation) is 
a good starting point to know more about this.

## Using 

You can start right away to use this.
Clone this repo, then 

```sh 
$ gradle run
```

You gonna see some messages. To a better experience without compiling program, 
use: 

```sh 
$ gradle -q --console plain run
```

You gonna see these messages: 

```sh 
Initializing interpreter
Initialized!
Input some numbers here with a postfix operator!
```

After that, just input the calculations, and then, the interpreter will 
input all operations made:

```sh 
$ 25 40 + 30 10 - *

40 + 25 = 65
10 - 30 = -20
-20 * 65 = -1300
```

## State management, how it works 

Simply, RPN interpreters uses an operand stack, where it stores all it's operands. 
to disambiguate the operation performed in the section above, we gonna illustrate this, 
enumerating all tokens:

```
1  2  3 4  5  6 7 
25 40 + 30 10 - * 
```

The evaluation goes for the order of tokens are entered.
First, we have `25` and `40`. They are numeric tokens, so they goes right to 
the stack:

```
STACK 
-----
25
-----
40
-----
```

When the interpreter sees an `Operator`, like `+`, `-` or whatever operand it 
supports, it pops two operands from the stack, and perform the operator on them,
pushing the result back to the stack:

```
STACK 
------
25  popped
------
40  popped
------

25 + 40 = 65

Now, 65 will be pushed to the stack 

STACK
------
65
------
```

After that, the stack will have only the result of the operation. The interpreter 
will make this process in a loop, and will resolve the expression above as 
`(40 + 25) * (10 - 30)`. We don't need the parenthesis, because the expressions 
are evaluated by the order they are put in postfix notation.
