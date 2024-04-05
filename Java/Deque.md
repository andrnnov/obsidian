#Java #Collections #Deque

## Интерфейс Deque

2024-04-05 11:54

Интерфейс Deque (Double Ended Queue) в Java Collection Framework представляет двустороннюю очередь, где добавление, удаление и поиск элементов могут происходить с обоих концов. Интерфейс Deque расширяет [Queue](Queue).

То есть мы можем добавить элемент не только в начала, но и в конец. И соответственно удалить элемент не только из конца, но и из начала.

Рассмотрим основные методы, предоставляемые интерфейсом `Deque`:
- `void addFirst(E obj)` **—** вставляет указанный элемент в начало очереди.
- `void addLast(E obj)` **—** вставляет указанный элемент в конец очереди.
- `E getFirst()` **—** возвращает, но не удаляет, первый элемент из очереди. Если очередь пуста, генерирует исключение `NoSuchElementException`
- `E getLast()` **—** возвращает, но не удаляет, последний элемент из очереди. Если очередь пуста, генерирует исключение `NoSuchElementException`
- `boolean offerFirst(E obj)` **—** добавляет элемент `obj` в самое начало очереди. Если элемент удачно добавлен, возвращает `true`, иначе - `false`
- `boolean offerLast(E obj)` **—** добавляет элемент `obj` в конец очереди. Если элемент удачно добавлен, возвращает `true`, иначе - `false`
- `E peekFirst()` **—** возвращает без удаления элемент из начала очереди. Если очередь пуста, возвращает значение `null`
- `E peekLast()` **—** возвращает без удаления последний элемент очереди. Если очередь пуста, возвращает значение `null`
- `E pollFirst()` **—** возвращает с удалением элемент из начала очереди. Если очередь пуста, возвращает значение `null`
- `E pollLast()` **—** возвращает с удалением последний элемент очереди. Если очередь пуста, возвращает значение `null`
- `E pop()` **—** возвращает с удалением элемент из начала очереди. Если очередь пуста, генерирует исключение `NoSuchElementException`
- `void push(E element)` **—** добавляет элемент в самое начало очереди
- `E removeFirst()` **—** Удаляет и возвращает первый элемент из очереди. Если очередь пуста, генерирует исключение `NoSuchElementException`
- `E removeLast()` **—** Удаляет и возвращает последний элемент из очереди. Если очередь пуста, генерирует исключение `NoSuchElementException`
- `boolean removeFirstOccurrence(Object obj)` **—** удаляет первый встреченный элемент `obj` из очереди. Если удаление произошло, то возвращает `true`, иначе возвращает false.
- `boolean removeLastOccurrence(Object obj)` **—** удаляет последний встреченный элемент `obj` из очереди. Если удаление произошло, то возвращает `true`, иначе возвращает false.

Это основные методы, которые предоставляет интерфейс Deque, и которые могут быть использованы для выполнения операций над двусторонней очередью, таких как добавление, удаление и просмотр элементов с обоих концов.

Данный интерфейс реализован в классах [LinkedList](Class-LinkedList), ArrayDeque и многопоточном классе LinkedBlockingDeque.

Класс [LinkedList](LinkedList) является наиболее используемым при работе с двусторонними очередями. Он не имеет ограничений на количество элементов и реализует быстродействующие методы добавления и удаления элементов с обоих концов. Класс ArrayDeque является другой реализацией не имеющей ограничения на число элементов. В нем реализована обертка для работы с индексами, обеспечивающая высокую производительность. Как и все реализации коллекций, данные реализации также не являются защищенными от многопоточного доступа. (Исторически такие коллекции как Vector и Hashtable являются защищенными от многопоточного доступа, но они не ориентированы на высокую производительность). Если вам нужна безопасная работа с потоками, используйте класс LinkedBlockingDeque. Класс LinkedBlockingDeque реализует интерфейс BlockingDeque наследуемый от интерфейса Deque. Данным класс может иметь ограничение на количество элементов. Если ограничение не задано, то оно равно значению Integer.MAX_VALUE.

Так как концептуально двусторонняя очередь является привязанной с двух сторон, то вы можете проводить поиск элементов в любом порядке. Используйте метод iterator() для поиска элементов с начала до конца и метод descendingIterator() для поиска элементов в обратном направлении с конца до начала. Однако вы не можете получить доступ к элементу по его местоположению, по крайней мере данный механизм не включен в интерфейс Deque. Однако класс [LinkedList](LinledList), реализующий интерфейс Deque, позволяет получить доступ в произвольному элементу через интерфейс [List](List), который он также реализует. Без выполнения требования по произвольному доступу, реализация интерфейса Deque, может быть выполнена более эффективно.

Для чего использовать двусторонние очереди? Двусторонние очереди предоставляют удобные структуры данных для использования в рекурсивных процедурах, как, например работа с лабиринтами и разбор исходных данных. Когда вы разбираете исходную часть, вы сохраняете правильные варианты, добавляя с одной стороны. Если вариант оказывается не верным вы удаляете его, возвращаясь к последнему верному элементу. В данном варианте вы работаете только с одним концом, как в стеке. Как только вы достигли конца, вам необходимо вернуться в начало для получения решения, которое начинается с последнего элемента. Другим типичным примером является планировщик заданий в операционной системе.

