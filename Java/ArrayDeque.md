#Java #Collection #Queue #Deque #ArrayDeque

## Java ArrayDeque

2024-04-08 12:42

В Java мы можем использовать `ArrayDeque` класс для реализации интерфейсов [Queue](Queue) и [Deque](Deque) с использованием [массивов](Array).
![[java-arraydeque-class.png]]

### Создание ArrayDeque

Чтобы создать массив deque, мы должны импортировать `java.util.ArrayDeque` пакет.
Вот как мы можем создать массив deque в Java:
```java
ArrayDeque<Type> animal = new ArrayDeque<>();
```
Здесь, Type указывает тип массива deque. Например,
```java
// Creating String type ArrayDeque
ArrayDeque<String> animals = new ArrayDeque<>();

// Creating Integer type ArrayDeque
ArrayDeque<Integer> age = new ArrayDeque<>();
```

### Методы ArrayDeque

Класс `ArrayDeque` предоставляет реализации для всех методов, присутствующих в интерфейсах [Queue](Queue) и [Deque](Deque).

#### Вставка элементов в [Deque](Deque)

**1. Добавьте элементы с помощью add(), addFirst() и addLast()**
- `add()` - вставляет указанный элемент в конец массива deque
- `addFirst()` - вставляет указанный элемент в начало массива deque
- `addLast()` - вставляет указанный в конце массива deque (эквивалент `add()`)

>**Примечание:** Если массив deque заполнен, все эти методы `add()`, `addFirst()` и `addLast()` выбрасывают `IllegalStateException`.

Например,
```java
import java.util.ArrayDeque;

class Main {
    public static void main(String[] args) {
        ArrayDeque<String> animals= new ArrayDeque<>();
        // Using add()
        animals.add("Dog");
        // Using addFirst()
        animals.addFirst("Cat");
        // Using addLast()
        animals.addLast("Horse");
        System.out.println("ArrayDeque: " + animals);
    }
}
```
**Вывод**
<p style="background-color: navy; color: yellow">
ArrayDeque: [Cat, Dog, Horse]</p>

**2. Вставьте элементы, используя offer(), offerFirst() и offerLast()**
- `offer()` - вставляет указанный элемент в конец массива deque
- `offerFirst()` - вставляет указанный элемент в начало массива deque
- `offerLast()` - вставляет указанный элемент в конец массива deque

>**Примечание:** `offer()`, `offerFirst()` и `offerLast()` возвращает `true`, если элемент успешно вставлен; если deque массива заполнен, эти методы возвращают `false`.

Например,
```java
import java.util.ArrayDeque;

class Main {
    public static void main(String[] args) {
        ArrayDeque<String> animals= new ArrayDeque<>();
        // Using offer()
        animals.offer("Dog");
        // Using offerFirst()
        animals.offerFirst("Cat");
        // Using offerLast()
        animals.offerLast("Horse");
        System.out.println("ArrayDeque: " + animals);
    }
}
```
**Вывод**
<p style="background-color: navy; color: yellow">
ArrayDeque: [Cat, Dog, Horse]</p>

>**Примечание:** Если deque массива заполнен:
>- `add()`метод выдаст [исключение](Exceptions)
>- метод `offer()` возвращает `false`

#### Доступ к элементам ArrayDeque

**1. Доступ к элементам с помощью getFirst() и getLast()**
- `getFirst()` - возвращает первый элемент массива deque
- `getLast()` - возвращает последний элемент массива deque

>**Примечание:** Если массив deque пуст, `getFirst()` и `getLast()` выдает `NoSuchElementException`.

Например,
```java
import java.util.ArrayDeque;

class Main {
    public static void main(String[] args) {
        ArrayDeque<String> animals= new ArrayDeque<>();
        animals.add("Dog");
        animals.add("Cat");
        animals.add("Horse");
        System.out.println("ArrayDeque: " + animals);

        // Get the first element
        String firstElement = animals.getFirst();
        System.out.println("First Element: " + firstElement);

        // Get the last element
        String lastElement = animals.getLast();
        System.out.println("Last Element: " + lastElement);
    }
}
```
**Вывод**
<p style="background-color: navy; color: yellow">
ArrayDeque: [Dog, Cat, Horse]<br>
First Element: Dog<br>
Last Element: Horse</p>

**2. Доступ к элементам с помощью методов peek(), peekFirst() и peekLast()**
- `peek()` - возвращает первый элемент массива deque
- `peekFirst()` - возвращает первый элемент массива deque (эквивалентно `peek()`)
- `peekLast()` - возвращает последний элемент массива deque

