#Java #Enumeration
### Интерфейс Enumeration

2024-01-18 14:10

**Интерфейс Enumeration** – определяет методы, с помощью которых вы можете перечислить (получить по одному) элементы в коллекции объектов.

Этот устаревший интерфейс был заменён [Iterator](Iterator). Хоть и не совсем, но Enumeration в Java считается устаревшим для нового кода. Однако он используется некоторыми методами, определёнными такими устаревшими классами, как [Vector](Vector) и [Properties](Properties), используется другими API классами и сейчас широко используется в коде приложений.
```java
public interface Enumeration<E> {
    boolean hasMoreElements();
    E nextElement();
}
```

#### Методы

Методы, объявленные Enumeration, приведены в следующей таблице:

| № | Метод и описание |
| ---- | ---- |
| 1 | **boolean hasMoreElements()**  <br>Когда реализован, он обязан вернуть true, пока всё ещё существуют элементы для извлечения, и false, когда все элементы были перечислены. |
| 2 | **Object nextElement()**  <br>Возвращает следующий объект в перечислении как общую ссылку [Object](Object). |

#### Пример 1

Следующий пример показывает использование Enumeration в Java.

```java
import java.util.Vector;
import java.util.Enumeration;

public class EnumerationTester {
   public static void main(String args[]) {
      Enumeration days;
      Vector dayNames = new Vector();
      
      dayNames.add("Воскресенье");
      dayNames.add("Понедельник");
      dayNames.add("Вторник");
      dayNames.add("Среда");
      dayNames.add("Четверг");
      dayNames.add("Пятница");
      dayNames.add("Суббота");
      days = dayNames.elements();
      
      while (days.hasMoreElements()) {
         System.out.println(days.nextElement()); 
      }
   }
}
```
Получим следующее:
<p style="background-color: navy; color: yellow">
Воскресенье<br>
Понедельник<br>
Вторник<br>
Среда<br>
Четверг<br>
Пятница<br>
Суббота</p>
#### Пример 2

Обратите внимание, что интерфейс Enumeration не имеет никаких методов для удаления или изменения элементов из коллекции. Это интерфейс только для чтения, который позволяет только просматривать коллекцию. Давайте посмотрим пример использования интерфейса Enumeration:
```java
import java.util.Arrays;
import java.util.Enumeration;
import java.util.Vector;
 
class Main {
    public static void main(String[] args) {
        // Create a Vector object
        Vector<String> names = new Vector<>(Arrays.asList("Aaron", "Bella", "Casey"));
        // Get an Enumeration object for the vector
        Enumeration<String> enumeration = names.elements();
        // Iterate over the vector using the enumeration
        while (enumeration.hasMoreElements()) {
            System.out.println(enumeration.nextElement());
        }
    }
}
```
Вывод:
<p style="background-color: navy; color: yellow">
Aaron<br>
Bella<br>
Casey</p>
#### Различие между `Enumeration` и [`Iterator`](Iterator) в Java

Функциональные возможности Enumeration и [Iterator](Iterator) схожи. Они оба позволяют нам последовательно обращаться к элементам коллекции, не зная ее базовой структуры. Однако у них также есть некоторые различия и компромиссы, которые мы должны понимать:
- Интерфейс Enumeration может использоваться только с устаревшими классами, такими как Vector или Hashtable, в то время как интерфейс [Iterator](Iterator) может использоваться с любым классом collection, таким как [List](List), [Set](Set), [Map](Map) и т.д. [Iterator](Iterator) официально занял место Enumeration в Java [Collections Framework](Collections). 
- Интерфейс Enumeration имеет только два метода: hasMoreElements() и nextElement(), в то время как интерфейс [Iterator](Iterator) имеет три метода: hasNext(), next() и remove(). 
- Интерфейс Enumeration не имеет никакого метода для удаления или изменения элементов из коллекции, в то время как интерфейс [Iterator](Iterator) имеет метод для удаления элементов из коллекции. 
- Интерфейс Enumeration - это интерфейс только для чтения, который допускает только обход коллекции, в то время как интерфейс [Iterator](Iterator) - это интерфейс чтения-записи, который допускает как обход, так и модификацию коллекции. 
- Enumeration по своей природе отказоустойчиво, в то время как [Iterator](Iterator) по своей природе быстродействующий. 
- Enumeration в Java перемещается только в прямом направлении. Существует еще один специальный тип итератора, называемый [[Iterator#ListIterator|ListIterator]], который облегчает двунаправленный доступ.
- [Iterator](Iterator) имеет более короткие имена методов – hasMore() и next(), в отличие от hasMoreElements() и nextElement() интерфейса Enumeration.