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

### hello-world

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
int age = 2333;
```

```clojure
(def name "biezhi")
(def age 2333)
```

### create list

```java
List<String> list = new ArrayList<>();
list.add("a");
list.add("b");
list.add("c");

List<String> list = Arrays.asList("a", "b", "c");
```

```clojure
(list "a" "b" "c")

'("a" "b" "c")
```

### add item to list

```java
list.add("d");

list.addAll(newList);
```

```clojure
;; returns a new collection with the xs 'added'
(conj (list "a" "b" "c") "d")
;;=> ("d" "a" "b" "c")

(cons "d" (list "a" "b" "c"))
;;=> ("d" "a" "b" "c")

(concat '("a" "b" "c") '("d" "e" "f"))
;;=> ("a" "b" "c" "d" "e" "f")
```

### get list item

```java
String a = list.get(0);
```

```clojure
;; get first by list
(first (list "a" "b" "c"))

;; get first by list
(second (list "a" "b" "c"))

;; get item by index
(nth (list "a" "b" "c") 1)
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