Например,
```java
import java.util.ArrayDeque;

class Main {
    public static void main(String[] args) {
        ArrayDeque<String> animals= new ArrayDeque<>();
        animals.add("Dog");
        animals.add("Cat");
        animals.add("Horse");
        System.out.println("ArrayDeque: " + animals);

        // Using peek()
        String element = animals.peek();
        System.out.println("Head Element: " + element);

        // Using peekFirst()
        String firstElement = animals.peekFirst();
        System.out.println("First Element: " + firstElement);

        // Using peekLast
        String lastElement = animals.peekLast();
        System.out.println("Last Element: " + lastElement);
    }
}
```
**Вывод**
<p style="background-color: navy; color: yellow">
ArrayDeque: [Dog, Cat, Horse]<br>
Head Element: Dog<br>
First Element: Dog<br>
Last Element: Horse</p>

>**Примечание:** Если массив deque пуст, `peek()`, `peekFirst()` и `getLast()` выдает `NoSuchElementException`.

#### Удалить элементы ArrayDeque

**1. Удалите элементы с помощью методов remove(), removeFirst(), removeLast()**:
- `remove()` - возвращает и удаляет элемент из первого элемента массива deque;
- `remove(element)` - возвращает и удаляет указанный элемент из заголовка массива deque;
- `removeFirst()` - возвращает и удаляет первый элемент из массива deque (эквивалентно `remove()`);
- `removeLast()` - возвращает и удаляет последний элемент из массива deque.

>**Примечание:** Если массив deque пуст, метод `remove()`, `removeFirst()` и `removeLast()` выдает исключение. Кроме того, `remove(element)` выдает исключение, если элемент не найден.

Например,
```java
import java.util.ArrayDeque;

class Main {
    public static void main(String[] args) {
        ArrayDeque<String> animals= new ArrayDeque<>();
        animals.add("Dog");
        animals.add("Cat");
        animals.add("Cow");
        animals.add("Horse");
        System.out.println("ArrayDeque: " + animals);

        // Using remove()
        String element = animals.remove();
        System.out.println("Removed Element: " + element);

        System.out.println("New ArrayDeque: " + animals);

        // Using removeFirst()
        String firstElement = animals.removeFirst();
        System.out.println("Removed First Element: " + firstElement);

        // Using removeLast()
        String lastElement = animals.removeLast();
        System.out.println("Removed Last Element: " + lastElement);
    }
}
```
**Вывод**
<p style="background-color: navy; color: yellow">
ArrayDeque: [Dog, Cat, Cow, Horse]<br>
Removed Element: Dog<br>
New ArrayDeque: [Cat, Cow, Horse]<br>
Removed First Element: Cat<br>
Removed Last Element: Horse</p>

**2. Удалите элементы с помощью методов poll(), pollFirst() и pollLast()**
- `poll()` - возвращает и удаляет первый элемент массива deque
- `pollFirst()` - возвращает и удаляет первый элемент массива deque (эквивалентно `poll()`)
- `pollLast()` - возвращает и удаляет последний элемент массива deque

>**Примечание:** Если массив deque пуст, `poll()`, `pollFirst()` и `pollLast()` возвращает `null`, если элемент не найден.

Например,
```java
import java.util.ArrayDeque;

class Main {
    public static void main(String[] args) {
        ArrayDeque<String> animals= new ArrayDeque<>();
        animals.add("Dog");
        animals.add("Cat");
        animals.add("Cow");
        animals.add("Horse");
        System.out.println("ArrayDeque: " + animals);

        // Using poll()
        String element = animals.poll();
        System.out.println("Removed Element: " + element);
        System.out.println("New ArrayDeque: " + animals);

        // Using pollFirst()
        String firstElement = animals.pollFirst();
        System.out.println("Removed First Element: " + firstElement);

        // Using pollLast()
        String lastElement = animals.pollLast();
        System.out.println("Removed Last Element: " + lastElement);
    }
}
```
**Вывод**
<p style="background-color: navy; color: yellow">
ArrayDeque: [Dog, Cat, Cow, Horse]<br>
Removed Element: Dog<br>
New ArrayDeque: [Cat, Cow, Horse]<br>
Removed First Element: Cat<br>
Removed Last Element: Horse</p>

**3. Удалить элемент: используя метод clear()**

