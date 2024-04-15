#Java #HashMap #Map

## HashMap в Java

2024-04-10 10:31

В Java _HashMap_ является частью коллекции Java начиная с Java 1.2. Этот класс находится в _package java.util_. Он обеспечивает базовую реализацию интерфейса [_Map_](Map) в Java. HashMap в Java хранит данные в парах (ключ, значение), и вы можете получить к ним доступ по индексу другого типа (например, целому числу). Один объект используется в качестве ключа (индекса) к другому объекту (значению). Если вы попытаетесь вставить дубликат ключа в _HashMap_, он заменит элемент соответствующего ключа.

Java _HashMap_ похожа на [Hashtable](Hashtable), но она несинхронизированная. Он также позволяет хранить нулевые ключи, но должен быть только один объект с нулевым ключом и может быть любое количество нулевых значений. Этот класс не дает никаких гарантий относительно порядка отображения. Чтобы использовать этот класс и его методы, вам необходимо импортировать `java.util.HashMap` пакет или его суперкласс.

### Объявление HashMap

```java
public class HashMap<K,V> extends AbstractMap<K,V>
                          implements Map<K,V>, Cloneable, Serializable
```
**Параметры:**
- Тип ключей, поддерживаемых этой картой
- Тип отображаемых значений

> __Примечание__: Keys и value не могут быть примитивным типом данных. Ключ в _Hashmap_ допустим, если он реализует [hashCode() и equals() методы](https://www.geeksforgeeks.org/internal-working-of-hashmap-java/) он также должен быть неизменяемым (immutable custom object), чтобы хэш-код и равенство оставались постоянными. Значением в hashmap может быть любой класс-оболочка, пользовательские объекты, массивы, любой ссылочный тип или даже null.
> __Например__: _Hashmap_ может иметь массив в качестве значения, но не в качестве ключа.

Класс _HashMap_ в Java реализует [сериализуемый](Serializable) и [клонируемый](Cloneable) интерфейс [Map<K, V>](Map) и PrinterStateReasons.

### Характеристики Java HashMap

_HashMap_ — это структура данных, которая используется для хранения и извлечения образцов на основе ключей. Некоторые из основных характеристик _HashMap_ включают в себя:
- Быстрое время доступа: _HashMap_ обеспечивают постоянный доступ к элементам во времени, что означает, что извлечение и вставка элементов происходит очень быстро.
- Использует функцию хеширования: _HashMap_ использует хэш-функцию для сопоставления ключей с индексами в массиве. Это позволяет быстро искать значения на основе ключей.
- Хранит пары ключ-значение. Каждый элемент в _HashMap_ состоит из пары ключ-значение. Ключ используется для поиска связанного значения.
- Поддерживает нулевые ключи и значения: _HashMap_ допускает нулевые значения и ключи. Это означает, что нулевой ключ можно использовать для хранения значения, а нулевое значение можно связать с ключом.
- Неупорядоченно: _HashMap_ не упорядочены, что означает, что порядок добавления элементов на карту не сохраняется. Однако [_LinkedHashMap_](LinkedHashMap) — это вариант _HashMap_, который сохраняет порядок вставки.
- Разрешает дубликаты: _HashMap_ допускает дублирование значений, но не дублирование ключей. Если добавляется дубликат ключа, предыдущее значение, связанное с ключом, перезаписывается.
- Потокобезопасность: _HashMap_ не являются потокобезопасными, а это означает, что если несколько потоков одновременно обращаются к одной и той же _HashMap_, это может привести к несогласованности данных. Если требуется безопасность потоков, можно использовать [[Concurrent#Concurrent Collections|ConcurrentHashMap]].
- Емкость и коэффициент загрузки: у _HashMap_ есть емкость, которая представляет собой количество элементов, которые он может содержать, и коэффициент загрузки, который является мерой того, насколько полной может быть _HashMap_ до изменения ее размера.

### Конструкторы Java HashMap

_HashMap_ предоставляет 4 конструктора, модификатор доступа каждого из которых является общедоступным. Они перечислены следующим образом:
1. HashMap()
2. HashMap(int initialCapacity)
3. HashMap (int initialCapacity, float loadFactor)
4. HashMap (Map map)

Теперь мы обсудим вышеупомянутые конструкторы один за другим, а также реализуем их с помощью чистых программ Java.

#### 1. HashMap()

Это конструктор по умолчанию, который создает экземпляр _HashMap_ с начальной емкостью 16 и коэффициентом загрузки 0,75.
```java
HashMap<K, V> hm = new HashMap<K, V>();
```
**Пример**
```java
// Java program to Demonstrate the HashMap() constructor
// Importing basic required classes
import java.io.*;
import java.util.*;
 
// Main class
// To add elements to HashMap
class GFG {
    // Main driver method
    public static void main(String args[]) {
        // No need to mention the
        // Generic type twice
        HashMap<Integer, String> hm1 = new HashMap<>();
 
        // Initialization of a HashMap using Generics
        HashMap<Integer, String> hm2 = new HashMap<Integer, String>();
 
        // Adding elements using put method
        // Custom input elements
        hm1.put(1, "one");
        hm1.put(2, "two");
        hm1.put(3, "three");
 
        hm2.put(4, "four");
        hm2.put(5, "five");
        hm2.put(6, "six");
 
        // Print and display mapping of HashMap 1
        System.out.println("Mappings of HashMap hm1 are : " + hm1);
 
        // Print and display mapping of HashMap 2
        System.out.println("Mapping of HashMap hm2 are : " + hm2);
    }
}
```
**Вывод**
<p style="background-color: navy; color: yellow">
Mappings of HashMap hm1 are : {1=one, 2=two, 3=three}<br>
Mapping of HashMap hm2 are : {4=four, 5=five, 6=six}</p>

#### 2. HashMap(int initialCapacity)

Он создает экземпляр HashMap с указанной начальной емкостью и коэффициентом загрузки 0,75.
```java
HashMap<K, V> hm = new HashMap<K, V>(int InitialCapacity);
```
__Пример__
```java
// Java program to Demonstrate
// HashMap(int initialCapacity) Constructor
// Importing basic classes
import java.io.*;
import java.util.*;
 
// Main class
// To add elements to HashMap
class AddElementsToHashMap {
    // Main driver method
    public static void main(String args[]) {
        // No need to mention the
        // Generic type twice
        HashMap<Integer, String> hm1 = new HashMap<>(10);
 
        // Initialization of a HashMap using Generics
        HashMap<Integer, String> hm2 = new HashMap<Integer, String>(2);
 
        // Adding elements to object of HashMap
        // using put method
 
        // HashMap 1
        hm1.put(1, "one");
        hm1.put(2, "two");
        hm1.put(3, "three");
 
        // HashMap 2
        hm2.put(4, "four");
        hm2.put(5, "five");
        hm2.put(6, "six");
 
        // Printing elements of HashMap 1
        System.out.println("Mappings of HashMap hm1 are : " + hm1);
 
        // Printing elements of HashMap 2
        System.out.println("Mapping of HashMap hm2 are : " + hm2);
    }
}
```
Вывод
<p style="background-color: navy; color: yellow">
Mappings of HashMap hm1 are : {1=one, 2=two, 3=three}<br>
Mapping of HashMap hm2 are : {4=four, 5=five, 6=six}</p>

#### 3. HashMap(int initialCapacity, float loadFactor)

Он создает экземпляр _HashMap_ с указанной начальной емкостью и указанным коэффициентом загрузки.
```java
HashMap<K, V> hm = new HashMap<K, V>(int InitialCapacity, float loadFactor);
```
**Пример**
```java
// Java program to Demonstrate
// HashMap(int initialCapacity,float loadFactor) Constructor
// Importing basic classes
import java.io.*;
import java.util.*;
 
// Main class
// To add elements to HashMap
class GFG {
    // Main driver method
    public static void main(String args[]) {
        // No need to mention the generic type twice
        HashMap<Integer, String> hm1 = new HashMap<>(5, 0.75f);
 
        // Initialization of a HashMap using Generics
        HashMap<Integer, String> hm2 = new HashMap<Integer, String>(3, 0.5f);
 
        // Add Elements using put() method
        // Custom input elements
        hm1.put(1, "one");
        hm1.put(2, "two");
        hm1.put(3, "three");
 
        hm2.put(4, "four");
        hm2.put(5, "five");
        hm2.put(6, "six");
 
        // Print and display elements in object of hashMap 1
        System.out.println("Mappings of HashMap hm1 are : " + hm1);
 
        // Print and display elements in object of hashMap 2
        System.out.println("Mapping of HashMap hm2 are : " + hm2);
    }
}
```
Вывод
<p style="background-color: navy; color: yellow">
Mappings of HashMap hm1 are : {1=one, 2=two, 3=three}<br>
Mapping of HashMap hm2 are : {4=four, 5=five, 6=six}</p>

####  4. HashMap (Map map)****

Он создает экземпляр _HashMap_ с теми же сопоставлениями, что и указанная карта.
```java
HashMap<K, V> hm = new HashMap<K, V>(Map map);
```
**Пример**
```java
// Java program to demonstrate the 
// HashMap(Map map) Constructor
import java.io.*;
import java.util.*;
 
class AddElementsToHashMap {
    public static void main(String args[]) {
        // No need to mention the
        // Generic type twice
        Map<Integer, String> hm1 = new HashMap<>();
 
        // Add Elements using put method
        hm1.put(1, "one");
        hm1.put(2, "two");
        hm1.put(3, "three");
 
        // Initialization of a HashMap
        // using Generics
        HashMap<Integer, String> hm2 = new HashMap<Integer, String>(hm1);
 
        System.out.println("Mappings of HashMap hm1 are : " + hm1);
       
        System.out.println("Mapping of HashMap hm2 are : " + hm2);
    }
}
```
Вывод
<p style="background-color: navy; color: yellow">
Mappings of HashMap hm1 are : {1=one, 2=two, 3=three}<br>
Mapping of HashMap hm2 are : {1=one, 2=two, 3=three}</p>

### Основные операции с Java HashMap

Класс _HashMap_ предоставляет различные методы для выполнения различных операций с хэш-картами. Рассмотрим некоторые часто используемые операции:
- Добавление элементов
- Элементы доступа
- Изменение элементов
- Удалить элементы

#### 1. Добавьте элементы в HashMap

Чтобы добавить отдельный элемент в _Hashmap_, мы используем `put()` метод класса _HashMap_. Например,
```java
import java.util.HashMap;

class Main {
  public static void main(String[] args) {
    // create a hashmap
    HashMap<String, Integer> numbers = new HashMap<>();

    System.out.println("Initial HashMap: " + numbers);
    // put() method to add elements
    numbers.put("One", 1);
    numbers.put("Two", 2);
    numbers.put("Three", 3);
    System.out.println("HashMap after put(): " + numbers);
  }
}
```
**Вывод**
<p style="background-color: navy; color: yellow">
Initial HashMap: {}<br>
HashMap after put(): {One=1, Two=2, Three=3}</p>

В приведенном выше примере мы создали _HashMap_ . Здесь мы использовали `put()` метод для добавления элементов.
Обратите внимание на утверждение,
```java
numbers.put("One", 1);
```
Здесь мы передаем `String` значение One в качестве ключа и `Integer` value 1 в качестве значения `put()` методу.

**Также читайте:**
- [Java HashMap put()](https://www.programiz.com/java-programming/library/hashmap/put)
- [Java HashMap putAll()](https://www.programiz.com/java-programming/library/hashmap/putall)
- [Java HashMap putIfAbsent()](https://www.programiz.com/java-programming/library/hashmap/putifabsent)

#### 2. Доступ к элементам HashMap

Мы можем использовать метод `get()` для доступа к значению из hashmap. Например,
```java
import java.util.HashMap;

class Main {
  public static void main(String[] args) {

    HashMap<Integer, String> languages = new HashMap<>();
    languages.put(1, "Java");
    languages.put(2, "Python");
    languages.put(3, "JavaScript");
    System.out.println("HashMap: " + languages);

    // get() method to get value
    String value = languages.get(1);
    System.out.println("Value at index 1: " + value);
  }
}
```
**Вывод**
<p style="background-color: navy; color: yellow">
HashMap: {1=Java, 2=Python, 3=JavaScript}<br>
Value at index 1: Java</p>

В приведенном выше примере обратите внимание на выражение,
```java
languages.get(1);
```
Здесь `get()` метод принимает **ключ** в качестве своего аргумента и возвращает соответствующее **значение**, связанное с ключом.

Мы также можем получить доступ к **ключам**, **значениям** и парам **ключ / значение** хэш-карты в виде заданных представлений, используя `keySet()`, `values()` и `entrySet()` методы соответственно. Например,
```java
import java.util.HashMap;

class Main {
  public static void main(String[] args) {
    HashMap<Integer, String> languages = new HashMap<>();

    languages.put(1, "Java");
    languages.put(2, "Python");
    languages.put(3, "JavaScript");
    System.out.println("HashMap: " + languages);

    // return set view of keys
    // using keySet()
    System.out.println("Keys: " + languages.keySet());

    // return set view of values
    // using values()
    System.out.println("Values: " + languages.values());

    // return set view of key/value pairs
    // using entrySet()
    System.out.println("Key/Value mappings: " + languages.entrySet());
  }
}
```
**Вывод**
<p style="background-color: navy; color: yellow">
HashMap: {1=Java, 2=Python, 3=JavaScript}<br>
Keys: [1, 2, 3]<br>
Values: [Java, Python, JavaScript]<br>
Key/Value mappings: [1=Java, 2=Python, 3=JavaScript]</p>

В приведенном выше примере мы создали hashmap с именем languages. Здесь мы получаем доступ к **ключам**, **значениям** и сопоставлениям **ключ / значение** из hashmap.

**Также читайте:**
- [Java HashMap get()](https://www.programiz.com/java-programming/library/hashmap/get)
- [Java Hashmap getOrDefault()](https://www.programiz.com/java-programming/library/hashmap/getordefault)
- [Набор ключей Java HashMap()](https://www.programiz.com/java-programming/library/hashmap/keyset)
- [Значения Java HashMap ()](https://www.programiz.com/java-programming/library/hashmap/values)
- [Java HashMap entrySet()](https://www.programiz.com/java-programming/library/hashmap/entryset)

#### 3. Измените значение HashMap

Мы можем использовать метод `replace()` для изменения значения, связанного с ключом в hashmap. Например,
```java
import java.util.HashMap;

class Main {
  public static void main(String[] args) {

    HashMap<Integer, String> languages = new HashMap<>();
    languages.put(1, "Java");
    languages.put(2, "Python");
    languages.put(3, "JavaScript");
    System.out.println("Original HashMap: " + languages);

    // change element with key 2
    languages.replace(2, "C++");
    System.out.println("HashMap using replace(): " + languages);
  }
}
```
**Вывод**
<p style="background-color: navy; color: yellow">
Original HashMap: {1=Java, 2=Python, 3=JavaScript}<br>
HashMap using replace(): {1=Java, 2=C++, 3=JavaScript}</p>
В приведенном выше примере мы создали hashmap с именем languages. Обратите внимание на выражение,
```java
languages.replace(2, "C++");
```
Здесь мы меняем значение, на которое ссылается ключ **2**, на новое значение C++.

Класс _HashMap_ также предоставляет некоторые варианты `replace()` метода. Чтобы узнать больше, посетите
- [Java HashMap replace()](https://www.programiz.com/java-programming/library/hashmap/replace)
- [Java HashMap replaceAll()](https://www.programiz.com/java-programming/library/hashmap/replaceall)

#### 4. Удалите элементы HashMap

Чтобы удалить элементы из hashmap, мы можем использовать метод remove() . Например,
```java
import java.util.HashMap;

class Main {
  public static void main(String[] args) {

    HashMap<Integer, String> languages = new HashMap<>();
    languages.put(1, "Java");
    languages.put(2, "Python");
    languages.put(3, "JavaScript");
    System.out.println("HashMap: " + languages);

    // remove element associated with key 2
    String value = languages.remove(2);
    System.out.println("Removed value: " + value);

    System.out.println("Updated HashMap: " + languages);
  }
}
```
**Вывод**
<p style="background-color: navy; color: yellow">
HashMap: {1=Java, 2=Python, 3=JavaScript}<br>
Removed value: Python<br>
Updated HashMap: {1=Java, 3=JavaScript}</p>

Здесь `remove()` метод принимает **ключ** в качестве своего параметра. Затем он возвращает **значение**, связанное с **ключом**, и удаляет **запись**.

Мы также можем удалить запись только при определенных условиях. Например,
```java
remove(2, "C++");
```
Здесь `remove()` метод удаляет **запись** только в том случае, если **ключ 2** связан с **значением C ++**. Поскольку **2** не связан с **C ++**, запись не удаляется.

Чтобы узнать больше, посетите [Java HashMap remove()](https://www.programiz.com/java-programming/library/hashmap/remove).

## Другие методы работы с HashMap

| Метод                                                                                             | Описание                                                     |
| ------------------------------------------------------------------------------------------------- | ------------------------------------------------------------ |
| [clear()](https://www.programiz.com/java-programming/library/hashmap/clear)                       | удаляет все сопоставления из _HashMap_                       |
| [compute()](https://www.programiz.com/java-programming/library/hashmap/compute)                   | вычисляет новое значение для указанного ключа                |
| [computeIfAbsent()](https://www.programiz.com/java-programming/library/hashmap/computeifabsent)   | вычисляет значение, если отображение для ключа отсутствует   |
| [computeIfPresent()](https://www.programiz.com/java-programming/library/hashmap/computeifpresent) | вычисляет значение для сопоставления, если присутствует ключ |
| [merge()](https://www.programiz.com/java-programming/library/hashmap/merge)                       | объединяет указанное отображение с _HashMap_                 |
| [clone()](https://www.programiz.com/java-programming/library/hashmap/clone)                       | создает копию _HashMap_                                      |
| [containsKey()](https://www.programiz.com/java-programming/library/hashmap/containskey)           | проверяет, присутствует ли указанный ключ в _Hashmap_        |
| [containsValue()](https://www.programiz.com/java-programming/library/hashmap/containsvalue)       | проверяет, `Hashmap` содержит ли указанное значение          |
| [size()](https://www.programiz.com/java-programming/library/hashmap/size)                         | возвращает количество элементов в _HashMap_                  |
| [isEmpty()](https://www.programiz.com/java-programming/library/hashmap/isempty)                   | проверяет, является ли _Hashmap_ пустым                      |

## Выполнение итерации по HashMap

Для перебора каждой записи hashmap мы можем использовать [Java for-each loop](https://www.programiz.com/java-programming/enhanced-for-loop). Мы можем перебирать **только ключи**, **только значения** и **сопоставление ключ/значение**. Например,
```java
import java.util.HashMap;
import java.util.Map.Entry;

class Main {
  public static void main(String[] args) {

    // create a HashMap
    HashMap<Integer, String> languages = new HashMap<>();
    languages.put(1, "Java");
    languages.put(2, "Python");
    languages.put(3, "JavaScript");
    System.out.println("HashMap: " + languages);

    // iterate through keys only
    System.out.print("Keys: ");
    for (Integer key : languages.keySet()) {
      System.out.print(key);
      System.out.print(", ");
    }

    // iterate through values only
    System.out.print("\nValues: ");
    for (String value : languages.values()) {
      System.out.print(value);
      System.out.print(", ");
    }
    
    // iterate through key/value entries
    System.out.print("\nEntries: ");
    for (Entry<Integer, String> entry : languages.entrySet()) {
      System.out.print(entry);
      System.out.print(", ");
    }
  }
}
```
**Вывод**
<p style="background-color: navy; color: yellow">
HashMap: {1=Java, 2=Python, 3=JavaScript}<br>
Keys: 1, 2, 3,<br>
Values: Java, Python, JavaScript,<br>
Entries: 1=Java, 2=Python, 3=JavaScript,</p>

Обратите внимание, что мы использовали _Map.Entry_ в приведенном выше примере. Это вложенный класс [_Map_](Map) интерфейса, который возвращает вид (элементы) карты.

Сначала нам нужно импортировать `java.util.Map.Entry` пакет, чтобы использовать этот класс.

Этот вложенный класс возвращает вид (элементы) карты.

### Создание HashMap из других карт

В Java мы также можем создавать _Hashmap_ из других карт. Например,
```java
import java.util.HashMap;
import java.util.TreeMap;

class Main {
  public static void main(String[] args) {

    // create a treemap
    TreeMap<String, Integer> evenNumbers = new TreeMap<>();
    evenNumbers.put("Two", 2);
    evenNumbers.put("Four", 4);
    System.out.println("TreeMap: " + evenNumbers);

    // create hashmap from the treemap
    HashMap<String, Integer> numbers = new HashMap<>(evenNumbers);
    numbers.put("Three", 3);
    System.out.println("HashMap: " + numbers);
  }
}
```
**Вывод**
<p style="background-color: navy; color: yellow">
TreeMap: {Four=4, Two=2}<br>
HashMap: {Two=2, Three=3, Four=4}</p>

В приведенном выше примере мы создали _TreeMap_ named `evenNumbers`. Обратите внимание на выражение,
```java
numbers = new HashMap<>(evenNumbers)
```
Здесь мы создаем _HashMap_ именованные числа с помощью [_TreeMap_](TreeMap). Чтобы узнать больше о _TreeMap_, посетите [Java TreeMap](https://www.programiz.com/java-programming/treemap).
