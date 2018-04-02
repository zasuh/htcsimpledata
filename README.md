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

### March 5th 2018 ###
- Information leads to data definition which leads to function definition.

### March 6th 2018 ###
- HtDD P2 - Demolish:
```
;; DATA DEFINITION
;; BuildingStatus is one of:
;; - "new"
;; - "old"
;; - "heritage"
;; interp. the status of a building in downtown Vancouver

;; <examples are redundant for enumerations>

#;
(define (fn-for-building-status bs)
  (cond [(string=? "new" bs) (...)]
        [(string=? "old" bs) (...)]
        [(string=? "heritage" bs) (...)]))

;; Template rules used:
;; - one of: 3 cases
;;  - atomic distinct: "new"
;;  - atomic distinct: "old"
;;  - atomic distinct: "heritage"

;; FUNCTION DEFINITION
;; String -> Boolean
;; produces true if the building status is old and false if the status is new or heritage

(check-expect (demolish? "new") false)
(check-expect (demolish? "old") true)
(check-expect (demolish? "heritage") false)

; stub (define (demolish? bs) false)

; <template taken from data definition>
(define (demolish? bs)
  (cond [(string=? "new" bs) false]
        [(string=? "old" bs) true]
        [else false]))
```

### March 7th 2018 ###
- Solution for HtDD P3 - Rocket Descent
```
; You are designing a program to track a rocket's journey as it descends 
; 100 kilometers to Earth. You are only interested in the descent from 
; 100 kilometers to touchdown. Once the rocket has landed it is done.
; 
; Design a data definition to represent the rocket's remaining descent. 
; Call it RocketDescent.


;; RocketDescent is Integer[0, 100]
;; interp. the number of kilometers remaining untill touchdown
(define RD1 100) ;start
(define RD2 50) ;middle
(define RD3 0) ;end

#;
(define (fn-for-rocket-descent rd)
    (cond [(and (number? rd)
              (<   0 rd)
              (<= rd 100))
         (... rd)]
         [else  (...)])) 

;; Template rules used;
;; -one of: 2 cases
;; -atomic non-distinct: Integer[0, 100]
;; -atomic distinct: false

; Design a function that will output the rocket's remaining descent distance 
; in a short string that can be broadcast on Twitter. 
; When the descent is over, the message should be "The rocket has landed!".
; Call your function rocket-descent-to-msg.


;; RocketDescent -> String
;; Takes the number of the distance and produces a string based on the distance
(check-expect (rocket-descent-to-msg 100) "Distance is 100 km")
(check-expect (rocket-descent-to-msg 50) "Distance is 50 km")
(check-expect (rocket-descent-to-msg 0) "The rocket has landed!")


;(define (rocket-descent-to-msg rd) "") stub

; <template from RocketDescent>
(define (rocket-descent-to-msg rd)
    (cond [(and (number? rd)
              (<   0 rd)
              (<= rd 100))
         (string-append "Distance is " (number->string rd) "km")]
         [else  "The rocket has landed"])) 
```

### March 8th 2018 ###
- Solution to HtDD Quiz:
```
;; Age is Natural
;; interp. the age of a person in years
(define A0 18)
(define A1 25)

#;
(define (fn-for-age a)
  (... a))

;; Template rules used:
;; - atomic non-distinct: Natural

; Consider the above data definition for the age of a person.
; 
; Design a function called teenager? that determines whether a person
; of a particular age is a teenager (i.e., between the ages of 13 and 19).

;; Age -> Boolean
;; Takes age and produces true if the person is a teenager (13 to 19)
(check-expect (teenager? 14) true)
(check-expect (teenager? 11) false)
(check-expect (teenager? 19) true)
(check-expect (teenager? 9) false) 

;(define (teenager? a) true) stub
;<template taken from above data definition>

#;
(define (teenager? a)
  (... a))

(define (teenager? a)
  (<= 13 a 19))

; Design a data definition called MonthAge to represent a person's age
; in months.

;; MonthAge is Natural
;; interp. the age of a person in months
(define MA1 72)
(define MA2 24)

#;
(define (fn-for-month-age ma)
  (... ma))

;; Template rulse used:
;; - atomic non-distinct: Natural

; Design a function called months-old that takes a person's age in years 
; and yields that person's age in months.

;; MonthAge -> YearAge
;; Takes the number of months the persons age is and converts to years.
(check-expect (months-old 3) 72)
(check-expect (months-old 0) 0)
(check-expect (months-old 5.5) 66)

;(define (months-old a) 0) stub
;<template taken from data definition above>

#;
(define (months-old a)
  (... a))

(define (months-old a)
  (* 12 a))

; Problem 4:
; 
; Consider a video game where you need to represent the health of your
; character. The only thing that matters about their health is:
; 
;   - if they are dead (which is shockingly poor health)
;   - if they are alive then they can have 0 or more extra lives
; 
; Design a data definition called Health to represent the health of your
; character.
; 
; Design a function called increase-health that allows you to increase the
; lives of a character.  The function should only increase the lives
; of the character if the character is not dead, otherwise the character
; remains dead.

;; Health is one of:
;; - "dead"
;; - Natural 
;; interp. player is either dead or has 0 or more extra lives
(define H1 "dead")
(define H2 5)

#;
(define (fn-for-health h)
  (cond [(number? n) (...)]
        [else (...)]))

;; Template used:
;; -one of: 2 cases
;; -atomic non-distinct: Natural
;; -atomic distinct: "dead"

;; Health -> Health
;; Takes player health and increases health if player is not dead
(check-expect (increase-health 2) 3)
(check-expect (increase-health "dead") "dead")
(check-expect (increase-health 5) 6)

;(define (increase-health h) 0) stub
;<template taken from data definition>

#;
(define (fn-for-health h)
  (cond [(number? n) (...)]
        [else (...)]))

(define (increase-health h)
  (cond [(number? h) (add1 h)]
        [else h]))
```
### March 9th 2018 ###
- The first phase of the How to Design Worlds (HtDW) recipe is to analyze the problem to identify constant information, changing information and required big-bang options.
- The second phase of the How to Design Worlds (HtDW) involves going from the analysis to the overall structure of the main program. This is our first example of a larger program, and we use the wish-list technique to manage the overall design work.
```
(require 2htdp/image)
(require 2htdp/universe)

;; A cat that walks from left to right across the screen.

;; =================
;; Constants:
(define WIDTH 600)
(define HEIGHT 400)

(define CTR-Y (/ HEIGHT 2))

(define MTS (empty-scene WIDTH HEIGHT))

(define CAT-IMG .)

;; =================
;; Data definitions:

;; Cat is Number
;;interp. x position of the car in screen coordinates
(define C1 0)
(define C2 (/ WIDTH 2))
(define C3 WIDTH)

#;
(define (fn-for-cat c)
  (... c))

;; Template rules used:
;; - atomic non-distinct: Number

;; =================
;; Functions:

;; Cat -> Cat
;; start the world with ...
;; 
(define (main c)
  (big-bang c                       ; Cat
            (on-tick   advance-cat) ; Cat -> Cat
            (to-draw   render)))    ; Cat -> Image

;; Cat -> Cat
;; produce the next cat, by advancing it 1 pixel to right
;; !!!
(define (advance-cat Cat) 0)


;; Cat -> Image
;; render the cat image at appropriate place on MTS
;; !!!
(define (render c) MTS)
```

