# Clojure Presentation Track

## Intro

Hello Everybody,

my name is Simone Mosciatti, I am Italian and I am going to introduce Clojure and functional programming.

I do have a weird accent, so if you cannot understand what I am saying please just raise your hand.

Let me ask you first:

*Who know clojure ?* few hands expected
*Who know functional programming ?* slightly more hands

Thank you.

## Clojure intro

Clojure is a Lisp dialect that run on the JVM.

Is definitely more than fast enough for most application but it is extremely slow in startup time.

Clojure is a very productive language and it is used for a lot of data intensive application and to run web application.

Actually is a good fit for most task, I won't write a micro controller in clojure though.

## What clojure looks like ?

``` clojure
(def one-to-ten (range 1 (inc 10))) ;; a variable

(defn multiply-by-two [num] ;; a function
  (* num 2))

(map multiply-by-two one-to-ten) ;; an expression
;; (2 4 6 8 10 12 14 16 18 20) this is a comment
```

Ok, it is different from what you usually see but it is an extremely simple concept.

The first thing after the bracket is a function, all the other things are arguments for such function, of course, argument to a function can be other function call.

That it's.

## Immutability and variable

Other than in the examples usually you do not define much variables.

If in OOP or procedural programming language we define variable and then we modify such variable, all this do not happen in clojure, or at least is not idiomatic...

We never modify variable in Clojure.

### How can we make any useful thing without modify variable ?

In clojure, similarly to other functional languages, you usually create a funnel of transformations, you plug your input in, and you get your output out.

This "funnel of transformations" is the composition of several functions.

In idiomatic clojure any function is a pure function, given the same input you will get the same output, any single time, and the function do not modify the environment.

This is extremely power full:

``` clojure
(def my-self
    {:name "Simone Mosciatti"
     :age 20
     :work "unemployed"
     :girlfriend "Extremely far from HERE :-("})

(defn split-name [{:keys [name] :as person}]
	(let [[name surname] (clojure.string/split name #" ")]
	  (assoc person :firstname name :lastname surname)))

(defn birthday [{:keys [age] :as person}]
	(assoc person :age (inc age)))

(defn find-job [person]
	(assoc person :work "Amazing company"))

(defn meet-girlfriend [person]
	(assoc person :girlfriend "Just next to me :-)"))

(defn perfect [user]
	(birthday (find-job (meet-girlfriend (split-name user)))))
(defn more-idiomatic-perfect [person]
	(-> person split-name birthday find-job meet-girlfriend))
(def perfect-perfect (comp split-name birthday find-job meet-girlfriend))
```

How it this approach useful ?

Any function can be tested in isolation, test is extremely simple, and atomic.

This approach scale, even with thousand of LOC we are still using pure function that are trivial to test.

Small recap: Clojure do not modify variable, it modify, and combine function in such a way to create a funnel, where you plug in your input value and where you get out your output value.

Function in idiomatic clojure are simple, small, and pure, are extremely easy to test (maybe even to easy).


