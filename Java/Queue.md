#Java #Collections #Queue

## Интерфейс Queue в Java

2024-04-05 10:53

Интерфейс Queue в Java Collection Framework предоставляет функциональность, характерную для очереди - структуры данных, работающей по принципу "первый пришел, первый обслужен" (FIFO). Интерфейс Queue расширяет [[Collections#Интерфейс Java Collection|Collection]].

### Операции с Queue

Рассмотрим основные методы, предоставляемые интерфейсом `Queue`:
- `boolean offer(E obj)` **—** Вставляет указанный элемент в эту очередь, если это возможно сделать немедленно, не нарушая ограничений очереди. В отличие от метода `add`, этот метод не выдает исключение, если добавить элемент не удается.
- `E peek()` — Возвращает, но не удаляет головной элемент этой очереди, или возвращает `null`, если этой очереди пуста.
- `E poll()` — Удаляет и возвращает головной элемент этой очереди, или возвращает `null`, если этой очереди пуста.
- `E remove()` — Удаляет и возвращает головной элемент этой очереди. Если очередь пуста, генерирует исключение `NoSuchElementException`.

Это основные методы, которые предоставляет интерфейс `Queue`, и которые могут быть использованы для выполнения операций над очередью, таких как добавление, удаление и просмотр элементов.

#### Метод add()

**add()** - добавляем элемент в конец очереди. (Поправка: если очередь с приоритетом - т.е. **PriorityQueue** - элемент ставится не обязательно в конец, а в соответствии со своим приоритетом):
```java
public class Test {
    public static void main(String[] args) {
        PriorityQueue<Integer> myPriorityQueue = new PriorityQueue<Integer>();
        myPriorityQueue.add(1);
        myPriorityQueue.add(2);
        myPriorityQueue.add(3);
        for(int pq : myPriorityQueue) {
            System.out.println(pq);
        }
    }
}
```
Тут мы добавили три **Integer**-а: 1, 2 и 3. Потом мы вывели нашу очередь в консоль - получили:
<p style="background-color: navy; color: yellow">
1<br>
2<br>
3</p>

#### Методы remove() и poll()

**remove()** и **poll()** - удаляем верхний элемент из очереди. 1. У метода **remove()** есть две формы - **remove()** и **remove(Object o)**, а у **poll()** - только одна. В первой форме оба метода одинаковые - они убирают "голову" (первый элемент) очереди. 

Например, тут мы используем метод **remove()**:
```java
public class Test {
    public static void main(String[] args) {
        PriorityQueue<Integer> myPriorityQueue = new PriorityQueue<Integer>();
 
        myPriorityQueue.add(1);
        myPriorityQueue.add(2);
        myPriorityQueue.add(3);
 
        for(int i: myPriorityQueue)
            System.out.println(i);
        myPriorityQueue.remove();
        System.out.println("After removing:");
        for(int i: myPriorityQueue)
            System.out.println(i);
    }
}
```
Получаем:
<p style="background-color: navy; color: yellow">
1<br>
2<br>
3<br>
After removing:<br>
2<br>
3</p>

Точно то же самое получим, если напишем вместо **remove()** **poll()**:
```java
public class Test {
    public static void main(String[] args) {
        PriorityQueue<Integer> myPriorityQueue = new PriorityQueue<Integer>();
 
        myPriorityQueue.add(1);
        myPriorityQueue.add(2);
        myPriorityQueue.add(3);
 
        for(int i: myPriorityQueue)
            System.out.println(i);
        myPriorityQueue.poll();
        System.out.println("After removing:");
        for(int i: myPriorityQueue)
            System.out.println(i);
    }
}
```
Получаем:
<p style="background-color: navy; color: yellow">
1<br>
2<br>
3<br>
After removing:<br>
2<br>
3</p>
Но **remove(Object o)** позволяет убирать любой элемент, не только сверху. Например, попробуем убрать двойку - она лежит в середине очереди:
```java
public class Test {
    public static void main(String[] args) {
        PriorityQueue<Integer> myPriorityQueue = new PriorityQueue<Integer>();
 
        myPriorityQueue.add(1);
        myPriorityQueue.add(2);
        myPriorityQueue.add(3);
 
        for(int i: myPriorityQueue)
            System.out.println(i);
        myPriorityQueue.remove(2);
        System.out.println("After removing:");
        for(int i: myPriorityQueue)
            System.out.println(i);
    }
}
```
Получаем:
<p style="background-color: navy; color: yellow">
1<br>
2<br>
3<br>
After removing:<br>
1<br>
3</p>

Методы будут действовать по-разному если у нас пустая очередь. Например:
```java
public class Test {
    public static void main(String[] args) {
        PriorityQueue<Integer> myPriorityQueue = new PriorityQueue<Integer>();
        myPriorityQueue.remove();
    }
}
```
Получаем:
![[Exception_Queue.png]]
Если **poll()** - ничего не произойдет:
```java
public class Test {
    public static void main(String[] args) {
        PriorityQueue<Integer> myPriorityQueue = new PriorityQueue<Integer>();
        myPriorityQueue.poll();
    }
}
```
Получим:
<p style="background-color: navy; color: yellow">
Process finished with exit code 0</p>

#### Метод offer()

**offer()** - пытается вставить в конец очереди. С английского "offer" переводится как "предложить". Почему "предлагаем"? Потому что в очередях с фиксированным размером у нас может не получится вставить элемент в очередь. Давайте попробуем его использовать:
```java
public class Test {
    public static void main(String[] args) {
        PriorityQueue<Integer> myPriorityQueue = new PriorityQueue<Integer>();
 
        myPriorityQueue.add(1);
        myPriorityQueue.add(2);
        myPriorityQueue.add(3);
        myPriorityQueue.offer(22);
 
        for(int i: myPriorityQueue)
            System.out.println(i);
    }
}
```
Получим:
<p style="background-color: navy; color: yellow">
1<br>
2<br>
3<br>
22</p>

#### Методы peek() и element()

**peek()** (от англ. "подсматривать"), и **element()** - показывают верхний элемент очереди. Например:
```java
public class Test {
    public static void main(String[] args) {
        PriorityQueue<Integer> myPriorityQueue = new PriorityQueue<Integer>();
 
        myPriorityQueue.add(1);
        myPriorityQueue.add(2);
        myPriorityQueue.add(3);
 
        System.out.println(myPriorityQueue.peek());
    }
}
```
Получим:
<p style="background-color: navy; color: yellow">
1</p>
Все верно, мы получили первый элемент - единицу.

Или, давайте попробуем применить **element()**:
```java
public class Test {
    public static void main(String[] args) {
        PriorityQueue<Integer> myPriorityQueue = new PriorityQueue<Integer>();
 
        myPriorityQueue.add(1);
        myPriorityQueue.add(2);
        myPriorityQueue.add(3);
 
        System.out.println(myPriorityQueue.element());
    }
}
```
Получаем то же самое - единицу:
<p style="background-color: navy; color: yellow">
1</p>
