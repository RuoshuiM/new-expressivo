# new-expressivo

This project follows [Problem Set 3 of MIT 6.005](https://ocw.mit.edu/ans7870/6/6.005/s16/psets/ps3/), which uses ANTLR. This system does not support additional operators such as "^", "-", and "/", and does not support "e" notation.

To compile the project in command line, run the following commands
(assuming we are at the root directory: new-expressivo/)

    javac -d bin/ -cp lib/antlr.jar src/expressivo/*.java src/expressivo/parser/*.java
    cd bin
    java -cp ../lib/antlr.jar:. expressivo.Main


# Using the system
(Information here is from [the pset assignment website](https://ocw.mit.edu/ans7870/6/6.005/s16/psets/ps3/))
<br><br>
In this system, a user can enter either an expression or a command.

An expression is a polynomial consisting of:

  * \+ and * (for addition and multiplication)
  * nonnegative numbers in decimal representation, which consist of digits and an optional decimal point (e.g. 7 and 4.2 )
  * variables, which are case-sensitive nonempty sequences of letters (e.g. y and Foo )
  * parentheses (for grouping)

Order of operations uses the standard PEMDAS rules.

Space characters around symbols are irrelevant and ignored, so 2.3*pi means the same as 2.3 * pi . Spaces may not occur within numbers or variables, so 2 . 3 * p i is not a valid expression.

When the user enters an expression, that expression becomes the current expression and is echoed back to the user: 

    > x * x * x
    x*x*x

    > x + x * x * y + x
    x + x*x*y + x

A command starts with ! . The command operates on the current expression, and may also update the current expression. Valid commands:

  * d/d var 
    <p>produces the derivative of the current expression with respect to the variable var , and updates the current expression to that derivative </p>
  * simplify var 1 = num 1 ... var n = num n 
    <p> substitutes num i for var i in the current expression, and evaluates it to a single number if the expression contains no other variables; does not update the current expression </p>

## Example Usage (assume all of the following code are typed into one session)
    > x * x * x
    x*x*x

    > !simplify x=2
    8

    > !d/dx
    (x*x)*1+(x*1+1*x)*x

    > !simplify x=0.5000
    .75

    > x * y
    x*y

    > !d/dy
    0*y+x*1
