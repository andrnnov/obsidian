#Java #Tuple #replaceFirst 

## [Пары в Java](https://codegym.cc/groups/posts/pairs-in-java)

2024-10-21 14:52

В программировании бывают ситуации, когда нам нужно работать с парами значений, где каждому значению соответствует ключ. То есть пара — это контейнер для хранения [кортежа](Tuple) из двух объектов.

В языке программирования C++ в библиотеке служебных программ есть шаблонный класс std::pair. Он хранит два значения одного типа. Эти значения называются первым и вторым элементами пары. Пары можно использовать для представления различных типов данных, таких как координаты, точки, цвета и так далее. Они также широко используются в контейнерных библиотеках C++, таких как std::map и std::set. В базовой библиотеке Java Development Kit (JDK) нет встроенного класса Pair. Однако многие разработчики используют сторонние библиотеки или реализации классов Pair, предоставляемые различными фреймворками и библиотеками, для работы с парами значений в Java. Прежде всего, это такие библиотеки, как Apache Commons и Guava, которые предоставляют свои собственные реализации классов для работы с парами и кортежами значений. Кроме того, если вам нужен класс Pair, вы можете использовать одну из этих сторонних библиотек или создать свой собственный класс Pair в соответствии с вашими потребностями.

### Класс Pair в JavaFX

Pair в Java является частью пакета javafx.util и используется для представления пары значений, где одно значение связано с ключом (отношение «ключ-значение»). Хотя это не встроенный класс в стандартной библиотеке Java, он обеспечивает простой и понятный способ управления парами «ключ-значение». Класс Pair имеет два поля: ключ и значение, представляющие ключ и значение, связанные с парой соответственно. Это делает его удобным контейнером для хранения связанных данных.

#### Пример использования класса Pair

Вот пример использования класса Java Pair:
```java
import javafx.util.Pair;

public class PairExample {
    public static void main(String[] args) {
//key and value
        Pair<String, Integer> agePair = new Pair<>("Alice", 25);
        System.out.println("Name: " + agePair.getKey());//get key
        System.out.println("Age: " + agePair.getValue());
    }
}
```
**Вывод:**
<p style="background-color: navy; color: yellow">
Name: Alice<br>
Age: 25</p>
В этом примере мы создаём экземпляр Pair с именем agePair, содержащий имя (ключ) и возраст (значение). Затем мы извлекаем и выводим имя и возраст с помощью методов getKey() и getValue(). Давайте рассмотрим другой пример, в котором мы используем пары для представления и вывода названий стран вместе с соответствующими столицами:
```java
import javafx.util.Pair;

public class CountryCapitalExample {
    public static void main(String[] args) {
        Pair<String, String> countryCapitalPair = new Pair<>("France", "Paris");
        System.out.println("Country: " + countryCapitalPair.getKey());//get key
        System.out.println("Capital: " + countryCapitalPair.getValue());
    }
}
```
**Вывод:**
<p style="background-color: navy; color: yellow">
Country: France<br>
Capital: Paris</p>

### Пары в Apache Commons Java

Apache Commons Lang — это широко используемая библиотека, которая предоставляет богатый набор служебных классов для различных распространённых задач программирования на Java. Среди множества функций Apache Commons Lang есть класс Pair, который позволяет разработчикам удобно работать с парами значений. Это может быть особенно полезно, когда нужно вернуть два значения из метода или сохранить связанные данные вместе. Вот пример использования Pair в Apache Commons:
```java
import org.apache.commons.lang3.tuple.Pair;

public class PairExample {
    public static void main(String[] args) {
        // Creating a Pair of values
        Pair<String, Integer> nameAndAge = Pair.of("John", 30);

        // Accessing the values
        String name = nameAndAge.getLeft();
        int age = nameAndAge.getRight();

        // Printing the values
        System.out.println("Name: " + name);
        System.out.println("Age: " + age);
    }
}
```
**Вывод:**
<p style="background-color: navy; color: yellow">
Name: John<br>
Age: 30</p>

В этом примере мы импортируем класс Pair из Apache Commons Lang и создаём Pair из [String](String) (имени) и [Integer](WrapperInteger) (возраста). Затем мы можем легко получить доступ к этим значениям и управлять ими с помощью методов getLeft() и getRight(). Apache Commons Lang предоставляет удобный способ работы с парами значений, делая ваш код более читаемым и удобным для поддержки.

### Класс Pair в библиотеке Guava

В библиотеке Guava вы можете работать с парами, используя класс Pair, предоставляемый пакетом com.google.common.collect.Pair в Guava похож на Pair в Apache Commons Lang и позволяет представлять простую пару из двух значений. Вот пример использования Pair в Guava:
```java
import com.google.common.collect.*;

public class GuavaPairExample {
    public static void main(String[] args) {
        // Creating a Pair of values
        Pair<String, Integer> nameAndAge = Pair.of("John", 30);

        // Accessing the values
        String name = nameAndAge.getFirst();
        int age = nameAndAge.getSecond();

        // Printing the values
        System.out.println("Name: " + name);
        System.out.println("Age: " + age);
    }
}
```
**Вывод:**
<p style="background-color: navy; color: yellow">
Name: John<br>
Age: 30</p>

В этом примере мы создаём пару, состоящую из строки (имени) и целого числа (возраста), с помощью .of(). Затем мы получаем доступ к значениям с помощью методов getFirst() и getSecond().

В этой программе мы импортируем необходимые классы из Guava. Затем мы создаём пару с именем nameAndAge со значениями «Джон» и 30, извлекаем значения с помощью getFirst() и getSecond(). Наконец, мы выводим значения в консоль.Pair из Guava — это простой способ работы с парами значений, который делает ваш код более выразительным и читаемым, когда вам нужно работать с парами связанных данных.
