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

* [`hello-world`](#hello-world)
* [`comment`](#comment)

</details>


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
```

```clojure
(list "a" "b" "c")

'("a" "b" "c")
```

### map

```java
Map<String, Integer> map = new HashMap<>();
map.put("name", "biezhi");
map.put("age", 2333);
map.put("url", "https://github.com/biezhi");
```

```clojure
(def map {:name "biezhi",
          :age   2333
          :url   "https://github.com/biezhi"})
```

# License

[MIT](LICENSE)