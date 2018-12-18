# Java Clojure Syntax Comparison

Comparison of some code snippets in the Java and Clojure.

- Java Version: `1.8.0_101`
- Clojure Version: `1.9`

## Table of Contents

### Basic

<details>
<summary>View contents</summary>

* [`Hello World`](#hello-world)
* [`Comment`](#comment)
* [`Variable`](#variable)

</details>

### List

<details>
<summary>View contents</summary>

* [`Create list`](#create-list)
* [`Add item`](#add-item-to-list)
* [`Get item`](#get-list-item)
* [`Get count`](#get-list-count)

</details>

### Array

<details>
<summary>View contents</summary>

* [`Create array`](#create-array)
* [`Get item`](#get-array-item)
* [`Get count`](#get-array-count)
* [`Two-dimensional array`](#two-dimensional-array)

</details>

### Map

<details>
<summary>View contents</summary>

* [`Create map`](#create-map)
* [`Get item`](#get-map-item)

</details>

### Function

<details>
<summary>View contents</summary>

* [`Define function`](#define-function)
* [`Function with parameters`](#function-with-parameters)
* [`Anonymous function`](#anonymous-function)
* [`With return value`](#with-return-value)

</details>

### Flow Control

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

### String

<details>
<summary>View contents</summary>

* [`toString`](#to-string)
* [`append`](#string-splice)
* [`replace`](#string-replace)
* [`join`](#string-join)
* [`split`](#string-split)
* [`substring`](#string-substring)

</details>

### IO

<details>
<summary>View contents</summary>

* [`read-file-as-string`](#read-file-as-string)

</details>

### Exception

<details>
<summary>View contents</summary>

* [`Throw exception`](#throw-exception)
* [`Try catch`](#try-catch)

</details>

### Thread

<details>
<summary>View contents</summary>

* [`Create thread`](#create-thread)
* [`Future`](#future)

</details>

### Examples

<details>
<summary>View contents</summary>

* [`Plus operation`](#plus-operation)

</details>

---

## Basic

### Hello World

Print `hello world` is the first thing in programming languages 😋

```java
System.out.print("Hello World\n");

System.out.println("Hello World");
```

```clojure
(print "Hello World\n")
;; => Hello World

(println "Hello World")
;; => Hello World
```

### Comment

```java
// This is a one-line comment

/**
 * This is a multi-line comment
 */
```

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

### Variable

```java
String name = "biezhi";
int age     = 2333;
```

In fact, variables cannot be defined in `clojure`. These values ​​are immutable, like in Java `final`.

```clojure
(def name "biezhi")
(def age  2333)
```

`def` can be creates and interns or locates a global var with the name of symbol.

### Create List

```java
List<String> list = new ArrayList<>();
list.add("a");
list.add("b");
list.add("c");

List<String> list = Arrays.asList("a", "b", "c");
```

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

### Add item to List

```java
list.add("d");

list.addAll(newList);
```

```clojure
;; returns a new collection with the xs 'added'
(conj my-list "d")
;;=> ("d" "a" "b" "c")

(cons "d" my-list)
;;=> ("d" "a" "b" "c")

(concat my-list '("d" "e" "f"))
;;=> ("a" "b" "c" "d" "e" "f")
```

### Get List item

```java
String a = list.get(0);
```

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

### Get List count

```java
int size = list.size();
```

```clojure
(count '(1 2 3))
;;=> 3
```

---

### Create Array

```java
String[] fruits = new String[3];
fruits[0] = "peach";
fruits[1] = "pear";
fruits[2] = "apple";

String[] fruits = {"peach", "pear", "apple"};
```

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

### Get Array item

```java
String pear = fruits[1];
```

```clojure
(second fruits)
;; => "pear"

(nth fruits 1)
;; => "pear"
```

### Get Array count

```java
int length = fruits.length;
```

```clojure
(count fruits)
;;=> 3
```

### Two dimensional array

```java
int[][] points = {
                {23, 45},
                {42, 88},
        };

int[] idx = points[0];
```

```clojure
(def points [[23, 45] [42, 88]])

(first points)
;;=> [23, 45]

(nth points 1)
;;=> [42, 88]
```

---

### Create Map

```java
Map<String, Integer> me = new HashMap<>();
me.put("name", "biezhi");
me.put("age", 2333);
```

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

### Get Map item

```java
String url = me.get("url");
```

```clojure
(:name me)
;;=> "biezhi"

(get me :name)
;;=> "biezhi"

(me :name)
;;=> "biezhi"
```

### Define function

```java
void sayHello() {
    System.out.println("hello");
}
```

```clojure
;; assign a function to a variable
(defn say-hello [] (println "hello"))

(say-hello)
;; => hello
```

### Function with parameters

```java
void sayHello(String name) {
    System.out.println("hello " + name);
}
```

```clojure
;; define a function with parameters
(defn say-hello [name] (println (str "hello " name)))

(say-hello "world")
;; => hello world
```

### Anonymous function

```java
Runnable r = () -> System.out.println("Hello Boy.");
r.run();
```

```clojure
;; the same but using an anonymous function
(def say-hello
 #(str "hello " %))

;; assign a function to a variable
(def say-hello
 (fn [name]
   (str "Hello " name)))

;; anonymous function using two arguments
(def hello-doc #(str "Hello " %1 %2))
```

### With return value

```java
String sayHello(String name) {
    return "hello " + name;
}
```

```clojure
(defn say-hello [name] (str "hello " name))
```

### If else

```java
int age = 23;
if (age > 18) {
    System.out.println("You have grown up, don't be like a child again.");
} else {
    System.out.println("Let's learn the cat call together, say 'miao miao miao'.");
}
```

```clojure
(def age 14)
(if (> age 18)
  (println "You have grown up, don't be like a child again.")
  (println "Let's learn the cat call together, say 'miao miao miao'."))
```

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

```clojure
(case 3
  3 "red"
  2 "blue"
  1 "pink"
  "#000")
;;=> "red"
```

### Not

```java
int flag = 2333;

if (flag != 100){
    // do some thing
}
```

```clojure
(def flag 2333)
(if (not (= 100 flag)) (println "not eq 2333"))
;;=> not eq 2333
```

### And

```java
boolean success = (result.ok && result.code == 200);
```

```clojure
(and (true? result.ok) (= 200 result.code))
```

### Or

```java
boolean success = (result.ok || result.code == 200);
```

```clojure
(or (true? result.ok) (= 200 result.code))
```

### For

```java
for (int i=0; i<10; i++){
    System.out.println("i = " + i);
}
```

```clojure
(doseq [i (range 10)] 
  (println (str "i =" i)))

(for [i (range 10)] 
  (do (println (str "i =" i))))
```

### While

```java
int seq = 10;
while (seq > 0) {
    System.out.prinln("seq = " + (seq--));
}
```

```clojure
(def seq-num (atom 10))
(while (> @seq-num 0)
   (do (println (str "seq = " @seq-num)) (swap! seq-num dec) ))
```

### to string

```java
Integer age = 2333;
System.out.println(age.toString());
```

```clojure
(str 2333)
;;=> "2333"
```

### String append

```java
String a = "hello " + "world " + 2333;
```

```clojure
(str "hello " "world " 2333)
;;=> "hello world 2333"
```

### String replace

```java
String url = "https://biezhi.me";
System.out.println("New url is: " + url.replace('.', '#');

String str = "A good day to you, sir.  Good day.";
System.out.println("New str is: " + url.replaceFirst("day", "night");

String str = "This is a String to use as an example to present raplaceAll";
System.out.println(str.replaceAll("This", "That"));
```

```clojure
(clojure.string/replace "https://biezhi.me" #"\." "#")

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

### String join

```java
String.join(", ", "jack", "biezhi", "rose", "mark")
```

```clojure
(clojure.string/join ", " ["jack", "biezhi", "rose", "mark"])
;;=> "jack, biezhi, rose, mark"
```

### String split

```java
"jack, biezhi, rose, mark".split(", ");

"h1e2l3l4o5w6o7r8d9d".split("\\d+");
```

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

### String substring

```java
"biezhi".substring(1);
"biezhi".substring(0, 3);
"biezhi".substring(0, 6);
```

```clojure
(subs "biezhi" 1)
;;=> "iezhi"

(subs "biezhi" 0 3)
;;=> "bie"

(subs "biezhi" 0 6)
;;=> "biezhi"
```

# License

[MIT](LICENSE)