### March 10th 2018 ###
```
(require 2htdp/image)
(require 2htdp/universe)

;; A cat that walks from left to right across the screen.

;; =================
;; Constants:
(define WIDTH 600)
(define HEIGHT 400)

(define CTR-Y (/ HEIGHT 2))

(define MTS (empty-scene WIDTH HEIGHT))

(define CAT-IMG .)

;; =================
;; Data definitions:

;; Cat is Number
;;interp. x position of the car in screen coordinates
(define C1 0)
(define C2 (/ WIDTH 2))
(define C3 WIDTH)

#;
(define (fn-for-cat c)
  (... c))

;; Template rules used:
;; - atomic non-distinct: Number

;; =================
;; Functions:

;; Cat -> Cat
;; start the world with ...
;; 
(define (main c)
  (big-bang c                       ; Cat
            (on-tick   advance-cat) ; Cat -> Cat
            (to-draw   render)))    ; Cat -> Image

;; Cat -> Cat
;; produce the next cat, by advancing it 1 pixel to right
(check-expect (advance-cat 3) 4)

; stub (define (advance-cat Cat) 0)
;<use template from Cat>

#;
(define (advance-cat c)
  (+ c 1))

;; Cat -> Image
;; render the cat image at appropriate place on MTS
(check-expect (render 4) (place-image CAT-IMG 4 CTR-Y MTS))

; stub (define (render c) MTS)
;<use template from Cat>

#;
(define (render c)
  (place-image CAT-IMG c CTR-Y MTS))
```
- Given an existing world program we can extend it with new behavior by using the analysis as a model of the program in order to plan the revision. 

```
(require 2htdp/image)
(require 2htdp/universe)

;; cat-v1.rkt

;; A cat that walks from left to right across the screen.

;; =================
;; Constants:

(define WIDTH 600)
(define HEIGHT 400)

(define CTR-Y (/ HEIGHT 2))

(define SPEED 3)

(define MTS (empty-scene WIDTH HEIGHT))

(define CAT-IMG .)




;; =================
;; Data definitions:

;; Cat is Number
;; interp. x position of the cat in screen coordinates
(define C1 0)           ;left edge
(define C2 (/ WIDTH 2)) ;middle
(define C3 WIDTH)       ;right edge
#;
(define (fn-for-cat c)
  (... c))

;; Template rules used:
;;  - atomic non-distinct: Number



;; =================
;; Functions:

;; Cat -> Cat
;; start the world with (main 0)
;; 
(define (main c)
  (big-bang c                       ; Cat
            (on-tick   advance-cat) ; Cat -> Cat
            (to-draw   render)))    ; Cat -> Image

;; Cat -> Cat
;; produce the next cat, by advancing it SPEED pixels to right
(check-expect (advance-cat 3) (+ 3 SPEED))

;(define (advance-cat c) 0) ;stub

;<use template from Cat>

(define (advance-cat c)
  (+ c SPEED)) 


;; Cat -> Image
;; render the cat image at appropriate place on MTS 
(check-expect (render 4) (place-image CAT-IMG 4 CTR-Y MTS)) 
              
;(define (render c) MTS) ;stub

;<use template from Cat>

(define (render c)
  (place-image CAT-IMG c CTR-Y MTS)) 
```
- We now extend the cat program to respond to keyboard events.
```

### March 11th 2018 ###
- Solution for HtDW P1 - Countdown:
```
(require 2htdp/image)
(require 2htdp/universe)

; Design an animation of a simple countdown. 
; 
; Your program should display a simple countdown, that starts at ten, and
; decreases by one each clock tick until it reaches zero, and stays there.
; 
; To make your countdown progress at a reasonable speed, you can use the 
; rate option to on-tick. If you say, for example, 
; (on-tick advance-countdown 1) then big-bang will wait 1 second between 
; calls to advance-countdown.
; 
; Remember to follow the HtDW recipe! Be sure to do a proper domain 
; analysis before starting to work on the code file.
; 
; Once you are finished the simple version of the program, you can improve
; it by reseting the countdown to ten when you press the spacebar.


;; Count down program that counts from 10 to 0.

;; =============
;; Constants

(define WIDTH 100)
(define HEIGHT 100)

(define CTR-Y (/ HEIGHT 2))
(define CTR-X (/ WIDTH 2))

(define MTS (empty-scene WIDTH HEIGHT))

(define TEXT-SIZE 36)
(define TEXT-COLOR "black")

;; =============
;; Data definition

;; CountDown is Natural[0, 10]
;; interp. Numbers that will be displayed for the countdown

(define START-TIME 10)
(define IN-PROGRESS 5)
(define END-TIME 0)

#;
(define (fn-for-countdown cd)
  (... cd))

;; Templates used:
;; -atomic non-distinct: Natural[0, 10]

;; =============
;; Functions

;; Countdown -> Countdown
;; called to run the animation, starting with (main 10)
;; no tests required for main function

(define (main cd)
  (big-bang cd
    (on-tick advance-countdown 1) ; Countdown -> Countdown
    (to-draw render-countdown)    ; Countdown -> Image
    (on-key handle-key)))         ; Countdown KeyEvent -> Countdown

