#Java #Functional-Interface
### Функциональные интерфейсы в Java ###

2023-12-14 16:47

В восьмой версии Java появилось понятие функциональные интерфейсы. Что же это? Функциональным считается интерфейс с одним не реализованным (абстрактным) методом. Под это определение попадают многие интерфейсы с “коробки”, такие, как, например, рассмотренный ранее интерфейс [Comparator](Comparator). А еще — интерфейсы, которые мы создаём сами, как, например:
```java
@FunctionalInterface
public interface Converter<T, N> {
   N convert(T t);
}
```
У нас получился интерфейс, задача которого — преобразовывать объекты одного типа в объекты другого (такой себе адаптер). 

Аннотация `@FunctionalInterface` не является чем-то сверхсложным и важным, так как её предназначение — сообщить компилятору, что данный интерфейс функциональный и должен содержать не более одного метода. 

Если же в интерфейсе с данной аннотацией более одного не реализованного (абстрактного) метода, компилятор не пропустит данный интерфейс, так как будет воспринимать его как ошибочный код.

Интерфейсы и без данной аннотации могут считаться функциональными и будут работать, а `@FunctionalInterface` является не более чем дополнительной страховкой. Вернёмся же к классу [Comparator](Comparator). Если заглянуть в его код (или [документацию](https://docs.oracle.com/javase/8/docs/api/java/util/Comparator.html)), можно увидеть, что у него есть гораздо больше одного метода. Тогда вы спросите: как же в таком случае он может считаться функциональным интерфейсом? 

Абстрактные интерфейсы могут иметь методы, которые не входят в ограничения одного метода:
- статические

Концепция интерфейсов подразумевает, что данная единица кода не может иметь реализованных методов. Но начиная с Java 8 появилась возможность использовать статические и дефолтные методы в интерфейсах. 

[Статические методы](Static) привязаны непосредственно к классу, и для вызова такого метода не нужен конкретный объект данного класса. То есть данные методы гармонично вписываются в представления об интерфейсах. В качестве примера добавим в предыдущий класс статический метод проверки объекта на null:
```java
@FunctionalInterface
public interface Converter<T, N> {
   N convert(T t);

   static <T> boolean isNotNull(T t){
       return t != null;
   }
}
```
Получив этот метод, компилятор не стал ругаться, а значит наш интерфейс все еще функциональный.
#### default методы ####

До появления Java 8, если бы нам было нужно создать в интерфейсе какой-то метод, который наследуется другими классами, мы могли бы создать только абстрактный метод, реализуемый в каждом конкретном классе. Но а что если этот метод будет одинаковым у всех классов? В таком случае чаще всего использовали [абстрактные классы](https://javarush.com/quests/lectures/questsyntaxpro.level17.lecture05).

Но начиная с Java 8 есть опция использовать интерфейсы с реализованными методами — методами по умолчанию. При наследовании интерфейса можно переопределить эти методы или же оставить всё как есть (оставить логику по умолчанию). При создании метода по умолчанию мы должны добавить ключевое слово — `default`:
```java
@FunctionalInterface
public interface Converter<T, N> {
   N convert(T t);

   static <T> boolean isNotNull(T t){
       return t != null;
   }

   default void writeToConsole(T t) {
       System.out.println("Текущий объект - " + t.toString());
   }
}
```
Опять же мы видим, что компилятор не начал ругаться, и мы не вышли за ограничения функционального интерфейса.

#### методы класса Object ####

Все классы наследуются от класса `Object`. Это не касается интерфейсов. Но если у нас в интерфейсе будет абстрактный метод, совпадающий сигнатурой с каким-то методом класса `Object`, такой метод (или методы) не поломает наше ограничение функционального интерфейса:
```java
@FunctionalInterface
public interface Converter<T, N> {
   N convert(T t);

   static <T> boolean isNotNull(T t){
       return t != null;
   }

   default void writeToConsole(T t) {
       System.out.println("Текущий объект - " + t.toString());
   }

   boolean equals(Object obj);
}
```
И снова компилятор у нас не ругается, поэтому интерфейс `Converter` всё ещё считается функциональным. 

Теперь вопрос: а зачем же нам ограничение одним не реализованным методом в функциональном интерфейсе? А затем, чтобы мы могли его реализовать с помощью лямбд. 
Давайте рассмотрим это на примере `Converter`.

Для этого создадим класс `Dog`:
```java
public class Dog {
  String name;
  int age;
  int weight;

  public Dog(final String name, final int age, final int weight) {
     this.name = name;
     this.age = age;
     this.weight = weight;
  }
}
```
И аналогичный ему `Raccoon` (енот):
```java
public class Raccoon {
  String name;
  int age;
  int weight;

  public Raccoon(final String name, final int age, final int weight) {
     this.name = name;
     this.age = age;
     this.weight = weight;
  }
}
```
Предположим, у нас есть объект `Dog`, и нам нужно на основе его полей создать объект `Raccoon`. То есть `Converter` конвертирует объект одного типа в другой. Как это будет выглядеть:
```java
public static void main(String[] args) {
  Dog dog = new Dog("Bobbie", 5, 3);

  Converter<Dog, Raccoon> converter = x -> new Raccoon(x.name, x.age, x.weight);

  Raccoon raccoon = converter.convert(dog);

  System.out.println("Raccoon has parameters: name - " + raccoon.name + ", age - " + raccoon.age + ", weight - " + raccoon.weight);
}
```
Запустив, мы получим вывод в консоль:
<p style="background-color: navy; color: yellow">Raccoon has parameters: name - Bobbbie, age - 5, weight - 3</p>
И это значит, что наш метод отработал корректно.

### Базовые функциональные интерфейсы Java 8 ###

Ну а теперь рассмотрим несколько функциональных интерфейсов, которые принесла нам Java 8 и которые активно используются в связке со Stream API.
#### Predicate ####

`Predicate` — функциональный интерфейс для проверки соблюдения некоторого условия. Если условие соблюдается, возвращает `true`, иначе — `false`:
```java
@FunctionalInterface
public interface Predicate<T> {
   boolean test(T t);
}
```
В качестве примера рассмотрим создание `Predicate`, который будет проверять на чётность числа типа `Integer`:
```java
public static void main(String[] args) {
   Predicate<Integer> isEvenNumber = x -> x % 2==0;

   System.out.println(isEvenNumber.test(4));
   System.out.println(isEvenNumber.test(3));
}
```
Вывод в консоль:
<p style="background-color: navy; color: yellow">true<br>
false</p>
#### Consumer ####

`Consumer` (с англ. — “потребитель”) — функциональный интерфейс, который принимает в качестве входного аргумента объект типа T, совершает некоторые действия, но при этом ничего не возвращает:
```java
@FunctionalInterface
public interface Consumer<T> {
   void accept(T t);
}
```
В качестве примера рассмотрим `Consumer`, задача которого — выводить в консоль приветствие с переданным строковым аргументом:
```java
public static void main(String[] args) {
   Consumer<String> greetings = x -> System.out.println("Hello " + x + " !!!");
   greetings.accept("Elena");
}
```
Вывод в консоль:
<p style="background-color: navy; color: yellow">Hello Elena !!!</p>
#### Supplier ####

`Supplier` (с англ. — поставщик) — функциональный интерфейс, который не принимает никаких аргументов, но возвращает некоторый объект типа T:
```java
@FunctionalInterface
public interface Supplier<T> {
   T get();
}
```
В качестве примера рассмотрим `Supplier`, который будет выдавать рандомные имена из списка:
```java
public static void main(String[] args) {
   ArrayList<String> nameList = new ArrayList<>();
   nameList .add("Elena");
   nameList .add("John");
   nameList .add("Alex");
   nameList .add("Jim");
   nameList .add("Sara");

   Supplier<String> randomName = () -> {
       int value = (int)(Math.random() * nameList.size());
       return nameList.get(value);
	};

   System.out.println(randomName.get());
}
```
И если мы это запустим, то увидим в консоли случайные результаты из списка имен.
#### Function ####

`Function` — этот функциональный интерфейс принимает аргумент T и приводит его к объекту типа R, который и возвращается как результат:
```java
@FunctionalInterface
public interface Function<T, R> {
   R apply(T t);
}
```
В качестве примера возьмём `Function`, который конвертирует числа из формата строк (`String`) в формат чисел (`Integer`):
```java
public static void main(String[] args) {
   Function<String, Integer> valueConverter = x -> Integer.valueOf(x);
   System.out.println(valueConverter.apply("678"));
}
```
Запустив, получим вывод в консоль:
<p style="background-color: navy; color: yellow">678</p>
P.S.: если в строку мы передадим не только числа, но и другие символы, вылетит [exception](https://javarush.com/quests/lectures/questsyntaxpro.level14.lecture01) — `NumberFormatException`.
#### UnaryOperator ####

`UnaryOperator` — функциональный интерфейс, принимает в качестве параметра объект типа T, выполняет над ним некоторые операции и возвращает результат операций в виде объекта того же типа T:
```java
@FunctionalInterface
public interface UnaryOperator<T> {
   T apply(T t);
}
```
`UnaryOperator`, который своим методом `apply` возводит число в квадрат:
```java
public static void main(String[] args) {
   UnaryOperator<Integer> squareValue = x -> x * x;
   System.out.println(squareValue.apply(9));
}
```
Вывод в консоль:
<p style="background-color: navy; color: yellow">81</p>
Мы рассмотрели пять функциональных интерфейсов. Это не все, что доступно нам начиная с Java 8 — это основные интерфейсы. Остальные из доступных — это их усложненные аналоги. Полный список можно посмотреть [в официальной документации Oracle](https://docs.oracle.com/javase/8/docs/api/java/util/function/package-summary.html).

