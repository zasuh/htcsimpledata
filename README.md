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
- From the evaluation section, I would need more tests to see if the function can pass on ALL cases. Other than that my solution is solid.

```
(define (aspect-ratio img)
  (cond [Q A]
        [Q A]
        [Q A]))
```
The conditional expressions are kind of like `else...if` statements in BSL. You ask a question and get an answer if the condition evaluates properly.
```
(define (aspect-ratio img)
  (cond [(> (image-height img) (image-width img)) "tall"]
        [(= (image-height img) (image-width img) "square"]
        [else "wide"]))
```

### March 1st 2018 ###
- In any program we have a *problem domain* ie: "a light is red" and in the `program` it might be represented with `0`, `1` would be yellow and `2` might be green. Basics of data definitions.

### March 2nd 2018 ###
```
;; CityName is String
;; interpretation: the name of a city
(define CN1 "Boston")
(define CN2 "Vancouver")
#;
(define (fn-for-city-name cn)
  (... cn)
  )

;; Template rules used
;; - atomic non-distinct rule: String

;; Functions:

;; CityName -> Boolean
;; Produce true if given city is Hogsmede
(check-expect (best? "Boston") false)
(check-expect (best? "Hogsmede") true)

;(define (best? cn) false) stub

; took template from CityName
(define (best? cn)
  (if(string=? cn "Hogsmede")
      true
      false))
```

### March 3rd 2018 ###
- Examples of *Data definition recipe*:
```
#;
PROBLEM:
Imagine that you are designing a program to manage ticket sales for a
theatre. (Also imagine that the theatre is perfectly rectangular in shape!) 
Design a data definition to represent a seat number in a row, where each 
row has 32 seats. (Just the seat number, not the row number.)
 

;; SeatNum is Natural[1, 32]
;; interp. seat numbers in a row, 1 and 32 are aisle seats
(define SN1 1) ;aisle
(define SN2 12) ;middle
(define SN3 32) ;aisle

#;
(define (fn-for-seat-num sn)
  (... sn)
  )

;; Template rules used:
;; -atomic non-distinct: Natural[1, 32]
```

- Enumeration:
```
#;
PROBLEM:
;As part of designing a system to keep track of student grades, you
;are asked to design a data definition to represent the letter grade 
;in a course, which is one of A, B or C.

;; LetterGrade is one of:
;; - "A"
;; - "B"
;; - "C"
;; interp. the letter grade in a course
(define LG1 "A")
(define LG2 "B")
(define LG3 "C")
;;<examples are reduntant for enumerations>

(define (fn-for-letter-grade lg)
  (cond [(string=? lg "A") (...)
         (string=? lg "B") (...)
         (string=? lg "C") (...)])
  )

;; Tempalte rules used:
;; -one of: 3 cases
;; -atomic distinct value: "A"
;; -atomic distinct value: "B"
;; -atomic distinct value: "C"
```

-Itemization:
```
;PROBLEM:

;Consider designing the system for controlling a New Year's Eve
;display. Design a data definition to represent the current state 
;of the countdown, which falls into one of three categories: 

; - not yet started
; - from 10 to 1 seconds before midnight
; - complete (Happy New Year!)

;; CountDown is one of:
;; - false
;; - Natuaral[1, 10]
;; - "complete"
;; interp. false means countdown has not yet started, natural means countdown is running
;; and how many second left, "complete" means countdown is over
(define CD1 false)
(define CD2 10)
(define CD3 1)
(define CD4 "complete")
#;
(define (fn-for-countdown c)
  (cond [(false? c) (...)]
        [(and (number? c) (<= 1 c) (<= c 10)) (... c)] ;mixed data itemization
        [else (...)])
  )

;; Template rules used:
;; -one of: 3 cases
;; -atomic distinct: false
;; -atomic non-distinct: Natural [1, 10]
;; -atomic distinct: "complete"
```

### March 4th 2018 ###
- Functions for previous problems with data definitions:
```
;; Data definitions:

;; SeatNum is Natural[1, 32]
;; Interp. Seat numbers in a row, 1 and 32 are aisle seats
(define SN1  1) ;aisle
(define SN2 12) ;middle
(define SN3 32) ;aisle
#;
(define (fn-for-seat-num sn)
  (... sn)) 

;; Template rules used:
;;  atomic non-distinct: Natural[1, 32]


;; Functions:

;; SeatNum -> Boolean
;; Produce true if the given number is on the aisle
(check-expect (aisle? 1) true)
(check-expect (aisle? 16) false)
(check-expect (aisle? 32) true)


;(define (aisle? sn) false) ;stub
; <use template from SeatNum>
(define (aisle sn)
  (or (= sn 1)
      (= sn 32))) 
```
```
;; Data definitions:

;; LetterGrade is one of: 
;;  - "A"
;;  - "B"
;;  - "C"
;; interp. the letter grade in a course
;; <examples are redundant for enumerations>
#;
(define (fn-for-letter-grade lg)
  (cond [(string=? lg "A") (...)]
        [(string=? lg "B") (...)]
        [(string=? lg "C") (...)]))

;; Template rules used:
;;  one-of: 3 cases
;;  atomic distinct: "A"
;;  atomic distinct: "B"
;;  atomic distinct: "C"


;; FUNCTIONS:

;; LetterGrade -> LetterGrade
;; Produce next highest letter grade (no change for A)
(check-expect (bump-up "A") "A")
(check-expect (bump-up "B") "A")
(check-expect (bump-up "C") "B")

; stub(define (bump-up lg) "A")
;<use template from LetterGrade>

(define (bump-up lg)
  (cond [(string=? lg "A") "A"]
        [(string=? lg "B") "A"]
        [(string=? lg "C") "B"]))
```
```
#; You are asked to contribute to the design for a very simple New Year's
Eve countdown display. You already have the data definition given below. 
You need to design a function that consumes Countdown and produces an
image showing the current status of the countdown. 

(require 2htdp/image)

;; Data definitions:

;; Countdown is one of:
;;  - false
;;  - Natural[1, 10]
;;  - "complete"
;; interp.
;;    false           means countdown has not yet started
;;    Natural[1, 10]  means countdown is running and how many seconds left
;;    "complete"      means countdown is over
(define CD1 false)
(define CD2 10)          ;just started running
(define CD3  1)          ;almost over
(define CD4 "complete")
#;
(define (fn-for-countdown c)
  (cond [(false? c) (...)]
        [(and (number? c) (<= 1 c) (<= c 10)) (... c)]
        [else (...)]))

;; Template rules used:
;;  - one of: 3 cases
;;  - atomic distinct: false
;;  - atomic non-distinct: Natural[1, 10]
;;  - atomic distinct: "complete"

;; Functions:

;; CountDown -> Image
;; Produce nice image of current state of countdown
(check-expect (countdown-to-image false) (square 0 "solid" "white"))
(check-expect (countdown-to-image 5) (text (number->string 5) 24 "black"))
(check-expect (countdown-to-image "complete") (text "Happy New Year!!!" 24 "red"))

; stub(define (countdown-to-image c) (square 0 "solid" "white"))
;<use template from Countdown>

(define (countdown-to-image c)
  (cond [(false? c)
         (square 0 "solid" "white")]
        [(and (number? c) (<= 1 c) (<= c 10))
         (text (number->string c) 24 "black")]
        [else
         (text "Happy New Year!!!" 24 "red")]))
```