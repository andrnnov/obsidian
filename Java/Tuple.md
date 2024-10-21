#Java #Tuple

## [Кортеж](https://codegym.cc/groups/posts/java-tuple)

2024-10-17 15:21

Кортежи — это фундаментальные структуры данных, которые встречаются во многих языках программирования. В этой статье мы рассмотрим, что такое кортежи, их различные варианты использования и то, как их можно реализовать в Java. Мы также обсудим отсутствие кортежей в основных библиотеках Java и представим пользовательский класс Tuple для практического применения.

### Что такое кортежи?

Кортеж — это упорядоченная совокупность элементов, которые могут быть разных типов данных. В отличие от массивов или списков, кортежи могут хранить разнородный набор значений, что делает их универсальными структурами данных. Доступ к элементам в кортеже обычно осуществляется по их позиции или индексу, а не по ключу, в отличие от словарей или карт.

### Примеры использования кортежей

- Несколько возвращаемых значений: кортежи часто используются для возврата нескольких значений из функции или метода в ситуациях, когда создание пользовательского класса или структуры было бы излишним.
- Группировка данных: кортежи могут группировать связанные данные, для которых не требуется определения нового класса. Например, хранение координат широты и долготы.
- Преобразование данных: кортежи можно использовать в конвейерах преобразования данных для представления промежуточных результатов.

### Класс кортежей в ядре Java?

В некоторых языках изначально есть структура данных «кортежи». Например, в Python, Haskell, Ruby, Rust, Kotlin и Go есть встроенные типы данных для кортежей. В Java нет встроенного класса или библиотеки «кортежи», но можно использовать массивы или коллекции для имитации кортежей, хотя это не так элегантно, как использование специальных классов «кортежи» или библиотек. В Java нет встроенных кортежей по нескольким причинам:

- Изначально Java была ориентирована на объекты, а не на примитивные типы данных. Кортежи можно считать разновидностью объектов, но у них есть некоторые отличия, например, они неизменяемы.
- В Java уже есть другие структуры данных, которые можно использовать для хранения нескольких значений, например списки и массивы.

Однако в Java есть возможность использовать библиотеки для реализации кортежей. Например, библиотека Google Guava предоставляет класс Tuple, который реализует неизменяемые кортежи. В последние годы наблюдается тенденция к использованию кортежей в Java. В Java 12 были добавлены новые операторы для работы с кортежами, а в Java 17 — новые методы для доступа к элементам кортежа. Это может указывать на то, что в будущем в Java могут быть добавлены встроенные кортежи.

### Внешние библиотеки для кортежей

Чтобы эффективно использовать кортежи в Java, разработчики часто обращаются к внешним библиотекам, таким как:

- Apache Commons Lang: Java Apache Commons Pairs — это библиотека, предоставляющая множество вспомогательных классов для работы с парами объектов. Она включает как изменяемые, так и неизменяемые пары, а также пары, которые могут хранить объекты разных типов.
- [javatuples](javatuples): библиотека, предназначенная для работы с кортежами и содержащая широкий спектр типов кортежей. JavaTuples — это мощная библиотека, предоставляющая разработчикам Java широкий спектр типов кортежей. JavaTuples упрощает работу с кортежами, предлагая предопределённые классы для кортежей различной арности (количества компонентов). JavaTuples упрощает создание кортежей, работу с ними и сопоставление шаблонов, что делает его отличным выбором для работы с кортежами в проектах на Java.

### Создание пользовательского класса кортежей

Для наглядности давайте создадим простой класс Tuple на Java и будем использовать его для хранения и извлечения значений:
```java
//custom javatuples class example
public class CustomTuple<A, B> {
   private A first;
   private B second;
//constructor of javatuples class
   public CustomTuple(A first, B second) {
       this.first = first;
       this.second = second;
   }

   public A getFirst() {
       return first;
   }

   public void setFirst(A first) {
       this.first = first;
   }

   public B getSecond() {
       return second;
   }

   public void setSecond(B second) {
       this.second = second;
   }

   @Override
   public String toString() {
       return "(" + first + ", " + second + ")";
   }
}
```
В этом примере мы создали класс CustomTuple, который принимает два параметра универсального типа A и B. У него есть методы получения и установки для доступа к элементам кортежа и их изменения. Метод toString() переопределён для предоставления строкового представления кортежа. Вот пример использования класса CustomTuple:
```java
public class CustomTupleExample {
   public static void main(String[] args) {
       // Create a custom tuple of String and Integer
       CustomTuple<String, Integer> customTuple = new CustomTuple<>("Hello", 42);

       // Access elements of the javatuples
       String first = customTuple.getFirst();
       Integer second = customTuple.getSecond();

       // Print the tuple
       System.out.println("Tuple: " + customTuple);

       // Modify the elements of the tuple
       customTuple.setFirst("World");
       customTuple.setSecond(99);

       // Print the modified tuple
       System.out.println("Modified Tuple: " + customTuple);
   }
}
```
Выходные данные этой программы находятся здесь:
<p style="background-color: navy; color: yellow">
Tuple: (Hello, 42) <br>
Modified Tuple: (World, 99)</p>

