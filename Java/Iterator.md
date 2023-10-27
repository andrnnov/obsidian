#java #Iterator #Collections
#### [Java Iterator](https://www.jenkov.com/tutorials/java-collections/iterator.html) ####

2023-10-27 12:39

Интерфейс Java Iterator представляет собой объект, способный выполнять итерацию по коллекции объектов Java, по одному объекту за раз. Интерфейс Iterator является одним из старейших механизмов в Java для итерации коллекций [Collections](Collections) объектов (хотя и не самым старым - Enumerator предшествовал итератору).
Чтобы использовать Iterator, вам нужно будет получить экземпляр итератора из коллекции объектов, по которым вы хотите выполнить итерацию. Полученный итератор отслеживает элементы в базовой коллекции, чтобы убедиться, что вы выполняете итерацию по всем из них. Если вы изменяете базовую коллекцию во время итерации через итератор, указывающий на эту коллекцию, итератор обычно обнаруживает это и генерирует исключение при следующей попытке получить следующий элемент из итератора.
#### Основные методы Итератора ####

Интерфейс  Iterator достаточно прост. Основными методами интерфейса итератора являются:

|Method|Description|
|:--|:--|
|hasNext()|Returns `true` if the Iterator has more elements, and `false` if not.|
|next()|Return the next element from the Iterator|
|remove()|Removes the latest element returned from next() from the Collection the Iterator is iterating over.|
|forEachRemaining()|Iterates over all remaining elements in the Iterator and calls a [Java Lambda Expression](https://www.jenkov.com/java/lambda-expressions.html) passing each remaining element as parameter to the lambda expression.|
#### Получение итератора ####

Чаще всего именно так вы будете взаимодействовать с итератором, получая его из какого-либо объекта Java, содержащего несколько вложенных объектов. Стандартная коллекция интерфейса Collection содержит метод, называемый iterator(). Вызвав iterator(), вы можете получить итератор из данной коллекции.
Вы также можете получить Iterator из многих структур данных Collection, например, List, Set, Map, Queue, Deque .
Вот несколько примеров получения итератора Java из различных типов коллекций Java:
```java
List<String> list = new ArrayList<>();
list.add("one");
list.add("two");
list.add("three");

Iterator<String> iterator = list.iterator();

Set<String> set = new HashSet<>();
set.add("one");
set.add("two");
set.add("three");

Iterator<String> iterator2 = set.iterator();
```
#### Итерация итератора ####

Вы выполняете итерацию объектов в итераторе, используя цикл while. Вот пример итерации элементов итератора Java с использованием цикла while:
```java
Iterator iterator = list.iterator();

while(iterator.hasNext()) {
    Object nextObject = iterator.next();
}
```
В приведенном выше примере Java следует обратить внимание на два метода. Первый метод - это метод Iterator hasNext(), который возвращает значение true, если итератор содержит больше элементов. Другими словами, если итератор еще не выполнил итерацию по всем элементам коллекции, из которой был получен итератор, метод hasNext() вернет значение true. Если итератор выполнил итерацию по всем элементам в базовой коллекции - метод hasNext() возвращает значение false.
Второй метод, на который следует обратить внимание, - это метод next(). Метод next() возвращает следующий элемент коллекции, по которому выполняется итерация итератора.
#### Порядок итерации ####

Порядок прохождения элементов, содержащихся в итераторе Java, зависит от объекта, который предоставляет итератор. Например, итератор, полученный из List, будет выполнять итерацию по элементам этого списка в том же порядке, в котором элементы хранятся внутри списка. С другой стороны, итератор, полученный из множества Set, не дает никаких гарантий относительно точной последовательности, в которой повторяются элементы в наборе Set.
#### Java List Iterator ####

Вот пример получения итератора из экземпляра списка List:
```java
List list = new ArrayList();

list.add("123");
list.add("456");
list.add("789");

Iterator iterator = list.iterator();
```
#### Java Set Iterator ####

Вот пример получения итератора из экземпляра множества Set: 
```java
Set set = new HashSet();

set.add("123");
set.add("456");
set.add("789");

Iterator iterator = set.iterator();
```
#### Модификация во время итерации ####

Некоторые коллекции не позволяют вам изменять коллекцию во время ее выполнения с помощью итератора. В этом случае вы получите ConcurrentModificationException при следующем вызове метода Iterator next(). Следующий пример приводит к исключению ConcurrentModificationException при выполнении:
```java
List<String> list = new ArrayList<>();

list.add("123");
list.add("456");
list.add("789");

Iterator<String> iterator = list.iterator();

while(iterator.hasNext()) {
    String value = iterator.next();

    if(value.equals("456")){
        list.add("999");
    }
}
```
Исключение ConcurrentModificationException генерируется из-за того, что итератор выходит из синхронизации с коллекцией, если вы изменяете коллекцию во время ее итерации с помощью итератора.
#### Удаление элементов во время итерации ####

Интерфейс Java Iterator имеет метод remove(), который позволяет вам удалить элемент, только что возвращенный next() из базовой коллекции. Вызов remove() не приводит к возникновению исключения ConcurrentModificationException. Вот пример удаления элемента из коллекции во время итерации его итератора:
```java
List<String> list = new ArrayList<>();

list.add("123");
list.add("456");
list.add("789");

Iterator<String> iterator = list.iterator();

while(iterator.hasNext()) {
    String value = iterator.next();

    if(value.equals("456")){
        iterator.remove();
    }
}
```
#### forEachRemaining() ####

Метод итератора forEachRemaining() может выполнять внутреннюю итерацию по всем элементам, оставшимся в итераторе, и для каждого элемента вызывать лямбда-выражение Java, передаваемое в качестве параметра forEachRemaining() . Вот пример использования метода Java Iterator forEachRemaining():
```java
List<String> list = new ArrayList<>();
list.add("Jane");
list.add("Heidi");
list.add("Hannah");

Iterator<String> iterator = list.iterator();
        
iterator.forEachRemaining((element) -> {
    System.out.println(element);
});
```
#### ListIterator ####

Java также содержит интерфейс под названием ListIterator, который расширяет интерфейс Iterator. Интерфейс Java ListIterator, который представляет собой двунаправленный итератор, то есть итератор, в котором вы можете перемещаться по элементам как вперед, так и назад.
```java
List<String> list = new ArrayList<>();
list.add("Jane");
list.add("Heidi");
list.add("Hannah");

ListIterator<String> listIterator = list.listIterator();
        
while(listIterator.hasNext()) {
    System.out.println(listIterator.next());
}
        
while(listIterator.hasPrevious()) {
    System.out.println(listIterator.previous());
}
```
Как вы можете видеть, в примере сначала выполняется итерация ListIterator вперед по всем элементам, а затем снова назад по всем элементам обратно к первому элементу.
#### Реализуем интерфейс итератора в собственном классе ####

Если у вас есть специальный, созданный на заказ тип коллекции, вы можете самостоятельно реализовать интерфейс Java Iterator, чтобы создать итератор, который может выполнять итерацию по элементам вашей пользовательской коллекции. В этом разделе я покажу вам супер простую пользовательскую реализацию интерфейса Java Iterator, которая даст вам представление о том, как выглядит реализация интерфейса Iterator самостоятельно.
Коллекция, для которой я буду реализовывать итератор, представляет собой стандартный список Java List. Это не будет полностью идеальной реализацией, поскольку она не сможет обнаруживать изменения в содержимом списка во время итерации, но этого достаточно, чтобы дать вам представление о том, как могла бы выглядеть реализация итератора. Вот он:
```java
import java.util.Iterator;
import java.util.List;

public class ListIterator <T> implements Iterator<T> {

    private List<T> source = null;
    private int index = 0;

    public ListIterator(List<T> source){
        this.source = source;
    }

    @Override
    public boolean hasNext() {
        return this.index < this.source.size();
    }

    @Override
    public T next() {
        return this.source.get(this.index++);
    }
}
```
Вот пример того, как это выглядит во время итерации приведенного выше ListIterator:
```java
import java.util.ArrayList;
import java.util.List;

public class ListIteratorExample {

    public static void main(String[] args) {
        List<String> list = new ArrayList();

        list.add("one");
        list.add("two");
        list.add("three");

        ListIterator<String> iterator = new ListIterator<>(list);
        while(iterator.hasNext()) {
            System.out.println( iterator.next() );
        }
    }
}
```
