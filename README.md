# Java Clojure Syntax Comparison

[![License](https://img.shields.io/badge/license-CC0--1.0-blue.svg)](https://github.com/biezhi/java-clojure-syntax-comparison/blob/master/LICENSE) [![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)

> Comparison of some code snippets in the Java and Clojure.

- Java Version: `1.8.0_101`
- Clojure Version: `1.9.0`

## Contents

### 📍 Basic

<details>
<summary>View contents</summary>

* [`Hello World`](#hello-world)
* [`Comment`](#comment)
* [`Variable`](#variable)

</details>

### 📚 List

<details>
<summary>View contents</summary>

* [`Create List`](#create-list)
* [`Add item`](#add-item-to-list)
* [`Get item`](#get-list-item)
* [`Get count`](#get-list-count)

</details>

### 📚 Array

<details>
<summary>View contents</summary>

* [`Create Array`](#create-array)
* [`Get item`](#get-array-item)
* [`Get count`](#get-array-count)
* [`Two-dimensional array`](#two-dimensional-array)

</details>

### 🗺 Map

<details>
<summary>View contents</summary>

* [`Create Map`](#create-map)
* [`Get item`](#get-map-item)

</details>

### 🎛️ Function

<details>
<summary>View contents</summary>

* [`Define Function`](#define-function)
* [`Function with parameters`](#function-with-parameters)
* [`Anonymous function`](#anonymous-function)
* [`With return value`](#with-return-value)
* [`Higher-order Function`](#higher-order-function)
* [`filter`](#filter)

</details>

### ✈️ Flow Control

<details>
<summary>View contents</summary>

* [`If Else`](#if-else)
* [`Switch`](#switch)
* [`Not`](#not)
* [`And`](#and)
* [`Or`](#or)
* [`For`](#for)
* [`While`](#while)

</details>

### 📜 String

<details>
<summary>View contents</summary>

* [`toString`](#to-string)
* [`append`](#string-splice)
* [`replace`](#string-replace)
* [`join`](#string-join)
* [`split`](#string-split)
* [`substring`](#string-substring)

</details>

### ⏱️ Date

<details>
<summary>View contents</summary>

* [`Now Time`](#now-time)

</details>

### ➗ Math

<details>
<summary>View contents</summary>

* [`average`](#average)

</details>

### 🔭 IO

<details>
<summary>View contents</summary>

* [`read-file-as-string`](#read-file-as-string)

</details>

### ❌ Exception

<details>
<summary>View contents</summary>

* [`Throw exception`](#throw-exception)
* [`Try catch`](#try-catch)

</details>

### ❇️ Thread

<details>
<summary>View contents</summary>

* [`Create thread`](#create-thread)
* [`Future`](#future)

</details>

---

## 📍 Basic

### Hello World

Print `hello world` is the first thing in programming languages 😋

```java
System.out.print("Hello World\n");

System.out.println("Hello World");
```

<details>
<summary>Clojure</summary>

```clojure
(print "Hello World\n")
;; => Hello World

(println "Hello World")
;; => Hello World
```

</details>

<br>[⬆ Back to top](#contents)

### Comment

```java
// This is a one-line comment

/**
 * This is a multi-line comment
 */
```

<details>
<summary>Clojure</summary>

```clojure
; (semicolon) reader macro
; i don't know what I should do

;; The syntax is like a function: (comment & body).
(comment "
    Here are the comments
")

;; This is used to comment out a form. 
;; a corresponding pair of ( and ), or [ and ]. 
;; The form can be nested.
(def my-vec #_[1 2 3] [3 4 5])
;; [1 2 3] was ignored
```

</details>

<br>[⬆ Back to top](#contents)

### Variable

```java
String name = "biezhi";
int age     = 2333;
```

<details>
<summary>Clojure</summary>

In fact, variables cannot be defined in `clojure`. These values ​​are immutable, like in Java `final`.

```clojure
(def name "biezhi")
(def age  2333)
```

`def` can be creates and interns or locates a global var with the name of symbol.

```clojure
(def my-number 234)
;;=> #'user/my-number
;; what's that returned thing, "#'user/my-number" ?

(type #'user/my-number)
;;=> clojure.lang.Var
; it is a Var. you just created the Var, at the same time, `my-number` has been bound to 234.

my-number
;;=> 234
user/my-number
;;=> 234
```

In other languages, a variable assignment looks like `var myvar = "something"`, `@myvar = "something"`, or `String myVar = "something"`.

Clojure does things in a different way. First, Clojure doesn’t call it a variable assignment. It is a *var binding*, and this idea is a bit different from assignment in other languages.

</details>

<br>[⬆ Back to top](#contents)

## 📚 List

### Create List

```java
List<String> list = new ArrayList<>();
list.add("a");
list.add("b");
list.add("c");

List<String> list = Arrays.asList("a", "b", "c");
```

<details>
<summary>Clojure</summary>

A list uses parentheses as its surrounding delimiters, and so an empty list would look like `()`, whereas a list with three elements could look like `("a" "b" "c")`.

```clojure
(def my-list (list "a" "b" "c"))

;; There is a special function called quote that tells Clojure to just treat the
;; list as data.
(def my-list (quote ("a" "b" "c")))

;; This syntax is actually more code to type than (list "a" "b" "c"),
;; so there is a shortcut for the quote function using the ' character
(def my-list '("a" "b" "c"))
```

One unique thing about lists is that the first element is always evaluated as a function call, with the remaining elements as arguments. So, defining a list just using `()` will cause an error.

</details>

<br>[⬆ Back to top](#contents)

### Add item to List

```java
list.add("d");

list.addAll(newList);
```

<details>
<summary>Clojure</summary>

```clojure
;; returns a new collection with the xs 'added'
(conj my-list "d")
;;=> ("d" "a" "b" "c")

(cons "d" my-list)
;;=> ("d" "a" "b" "c")

(concat my-list '("d" "e" "f"))
;;=> ("a" "b" "c" "d" "e" "f")
```

</details>

<br>[⬆ Back to top](#contents)

### Get List item

```java
String a = list.get(0);
```

<details>
<summary>Clojure</summary>

```clojure
;; get first by list
(first my-list)
;;=> a

;; get first by list
(second my-list)
;;=> b

;; get item by index
(nth my-list 1)
;;=> b
```

</details>

<br>[⬆ Back to top](#contents)

### Get List count

```java
int size = list.size();
```

<details>
<summary>Clojure</summary>

```clojure
(count '(1 2 3))
;;=> 3
```

</details>

<br>[⬆ Back to top](#contents)

## 📚 Array

### Create Array

```java
String[] fruits = new String[3];
fruits[0] = "peach";
fruits[1] = "pear";
fruits[2] = "apple";

String[] fruits = {"peach", "pear", "apple"};
```

<details>
<summary>Clojure</summary>

```clojure
;; Vector []
;; A vector looks like an array and is better for random access.
;; A vector has an index to look up elements at a specific point, speeding up random access
;; Vectors and maps are the most common data structures use to hold data in Clojure

;; you can use the vector function to create a new vector
(def fruits (vector "peach", "pear", "apple"))

;; Usually you just use the [] notation to create a vector to help keep your code readable
(def fruits ["peach", "pear", "apple"])
```

</details>

<br>[⬆ Back to top](#contents)

### Get Array item

```java
String pear = fruits[1];
```

<details>
<summary>Clojure</summary>

```clojure
(second fruits)
;; => "pear"

(nth fruits 1)
;; => "pear"
```

</details>

<br>[⬆ Back to top](#contents)

### Get Array count

```java
int length = fruits.length;
```

<details>
<summary>Clojure</summary>

```clojure
(count fruits)
;;=> 3
```

</details>

<br>[⬆ Back to top](#contents)

### Two dimensional array

```java
int[][] points = {
                {23, 45},
                {42, 88},
        };

int[] idx = points[0];
```

<details>
<summary>Clojure</summary>

```clojure
(def points [[23, 45] [42, 88]])

(first points)
;;=> [23, 45]

(nth points 1)
;;=> [42, 88]
```

</details>

<br>[⬆ Back to top](#contents)

## 🗺 Map

### Create Map

```java
Map<String, Integer> me = new HashMap<>();
me.put("name", "biezhi");
me.put("age", 2333);
```

<details>
<summary>Clojure</summary>

```clojure
;; Map {}
;; A key / value pair data structure
;; keys are usually defined as a :keyword, although they can be anything

;; Typicall a :keyword is used for a the key in a map, with the value being
;; a string, number or another keyword
(def me {:name "biezhi",
         :age   2333
         :url   "https://github.com/biezhi"})
```

</details>

<br>[⬆ Back to top](#contents)

### Get Map item

```java
me.get("url");
```

<details>
<summary>Clojure</summary>

```clojure
(:name me)
;;=> "biezhi"

(get me :name)
;;=> "biezhi"

(me :name)
;;=> "biezhi"
```

</details>

<br>[⬆ Back to top](#contents)

## 🎛️ Function

### Define function

```java
void sayHello() {
    System.out.println("hello");
}
```

<details>
<summary>Clojure</summary>

```clojure
;; assign a function to a variable
(defn say-hello [] (println "hello"))

(say-hello)
;; => hello
```

</details>

<br>[⬆ Back to top](#contents)

### Function with parameters

```java
void sayHello(String name) {
    System.out.println("hello " + name);
}
```

<details>
<summary>Clojure</summary>

```clojure
;; define a function with parameters
(defn say-hello [name] (println (str "hello " name)))

(say-hello "world")
;; => hello world
```

</details>

<br>[⬆ Back to top](#contents)

### Anonymous function

```java
Runnable task = () -> System.out.println("Hello Boy.");
task.run();
```

<details>
<summary>Clojure</summary>

```clojure
(def say-hello
  (fn []
    (str "hello world")))

;; assign a function to a variable
(def say-hello
 (fn [name]
   (str "Hello " name)))

;; the same but using an anonymous function
(def say-hello
 #(str "hello " %))

;; anonymous function using two arguments
(def hello-doc #(str "Hello " %1 %2))
```

</details>

<br>[⬆ Back to top](#contents)

### With return value

```java
String sayHello(String name) {
    return "hello " + name;
}
```

<details>
<summary>Clojure</summary>

```clojure
(defn say-hello [name] (str "hello " name))
```

</details>

<br>[⬆ Back to top](#contents)

### Higher-order function

```java
public void onConsumer(Consumer<String> consumer) {
    consumer.accept("let's go");
}
   
public Function<String, Integer> myConvert(){
    return Integer::parseInt;
}
```

<details>
<summary>Clojure</summary>

A higher-order function is:

- a function that takes one or more functions as arguments
- or a function that returns a function

In other languages, this feature may have another name. For example, Ruby names it block for a callee function, although the caller doesn’t have specific name.

In Clojure, caller functions are high-order functions while callees don’t have specific names. Some well known higher-order functions are `map`, `reduce`, `remove`, `filter`, and `iterate`. 

```clojure
(defn on-consumer [fn] (fn "let's go"))
(on-consumer str)
;;=> "let's go"

(defn my-convert [str] (Integer. str))
(my-convert "123")
;;=> 123
```

</details>

<br>[⬆ Back to top](#contents)

### filter

```java
long count = IntStream.of(3, 5, 10, 2, 29, 1, 24, 13)
                      .filter(i -> i < 10)
                      .count();
```

<details>
<summary>Clojure</summary>

The `filter` function is a commonly-used `higher-order functions`. It takes a function as an argument. The `filter` function works as its name implies. It filters out values in a sequence that don’t meet the given condition. To perform this filtering, `filter` takes a function and a sequence for its arguments. The function given to the `filter` must return a truthy value, and is called a predicate function.

The syntax is: `(filter pred coll)`

```clojure
(filter #(< % 10) [3 5 10 2 29 1 24 13])
;;=> (3 5 2 1)

(count (filter #(< % 10) [3 5 10 2 29 1 24 13]))
;;=> 4

(filter odd? (range 10))
;;=> (1 3 5 7 9)
```

</details>

<br>[⬆ Back to top](#contents)

## ✈️ Flow Control

### If else

```java
int age = 23;
if (age > 18) {
    System.out.println("You have grown up, don't be like a child again.");
} else {
    System.out.println("Let's learn the cat call together, say 'miao miao miao'.");
}
```

<details>
<summary>Clojure</summary>

“If it is a good weather, I will go to a park; otherwise, I’ll go to a cafe.” This is called “if-branching” in the programming world. Since the if-branching uses simple conditionals, it is frequently used to divide into two states: true or false.

In Clojure, `if` is a special form. The syntax is:

```clojure
(if test then else?) or (if test then)
```

```clojure
(def age 14)
(if (> age 18)
  (println "You have grown up, don't be like a child again.")
  (println "Let's learn the cat call together, say 'miao miao miao'."))
```

In addition, Clojure has a unique way of using the `if` conditional with the `let` binding. It is `if-let` macro, which is useful when we want to use the result of *test*.

The syntax is:

```clojure
(if-let bindings then) or (if-let bindings then else & oldform)
```

```clojure
(defn weather-is-good?
        [weather]
        (if-let [actual (= :good weather)]
                (str "The weather is good? " actual)
                "The weather is at least not good."))

(weather-is-good? :good)
;;=> "The weather is good? true"

(weather-is-good? :bad)
;;=> "The weather is at least not good."
```

</details>

---

```java
int temp = 10;
if (temp > 65) {
    System.out.println("I'll enjoy walking at a park.");
} else if (temp > 45) {
    System.out.println("I'll spend time at a cafe.");
} else {
    System.out.println("I'll curl up in my bed.");
}
```

<details>
<summary>Clojure</summary>

```clojure
(defn what-to-do
        [temp]
        (cond
         (> temp 65) "I'll enjoy walking at a park."
         (> temp 45) "I'll spend time at a cafe."
         :else "I'll curl up in my bed."))

(what-to-do 70)
;;=> "I'll enjoy walking at a park."

(what-to-do 50)
;;=> "I'll spend time at a cafe."

(what-to-do 30)
;;=> "I'll curl up in my bed."
```

Clojure has `condp` macro also. The usage is similar to `cond`, but it takes a part of test right after the condp.

The syntax is: `(condp pred expr & clauses)`

```clojure
(defn what-to-do-p
        [temp]
        (condp < temp
               65 "I'll enjoy walking at a park."
               45 "I'll spend time at a cafe."
               "I'll curl up in my bed"))

(what-to-do-p 70)
;;=> "I'll enjoy walking at a park."

(what-to-do-p 50)
;;=> "I'll spend time at a cafe."

(what-to-do-p 30)
;;=> "I'll curl up in my bed."
```

</details>

<details>

<br>[⬆ Back to top](#contents)

### Switch

```java
int color = 3;
switch(color) {
    case 3:
        return "red";
    case 2:
        return "blue";
    case 1:
        return "pink";
    default:
        return "#000";
}
```

<details>
<summary>Clojure</summary>

The `case` macro is a similar conditional to `cond/condp`. It branches to multiple clauses. The difference is that `case` doesn’t evaluate branching expressions. In `case`, it should be a constant. What we can do with `case` looks like `map (data structure)`.

The syntax is: `(case e & clauses)`

```clojure
(case 3
  3 "red"
  2 "blue"
  1 "pink"
  "#000")
;;=> "red"

(defn cases-to-do [temp]
  (case temp
        :65-80 "I'll enjoy walking at a park."
        :45-64 "I'll spend time at a cafe."
        "I'll curl up in my bed"))

(cases-to-do :65-80)
;;=> "I'll enjoy walking at a park."

(my-cases :45-64)
;;=> "I'll spend time at a cafe."

(my-cases :other)
;;=> "I'll curl up in my bed"

(my-cases :30) ; hash-map can't take a key that doesn't match anything
;;=> nil
```

</details>

<br>[⬆ Back to top](#contents)

### Not

```java
int flag = 2333;

if (flag != 100){
    // do some thing
}
```

<details>
<summary>Clojure</summary>

```clojure
(def flag 2333)
(if (not (= 100 flag)) (println "not eq 2333"))
;;=> not eq 2333
```

</details>

<br>[⬆ Back to top](#contents)

### And

```java
boolean success = (result.ok && result.code == 200);
```

<details>
<summary>Clojure</summary>

```clojure
(and (true? result.ok) (= 200 result.code))
```

</details>

<br>[⬆ Back to top](#contents)

### Or

```java
boolean success = (result.ok || result.code == 200);
```

<details>
<summary>Clojure</summary>

```clojure
(or (true? result.ok) (= 200 result.code))
```

</details>

<br>[⬆ Back to top](#contents)

### For

```java
for (int i=0; i<10; i++){
    System.out.println("i = " + i);
}
```

<details>
<summary>Clojure</summary>

The *for loop* is a common concept in computer languages. When we want to apply the same logic (operations) to each element of a given array (vector or list in Clojure), we apply the idea of a *for loop* to that. In general, this involves incrementing (or decrementing) an index and performing a similar function on each element. However, the way to implement a for loop varies from language to language. Some use an index variable explicitly. Others use an iterator. Some use neither. Clojure takes a very different approach. 

Clojure’s `for` is categorized as a sequence operator, like `map`(core function) or `reduce`. More importantly, in Clojure, `for` is used for *list comprehension*, which means it creates a list from a given `list`. 

The syntax of the `for` macro is: `(for [binding-form coll-expr filter-expr?] expr)`

```clojure
(for [i (range 10)] 
  (do (println (str "i =" i))))

(for [w ["LOVe" "coding" "hEllo" "worLD!"]]
           (clojure.string/capitalize w))
; like let, *for* takes binding-form
;;=> ("Love" "Coding" "Hello" "World!")

; we can get the same result using the *map* core function
(map clojure.string/capitalize ["LOVe" "coding" "hEllo" "worLD!"])
;;=> ("Love" "Coding" "Hello" "World!")

; include only when length of the word exceeds 5
(for [w ["LOVe" "coding" "hEllo" "worLD!"] :when (> (count w) 5)]
           (clojure.string/capitalize w))
;;=> ("Coding" "World!")

; using let binding
(for [w ["LOVe" "coding" "hEllo" "worLD!"] :let [length (count w)]]
           (str (clojure.string/capitalize w) ": " length))
;;=> ("Love: 4" "Coding: 6" "Hello: 5" "World!: 6")

; when the input consists of multiple vectors
(for [x ["a" "b" "c"]
      y ["a" "b" "c"]
      z ["a" "b" "c"]]
     (str x y z))
;;=> ("aaa" "aab" "aac" "aba" "abb" "abc" "aca" "acb" "acc" "baa" "bab" "bac" "bba" "bbb" "bbc" "bca" "bcb" "bcc" "caa" "cab" "cac" "cba" "cbb" "cbc" "cca" "ccb" "ccc")
```

</details>

```java
String someJoin(String[] coll, String result) {
    if (coll.length == 1) {
        return result + coll[0];
    }
    StringBuilder sbuf = new StringBuilder();
    for (String str : coll) {
        sbuf.append(str).append(", ");
    }
    return sbuf.substring(0, sbuf.length() - 2);
}
```

<details>
<summary>Clojure</summary>

While `for` is somewhat like a loop, `recur` is a real loop in Clojure. `recur` represents such a remarkable idea that we might even say, “this *is* Clojure.”

If you have a programming background, you may have heard of tail *recursion*, which is a major feature of functional languages. This `recur` special form is the one that implements *tail recursion*. As the words “*tail recursion*” indicate, recur must be called in the tail position. In other words, `recur` must be the last thing to be evaluated. 

The syntax of the recur macro is: `(recur exprs*)`

```clojure
(defn some-join [coll result]
        (if (= 1 (count coll)) (str result (first coll))
          (recur (rest coll) (str result (first coll) ", "))))

(some-join ["hello" "world" "love" "coding"] "Words: ")
;;=> "Words: hello, world, love, coding"

; when we want to do something just before the recur
; we can use *do*
(defn some-join [coll result]
      (if (= 1 (count coll)) (str result (first coll))
        (do
          (println result)
          (recur (rest coll) (str result (first coll) ", ")))))

(some-join ["hello" "world" "love" "coding"] "Words: ")
;;=> Words:
;;=> Words: hello,
;;=> Words: hello, world,
;;=> "Words: hello, world, love, coding"

; however, just for printing out the process, let binding works
(defn some-join [coll result]
  (let [_ (println result)]
    (if (= 1 (count coll)) (str result (first coll))
      (recur (rest coll) (str result (first coll) ", ")))))

(some-join ["hello" "world" "love" "coding"] "Words: ")
;;=> Words:
;;=> Words: hello,
;;=> Words: hello, world,
;;=> Words: hello, world, love,
;;=> "Words: hello, world, love, coding"

; we attempted the same thing as clojure.string/join function does
(str "Words: " (clojure.string/join ", " ["hello" "world" "love" "coding"]))
;;=> "Words: hello, world, love, coding"
```

</details>

<br>[⬆ Back to top](#contents)

### While

```java
int seq = 10;
while (seq > 0) {
    System.out.prinln("seq = " + (seq--));
}
```

<details>
<summary>Clojure</summary>

```clojure
(def seq-num (atom 10))
(while (> @seq-num 0)
   (do (println (str "seq = " @seq-num)) (swap! seq-num dec) ))
```

</details>

<br>[⬆ Back to top](#contents)

## 📜 String

### to string

```java
Integer age = 2333;
System.out.println(age.toString());
```

<details>
<summary>Clojure</summary>

```clojure
(str 2333)
;;=> "2333"
```

</details>

<br>[⬆ Back to top](#contents)

### String append

```java
String a = "hello " + "world " + 2333;
```

`str` is a function that turns its arguments into strings.

<details>
<summary>Clojure</summary>

```clojure
(str "hello " "world " 2333)
;;=> "hello world 2333"

(str :a-keyword)
;;=> ":a-keyword"

(str false)
;;=> "false"

(map str (range 10))
;;=> ("0" "1" "2" "3" "4" "5" "6" "7" "8" "9")
```

When `str` is given multiple arguments, then it will concatenate them all into one big string.

```clojure
(str "I need " 5 " of these")
;;=> "I need 5 of these"

(str "In "
     (rand-nth ["summer" "winter"])
     " I like to go "
     (rand-nth ["swimming" "running"]))
;;=> "In summer I like to go swimming"
```

</details>

<br>[⬆ Back to top](#contents)

### String replace

```java
String url = "https://biezhi.me";
System.out.println("New url is: " + url.replace('.', '#');

String str = "A good day to you, sir.  Good day.";
System.out.println("New str is: " + url.replaceFirst("day", "night");

String str = "This is a String to use as an example to present raplaceAll";
System.out.println(str.replaceAll("This", "That"));
```

<details>
<summary>Clojure</summary>

```clojure
(clojure.string/replace "https://biezhi.me" #"\." "#")

;; replace with Java method
(.replace "https://biezhi.me" "." "#")

;; Only replace the first match.
(clojure.string/replace-first "A good day to you, sir.  Good day." #"day" "night")
;;=> "A good night to you, sir.  Good day."

;; If there are no matches, return the original string.
(clojure.string/replace-first "A good day to you, sir." #"madam" "master")
;;=> "A good day to you, sir."

;; To title case
(clojure.string/replace "hello world" #"\b." #(.toUpperCase %1))
;;=> "Hello World"

;; replaces all a's with 1 and all b's with 2
(clojure.string/replace "a b a" #"a|b" {"a" "1" "b" "2"})
;=> "1 2 1"
```

</details>

<br>[⬆ Back to top](#contents)

### String join

```java
String.join(", ", "jack", "biezhi", "rose", "mark")
```

<details>
<summary>Clojure</summary>

```clojure
(clojure.string/join ", " ["jack", "biezhi", "rose", "mark"])
;;=> "jack, biezhi, rose, mark"
```

</details>

<br>[⬆ Back to top](#contents)

### String split

```java
"jack, biezhi, rose, mark".split(", ");

"h1e2l3l4o5w6o7r8d9d".split("\\d+");
```

<details>
<summary>Clojure</summary>

```clojure
(clojure.string/split "jack, biezhi, rose, mark" #", ")
;;=> ["jack" "biezhi" "rose" "mark"]

(clojure.string/split "h1e2l3l4o5w6o7r8d9d" #"\d+")
;;=> ["h" "e" "l" "l" "o" "w" "o" "r" "d" "d"]

;; Note that the 'limit' arg is the maximum number of strings to
;; return (not the number of splits)
(clojure.string/split "q1w2e3r4t5y6u7i8o9p0" #"\d+" 5)
;;=> ["q" "w" "e" "r" "t5y6u7i8o9p0"]

;; to get back all the characters of a string, as a vector of strings:
(clojure.string/split " q1w2 " #"")
;;=> [" " "q" "1" "w" "2" " "]

;; Note: sequence, in contrast, would return characters.
;; Using lookarounds (lookahead, lookbehind) one can keep the matching characters:
(clojure.string/split " something and ACamelName " #"(?=[A-Z])")
;;=> [" something and " "A" "Camel" "Name "]
```

</details>

<br>[⬆ Back to top](#contents)

### String substring

```java
"biezhi".substring(1);
"biezhi".substring(0, 3);
"biezhi".substring(0, 6);
```

<details>
<summary>Clojure</summary>

```clojure
(subs "biezhi" 1)
;;=> "iezhi"

(subs "biezhi" 0 3)
;;=> "bie"

(subs "biezhi" 0 6)
;;=> "biezhi"
```

</details>

<br>[⬆ Back to top](#contents)

# Clojure Links

- [clojure-through-code](https://github.com/practicalli/clojure-through-code)
- [clojure docs](https://clojuredocs.org/quickref)
- [learn clojure](https://hackr.io/tutorials/learn-clojure)
