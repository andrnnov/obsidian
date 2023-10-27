#Java #Iterable #Collections 
#### [Java Iterable](https://www.jenkov.com/tutorials/java-collections/iterable.html) ####

Интерфейс Iterable представляет собой набор объектов, который является итерабельным. Это означает, что класс, реализующий итерационный интерфейс Java, может выполнять итерацию своих элементов. Вы можете выполнять итерацию объектов Java Iterable тремя способами: путем получения итератора Java из Iterable или путем вызова метода Java Iterable forEach(). 
#### Выполните итерацию с помощью цикла for-each ####

Первый способ - это использование цикла Java for-each. Ниже приведен пример, показывающий, как выполнить итерацию элементов списка Java с помощью цикла for-each. Поскольку интерфейс Java List расширяет интерфейс Collection, а интерфейс Collection расширяет интерфейс Iterable, объект List может использоваться с циклом for-each.
```java
List<String> list = new ArrayList<>();

list.add("one");
list.add("two");
list.add("three");

for( String element : list ){
    System.out.println( element.toString() );
}
```
В этом примере сначала создается новый список и добавляются к нему 3 элемента. Затем он использует цикл for-each для перебора элементов списка и выводит значение toString() каждого элемента.
#### Итерация объекта с помощью итератора ####

Второй способ, которым вы можете выполнить итерацию элементов Java Iterable, - это получить из него Java-итератор, вызвав метод Iterable iterator(). Затем вы можете выполнить итерацию по этому итератору так же, как и с любым другим итератором.  Вот пример итерации элементов Java Iterable:
```java
List<String> list = new ArrayList<>();

list.add("one");
list.add("two");
list.add("three");

Iterator<String> iterator = list.iterator();

while(iterator.hasNext()) {
    String element = iterator.next();
    System.out.println( element );
}
```
#### Итерацию Iterable с помощью его метода forEach() ####

Третий способ перебора элементов Java Iterable - это использование его метода forEach(). Метод forEach() принимает лямбда-выражение Java в качестве параметра. Это лямбда-выражение вызывается один раз для каждого элемента в Iterable. Вот пример итерации элементов Iterable с помощью его метода forEach():
```java
List<String> list = new ArrayList<>();

list.add("one");
list.add("two");
list.add("three");

list.forEach( (element) -> {
    System.out.println( element );
});
```
#### Интерфейс Iterable ####

Iterable интерфейс Java имеет три метода, из которых необходимо реализовать только один. Два других имеют реализации по умолчанию. Вот определение итерационного интерфейса:
```java
public interface Iterable<T> {
  Iterator<T>    iterator();
  Spliterator<T> spliterator();
  void forEach(Consumer<? super T> action);
}
```
Метод, который вы должны реализовать, называется iterator(). Этот метод должен возвращать Java-итератор, который можно использовать для итерации элементов объекта, реализующего итерационный интерфейс. Получение итератора происходит за кулисами, поэтому вы не видите, как это делается. Компилятор Java позаботится о генерации кода для этого, когда вы используете Iterable с циклом for-each.
#### Реализации Iterable в Java ####

Интерфейс Iterable (java.lang.Iterable) - один из корневых интерфейсов Java [Collections](Collections) API. Таким образом, в Java существует несколько классов, реализующих итерационный интерфейс Java. Таким образом, эти классы могут выполнять итерацию своих внутренних элементов.
Существует также несколько Java-интерфейсов, которые расширяют итерационный интерфейс. Классы, реализующие интерфейс, который расширяет итерационный интерфейс, таким образом, также реализуют итерационный интерфейс. Такие классы также могут иметь итерацию своих элементов.
Интерфейс Collection расширяет Iterable, поэтому все подтипы Collection также реализуют Iterable интерфейс. Например, как интерфейсы Java List, так и Set расширяют интерфейс Collection и, следовательно, также итерационный интерфейс.
#### Реализация Interable ####

Простой пример реализации Interable:
```java
public class Persons implements Iterable {
    private List<Person> persons = new ArrayList<Person>();    
    
    public Iterator<Person> iterator() {
        return this.persons.iterator();
    }
}
```
Экземпляр Persons может быть использован с циклом Java for-each следующим образом:
```java
Persons persons = ... //obtain Persons instance with Person objects inside.

for(Person person : persons) {
    // do something with person object.
}
```
#### Получение Spliterator (разделителя) ####

Вы можете получить Java Spliterator из Java Iterable с помощью его метода spliterator(). Я не буду здесь вдаваться в интерфейс Spliterator - просто покажу, как получить Spliterator из итерационного:
```java
List<String> list = new ArrayList<>();

list.add("one");
list.add("two");
list.add("three");

Spliterator<String> spliterator = list.spliterator();
```
#### Производительность Iterable ####

Если вы пишете какой-то код, которому необходимо многократно выполнять итерацию коллекции в замкнутом цикле, скажем, выполнять итерацию списка Java тысячи раз в секунду, итерация списка с помощью цикла Java for-each медленнее, чем итерация списка с помощью стандартного цикла for, как показано здесь:
```java
for(int i=0; i<list.size(); i++) {
    Object obj = list.get(i);
}
```
Причина, по которой цикл for-each выполняется медленнее, заключается в том, что каждая итерация будет вызывать метод List iterator(), который создаст новый объект Iterator. Создание нового объекта тысячи, возможно, даже миллионы раз в секунду приводит к небольшому снижению производительности по сравнению с простым повторением списка с использованием стандартного цикла for.
Для большинства стандартных бизнес-приложений, где коллекции периодически повторяются, эта разница в производительности не имеет значения. Это имеет значение только для очень плотных циклов, которые выполняются тысячи раз в секунду.