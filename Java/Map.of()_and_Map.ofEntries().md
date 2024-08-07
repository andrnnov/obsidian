#Java #Map 

### [Методы Map.of() и Map.ofEntries() в Java](https://www.techiedelight.com/immutable-map-java/)

2024-07-24 12:22

Java 9 сделала создание экземпляров [Map](Map) очень удобным, предоставив статические фабричные методы в [Map](Map) интерфейсе, который создает компактный, неизменяемый экземпляр [Map](Map). Например, `Map.of()` метод позволяет нам создавать неизменяемую карту, содержащую до `10` пар ключ-значение. Синтаксис таков:
```java
Map.of() // creates an empty map  
Map.of(k1, v1) // creates a singleton map  
Map.of(k1, v1, k2, v2)  
Map.of(k1, v1, k2, v2, k3, v3)  
…  
Map.of(k1, v1, k2, v2, k3, v3, …, k10, v10)
```
Здесь, k это тип ключей и v это тип значений. Результирующая карта будет неизменяемой картой, что означает, что мы не можем изменять ее путем добавления, удаления или обновления ее элементов. Если мы попытаемся это сделать, мы получим UnsupportedOperationException. Например, чтобы создать неизменяемую карту стран и континентов, мы можем написать:
```java
import java.util.Map;
 
class Main
{
    public static void main(String[] args) {
        Map<String, String> immutableMap = Map.of("India", "Asia", 
		        "France", "Europe", "Brazil", "South America");
        // {Brazil=South America, India=Asia, France=Europe}
        System.out.println(immutableMap);
		// updating any key will result in java.lang.UnsupportedOperationException
        try {
            immutableMap.put("Germany", "Europe");
        } catch (UnsupportedOperationException ex) {
            System.out.println("Cannot modify an immutable map");
        }
 
    }
}
```

### Использование `Map.ofEntries()` метода

Существует перегрузка без переменных `Map.of()`, которая может обрабатывать любое количество сопоставлений. Чтобы создать неизменяемую карту с произвольным количеством записей, мы можем использовать `Map.ofEntries()` метод с `Map.Entry` объектами в качестве аргументов. Он включает в себя перегрузки [varargs](varargs), поэтому фиксированного ограничения на размер карты нет. Этот метод требует, чтобы каждая пара ключ-значение была вставлена в рамку. Мы можем использовать `Map.entry()` метод для создания `Map.Entry` объекта из ключа и значения. Вот синтаксис:
```java
Map.ofEntries(  
  entry(k1, v1),  
  entry(k2, v2),  
  entry(k3, v3),  
  // …  
  entry(kn, vn)  
);
```
Как и раньше, результирующая карта будет неизменяемой картой, что означает, что мы получим UnsupportedOperationException, если попытаемся ее изменить. Например, чтобы создать неизменяемую карту фруктов и их цветов, мы можем написать:
```java
import java.util.Map;
 
class Main
{
    public static void main(String[] args) {
        Map<String, String> immutableMap = Map.ofEntries(
                Map.entry("Strawberry", "Red"),
                Map.entry("Blueberry", "Blue"),
                Map.entry("Papaya", "Green")
        );
        // {Blueberry=Blue, Papaya=Green, Strawberry=Red}
        System.out.println(immutableMap);
    }
}
```
Основное различие между Map.of() и Map.ofEntries() методами заключается в том, что Map.of() принимает фиксированное количество пар ключ-значение в качестве аргументов, в то время как Map.ofEntries() принимает переменное количество Map.Entry объектов в качестве аргументов. Оба этих метода возвращают экземпляр [Map](Map) интерфейса, а не конкретный класс реализации. Следовательно, мы не должны делать никаких предположений относительно идентичности или производительности возвращаемых карт.

### Характеристики `Map.of()` и `Map.ofEntries()` методов

Экземпляры map, созданные методами `Map.of()` и `Map.ofEntries()` , обладают следующими характеристиками:
1. Они структурно неизменяемы. Ключи и значения нельзя добавлять, удалять или обновлять. Любая попытка сделать это приведет к `UnsupportedOperationException`. Однако, если содержащиеся ключи или значения изменяемы, это может привести к непоследовательному поведению карты или к изменению ее содержимого.
2. Они не допускают `null` ключей или значений. Любая попытка использовать `null` ключ или значение приведет к появлению `NullPointerException`.
3. Они сериализуемы, если все ключи и значения [сериализуемы](Serializable).
4. Если мы передадим дубликаты ключей статическому фабричному методу, они не будут приняты при создании карты. Вместо этого будет выдан `IllegalArgumentException`.
5. Они имеют неопределенный порядок итераций сопоставлений, который может меняться в разных реализациях или вызовах.
6. Возвращаемые экземпляры основаны на их значениях, а не на идентификаторах. Вызывающим не следует ожидать, что каждый раз будет возвращаться один и тот же экземпляр. [Фабрики](Factory) могут либо создавать новые экземпляры, либо использовать существующие. Таким образом, операции, которые зависят от идентификатора экземпляров (такие как равенство ссылок (`==`), получение их идентификационного хэш-кода или их синхронизация), не заслуживают доверия и не должны использоваться.
7. Они оптимизированы с точки зрения производительности и использования памяти в зависимости от количества и типа пар ключ-значение.

### Создайте изменяемую (mutable) копию

Чтобы создать изменяемую карту (mutable map) из неизменяемой карты, мы можем использовать конструктор или метод копирования конкретной реализации карты, такой как [HashMap](HashMap) или [LinkedHashMap](LinkedHashMap). Например:
```java
import java.util.HashMap;
import java.util.Map;
 
class Main { 
    public static void main(String[] args) {
        Map<String, String> map = new HashMap<>(Map.of("India", "Asia", 
		        "France", "Europe"));
        map.put("Brazil", "South America");
        // {France=Europe, Brazil=South America, India=Asia}
        System.out.println(map);
    }
}
```
Также обратите внимание, что статические фабричные методы для конкретных классов коллекций, такие как [HashMap](HashMap), не включены в Java 9. Поскольку статические методы в интерфейсах не наследуются, вызвать их через реализующий класс или экземпляр типа интерфейса будет невозможно.