;; Countdown -> Countdown
;; If cd = 0, keep 0, otherwise remove 1
(check-expect (advance-countdown 10) 9)
(check-expect (advance-countdown 5) 4)
(check-expect (advance-countdown 3) 2)
(check-expect (advance-countdown 0) 0)


;(define (advance-countdown cd) 0) ;stub
;<template taken from data definition>

(define (advance-countdown cd)
  (if (= cd 0)
      0
      (- cd 1)))

;; Countdown -> Image
;; Shows image (number) for the appropriate countdown
(check-expect (render-countdown 10) (place-image (text "10" TEXT-SIZE TEXT-COLOR CTR-X CTR-Y MTS)))
(check-expect (render-countdown 0) (place-image (text "0" TEXT-SIZE TEXT-COLOR CTR-X CTR-Y MTS)))

;(define (render-countdown cd) MTS) ;stub
;<template taken from data definition>

(define (render-countdown cd)
  (place-image (text (number->string)
   TEXT-SIZE TEXT-COLOR CTR-X CTR-Y MTS)))

;; Countdown KeyEvent -> Countdown
;; reset the countdown to 10 when the spacebar is pressed
(check-expect (handle-key 0 " ") 10)
(check-expect (handle-key 5 " ") 10)
(check-expect (handle-key 5 "left") 5)

#;
(define (handle-key cd ke)    ;stub
  0)

;<template from KeyEvent>

(define (handle-key cd ke)
  (cond [(key=? ke " ") 10]
        [else cd]))
```

### March 12th 2018 ###
- A new mechanism from the BSL language allows us to build multi-part (or compound) values and later to desconstruct the compound values to get the individual values back.
- Basic design-struct definition:
```
(define-struct pos (x y))

(define P1(make-pos 3 6);constructor)
(define P2(make-pos 2 8))

(pos-x P1) ;selector for x(3)
(pos-y P2) ;selector for y(8)

(pos? P1) ;predicate(true)
(pos? "hello") ;predicate(false)
```
- Compound data definition example:
```
; Design a data definition to represent hockey players, including both 
; their first and last names.


(define-struct player(fn ln))
;; Player is (make-player String String)
;; interp. (make-player fn ln) is a hockey player with
;; fn is first name and ln is last name.
(define P1 (make-player "Bobby" "Orr"))
(define P2 (make-player "Anze" "Kopitar"))

(define (fn-for-player p)
  (... (player-fn p) ;String
       (player-ln p))) ;String

;; Template rules used:
;; - Compound: 2 fields
```

### March 13th 2018 ###
```
;; Data definitions
;; ================

(define-struct movie (title budget rd))
;; Movie is (make-movie String Number Number)
;; interp. a movie with a title, a budget and release date

(define MOVIE1 (make-movie "Titanic" 200000000 1997))
(define MOVIE2 (make-movie "Avatar" 237000000 2009))
(define MOVIE3 (make-movie "Avengers" 220000000 2012))

#;
(define (fn-for-movie m)
  (... (movie-title m)  ;String
       (movie-budget m) ;Number
       (movie-rd m)))   ;Number
;; Template rules used:
;; - compound: 3 fields

;; Functions
;; ================

;; Movie Movie -> String
;; Consumes year of 2 movies release and produces the more recent movie
(check-expect (chrono-movie M1 M2) "Avatar")
(check-expect (chrono-movie M2 M3) "Avengers")

;(define (chrono-movie m1 m2) "") ;stub

#;
(define (fn-for-movie m1 m2)
  (... (movie-title m1)
       (movie-budget m1)
       (movie-rd m1)
       (movie-title m2)
       (movie-budget m2)
       (movie-rd m2)))

(define (chrono-movie m1 m2)
  (if ( > (movie-rd m1) (movie-rd m2))
      (movie-title m1)
      (movie-title m2)))
```

### March 14th 2018 ###
- Solution for Compound P2 - Student:
```
; PROBLEM A:
; 
; Design a data definition to help a teacher organize their next field trip. 
; On the trip, lunch must be provided for all students. For each student, track 
; their name, their grade (from 1 to 12), and whether or not they have allergies.


;; Data definitions
;; ================

(define-struct student (name grade allergies))
;; Student is (make-student String Natural Boolean)
;; interp. a student with a name, grade and whether or not they have allergies

(define STUDENT1 (make-student "John" 6 true))
(define STUDENT2 (make-student "Elise" 1 false))
(define STUDENT3 (make-student "Tyler" 8 false))
(define STUDENT1 (make-student "Kerry" 12 true))

