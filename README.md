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
* [`replace`](#replace)
* [`join`](#join)
* [`split`](#split)

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

### comment

```java
// This is a one-line comment

/**
 * This is a multi-line comment
 */
```

```clojure
; i don't know what I should do

(comment "
    Here are the comments
")
```

### variable

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

### create list

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

### add item to list

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

### get list item

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

### get list count

```java
int size = list.size();
```

```clojure
(count '(1 2 3))
;;=> 3
```

---

### create array

```java
String[] fruits = new String[3];
fruits[0] = "peach";
fruits[1] = "pear";
fruits[2] = "apple";

String[] fruits = {"peach", "pear", "apple"};
```

```clojure
(def fruits ["peach", "pear", "apple"])
```

### get array item

```java
String pear = fruits[1];
```

```clojure
(second fruits)
;; => "pear"

(nth fruits 1)
;; => "pear"
```

### get array count

```java
int length = fruits.length;
```

```clojure
(count fruits)
;;=> 3
```

### two dimensional array

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

### create map

```java
Map<String, Integer> me = new HashMap<>();
me.put("name", "biezhi");
me.put("age", 2333);
```

```clojure
(def me {:name "biezhi",
          :age   2333
          :url   "https://github.com/biezhi"})
```

### get map item

```java
String url = me.get("url");
```

```clojure
;; get item by keyword
(:name me)
;; => "biezhi"

;; get by "get" function
(get me :name)
;; => "biezhi"
```

### define function

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

### function with parameters

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

### anonymous function

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

### with return value

```java
String sayHello(String name) {
    return "hello " + name;
}
```

```clojure
(defn say-hello [name] (str "hello " name))
```

# License

[MIT](LICENSE)