______
09-16-2023 | 07:51
Status: #Research 
Tags: #mathConcepts #Calculus 


# [[Difference Quotient]] and Average [[Rate of Change]]


![[DifferenceQuotient1]]
Definition. A [[Secant]] line is a line between two points on the graph of a function
[[Rate of Change]]: The average rate of change for $f(x)$ on the interval $[a,b]$ is: 
- the [[Slope]] of the [[Secant]] line between the points $(a,f(a))$ and $(b,f(b))$
[[Slope]]: $M = \frac{rise}{run} = \frac{\Delta{y}}{\Delta{x}} = \frac{f(b)-f(a)}{b-a}$


- Ex: The average [[Rate of Change]] for $f(x) = \sqrt{x}$ on the interval $[1,4]$ is 
>[!hint] $m = \frac{f(4)-f(1)}{4-1} = \frac{\sqrt{4}-\sqrt{1}}{4-1} = \frac{2-1}{3} = \frac{1}{3}$

### [[Rate of Change]] Formula: $=\frac{f(x+h)*f(x)}{h}$

![[DifferenceQuotient2]]

Definition. A [[Difference Quotient]] represents: 
the average [[Rate of Change]] of a function $f(x)$ on the interval $[x,x+h]$
(i.e. the [[Slope]] of the secant line between the points $(x,f(x))$ and $(x+h,f(x+h)$)

[[Slope]]: $m = \frac{f(b)-f(a)}{b-a} = \frac{f(x+h) - f(x)}{(x+h)-(x)}$ then, cancel x's in the denominator $= \frac{f(x+h)-f(x)}{h}$
                          ^ (average [[Rate of Change]] formula)

- Ex: Find and simplify the [[Difference Quotient]] for $f(x)=2x^2-x+3$
( remember [[Difference Quotient]] ONLY for THIS example = $\frac{f(x+h)-f(x)}{h}$ )

>$f(x+h)=2(x+h)^2-(x+h)+3$ 
>$= 2(x+h)(x+h)-x-h+3$
>$= 2(x^2+xh+hx+h^2)-x-h+3$ 
>$= 2x^2+2xh+2hx+2h^2-x-h+3$ -- add up 2xh + 2hx
>$= 2x^2+4xh+2h^2-x-h+3$
>therefore,$f(x+h)-f(x)=2x^2+4xh+2h^2-x-h+3-(2x^2-x+3)$
>Cancel the 2x, x, and 3 : $=4xh+2h^2-h$
>$\frac{f(x+h)-f(x)}{h} = \frac{4xh+2h^2-h}{h}$ -- factor out h -- $=4x+2h-1$
>

### [[Difference Quotient]] Formula: $=\frac{f(b)-f(a)}{b-a}$