#;
(define (fn-for-student s)
  (... (student-name s)      ;String
       (student-grade s)     ;Natural
       (student-allergies s) ;Boolean
;; Template rules used:
;; - compound: 3 fields

; To plan for the field trip, if students are in grade 6 or below, the teacher 
; is responsible for keeping track of their allergies. If a student has allergies, 
; and is in a qualifying grade, their name should be added to a special list. 
; Design a function to produce true if a student name should be added to this list.

       
;; Functions
;; ================

;; Student -> Boolean
;; Consumes student, produces true if student is in grade 6 or below, has allergies
(check-expect (add-name? S1) true)
(check-expect (add-name? S2) false)
(check-expect (add-name? (make-student "Alex" 9 true) false))
(check-expect (add-name? (make-student "Natasha" 4 false) false))

;(define (add-name? s) false) ;stub
; <template taken from data definition>

(define (add-name? s)
  (and (<= (student-grade 6)
           (student-allergies? true)))
```

### March 15th 2018 ###
```
(define WIDTH 400)
(define HEIGHT 200)

(defin CTR-Y (/ HEIGHT 2))

(define RCOW .)

(define LCOW .)

(define MTS (empty-scene WIDTH HEIGHT))

;; Data definitions
;; ================
(define-struct cow (x dx))
;; Cow is (make-cow Natural[0, WIDTH] Interger)
;; interp. (make-cow x dx) is a cow with x coordinate x and velocity dx
;;         x is the center of the cow, x is in screen coordinates (pixels)
;;         dx is in pixels per tick

(define C1 (make-cow 10 3)) ;at 10, moving left -> right
(define C2 (make-cow 20 -4)) ;at 20, moving right -> left

#;
(define (fn-for-cow c)
  (... (cow-x c)    ;Natural[0, WIDTH]
       (cow-dx c))) ;Integer

;; Template rules used:
;; - compound: 2 fields


;; Functions
;; ================

;; Cow -> Cow
;; called to make the cow go for a walk; start with (main (make-cow 0 3))
;; no tests for main function
(define (main c)
  (big-bang c
            (on-tick next-cow)       ; Cow -> Cow
            (to-draw render-cow)     ; Cow -> Image
            (on-key  handle-key)))   ; Cow KeyEvent -> Cow



;; Cow -> Cow  
;; increase cow x by dx; bounce off edges
(check-expect (next-cow (make-cow 20 3)) (make-cow (+ 20 3) 3) ;middle
(check-expect (next-cow (make-cow 20 -3)) (make-cow (-20 3) -3)
              
(check-expect (next-cow (make-cow (- WIDTH 3) 3) (make-cow WIDTH 3)) ;edge
(check-expect (next-cow (make-cow 3 -3)) (make-cow 0 -3))

(check-expect (next-cow (make-cow (- WIDTH 2) 3) (make-cow WIDTH -3)) ;tries to pass edge
(check-expect (next-cow (make-cow 2 -3)) (make-cow 0 3))

(define (next-cow c) c)      ;stub

;<took template from Cow>
(define (next-cow c)
  (cond [(> (+ (cow-x c) (cow-dx c)) WIDTH) (make-cow WIDTH (- (cow-dx c)))]
        [(< (+ (cow-x c) (cow-dx c)) 0) (make-cow 0 (- (cow-dx c)))]
        [else (make-cow (+ (cow-x c) (cow-dx c)) (cow-dx c))]))

;; Cow -> Image
;; place appropriate cow image on MTS at (cow-x c) and CTR-Y
(check-expect (render-cow (make-cow 99 3))
              (place-image RCOW 99 CTR-Y MTS))
(check-expect (render-cow (make-cow 33 -3))
              (place-image RCOW 33 CTR-Y MTS))

;(define (render-cow c) MTS)  ;stub  
;<took template from Cow>

(define (render-cow c)
  (place-image (choose-image c) (cow-x c) CTR-Y MTS))

;; Cow -> Image
;; produce RCOW or LCOW depending on direction cow is going.
(check-expect (choose-image (make-cow 10 3)) RCOW)
(check-expect (choose-image (make-cow 10 -3)) LCOW)
(check-expect (choose-image (make-cow 11 0)) LCOW)

;(define (choose-image c) RCOW); stub
;<took template from Cow>

(define (choose-image c)
  (if (> (cow-dx) 0)
      RCOW
      LCOW))

;; Cow KeyEvent-> Cow
;; reverse direction of cow travel when space bar is pressed
(check-expect (handle-key 

(define (handle-key c ke) c) ;stub
```

### March 18th 2018 ###
- Solution for Compound Data Quiz:
```
; Create a program that allows you to click on a spot on the screen to create a flower,
; which then grows over time.
; If you click again the first flower is replaced by a new one at the new position.

(require 2htdp/image)
(require 2htdp/universe)

;; Constants
;; ==========

(define WIDTH 500)
(define HEIGHT 500)
(define MTS (empty-scene 500 500 "lightgreen"))

(define CENTER (cirlce 15 "solid" "lightyellow"))
(define PETAL (ellipse 30 50 "solid" "purple"))
(define FLOWER
  (overlay (above CENTER(rectangle 1 10 0 "white"))
           (overlay/align "center" "top" (above (beside (rotate 216 PETAL) (rectangle 1 1 0 "white")(rotate 144 PETAL))
                                                (rotate 180 (beside (rotate 72 PETAL)(rectangle 10 0 0 "white")(rotate 288 PETAL))))
                          (above (rectangle 1 61 0 "white") PETAL))))

;; Data Definitions
;; ================

(define-struct flower (x y size))
;; Flower is (make-flower Integer Integer Natural)
;; interp. a flower with x position, y position and a side length
(define F0 (make-flower 0 0 0))
(define F1 (make-flower (/ WIDTH 2) (/HEIGHT 2) 15))

#;
(define (fn-for-flower)
  (... (flower-x)
       (flower-y)
       (flower-size)))

;; Template rules used:
;; Compound: 3 fields


;; Functions
;; =========

;; Flower -> Flower
;; starts the animation: start with (main (make-flower (/ WIDTH 2) (/ HEIGHT 2) 0))

(define (main f)
  (big-bang f
    (on-tick tock)          ;Flower -> Flower
    (to-draw render)        ;Flower -> Image
    (on-mouse handle-mouse) ;Flower Integer Integer MouseEvent -> Flower

;; Flower -> Flower
;; adds 1 to the size of the flower every clock tick
(check-expect (tock (make-flower 0 0 5)) (make-flower 0 0 6))
(check-expect (tock (make-flower 20 30 19)) (make-flower 20 30 20))    
(check-expect (tock (make-flower 30 40 49)) (make-flower 30 40 50))

;(define (tock f) f) ;stub
; <took template from Flower>

(define (tock f)
  (make-flower (flower-x f)
               (flower-y f)
               (add1 (flower-size f))))

;; Flower -> Flower
;; renders the flower on the screen
(check-expect (render (make-flower 10 10 20)) (place-image (rotate 20 (scale (/ 20 100) FLOWER))
                                                           10 10 MTS))
(check-expect (render (make-flower 20 20 0)) (place-image empty-image
                                                           20 20 MTS))
(check-expect (render (make-flower 10 10 40)) (place-image (rotate 40 (scale (/ 40 100) FLOWER))
                                                           10 10 MTS))

; (define (render f) MTS) ;stub
; <took template from Flower>

(define (render f)
  (place-image (if (zero? (flower-size f))
                    empty-image
                    (rotate (flower-size f) (scale (/ (flower-size f) 100) FLOWER)))
               (flower-x f)
               (flower-y f)
               MTS))

;; Flower Integer Intger MouseEvent -> Flower
;; replace the flower with a new one of size 0 at the mouse-Click
(check-expect (handle-mouse (make-flower 0 0 0) 5 5 "button-down") (make-flower 5 5 0))
(check-expect (handle-mouse (make-flower 0 0 0) 5 5 "button-up") (make-flower 0 0 0))
(check-expect (handle-mouse (make-flower 50 50 55) 10 10 "button-down") (make-flower 10 10 0))

; (define (handle-mouse f x y me) f) ;stub
; <took template from MouseEvent>

(define (handle-mouse f x y me)
  (cond [(mouse=? me "button-down")(make-flower x y 0)]
        [else f]))
```
- List constructinon and syntax:
```
(require 2htdp/image)

empty

(define L1(cons "Flames" empty)) ;a list with "Flames" in front of an empty list
(define L2(cons "Leafs" (cons "Flames" empty))) ;list with 2 elements

(cons (string-append "C" "anucks") empty)
;; expressions that produce lists can be formed out of non-value expressions
;; list values are formed out of values only, no other expressions

;(cons 10 (cons 9 (cons 10 empty))) ;list with 3 elements
(define L3(cons (square 10 "solid" "blue")
      (cons (triangle 20 "solid" green)
       empty)))

(first L1) ;Flames
(first L2) ;10
(first L3) ;Blue Square of size 10

(rest L1) ;empty
(rest L2)
(rest L3)

(first (rest L2))        ;how do I get the second element of L2?
(first (rest (rest L2))) ;third element

(empty? empty) ;true
(empty? L1)    ;false
```

### March 19th 2018 ###
```
; Information:
; UBC
; McGill
; Team Who Must Not Be Named
; 
; Data:
; "UBC"
; "McGill"
; "Team Who Must Not Be Named
; "
; 
; (cons "UBC"
;      (cons "McGill") empty)


;; ListOfString is one of:
;; - empty
;; - (cons String ListOfString)
;; interp. a list of strings
(define LOS1 empty)
(define LOS2 (cons "McGill" empty))
(define LOS3 (cons "UBC" (cons "McGill" empty)))

(define (fn-for-los los)
  (cond [(empty? los) (...)]
        [else
         (... (first los)    ;String
              (fn-for-los (rest los)))])) ;ListOfString

;; Template rules used:
;; - one of: 2 cases
;; - atomic distinct: empty
;; - compound: (cons String ListOfString)
```

### March 20th 2018 ###
```
;; Function
;; ============

;; ListOfString -> Boolean
;; produce true if los includes "UBC"
(check-expect (contains-ubc? empty) false)
(check-expect (contains-ubc? (cons "McGill" empty)) false)
(check-expect (contains-ubc? (cons "UBC" empty)) true)
(check-expect (contains-ubc? (cons "McGill" (cons "UBC" empty))) true)

;(define (contains-ubc los) false) ;stub
;<took template from ListOfString>

(define (contains-ubc? los)
  (cond [(empty? los) false]
        [else
         (if (string=?  (first los) "UBC")
             true
             (contains-ubc? (rest los)))]))
```

### March 21st 2018 ###
```
;; ListOfString is one of: 
;;  - empty
;;  - (cons String ListOfString)
;; interp. a list of strings
(define LOS1 empty)
(define LOS2 (cons "McGill" empty))
(define LOS3 (cons "UBC" (cons "McGill" empty)))
#;
(define (fn-for-los los)
  (cond [(empty? los) (...)]
        [else
         (... (first los)     
              (fn-for-los (rest los)))]))

;; Template rules used:
;;  - one of: 2 cases
;;  - atomic distinct: empty
;;  - compound: (cons String ListOfString)
;;  - self-reference: (rest los) is ListOfString

;; ListOfString -> Boolean
;; produce true if los includes "UBC"
(check-expect (contains-ubc? empty) false)
(check-expect (contains-ubc? (cons "McGill" empty)) false)
(check-expect (contains-ubc? (cons "UBC" empty)) true)
(check-expect (contains-ubc? (cons "McGill" (cons "UBC" empty))) true)

;(define (contains-ubc? los) false) ;stub

(define (contains-ubc? los)
  (cond [(empty? los) false]
        [else
         (if (string=? (first los) "UBC")
             true
             (contains-ubc? (rest los)))]))
```
```
;; Data definitions:

;; ListOfNumber is one of:
;;  - empty
;;  - (cons Number ListOfNumber)
;; interp. each number in the list is an owl weight in ounces
(define LON1 empty)
(define LON2 (cons 60 (cons 42 empty)))
#;
(define (fn-for-lon lon)
  (cond [(empty? lon) (...)]
        [else
         (... (first lon)
              (fn-for-lon (rest lon)))]))

;; Template rules used:
;;  - one of: 2 cases
;;  - atomic distinct: empty
;;  - compound: (cons Number ListOfNumber)
;;  - self-reference: (rest lon) is ListOfNumber

  

;; Functions:

;; ListOfNumber -> Number
;; produce sum of weights of owls in lon
(check-expect (sum empty) 0)
(check-expect (sum (cons 20 empty)) 20)
(check-expect (sum (cons 32 (cons 20 empty))) (+ 32 20))

;(define (sum lon) 0) ;stub

(define (sum lon)
  (cond [(empty? lon) 0]
        [else
         (+ (first lon)          
            (sum (rest lon)))]))
```

### March 22nd 2018 ###
```
;; ListOfNumber -> Natural
;; produce total number of weights in consumed list
(check-expect (count empty) 0)
(check-expect (count (cons 12 empty)) (+ 1 0))
(check-expect (count (cons 35 (cons 12 empty))) (+ 1 (+ 1 0)))

;(define (count lon) 0) stub

(define (count lon)
  (cond [(empty? lon) 0]
        [else
         (+ 1
              (count (rest lon)))]))
```

### March 23rd 2018 ###
- Solution for Self reference P2 - Double all:
```
;; Data definitions:

;; ListOfNumber is one of:
;;  - empty
;;  - (cons Number ListOfNumber)
;; interp. a list of numbers
(define LON1 empty)
(define LON2 (cons 60 (cons 42 empty)))
#;
(define (fn-for-lon lon)
  (cond [(empty? lon) (...)]
        [else
         (... (first lon)
              (fn-for-lon (rest lon)))]))

;; Template rules used:
;;  - one of: 2 cases
;;  - atomic distinct: empty
;;  - compound: (cons Number ListOfNumber)
;;  - self-reference: (rest lon) is ListOfNumber

;; Functions:

;; ListOfNumber -> ListOfNumber
;; produces multiplied by 2 ListOfNumber
(check-expect (double-all empty) empty)
(check-expect (double-all LON 2(cons 60 (cons 42 empty))))
(check-expect (double-all (cons 10 (cons 20 (cons 40 empty))))
              (cons 20 (cons 40 (cons 80 empty))))

;(define (double-all lon) empty) ;stub
;<took template from ListOfNumber>

#;
(define (double-all lon)
  (cond [(empty? lon) empty]
        [else
         (cons (* 2 (first lon))
              (double-all (rest lon)))]))
```
- Solution for Self Reference P5 - Largest:
```
;; Data definitions:

;; ListOfNumber is one of:
;;  - empty
;;  - (cons Number ListOfNumber)
;; interp. a list of numbers
(define LON1 empty)
(define LON2 (cons 60 (cons 42 empty)))
#;
(define (fn-for-lon lon)
  (cond [(empty? lon) (...)]
        [else
         (... (first lon)
              (fn-for-lon (rest lon)))]))

;; Template rules used:
;;  - one of: 2 cases
;;  - atomic distinct: empty
;;  - compound: (cons Number ListOfNumber)
;;  - self-reference: (rest lon) is ListOfNumber

;; Functions:

;; ListOfNumber -> Number
;; consumes a list of numbers and produces the largest number in the list
(check-expect (largest empty) empty)
(check-expect (largest (cons 4 (cons 7 (cons 9 empty)))) 9)
(check-expect (largest (cons 14 (cons 10 (cons 50 (cons 3 (cons 49 empty)))))) 50)

;(define (largest lon) 0) ;stub
;<took template from ListOfNumber>

(define (largest lon)
  (cond [(empty? lon) 0]
        [else
         (if (> (first lon) (largest (rest lon)))
              (first lon)
              (largest (rest lon)))]))
```

### March 25th 2018 ###
- Solution for Self-Reference P3 - Boolean List:
```
; Design a data definition to represent a list of booleans. Call it ListOfBoolean.


;; =================
;; Data definitions:

;; ListOfBoolean is one of:
;; - empty
;; - (cons Boolean ListOfBoolean)
;; interp. a list of booleans
(define LOB1 empty)
(define LOB2 (cons true (cons false empty)))

#;
(define (fn-for-lob lob)
    (cond [(empty? lob) (...)]
        [else
         (... (first lob)
              (fn-for-lob (rest lob)))]))

;; Template rules used:
;; - one of: 2 cases
;; - atomic distinct: empty
;; - compound: (cons Boolean ListOfBoolean)
;; - self-reference: (rest lob) is ListOfBoolean

; Design a function that consumes a list of boolean values and produces true 
; if every value in the list is true. If the list is empty, your function 
; should also produce true. Call it all-true?


;; =================
;; Functions:

;; ListOfBoolean -> Boolean
;; consumes a list of boolean values and produces true 
;; if every value in the list is true. If list is empty also produces true.
(check-expect (all-true? empty) true)
(check-expect (all-true? (cons true (cons true (cons true empty)))) true)
(check-expect (all-true? (cons false (cons true (cons false empty)))) false)
(check-expect (all-true? (cons false (cons false (cons false empty)))) false)

;(define (all-true? lob) false) ;stub
;<took template from ListOfBoolean>

(define (all-true? lob)
    (cond [(empty? lob) true]
        [else
         (and (first lob)
              (all-true? (rest lob)))]))
```
- Solution for Self-Reference P6 - Image List:
```
(require 2htdp/image)

;; =================
;; Data definitions:

; Design a data definition to represent a list of images. Call it ListOfImage.


;; ListOfImage is one of:
;; - empty
;; - (cons Image ListOfImage)
;; interp. a list of images
(define LOI1 empty)
(define LOI2 (cons (circle 30 "solid" "black") empty))
(define LOI3 (cons (circle 50 "solid" "red") (cons (circle 20 "solid" "blue") empty)))

#;
(define (fn-for-loi loi)
    (cond [(empty? loi) (...)]
        [else
         (... (first loi)
              (fn-for-loi (rest loi)))]))

;; Template rules used:
;; - one of: 2 cases
;; - atomic distinct: empty
;; - compound: (cons Image ListOfImage)
;; - self-reference: (rest loi) is ListOfImage

;; =================
;; Functions:

; Design a function that consumes a list of images and produces a number 
; that is the sum of the areas of each image. For area, just use the image's 
; width times its height.


;; ListOfImage -> Number
;; consumes list and produces sum of the areas of each image
(check-expect (area-sum empty) empty)
(check-expect (area-sum (cons (rectangle 5 10 "solid" "black")
                              (cons (rectangle 4 8 "solid" "blue") empty))) 82)
(check-expect (area-sum (cons (square 5 "solid" "black")
                              (cons (square 6 "solid" "blue") empty))) 58)

;(define (area-sum loi) empty) ;stub
;<took template from ListOfImage>

(define (area-sum loi)
    (cond [(empty? loi) empty]
        [else
         (+ (* (image-width (first loi))
                (image-height (first loi)))
              (area-sum (rest loi)))]))
```

### March 26th 2018 ###
```
(require 2htdp/image)

;; Constants

(define FONT-SIZE 24)
(define FONT-COLOUR "black")

(define Y-SCALE 1/200)
(define BAR-WIDTH 30)
(define BAR-COLOUR "lightblue")

;; Data Definitions:

(define-struct school (name tuition))
;; School is (make-school String Natural)
;; interp. name is the school's name tuition is international student's tuition in USD

(define S1 (make-school "Schooll" 27797))
(define S1 (make-school "School2" 44886))
(define S1 (make-school "School3" 23867))

(define (fn-for-school s)
  (... (school-name s)
       (school-tuition s)))

;; Template rules used:
;; - compound: (make-school String Natural)

;; ListOfSchool is one of:
;; - empty
;; - cons (School ListOfSchool)
;; interp. a list of schools
(define LOS1 empty)
(define LOS2 (cons S1 (cons S2 (cons S3 empty))))

(define (fn-for-los los)
  (cond [(empty? los) (...)]
        [else
         (... (first los)
              (fn-for-los (rest los)))]))

;; Template rules used:
;; - one of: 2 cases
;; - atomic distinct: empty
;; - compound: (cons School ListOfSchool)
;; - reference: (first los)
;; - self-reference: (rest los) is ListOfSchool
```

### March 27th 2018 ###
- Continued from yesterday:
```
;; Functions:

;; ListOfSchool -> Image
;; produce bar chart showing names and tuitions of the consumed schools
(check-expect (chart empty) (square 0 "solid" "white"))
(check-expect (chart (cons (make-school "S1" 8000) empty))
              (beside (overlay/align "center" "bottom"
                      (rotate 90 (text "S1" FONT-SIZE FONT-COLOR))
                      (rectangle BAR-WIDTH (* 8000 Y-SCALE) "outline" "black")
                      (rectangle BAR-WIDTH (* 8000 Y-SCALE) "solid" BAR-COLOR))
                      (square 0 "solid" "white")))
(check-expect (chart (cons (make-school "S2" 12000) (cons (make-school "S1" 8000) empty)))
              (beside/align "bottom" (overlay/align "center" "bottom"
                      (rotate 90 (text "S1" FONT-SIZE FONT-COLOR))
                      (rectangle BAR-WIDTH (* 12000 Y-SCALE) "outline" "black")
                      (rectangle BAR-WIDTH (* 12000 Y-SCALE) "solid" BAR-COLOR))
              (beside/align "bottom" (overlay/align "center" "bottom"
                      (rotate 90 (text "S2" FONT-SIZE FONT-COLOR))
                      (rectangle BAR-WIDTH (* 8000 Y-SCALE) "outline" "black")
                      (rectangle BAR-WIDTH (* 8000 Y-SCALE) "solid" BAR-COLOR))
              (square 0 "solid" "white"))))

;(define (chart los) (square 0 "solid" "white")) ;stub

(define (chart los)
  (cond [(empty? los) (square 0 "solid" "white")]
        [else
         (beside/align "bottom"
                       (make-bar (first los))
                       (chart (rest los)))]))
;; School -> Image
;; produce the bar for a single school in the bar chart
(check-expect (make-bar (make-school "S1" 8000))
              (overlay/align "center" "bottom"
                      (rotate 90 (text "S2" FONT-SIZE FONT-COLOR))
                      (rectangle BAR-WIDTH (* 8000 Y-SCALE) "outline" "black")
                      (rectangle BAR-WIDTH (* 8000 Y-SCALE) "solid" BAR-COLOR)))
;; !!!
;(define (make-bar s) (square 0 "solid" "white")) ;stub

(define (make-bar s)
  (overlay/align "center" "bottom"
                 (rotate 90 (text (school-name s) FONT-SIZE FONT-COLOR))
                 (rectangle BAR-WIDTH (* (school-tuition s) Y-SCALE) "outline" "black")
                 (rectangle BAR-WIDTH (* (school-tuition s) Y-SCALE) "solid" BAR-COLOR)))
```

### March 29th 2018 ###
- Solution for Reference P1 - Alternative Tuition Graph:
```
(define-struct school (name tuition next))
;; School is one of:
;;  - false
;;  - (make-school String Natural School)
;; interp. an arbitrary number of schools, where for each school we have its
;;         name and its tuition in USD

; PROBLEM A:
; 
; Confirm for yourself that this is a well-formed self-referential data 
; definition.


; It is well formed because it contains a base case and a reference case.

; PROBLEM B:
; 
; Complete the data definition making sure to define all the same examples as 
; for ListOfSchool in the videos.


(define S1 false)
(define S2 (make-school "School1" 46000
                        (make-school "School2" 32000
                                     (make-school "School3" 56000))))

#;
(define (fn-for-school s)
  (cond [(false? s) (...)]
        [else 
         (...(school-name s)
             (school-tuition s)
             (fn-for-school(school-next s)))]))

;; Template rules used:
;; - one of: 2 cases
;; - atomic distinct: false
;; - compound: (make-school String Natural School)
;; - atomic non-distinct: (school-name s) is String
;; - atomic non-distinct: (school-tuition s) is Natural
;; - self-reference: (school-next s) is School

; PROBLEM C:
; 
; Design the chart function that consumes School. Save yourself time by simply 
; copying the tests over from the original version of chart.


;; Constants

(define FONT-SIZE 24)
(define FONT-COLOUR "black")

(define Y-SCALE 1/200)
(define BAR-WIDTH 30)
(define BAR-COLOUR "lightblue")

;; Functions

;; ListOfSchool -> Image
;; produce bar chart showing names and tuitions of the consumed schools
(check-expect (chart empty) (square 0 "solid" "white"))
(check-expect (chart (cons (make-school "S1" 8000) empty))
              (beside (overlay/align "center" "bottom"
                      (rotate 90 (text "S1" FONT-SIZE FONT-COLOR))
                      (rectangle BAR-WIDTH (* 8000 Y-SCALE) "outline" "black")
                      (rectangle BAR-WIDTH (* 8000 Y-SCALE) "solid" BAR-COLOR))
                      (square 0 "solid" "white")))
(check-expect (chart (cons (make-school "S2" 12000) (cons (make-school "S1" 8000) empty)))
              (beside/align "bottom" (overlay/align "center" "bottom"
                      (rotate 90 (text "S1" FONT-SIZE FONT-COLOR))
                      (rectangle BAR-WIDTH (* 12000 Y-SCALE) "outline" "black")
                      (rectangle BAR-WIDTH (* 12000 Y-SCALE) "solid" BAR-COLOR))
              (beside/align "bottom" (overlay/align "center" "bottom"
                      (rotate 90 (text "S2" FONT-SIZE FONT-COLOR))
                      (rectangle BAR-WIDTH (* 8000 Y-SCALE) "outline" "black")
                      (rectangle BAR-WIDTH (* 8000 Y-SCALE) "solid" BAR-COLOR))
              (square 0 "solid" "white"))))

;(define (chart los) (square 0 "solid" "white")) ;stub
;<took template from School>

(define (chart s)
  (cond [(false? s) (square 0 "solid" "white")]
        [else
         (beside/align "bottom" 
                       (overlay/align "center" "bottom"
                                      (rotate 90 (text (school-name s) FONT-SIZE FONT-COLOR))
                                      (rectangle BAR-WIDTH (* (school-tuition s) Y-SCALE) "outline" "black")
                                      (rectangle BAR-WIDTH (* (school-tuition s) Y-SCALE) "solid" BAR-COLOR))
                       (chart (school-next s)))])) 
```

### March 30th 2018###
```
;; Natural is one of:
;;  - 0 base case
;;  - (add1 Natural) SR
;; interp. a natural number
(define N0 0)         ;0
(define N1 (add1 N0)) ;1
(define N2 (add1 N1)) ;2

(define (fn-for-natural n)
  (cond [(zero? n) (...)]
        [else
         (... ;n                           ;template rules wouldn't normally put this
          ;                            ;here, but we will see that we end up coming
          ;                            ;back to add it
          (fn-for-natural (sub1 n)))]))

;; Template rules used:
;;  - one-of: two cases
;;  - atomic distinct: 0
;;  - compound: (add1 Natural)
;;  - self-reference: (sub1 n) is Natural

;; Functions
;; =============

;; Natural -> Natural
;; produce sum of Natural[0, n]
(check-expect (sum 0) 0)
(check-expect (sum 1) 1)
(check-expect (sum 3) (+ 0 1 2 3))

;(define (sum n) 0) ;stub 0

(define (sum n)
  (cond [(zero? n) 0]
        [else
         (+ n
          (sum (sub1 n)))]))

;; Natural -> ListOfNatural
;; produce (cons n (cons n-1 ... empty)) not including 0
(check-expect (to-list 0) empty)
(check-expect (to-list 1) (cons 1 empty))
(check-expect (to-list 2) (cons 2 (cons 1 empty)))

;(define (to-list n) empty) ;stub

(define (to-list n)
  (cond [(zero? n) empty]
        [else
         (cons n
          (to-list (sub1 n)))]))
```

### April 1st 2018 ###
```
;; NATURAL is one of:
;; - empty
;; - (cons "!" NATURAL)
;; interp. a natural number, the number of "!" in the list is the number

(define N0 empty)         ;0
(define N1 (cons "!" N0)) ;1
(define N2 (cons "!" N1)) ;2
(define N3 (cons "!" N2))
(define N4 (cons "!" N3))
(define N5 (cons "!" N4))
(define N6 (cons "!" N5))
(define N7 (cons "!" N6))
(define N8 (cons "!" N7))
(define N9 (cons "!" N8))

;; These are the primitives that operate NATURAL:
(define (ZERO? n) (empty? n))  ;Any -> Boolean
(define (ADD1 n) (cons "!" n)) ;NATURAL -> NATURAL
(define (SUB1 n) (rest n))     ;NATURAL[>0] -> NATURAL

#;
(define (fn-for-NATURAL n)
  (cond [(ZERO? n) (...)]
        [else
         (... n
              (fn-for-NATURAL (SUB1 n)))]))

;; ADDITION

;; NATURAL NATURAL -> NATURAL
;; produce a + b
(check-expect (ADD N2 N0) N2)
(check-expect (ADD N0 N3) N3)
(check-expect (ADD N3 N4) N7)

;(define (ADD a b) N0) ;stub

(define (ADD a b)
  (cond [(ZERO? b) a]
        [else
         (ADD (ADD1 a) (SUB1 b))])) ;take 1 away from b and add it to a


;; SUBTRACTION

;; NATURAL NATURAL -> NATURAL
;; produce a - b
(check-expect (SUB N2 N0) N2)
(check-expect (SUB N5 N3) N2)
(check-expect (SUB N7 N2) N5)

;(define (SUB a b) N0) ;stub

(define (SUB a b)
  (cond [(ZERO? b) a]
        [else
         (SUB (SUB1 a) (SUB2 b))]))
```

- Solution for Natural P2 - Decreasing Image:
```
(define TEXT-SIZE 20)
(define TEXT-COLOR "black")
(define SPACING (text " " TEXT-SIZE TEXT-COLOR)

;; Natural -> Image
;; produces an image from n to 0 side by side
(check-expect (decreasing-image 0) (text "0" 20 black))
(check-expect (decreasing-image 3) (beside (text "3" 20 "black") SPACING
                                           (text "2" 20 "black") SPACING
                                           (text "1" 20 "black") SPACING
                                           (text "0" 20 "black")))

;(define (decreasing-image n) empty-image) ;stub

(define (decreasing-image n)
  (cond [(zero? n) (text "0" TEXT-SIZE TEXT-COLOR)]
        [else
         (beside (text (number -> string n) TEXT-SIZE TEXT-COLOR)
              SPACING
              (decreasing-image (sub1 n)))]))
```

- Solution for Natural P3 - Odd numbers:
```
;; Natural -> ListOfNatural
;; produces a list of odd numbers from n down to 1
(check-expect (odd-from-n 0) empty)
(check-expect (odd-from-n 15) (list 13 11 9 7 5 3 1))
(check-expect (odd-from-n 7) (list 7 5 3 1))

;(define (odd-from-n n) empty) ;stub

(define (odd-from-n n)
  (cond [(zero? n) empty]
        [else
         (if (odd? n)
             (cons n (odd-from-n) (sub1 n))
             (odd-from-n (sub1 n)))]))
```

### April 2nd 2018 ###
- Functions composition Pt2:
```
(define BLANK (square 0 "solid" "black"))

;; Data definitions:

;; ListOfImage is one of:
;; - empty
;; - (cons Image ListOfImage)
;; interp. An arbitrary number of images
(define LOI1 empty)
(define LOI2 (cons (rectangle 10 20 "solid" "black")
                   (cons (rectangle 20 30 "solid" "red") empty)))

#;
(define (fn-for-loi loi)
  (cond [(empty? loi) (...)]
        [else
         (... n
              (fn-for-loi (rest loi)))]))

;; Functions:

;; ListOfImage -> Image
;; lay out images left to right in increasing order of size
(check-expect (arrange-images (cons (rectangle 10 20 "solid" "black")
                              (cons (rectangle 20 30 "solid" "red") empty)))
              (beside (rectangle 10 20 "solid" "black")
                      (rectangle 20 30 "solid" "red")
                      BLANK))
(check-expect (arrange-images (cons (rectangle 20 30 "solid" "black")
                              (cons (rectangle 10 20 "solid" "red") empty)))
              (beside (rectangle 10 20 "solid" "black")
                      (rectangle 20 30 "solid" "red")
                      BLANK))


;(define (arrange-images loi) BLANK) ;stub

(define (arrange-images loi)
  (layout-images (sort-images loi)))

;; ListOfImage -> Image
;; place images beside eachother in order of list
;; !!!
(define (layout-images loi) BLANK)

;; ListOfImage -> ListOfImage
;; sort images in increasing order of size
;; !!!
(define (sort-image loi) loi)
```