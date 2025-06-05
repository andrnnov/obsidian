#Java #String 
### [Методы класса String, появившиеся в Java 11](https://topjava.ru/blog/java-11-string-api-additions)

2024-01-25 15:07

В Java 11 добавили несколько полезных методов в классе **[String](String)**.

#### repeat()

Как следует из названия, метод **repeat()** повторяет **n** раз (где **n** передается в качестве параметра) содержимое строки, а затем возвращает сконкатенированный результат:
```java
public class StringRepeat {

    public static void main(String[] args) {
        String strRepeat = "Knock ".repeat(2);

        System.out.println(strRepeat); // "Knock Knock "
        System.out.println(strRepeat.equals("Knock Knock ")); // true
    }
}
```
Если в качестве аргумента передать отрицательное число, например -1, то будет выброшено исключение **java.lang.IllegalArgumentException: count is negative: -1**  

Помимо этого, **repeat()** возвращает пустую строку, если значение исходной строки, которую нужно повторить, так же является пустой строкой или число повторений равно нулю.

Однако, в версиях до Java 11 этого метода не существует. Вместо этого можно использовать класс `StringUtils` из Apache Commons Lang, который предоставляет метод `repeat()`.
```java
import org.apache.commons.lang3.StringUtils;
 
String str = "abc";
String repeated = StringUtils.repeat(str, 3); // "abcabcabc"
```
Класс `StringUtils` не входит в стандартную библиотеку Java, поэтому его нужно добавить в проект. Он предоставляет множество других полезных методов для работы со строками, что может быть полезно при разработке.

#### strip()

Метод **strip()** возвращает строку со всеми удаленными начальными и конечными пробелами:
```java
public class StringStrip {

    public static void main(String[] args) {
        String strStrip = "\u2006  java \n \t".strip();

        System.out.println(strStrip); // "java"
        System.out.println(strStrip.equals("java")); // true
    }
}
```
В Java 11 также были добавлены методы **stripLeading()** и **stripTrailing()**, которые обрабатывают начальные и конечные пробелы соответственно.

#### Различия между strip() и trim()

**strip()** определяет, является ли символ пробелом или нет, основываясь на **Character.isWhitespace()**. Другими словами, он знает о разных пробельных символах Unicode. Это отличает его от [[String#Обрезка строки с помощью trim()|trim()]], который определяет пробел, как любой символ, который меньше или равен пробелу из Unicode (U+0020).  

Давайте применим **trim()** к предыдущему примеру. Результат будет другим:
```java
public class StringTrim {

    public static void main(String[] args) {
        String strTrim = "\u2006  java \n \t".trim();

        System.out.println(strTrim); // "   java"
        System.out.println(strTrim.equals("java")); // false
    }
}
```
Обратите внимание, как **trim()** обрезал начальные пробелы, но не смог убрать конечные. Это связано с тем, что **trim()** не знает о пробельных символах Unicode, которые имеют код больше U+0020.

#### isBlank()

Метод экземпляра **isBlank()** возвращает **true**, если строка пуста или содержит только пробелы, иначе — **false**:
```java
public class StringIsBlank {

    public static void main(String[] args) {
        String strIsBlank = "\u2006   \n \t";
        String strEmpty = "";

        System.out.println(strIsBlank.isBlank()); // true
        System.out.println(strEmpty.isBlank());   // true
    }
}
```
Метод **isBlank()** распознает пробельные символы Unicode, как и **strip()**.

#### lines()

Метод **lines()** возвращает **[Stream](StreamAPI)** строк, извлеченных из исходной строки, разделенных ограничителями:
```java
public class StringLines {

    public static void main(String[] args) {
        String str = "Write \n once, \nrun anywhere\n (WORA)";
        str.lines().map(String::strip).forEach(System.out::println);
    }
}
```
В консоль будут выведены четыре строки без пробелов и ограничителей строк:
<p style="background-color: navy; color: yellow">
Write<br>
once,<br>
run anywhere<br>
(WORA)</p>