Чтобы удалить все элементы из массива deque, мы используем метод `clear()`. Например,
```java
import java.util.ArrayDeque;

class Main {
    public static void main(String[] args) {
        ArrayDeque<String> animals= new ArrayDeque<>();
        animals.add("Dog");
        animals.add("Cat");
        animals.add("Horse");
        System.out.println("ArrayDeque: " + animals);

        // Using clear()
        animals.clear();

        System.out.println("New ArrayDeque: " + animals);
    }
}
```
**Вывод**
<p style="background-color: navy; color: yellow">
ArrayDeque: [Dog, Cat, Horse]<br>
New ArrayDeque: []</p>

#### Повторение ArrayDeque

- `iterator()` - возвращает [итератор](Iterator), который можно использовать для выполнения итерации по массиву deque
- `descendingIterator()` - возвращает итератор, который можно использовать для выполнения итерации по массиву deque в обратном порядке

Чтобы использовать эти методы, мы должны импортировать `java.util.Iterator` пакет. Например,
```java
import java.util.ArrayDeque;
import java.util.Iterator;

class Main {
    public static void main(String[] args) {
        ArrayDeque<String> animals= new ArrayDeque<>();
        animals.add("Dog");
        animals.add("Cat");
        animals.add("Horse");

        System.out.print("ArrayDeque: ");

        // Using iterator()
        Iterator<String> iterate = animals.iterator();
        while(iterate.hasNext()) {
            System.out.print(iterate.next());
            System.out.print(", ");
        }

        System.out.print("\nArrayDeque in reverse order: ");
        // Using descendingIterator()
        Iterator<String> desIterate = animals.descendingIterator();
        while(desIterate.hasNext()) {
            System.out.print(desIterate.next());
            System.out.print(", ");
        }
    }
}
```
**Вывод**
<p style="background-color: navy; color: yellow">
ArrayDeque: [Dog, Cat, Horse]<br>
ArrayDeque in reverse order: [Horse, Cat, Dog]</p>

### Другие методы

| Методы              | Описания                                                                                                                                    |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| `element()`         | Возвращает элемент из заголовка массива deque.                                                                                              |
| `contains(element)` | Выполняет поиск в массиве deque указанного элемента.  <br>  <br>Если элемент найден, он возвращает `true`, если нет, он возвращает `false`. |
| `size()`            | Возвращает длину массива deque.                                                                                                             |
| `toArray()`         | Преобразует array deque в array и возвращает его.                                                                                           |
| `clone()`           | Создает копию массива deque и возвращает ее.                                                                                                |

### ArrayDeque как стек

Для реализации **стеков LIFO (Last-In-First-Out)** в Java рекомендуется использовать deque вместо [классом Stack](https://www.programiz.com/java-programming/stack). Класс `ArrayDeque` будет быстрее, чем класс `Stack`.

`ArrayDeque` предоставляет следующие методы, которые могут быть использованы для реализации стека.
- `push()` - добавляет элемент в верхнюю часть стека
- `peek()` - returns an element from the top of the stack
- `pop()` - возвращает и удаляет элемент из верхней части стека

Например,
```java
import java.util.ArrayDeque;

class Main {
    public static void main(String[] args) {
        ArrayDeque<String> stack = new ArrayDeque<>();

        // Add elements to stack
        stack.push("Dog");
        stack.push("Cat");
        stack.push("Horse");
        System.out.println("Stack: " + stack);

        // Access element from top of stack
        String element = stack.peek();
        System.out.println("Accessed Element: " + element);

        // Remove elements from top of stack
        String remElement = stack.pop();
        System.out.println("Removed element: " + remElement);
    }
}
```
**Вывод**
<p style="background-color: navy; color: yellow">
Stack: [Horse, Cat, Dog]<br>
Accessed Element: Horse<br>
Removed Element: Horse</p>

---

## ArrayDeque и Класс LinkedList

Как `ArrayDeque`, так и [Java LinkedList](Class-LinkedList) реализует [Deque](Deque) интерфейс. Однако между ними существуют некоторые различия.
- [LinkedList](Class-LinkedList) поддерживает `null` элементы, тогда как `ArrayDeque` этого не делает.
- Каждый узел в связанном списке содержит ссылки на другие узлы. Вот почему [LinkedList](Class-LinkedList) требуется больше памяти, чем `ArrayDeque`.
- Если вы реализуете очередь или структуру данных deque, an, `ArrayDeque` вероятно, будет быстрее, чем a [LinkedList](Class-LinkedList) .