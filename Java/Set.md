#Java #Collections #Set

#### [Java Set](https://www.jenkov.com/tutorials/java-collections/set.html) ####

2023-10-30 17:42

Интерфейс Java Set, java.util.Set, представляет собой коллекцию объектов, где каждый объект в наборе Java уникален. Другими словами, один и тот же объект не может встречаться более одного раза в наборе Java. Интерфейс Java Set - это стандартный интерфейс Java, и он является подтипом интерфейса Java [Collection](Collections), что означает, что Set наследуется от Collection.

Вы можете добавить любой объект Java в набор Java. Если набор не типизирован, используя Java Generics, то вы даже можете смешивать объекты разных типов (классов) в одном наборе. Однако на самом деле смешивание объектов разных типов в одном наборе не часто выполняется.

Интерфейсы `Set` и [List](https://www.jenkov.com/tutorials/java-collections/list.html ) очень похожи друг на друга. Оба интерфейса представляют собой набор элементов. Однако есть некоторые существенные различия. Эти различия отражены в методах, содержащихся в интерфейсах "Set" и "List".

Первое различие между интерфейсом Java Set и List заключается в том, что один и тот же элемент не может встречаться более одного раза в Set Java. Это отличается от List Java, где каждый элемент может встречаться более одного раза.

Второе различие между интерфейсами Java Set и Java List заключается в том, что элементы в Set не имеют гарантированного внутреннего порядка. Элементы в List имеют внутренний порядок, и элементы могут повторяться в этом порядке. 
#### Пример Java Set ####

Сначала приведем простой пример Java Set, который даст вам представление о том, как работают множество:
```java
package com.jenkov.collections;

import java.util.HashSet;

public class SetExample {

    public static void main(String[] args) {

        Set setA = new HashSet();

        setA.add(element);

        System.out.println( setA.contains(element) );
    }
}
```
В этом примере создается HashSet, который является одним из классов в Java API, реализующих интерфейс Set. Затем он добавляет объект string к множеству и, наконец, проверяет, содержит ли множество только что добавленный элемент.
#### Установленные реализации ####

Будучи подтипом Collection, все методы в интерфейсе Collection также доступны в интерфейсе Set.

Поскольку Set - это интерфейс, вам нужно создать экземпляр конкретной реализации интерфейса, чтобы использовать его. Вы можете выбрать одну из следующих реализаций множества в Java Collections API:
- java.util.EnumSet
- java.util.HashSet
- java.util.LinkedHashSet
- java.util.TreeSet

Каждая из этих реализаций множеств ведет себя немного по-разному в отношении порядка элементов при итерации множества и времени, необходимого для вставки элементов в множество и доступа к ним.

HashSet поддерживается HashMap. Это не дает никаких гарантий относительно последовательности элементов при их повторении.

LinkedHashSet отличается от HashSet тем, что гарантирует, что порядок элементов во время итерации совпадает с порядком, в котором они были вставлены в LinkedHashSet. Повторная вставка элемента, который уже находится в LinkedHashSet, не изменяет этот порядок.

TreeSet также гарантирует порядок элементов при итерации, но порядок - это порядок сортировки элементов. Другими словами, порядок, в котором элементы были бы отсортированы, если бы вы использовали Collections.sort() в списке или массиве, содержащем эти элементы. Этот порядок определяется либо их естественным порядком (если они реализуют Comparable), либо конкретной реализацией компаратора.
#### Создание множества Set ####

Вот несколько примеров того, как создать экземпляр Set:
```java
package com.jenkov.collections;

import java.util.HashSet;
import java.util.LinkedHashSet;
import java.util.Set;
import java.util.TreeSet;

public class SetExample {

    public static void main(String[] args) {

        Set setA = new HashSet();
        Set setB = new LinkedHashSet();
        Set setC = new TreeSet();

    }
}
```
#### Generic Sets ####

По умолчанию вы можете поместить любой объект в множество, но начиная с Java 5, Java Generics позволяет ограничить типы объектов, которые вы можете вставить в множество Set. Вот пример:
```java
Set<MyObject> set = new HashSet<MyObject>();
```
Теперь в это множество могут быть вставлены только экземпляры MyObject. Затем вы можете получить доступ к его элементам и выполнять их итерацию, не приводя их в действие. Вот как это выглядит:
```java
for(MyObject anObject : set){
   //do someting to anObject...
}
```
Считается хорошей практикой всегда указывать общий тип для Java-набора, когда вы его знаете. В большинстве примеров в этом руководстве используются универсальные типы.
#### Set.of() ####

Начиная с Java 9 интерфейс Set содержит набор статических фабричных методов, которые могут создавать неизменяемые экземпляры Set.

Статические фабричные методы Java Set вызываются of() и принимают либо ноль, либо больше параметров. Вот первый пример создания пустого неизменяемого множества с помощью Set.of() :
```java
Set set = Set.of();
```
В этом примере создается неизменяемое множество без указания общего типа.

Спецификация типа возвращаемого множества Set выглядит следующим образом:
```java
Set<String> set3 = Set.<String>of();
```
Вы также можете создавать неизменяемые экземпляры множества, которые содержат элементы по вашему выбору. Вы передаете эти элементы методу of(). Вот пример того, как выглядит создание множества, содержащего элементы, с использованием метода Set.of():
```java
Set<String> set3 = Set.<String>of("val1", "val2", "val3");
```
#### Добавление элементов в множество Set ####

Чтобы добавить элементы в множество Set, вы вызываете его метод add(). Этот метод унаследован от интерфейса Collection. Вот несколько примеров:
```java
Set<String> setA = new HashSet<>();

setA.add("element 1");
setA.add("element 2");
setA.add("element 3");
```
Три вызова add() добавляют экземпляры String в набор.
#### Итерация Set элементов ####

Существует два способа перебора элементов множества Set Java:
- Используя итератор, полученный из множества Set. 
- Используя цикл for-each.

При итерации элементов в множестве порядок расположения элементов зависит от того, какую реализацию множества вы используете, как упоминалось ранее.
#### Выполнить итерацию множества с помощью итератора ####

Чтобы выполнить итерацию элементов множества с помощью Java-итератора, вы должны сначала получить итератор из множества. Вы получаете итератор из множества, вызывая метод iterator(). Вот пример получения итератора из множества:
```java
Set<String> setA = new HashSet<>();

setA.add("element 1");
setA.add("element 2");
setA.add("element 3");

Iterator<String> iterator = set.iterator();

while(iterator.hasNext(){
  String element = iterator.next();
}
```
#### Итерация множества с использованием цикла For-Each ####

Второй способ перебора элементов множества - это использование цикла for-each. Вот как выглядит итерация элементов множества с использованием цикла for-each:
```java
Set set = new HashSet();

for(Object object : set) {
    String element = (String) object;
}
```
Интерфейс Set реализует интерфейс Interable Java. Вот почему вы можете перебирать элементы набора, используя цикл for-each. Если в наборе указан общий тип, вы можете использовать этот тип в качестве типа переменной внутри цикла for-each. Вот как это выглядит:
```java
Set<String> set = new HashSet<>();

for(String str : set) {
    System.out.println(str);
}
```
Это предпочтительный способ использования цикла for-each - в сочетании с универсальным типом, указанным для коллекции, в которой используется цикл for-each.
#### Итерация множества с использованием Java Stream API ####

Третий способ итерации Java-множества - через Java Stream API. Чтобы выполнить итерацию множества Java с помощью Java Stream API, вы должны создать поток из множества. Вот пример создания потока Java из множества и итерации множества:
```java
Set<String> set = new HashSet<>();

set.add("one");
set.add("two");
set.add("three");

Stream<String> stream = set.stream();

stream.forEach((element) ->   
        { System.out.println(element); });
```
#### Удаление элементов из множества Set  ####

Вы удаляете элементы из множества Java, вызывая метод remove(Object o). Вот пример удаления элемента из набора Java:
```java
set.remove("object-to-remove");
```
Невозможно удалить объект на основе индекса в множестве, поскольку порядок элементов зависит от реализации множества.
#### Удаление всех элементов множества Set ####

Вы можете удалить все элементы из множества, используя метод clear(). Вот пример удаления всех элементов:
```java
set.clear();
```
#### Добавьте все элементы из Другой Коллекции ####

Интерфейс Java List имеет метод, называемый addAll(), который добавляет все элементы из другой коллекции (списка или множестваа) в множество. В теории множеств это соответствует объединению множества и другой коллекции. Вот пример добавления всех элементов из другого множества:
```java
Set<String> set = new HashSet<>();
set.add("one");
set.add("two");
set.add("three");

Set<String> set2 = new HashSet<>();
set2.add("four");

set2.addAll(set);
```
После выполнения этого примера множество set2 будет содержать строковый элемент four, а также три строковых элемента one, two и three из set.
#### Удаление всех элементов из другой коллекции ####

Метод removeAll() удаляет все элементы в множества, которые также присутствуют в другой коллекции. В теории множеств это называется разницей между множеством и другой коллекцией. Вот пример удаления всех элементов из множества, которые также присутствуют в другой коллекции:
```java
Set<String> set = new HashSet<>();
set.add("one");
set.add("two");
set.add("three");

Set set2 = new HashSet();
set2.add("three");

set.removeAll(set2);
```
После запуска этого примера множество будет содержать строковые элементы one и two. Элемент three был удален, поскольку он присутствовал в set2, который был задан в качестве параметра для set.removeAll(set2) .
#### Сохранить все элементы, присутствующие в другой коллекции ####

Интерфейс Java Set также имеет метод, который сохраняет все элементы в множестве, которые также присутствуют в другой коллекции. Все элементы, найденные в множестве, которых нет в другой коллекции, будут удалены. В теории множеств это называется пересечением между множеством и другой коллекцией. Вот пример сохранения всех элементов в множестве Java, которые также присутствуют в другом множестве:
```java
Set<String> set = new HashSet<>();
set.add("one");
set.add("two");
set.add("three");

Set<String> set2 = new HashSet<>();
set2.add("three");
set2.add("four");

set.retainAll(set2);
```
После запуска этого Java-кода множество будет содержать только строковый элемент three. Это единственный элемент, который присутствует как в set, так и в set2.
#### Set Size ####

Вы можете проверить размер множества Java, используя метод size(). Размер множества - это количество элементов, содержащихся в множестве. Вот пример считывания размера множества:
```java
Set<String> set = new HashSet<>();

set.add("123");
set.add("456");
set.add("789");

int size = set.size();
```
После выполнения этого Java-кода переменная `size` будет иметь значение 3, потому что в `Set`, созданный в примере, было добавлено 3 элемента.
#### Проверьте, пусто ли значение множества Set ####

Вы можете проверить, является ли множество пустым, что означает, что он не содержит элементов, вызвав метод isEmpty() для набора. Вот пример проверки того, является ли множество пустым:
```java
Set<String> set = new HashSet<>();

boolean isEmpty = set.isEmpty();
```
После запуска этого Java-кода переменная isEmpty будет содержать значение true, поскольку множество пусто (в нем нет элементов). 
Вы также можете проверить, является ли множество пустым, сравнив значение, возвращаемое методом size(), с 0. Вот пример, который показывает, как:
```java
Set<String> set = new HashSet<>();

boolean isEmpty = (set.size() == 0);
```
После запуска этого Java-кода переменная isEmpty будет содержать значение true, потому что метод Set size() возвращает 0 - потому что Set в примере не содержит элементов.
#### Проверьте, содержит ли Set элемент ####

Вы можете проверить, содержит ли множество данный элемент (объект), вызвав метод contains(). Вот пример проверки того, содержит ли множество заданный элемент:
```java
Set<String> set = new HashSet<>();

set.add("123");
set.add("456");

boolean contains123 = set.contains("123");
```
После запуска этого Java-кода переменная contains123 будет содержать значение true, потому что множество фактически содержит строку 123. 

Чтобы определить, содержит ли множество элемент, множество будет внутренне перебирать свои элементы и сравнивать каждый элемент с объектом, переданным в качестве параметра. При сравнении используется метод Java equals элемента, чтобы проверить, равен ли элемент параметру. Поскольку к множеству можно добавлять нулевые значения, также можно проверить, содержит ли множество нулевое значение. Вот как вы проверяете, содержит ли множество нулевое значение:
```java
set.add(null);

containsElement = set.contains(null);

System.out.println(containsElement);
```
Очевидно, что если входной параметр contains() равен null, метод contains() не будет использовать метод equals() для сравнения с каждым элементом, а скорее будет использовать оператор `==`.
#### Convert Java Set to List ####

Вы можете преобразовать множество Set в List, создав список и вызвав его метод addAll(), передав множество в качестве параметра методу addAll(). Вот пример преобразования Set в List:
```java
Set<String> set = new HashSet<>();
set.add("123");
set.add("456");

List<String> list = new ArrayList<>();
list.addAll(set);
```
После запуска этого примера Java список будет содержать строковые элементы 123 и 456 - поскольку это были все элементы, присутствующие в множестве при вызове List addAll(set).