Давайте рассмотрим еще один пример использования пользовательского класса tuple.
```java
public class CustomTupleExample {
        public static void main(String[] args) {
            // Create a list of custom tuples to represent people's names and ages
            CustomTuple<String, Integer> person1 = new CustomTuple<>("Johnny", 11);
            CustomTuple<String, Integer> person2 = new CustomTuple<>("Ivy", 13);
            CustomTuple<String, Integer> person3 = new CustomTuple<>("Rick", 12);

            // Print the information for each person
            System.out.println("Person 1: " + person1);
            System.out.println("Person 2: " + person2);
            System.out.println("Person 3: " + person3);

            // Update the age of Person 1
            person1.setSecond(12);

            // Print the updated information for Person 2
            System.out.println("Updated Person 2: " + person2);
        }
}
```

В этом примере мы создаем список пользовательских кортежей, каждый из которых представляет имя пользователя (строка) и возраст (целое число). Затем мы печатаем информацию для каждого пользователя и обновляем возраст одного из них. Это демонстрирует, как пользовательский класс Tuple может использоваться для хранения пар данных и манипулирования ими. Выходные данные этой программы находятся здесь:
<p style="background-color: navy; color: yellow">
Person 1: (Johnny, 11)<br>
Person 2: (Ivy, 13)<br>
Person 3: (Rick, 12)<br>
Updated Person 2: (Ivy, 12)</p>

Конечно, мы можем реализовать триплеты и любую другую подобную структуру данных.
```java
public class Triplet<A, B, C> {
    private final A first;
    private final B second;
    private final C third;

    public Triplet(A first, B second, C third) {
        this.first = first;
        this.second = second;
        this.third = third;
    }

    public A getFirst() {
        return first;
    }

    public B getSecond() {
        return second;
    }

    public C getThird() {
        return third;
    }

    @Override
    public String toString() {
        return "(" + first + ", " + second + ", " + third + ")";
    }
}
```

### Еще один пример: преобразование кортежа в массив

Давайте изменим наш класс CustomTuple, добавив в него один простой метод для преобразования кортежа в массив объектов. Вот наш метод:
```java
//custom javatuples class example
public class CustomTuple<A, B> {
   private A first;
   private B second;
//constructor of javatuples class
   public CustomTuple(A first, B second) {
       this.first = first;
       this.second = second;
   }

   public A getFirst() {
       return first;
   }

   public void setFirst(A first) {
       this.first = first;
   }

   public B getSecond() {
       return second;
   }

   public void setSecond(B second) {
       this.second = second;
   }

   @Override
   public String toString() {
       return "(" + first + ", " + second + ")";
   }

   public Object[] toArray() {
       return new Object[]{first, second};
   }
}
```
Вот пример использования этого метода:
```java
import java.util.Arrays;
public class CustomTupleExample {
        public static void main(String[] args) {
            // Create a list of custom tuples to represent people's names and ages
            CustomTuple<String, Integer> tuple = new CustomTuple<>("Johnny", 11);

            // Convert the tuple to an array
            Object[] array = tuple.toArray();

            // Print the array
            System.out.println(Arrays.toString(array));
        }
}
```
Результатом является:
<p style="background-color: navy; color: yellow">
[Johnny, 11]</p>

### Заключение

В этой статье мы рассмотрели, что такое кортежи, обсудили различные варианты их использования и подчеркнули, что они отсутствуют в базовой версии Java. Мы представили внешние библиотеки для работы с кортежами и продемонстрировали, как создать и использовать пользовательский класс Tuple в Java. Кортежи — это удобный способ работы с упорядоченными наборами разнородных данных, заполняющий нишу, которую не полностью заполняют встроенные в Java структуры данных.


