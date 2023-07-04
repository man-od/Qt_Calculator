# Qt_Calculator
Implementation of SmartCalc

In this project implement an extended version of the usual calculator, which can be found in the standard applications of each operating system in the C programming language using structured programming. In addition to basic arithmetic operations such as add/subtract and multiply/divide, to supplement the calculator with the ability to calculate arithmetic expressions by following the order, as well as some mathematical functions (sine, cosine, logarithm, etc.).

Besides calculating expressions, it should also support the use of the _x_ variable and the graphing of the corresponding function.

As for other improvements you can consider a credit calculator.

### Polish notation and reverse Polish notation
Despite the absolute convenience of working with the classical form of writing expressions, when it comes to writing programs, queries are most often formed in the format `what to do -> what data to perform operations with`. So, around 1920, the Polish logician Jan Lukasiewicz invented  prefix notation (later also called Polish notation or normal Polish notation) in order to simplify propositional logic.

Let's take a look at the ways to write expressions:

The expression written in conventional infix notation:

>2 / (3 + 2) * 5

The expression written in Polish prefix notation:

>\* (/ 2 (+ 3 2)) 5

Normally parentheses between operations of equal priority are unnecessary and the final expression looks like this:

>\* / 2 (+ 3 2) 5

The expression written in Reverse Polish (bracketless) notation:

> 2 3 2 + / 5 *

### Dijkstra's algorithm
Edsger Dijkstra invented an algorithm for converting expressions (including functions) from infix to Reverse Polish notation. The algorithm was named the "shunting-yard algorithm", because its operation resembles that of a railroad shunting yard.

>Before we look at the algorithm itself, let's make a small remark and introduce the token. A token is the simplest unit of morphological parsing of an expression. So, the expression 2 / (3 + 2) * 5 (the blanks are added for easy perception and do not carry any semantic sense), broken down into tokens, will look like this [2], [/], [(], [3], [+], [2], [)], [*], [5], where [2, 3, 5] are numerical tokens, [/, (, +, ), *] - are tokens-operations.

The Shunting-yard algorithm is stack-based. There are two text variables involved in the conversion: the input and the output string. The conversion process uses the stack to store operations not yet added to the output string. The conversion program sequentially reads each token from the input string and on each step does some actions based on which tokens have been read.

#### Implementation of the algorithm
As long as there are unprocessed tokens in the input string, read the next token:

If the token is:
- A number – put it into the output queue

- A function or a left parenthesis – push it onto the stack

- A function arguments separator (e.g. comma):
    - Move operators from the stack to the output queue until the token at the top of the stack is a left parenthesis. If there is no left parenthesis in the stack, there is an error in the expression.

- Operator (O1):
    - While there is an token-operator O2 at the top of the stack, that has greater precedence than O1 or they have the same precedence and O1 is left-associative:
    - Pop O2 from the stack into the output queue
    - Push O1 onto the stack

- A right parenthesis:
    - While the token at the top of the stack is not a left parenthesis, pop the token-operators from the stack into the output queue.
    - Pop the left parenthesis from the stack and discard it.
    - If there is a function token at the top of the stack, then pop the function from the stack into the output queue
    - If the stack ended before the left parenthesis was read, there is an error in the expression.

If there are no more tokens left in the input string:
- As long as there are operators in the stack:
    - If there is a parenthesis at the top of the stack - there is an error in the expression.
    - Pop the operator from the stack onto the output queue

End.

## Implementation of SmartCalc
- The program must be developed in C language of C11 standard using gcc compiler. You can use any additional QT libraries and modules
- The program code must be located in the src folder
- The program must be built with Makefile which contains standard set of targets for GNU-programs: all, install, uninstall, clean, dvi, dist, test, gcov_report. Installation directory could be arbitrary, except the building one
- The program must be developed according to the principles of structured programming
- When writing code it is necessary to follow the Google style
- Prepare full coverage of modules related to calculating expressions with unit-tests using the Check library
- GUI implementation, based on any GUI library with API for C89/C99/C11

## Credit calculator
Provide a special mode "credit calculator"
- Input: total credit amount, term, interest rate, type (annuity, differentiated)
- Output: monthly payment, overpayment on credit, total payment
