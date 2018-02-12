# HOW TO CODE: SIMPLE DATA - NOTES AND CODE #

### February 10th 2018 ###
- First question is always: *What do we want our program to do?*
- How do we break down a problem? Into *well chosen smaller pieces*.
- The first exercise asks us to calculate a side of a triangel using Pythagora's Theorem: c^2 = a^2 + b^2. The answer is 25 or 5^2 or in BSL code: `(sqrt (+ (* 4 4) 9))`

### February 11th 2018 ###
- Define a constant or variable: `(define NAME VALUE)`

### February 12th 2018 ###
- In BSL or for that matter in most programming languages, functions are reusable blocks of code that produce a different value each time.
- Parameters of functions stand for varying values, this is why we can produce a different output each time. 
```
(define (bulb c)
  (circle 40 "solid" c)
(bulb "purple")
```
Where bulb is the name of the function, c is the parameter which stands for the changing value and purple is the parameter that we passed into the function.
- We've talked about reusability by using functions. So instead of this:
```
(above (circle 40 "solid" "red")         
       (circle 40 "solid" "yellow")
       (circle 40 "solid" "green"))
```
we use:
```
(above (bulb "red")
       (bulb "yellow")
       (buld "green"))
```
which is still repeating ourselves, but the code is much more cleaner. The only thing that is different is the colour parameter, which if we look back is c.
- Example: `(foo (+ 1 1) 4)` will first evaluate the first parameter to 2 and then start applying the parameters to the functions body. Evaluation also goes from left to right.
- *Predicates* are primitives or in some cases functions that produce a boolean value.