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

### February 13th 2018 ###
- Using the Stepper allow you to run through all the steps of the evaluation of the code.
- You can right click on a definition of an object or function for example and can see "Enter Dr.Racket help desk" which is the full documentation for the BSL language.

### February 14th 2018 ###
- Learning the recipe "How To Design Functions" to design functions which operate on primitive data.
- *First* is the signature, purpose and stub of the function.
```
; ; Number -> Number (Signature)
; ; Produce 2 times the given number (Purpose)

(define (double n) 0) this is the stub
```

-*Second* is adding examples.
```
; ; Number -> Number (Signature)
; ; Produce 2 times the given number (Purpose)
(check-expect (double 3) 6) ;example
(check-expect (double 4.2) 8.4) ;example

(define (double n) 0) this is the stub
```

-*Third* is inventory, meaning the template and constants.
```
; ; Number -> Number (Signature)
; ; Produce 2 times the given number (Purpose)
(check-expect (double 3) 6) ;example
(check-expect (double 4.2) 8.4) ;example

(define (double n) 0) ;this is the stub

(define (double n) ;this is the template
  (...n))
```

-*Fourth* is the code body.
```
; ; Number -> Number (Signature)
; ; Produce 2 times the given number (Purpose)
(check-expect (double 3) 6) ;example
(check-expect (double 4.2) (* 2 4.2) ;example

(define (double n) 0) ;this is the stub

;(define (double n) ;this is the template
 ; (...n))

(define (double n) ;function body or how the function works
  (* 2 n))
```

-*Fifth* and finally is testing and debugging, which consists just by running and checking to see if the code works, correcting the mistakes along the way.
```
;; Number -> Number
;; Produces 2 time the given number
(check-expect (double 3) 6) ;testing
(check-expect (double 4.2) 8.4) ;testing

;(define (double n) 0) ;this is the stub
;(define (double n) ;this is the template
;  (... n))

(define (double n) 
  (* 2 n))
->Both tests passed!
```

### February 15th 2018 ###
- The signature should be what the function gets as a parameter and outputs, think in primitive types.
- The purpose should be a more elaborate description of what the function has to do.
- `check-expect` should have some good exaples of how the function should run. Try different primitive types, write at least two tests.
- Example should contain the standard `(define (nameOfFunction parameter) value)` syntax, usually with a dummy value like 0 or maybe an empty string.
- The template should contain a dummy function body ie: `(... parameter)`
- If a test fails `(check-expect)`, it could be that the function definition is wrong, the test is wrong or both are wrong. Check the test first before checking the function definition.

### February 16th 2018 ###
- Using the recipe for defining the function:
```
(require 2htdp/image)

;; Image -> Natural Number
;; Produce image width * height (area)
(check-expect (image-area (rectangle 2 3 "solid" "red")) (* 2 3))

; stub (define (image-area img) 0)
; template(define (image-area img)
  ;(... img))

(define (image-area img)
  (* (image-width img) (image-height img)))
```
- When designing functions where the output is a boolean, the purpose has to be very clear WHEN the function should produce true or in some cases when it should produce false.
- Another example from today's lesson, where the case can be true, false or both sides of the rectangle can be the same, which means we can't really determine whether or not it's tall or not:
```
(require 2htdp/image)
;; Image -> Boolean
;; Produce true if the image is tall (height is greater than width)
(check-expect (tall? (rectangle 2 3 "solid" "red")) true)
(check-expect (tall? (rectangle 3 2 "solid" "red")) false)
(check-expect (tall? (rectangle 3 3 "solid" "red")) false)

; stub(define (tall? img) false)
; template(define (tall? img
    ;(... img))

(define (tall? img)
  (if (> (image-height img) (image-width img))
      true
      false))
```

### February 25th 2018 ###
- DESIGN a function that consumes a string and determines whether its length is
less than 5 using the function recipe:
```
;; String -> Boolean
;; Compares the string length to 5 characters and outputs true or false

(check-expect (less-than-5? "") true)
(check-expect (less-than-5? "aaa") true)
(check-expect (less-than-5? "bbbbbb") false)
(check-expect (less-than-5? "123456") false)

;(define (less-than-5? s) true)stub

;(define (less-than-5? s)
;  (...s)) template

(define (less-than-5? s)
  (< (string-length s) 5))
```

### February 26th 2018 ###
- Design a function to put a box around a given image.
```
(require 2htdp/image)

; Image -> Image
; Use boxify around an image
(check-expect (boxify (circle 10 "solid" "red"))
              (overlay (rectangle 22 22 "outline" "black")
                       (circle 10 "solid" "red")))

(check-expect (boxify (circle 10 "solid" "blue"))
              (overlay (rectangle 22 22 "outline" "black")
                       (circle 10 "solid" "blue")))

; stub (define (boxify i) (circle 2 "solid" "green"))

(define (boxify i)
  (overlay (rectangle (+ (image-width i) 2)
                      (+ (image-height i) 2)
                      "outline"
                      "black")
           i))
```
I had to constantly check the solution for this one. It completely messed with me on how the recipe was suppose to be implemented.

### February 27th 2018 ###
``` 
(require 2htdp/image)

; Image -> Boolean
; Takes two images, compares, produces true if the first is larger
(check-expect (larger? (circle 3 "solid" "red") (circle 1 "solid" "red")) true)
(check-expect (larger? (circle 3 "solid" "red") (circle 4 "solid" "red")) false)
(check-expect (larger? (circle 6 "solid" "red") (circle 4 "solid" "red")) true)

; (define (larger? img) true) stub
; (define (larger? img)
;    (...img) example
```
This one kicked my ass as well. I knew there was something similar to larger? but couldn't find what I was looking for.

### Feburary 28th 2018 ###
```
(require 2htdp/image)

; Image -> Boolean
; Takes two images, compares, produces true if the first is larger or false if not.
(check-expect (larger? (circle 3 "solid" "red") (circle 1 "solid" "red")) true)
(check-expect (larger? (circle 3 "solid" "red") (circle 4 "solid" "red")) false)
(check-expect (larger? (circle 6 "solid" "red") (circle 4 "solid" "red")) true)

; (define (larger? img) true) stub

; (define (larger? img)
;    (...img) example

(define (larger? image1 image2)
  (if (and (> (image-width image1) (image-width image2))
           (> (image-height image1) (image-height image2)))
      true
      false))
```
Finished the problem from yesterday.