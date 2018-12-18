# Java Clojure Syntax Comparison

Comparison of some code snippets in the Java and Clojure.

- Java Version: `1.8.0_101`
- Clojure Version: `1.9`

## Table of Contents

### Basic

<details>
<summary>View contents</summary>

* [`hello-world`](#hello-world)
* [`comment`](#comment)
* [`variable`](#variable)
* [`function`](#function)
* [`list`](#list)
* [`array`](#array)
* [`map`](#map)
* [`struct`](#struct)

</details>

### Flow Control

<details>
<summary>View contents</summary>

* [`if-else`](#if-else)
* [`switch`](#switch)
* [`not`](#not)
* [`and`](#and)
* [`or`](#or)
* [`for`](#for)
* [`while`](#while)

</details>

### String

<details>
<summary>View contents</summary>

* [`to-string`](#to-string)
* [`replace`](#replace)
* [`join`](#join)
* [`split`](#split)

</details>

### IO

<details>
<summary>View contents</summary>

* [`read-file-as-string`](#read-file-as-string)
* [`comment`](#comment)

</details>

### Exception

<details>
<summary>View contents</summary>

* [`throw-exception`](#throw-exception)
* [`try-catch`](#try-catch)

</details>

### Thread

<details>
<summary>View contents</summary>

* [`create-thread`](#create-thread)
* [`future`](#future)

</details>

### Examples

<details>
<summary>View contents</summary>

* [`plus-operation`](#plus-operation)
* [`comment`](#comment)

</details>

---

## Basic

### hello-world

```java
System.out.println("Hello World");
```

```clojure
(println "Hello World")
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

### function

**Normal method without parameters**

```java
void sayHello() {
    System.out.println("hello");
}
```

```clojure
(defn say-hello [] (println "hello"))
```

**Method of receiving a parameter**

```java
void sayHello(String name) {
    System.out.println("hello " + name);
}
```

```clojure
(defn say-hello [name] (println (str "hello " name)))
```

### list

```java
List<String> list = new ArrayList<>();
list.add("a");
list.add("b");
list.add("c");

List<String> list = Arrays.asList("a", "b", "c");

String item = list.get(1);
```

```clojure
(list "a" "b" "c")

'("a" "b" "c")

;; returns a new collection with the xs 'added'
(conj (list "a" "b" "c") "d")
;;=> ("d" "a" "b" "c")

(cons "d" (list "a" "b" "c"))
;;=> ("d" "a" "b" "c")

;; get first by list
(first (list "a" "b" "c"))

;; get first by list
(second (list "a" "b" "c"))

;; get item by index
(nth (list "a" "b" "c") 1)
```

### map

```java
Map<String, Integer> map = new HashMap<>();
map.put("name", "biezhi");
map.put("age", 2333);
map.put("url", "https://github.com/biezhi");

String name = map.get("name");
```

```clojure
(def map {:name "biezhi",
          :age   2333
          :url   "https://github.com/biezhi"})

;; get item by keyword
(:name map)
;; => "biezhi"

;; get by "get" function
(get map :name)
;; => "biezhi"
```

# License

[MIT](LICENSE)