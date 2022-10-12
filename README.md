# Intro

You are tasked to develop a program that can evaluate mathematical expressions of any length and complexity. Do NOT worry about unary operators (-), such as

```
-3 + 5
```

I am leaving it as a bonus (see below). However, remember to replace all SPACES with an empty string ("") before you start working on parsing the input string and evaluating its mathematical value. In other words, your program should not depend on the spaces in the input at all. Some inputs may contain lots of spaces, others may have none.

## Available operators and operands 

The operators that your program should support include `+ - * / ( )`. You are more than welcome to add `log`, `sin`, `^`, etc. for bonus points.

The operands can be any non-negative integers (integers >= 0).

For example, your program should be able to evaluate such expressions as:

- with spaces  
  `591 + 10 * 6 / (442 - 3 * ( 61 + 7 - 8 )) + 4 / 2`

- and without spaces  
  `591+10*6/(442-3*(61+7-8))+4/2`

# High-level view of the algorithm

1. Read user's input into a `String` and replace all spaces with an empty string.

2. Parse the input according to the "infix to postfix" conversion algorithm using stacks as we did in class (follow the video recording on "Canvas -> Zoom" from October 10th - that's when we went over it).

3. Evaluate the postfix expression using stacks and the last number you pop out from the stack will be your final result.

4. Google, google, and again, google (and youtube it). May the google be with you (or duckduckgo/startpage if you prefer privacy).

# Deeper algorithm ideas

## Infix to postfix conversion

Let's say you have the following input: `2 + 3 * ((5 - 8 / 4) + 6) / 9`, and you also created an `ArrayList<String> out` that will store the postfix notation of your input. You also created a `Stack<String> ops` that will store your operators. Let's read it from left to right, following the rules:

1. Operand -> add it to the `out`. NOTE: operands will be multi-digit numbers such as `234 + 45`. We simplified it to single-digit numbers for the example sake.
2. Operator -> check what is on the `ops` stack:
   - if `ops` is empty, push the operator to `ops`
   - if `ops.peek()` has `(`, push the operator to `ops`
   - if `ops.peek()` contains an operator that is _less_ than the current operator (on the precedence scale according to PEMDAS), **continuously** (in a loop) pop from `ops` stack to `out` _until_ `ops.peek()` has an operator that is either a `(`, the same/greater precedence scale, or does not exist (meaning that `ops` is empty)
   - if neither of the above cases happened, then just push the operator to the `ops` stack
3. `(` -> push it to the `ops` stack
4. `)` -> do the following:
   - continuously pop from the `ops` stack until you encounter `(`
   - pop `(` from the stack as it's going to be at the top of the stack and you do not want it to be added to `out`

# Bonus

1. Your calculator can support unary operations to evaluate `-(3 + 5)` or similar expressions. (+10 points to your midterm quiz or final)

2. Your calculator can support floating-point operands. For example, `3.56 + 5.97 / 4.63` should return the decimal value 4.85 (or the full number will also work). (+10 points to your midterm quiz or final)

3. Your calculator supports all of the above-mentioned bonuses as well as it throws `RuntimeException` with a message when you:
    - try to divide by zero
    - try to enter characters that are not supported by this calculator, and
    - try to evaluate expressions that do not make sense (e.g., 5+++3--8*/+9).
    - Additionally, you can explain to me every line of your code and answer any questions about your code.

 If you do all of these bonus options - that is an ultra-kill, so it is worth +50 to your midterm quiz or final.