**Пример реализации Deque в классе ArrayDeque:**
```java
import java.util.Deque;
import java.util.ArrayDeque;

class Main {

    public static void main(String[] args) {
        // Creating Deque using the ArrayDeque class
        Deque<Integer> numbers = new ArrayDeque<>();

        // add elements to the Deque
        numbers.offer(1);
        numbers.offerLast(2);
        numbers.offerFirst(3);
        System.out.println("Deque: " + numbers);

        // Access elements of the Deque
        int firstElement = numbers.peekFirst();
        System.out.println("First Element: " + firstElement);

        int lastElement = numbers.peekLast();
        System.out.println("Last Element: " + lastElement);

        // Remove elements from the Deque
        int removedNumber1 = numbers.pollFirst();
        System.out.println("Removed First Element: " + removedNumber1);

        int removedNumber2 = numbers.pollLast();
        System.out.println("Removed Last Element: " + removedNumber2);

        System.out.println("Updated Deque: " + numbers);
    }
}
```
Вывод:
<p style="background-color: navy; color: yellow">
Deque: [3, 1, 2]<br>
First Element: 3<br>
Last Element: 2<br>
Removed First Element: 3<br>
Removed Last Element: 2<br>
Updated Deque: [1]</p>

**Пример программы Blocked**, демонстрирует использование интерфейса Deque, а вернее класса LinkedBlockingDeque с установленными границами очереди. Конечно, это не лучший пример использования двусторонней очереди, но он позволяет показать применение API и события, возникающие при достижении предела очереди. Данная программа получает 23 названия месяцев (полные и сокращенные) и по одному добавляет их в начало очереди, поддерживающей шесть элементов. Другой поток удаляет элементы из начала и конца двусторонней очереди, основываясь на количестве элементов, находящихся в коллекции.
```java
import java.io.*;
import java.util.*;
import java.util.concurrent.*;

public class Blocked {
  public static void main(String args[]) {
    Calendar now = Calendar.getInstance();
    Locale locale = Locale.getDefault();
    final Console console = System.console();
    final Map names = now.getDisplayNames(Calendar.MONTH,
        Calendar.ALL_STYLES, locale);
    console.printf("Starting names: %s%n", names);
    final Deque deque = new LinkedBlockingDeque(6);
    // Добавление элемента в начало
    new Thread() {
      public void run() {
        Set keys = names.keySet();
        Iterator itor = keys.iterator();
        String element = null;
        while (itor.hasNext() || element != null) {
          if (element == null) {
            element = itor.next();
            console.printf("MapGot: %s%n", element);
          }
          console.printf("Offering: %s%n", element);
          if (deque.offerFirst(element)) {
            console.printf("MapRemoving: %s%n", element);
            itor.remove();
            element = null;
          } else {
            try {
              Thread.sleep(250);
            } catch (InterruptedException ignored) {
            }
          }
        }
        try {
          Thread.sleep(3500);
        } catch (InterruptedException ignored) {
        }
        System.exit(0);
      }
    }.start();
    while (true) {
      if ((deque.size() % 2 == 1)) {
        // удаление из начала
        console.printf("Remove head: %s%n", deque.pollFirst());
      } else {
        // удаление из конца
        console.printf("Remove tail: %s%n", deque.pollLast());
      }
      // пауза между циклами
      try {
        Thread.sleep(500);
      } catch (InterruptedException ignored) {
      }
    }
  }
}
```
Как показано ниже, при выполнении программы, выводится множество строк. Это происходит из-за частого использования оператора printf(). Строка выводится на экран каждый раз, когда элемент получается из источника, удаляется из источника, добавляется в двустороннюю очередь или удаляется из нее. Обратите внимание на случай, когда добавление происходит в полную двустороннюю очередь.
<p style="background-color: navy; color: yellow">
   Starting names: {Jun=5, March=2, December=11, April=3, <br>
   November=10, September=8, October=9, Sep=8, Aug=7, Apr=3, <br>
   May=4, June=5, Feb=1, Dec=11, Oct=9, Jan=0, Mar=2, Jul=6, <br>
   August=7, January=0, February=1, July=6, Nov=10}<br>
   Remove tail: null<br>
   MapGot: Jun<br>
   Offering: Jun<br>
   MapRemoving: Jun<br>
   MapGot: March<br>
   Offering: March<br>
   MapRemoving: March<br>
   ...<br>
   Remove tail: Jul<br>
   Remove head: Nov<br>
   Remove tail: August<br>
   Remove head: July<br>
   Remove tail: January<br>
   Remove head: February<br>
   Remove tail: null</p>
Следует отметить две вещи. Первое, используется только 23 элемента (а не 24) для представления полных и сокращенных названий месяцев, тат как "May" используется для обоих представлений. Метод getDisplayNames() возвращает таблицу, таким образом значение "May" не может быть ключом для двух полей, полного и сокращенного. Второе, если единственное, что вам необходимо - это добавление элементов с одного конца и извлечение их с другого используйте реализацию интерфейса [Queue](Queue), вместо Deque.
