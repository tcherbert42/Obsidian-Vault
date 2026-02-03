#school #Pre-Calculus 
- Inverse Functions (cryptography, encrypting, and decrypting)             } - Transformations
- Composition of Functions                                                                                }
- Exponential Functions(bacteria growth, chemistry / biology(doubling over time, ex: interest rates))
- Logarithmic Functions(Reverse of an exponential function / undo an exponential(how calculators work))


## Inverse Functions
Equations use x + y
- Relation  = collection of ordered pairs
- Function = A special type of relation  ( still uses ordered pairs ), where every value for the input yields one value for the output. The input must be  consistent. Traditionally, X is the input and Y is replaced with f(x). 


### One-to-one function:
( More Restrictions )
 - A special function where every ouput value comes from only one input value. 


#### Example of a function that is not one-to-one:
## $f(x) = x^2$

- The result of 9 comes from x = 3 AND x = -3


#### Question Example:
## $f(x) = -3x-15$

- ^ is a one-to-one function. What makes f(x) = 27?

$-3x-15 = 27$
		+15     +15
		-3x =  42
             x = -14


### Function Composition:
- Functions acting in a particular order where the result from a prior function becomes the input of a subsequent function. 
( an answer from a previous function, answers the other function )


#### Ex: Working Notation
Let $f(x) = 2x - 5$ and $g(x) = x^2-4x$
Find: f(-2) = $2(-2)-5$ = - 9
Find: g(-3) = $-3^2-4(-3)$ = 9 + 12 = 21

Find: g(d+3) = $(d+3)^2 - 4(d+3)$ = $d^2 + 6d + 9 -4d -12$ = $d^2 + 2d - 3$

Find: f(g(x)) = $2(x^2 -4x) - 5$ = $2x^2 -8x -5$
Find g(f(x)) = $(2x-5)^2 - 4(2x-5)$ = $4x^2-20x+25-8x+20$ = $4x^2 -28x +45$

Traditional Notation: (f o g)(x)
name of a new function ^


## Function Arithmetic
(f + g)(x)  =  f(x) + g(x)  
(f - g)(x)  =  f(x) -  g(x)
(f * g)(x)  =  (f(x) * g(x))
(f / g)(x)  =  
( -- singular name -- )  =  working version

### Singular name of a composition 
Working Form:     g(f(f(g(x))))
Read as: g of f of f of g of x
Singular Name: (g o f o f o g)(x)

#### Ex:
(g o f o f o g)(x) = g(f(f(g(x))))

= g(f(f($x^2-4x$))) = g(f(2($x^2-4x$)-5))
= g(2(2($x^2-4x$)-5 )-5 )
= $(2(2(x^2-4x) -5 ) - 5)^2 -4(2(2(x^2-4x) -5) -5)$
= $(4x^2 -16x-10 -5)^2 - 4(4x^2-16x-10-5)$

Definiton: Two Functions f and g are inverse functions if and only if (f o g)(x) = x, for all x in the domain of g and (g o f)(x) = x for all x in the domain of f. 


