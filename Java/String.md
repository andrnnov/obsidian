#Java #String
### [Класс String в Java](https://javarush.com/groups/posts/2347-klass-string-v-java) ###

Класс **String** в Java предназначен для работы со строками в Java. Все строковые литералы, определенные в Java программе (например, "abc") — это экземпляры класса String. Давай посмотрим на его ключевые характеристики:

1. Класс реализует интерфейсы [Serializable](Serializable) и `CharSequence`. Поскольку он входит в пакет `java.lang`, его не нужно импортировать.
2. Класс **String** в Java — это **final** класс, который не может иметь потомков.
3. Класс String — immutable класс, то есть его объекты не могут быть изменены после создания. Любые операции над объектом String, результатом которых должен быть объект класса String, приведут к созданию нового объекта.
4. Благодаря своей неизменности, объекты класса String являются потокобезопасными и могут быть использованы в многопоточной среде.
5. Каждый объект в Java может быть преобразован в строку через метод [[Object#Метод toString()|toString]], унаследованный всеми Java-классами от класса [Object](Object).
#### Работа с Java String ####

Это один из самых часто используемых классов в Java. В нем есть методы для анализа определенных символов строки, для сравнения и поиска строк, извлечения подстрок, создания копии строки с переводом всех символов в нижний и верхний регистр и прочие. Список всех методов класса String можно изучить в [официальной документации](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html). Также в Java реализован несложный механизм конкатенации (соединения строк), преобразования примитивов в строку и наоборот. Давай рассмотрим некоторые примеры работы с классом String в Java.
#### Создание строк ####

Проще всего создать экземпляр класса String, присвоив ему значение строкового литерала:
```java
String s = "I love movies";
```
Однако у класса String есть много [конструкторов](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html#String--), которые позволяют:

- создать объект, содержащий пустую строку
- создать копию строковой переменной
- создать строку на основе массива символов
- создать строку на основе массива байтов (с учетом кодировок)
- и т.д.
#### Строковые литералы в виде констант или одиночных элементов ####

Если вы используете ту же строку (например, "Hello World") в объявлениях других строковых переменных, виртуальная машина Java может создать в памяти только один экземпляр String. Таким образом, строковый литерал становится де-факто константой или синглтоном. Различные переменные, инициализированные одной и той же постоянной строкой, будут указывать на один и тот же экземпляр строки в памяти. Вот пример Java String constant / singleton:
```java
String myString1 = "Hello World";
String myString2 = "Hello World";
```
В этом случае виртуальная машина Java заставит как myString1, так и myString2 указывать на один и тот же строковый объект.

Точнее, объекты, представляющие строковые литералы Java, получаются из пула постоянных строк, который виртуальная машина Java хранит внутри себя. Это означает, что даже классы из разных проектов, скомпилированные отдельно, но используемые в одном и том же приложении, могут совместно использовать объекты constant String. Общий доступ происходит во время выполнения. Это не функция времени компиляции.

Если вы хотите быть уверены, что две строковые переменные указывают на отдельные строковые объекты, используйте оператор new следующим образом:
```java
String myString1 = new String("Hello World");
String myString2 = new String("Hello World");
```
Несмотря на то, что значение (текст) двух созданных строк Java одинаковое, виртуальная машина Java создаст в памяти два разных объекта для их представления.

### Конструкторы

#### 1. String(byte[] byte_arr)

Создайте новую строку путем декодирования __массива байтов__. Для декодирования используется набор символов платформы по умолчанию.

**Пример:**
```java
byte[] b_arr = {71, 101, 101, 107, 115};
String s_byte =new String(b_arr); //Geeks
```

#### 2. String(byte[] byte_arr, Charset char_set)
Создайте новую строку путем декодирования массива байтов. Он использует char_set для декодирования.

**Пример:**
```java
byte[] b_arr = {71, 101, 101, 107, 115};
Charset cs = Charset.defaultCharset();
String s_byte_char = new String(b_arr, cs); //Geeks
```

#### 3. String(byte[] byte_arr, String char_set_name)

Создайте новую строку путем декодирования массива байтов. Он использует char_set_name для декодирования. Он выглядит аналогично приведенным выше конструкциям, и они появляются перед аналогичными функциями, но он принимает строку (которая содержит char_set_name) в качестве параметра, в то время как приведенный выше конструктор принимает CharSet.

**Пример:**
```java
byte[] b_arr = {71, 101, 101, 107, 115};
String s = new String(b_arr, "US-ASCII"); //Geeks
```

#### 4. String(byte[] byte_arr, int start_index, int length)

Создайте новую строку из массива bytes в зависимости от start_index(начальной позиции) и длины (количества символов от начальной позиции).

**Пример:**
```java
byte[] b_arr = {71, 101, 101, 107, 115};
String s = new String(b_arr, 1, 3); // eek
```

#### 5. String(byte[] byte_arr, int start_index, int length, Charset char_set)

Создайте новую строку из массива bytes в зависимости от start_index(начальной позиции) и длины (количества символов от начальной позиции). Использует char_set для декодирования.

**Пример:**
```java
byte[] b_arr = {71, 101, 101, 107, 115};
Charset cs = Charset.defaultCharset();
String s = new String(b_arr, 1, 3, cs); // eek
```

#### 6. String(byte[] byte_arr, int start_index, int length, String char_set_name)

Создайте новую строку из массива bytes в зависимости от start_index(начальной позиции) и длины (количества символов от начальной позиции). Использует char_set_name для декодирования.

**Пример:**
```java
byte[] b_arr = {71, 101, 101, 107, 115};
String s = new String(b_arr, 1, 4, "US-ASCII"); // eeks
```

#### 7. String(char[] char_arr)

Выделяет новую строку из заданного массива символов

**Пример:**
```java
char char_arr[] = {'G', 'e', 'e', 'k', 's'};
String s = new String(char_arr); //Geeks
```

#### 8. String(char[] char_array, int start_index, int count)

Выделяет строку из заданного массива символов, но выбирает количество символов из start_index.

**Пример:**
```java
char char_arr[] = {'G', 'e', 'e', 'k', 's'};
String s = new String(char_arr , 1, 3); //eek
```

#### 9. String(int[] uni_code_points, int offset, int count)

Выделяет строку из массива uni_code_array, но выбирает количество символов из start_index.

**Пример:**
```java
int[] uni_code = {71, 101, 101, 107, 115};
String s = new String(uni_code, 1, 3); //eek
```

#### 10. String(StringBuffer s_buffer)

Выделяет новую строку из строки в s_buffer

**Пример:**
```java
StringBuffer s_buffer = new StringBuffer("Geeks");
String s = new String(s_buffer); //Geeks
```

#### 11. String(StringBuilder s_builder)

Выделяет новую строку из строки в s_builder

**Пример:**
```java
StringBuilder s_builder = new StringBuilder("Geeks");
String s = new String(s_builder); //Geeks
```

### Методы String

#### Строковый метод charAt()

Метод String **charAt()** возвращает символ по указанному индексу в строке. Индекс первого символа строки равен 0, второго символа — 1 и т. д. Значение индекса должно находиться в диапазоне от 0 до length() – 1.

Если значение индекса больше или равно длине строки или отрицательному числу, оно возвращает **исключение StringIndexOutOfBoundsException.**

**Пример:**
```java
// Java Program to demonstrate use of
// String charAt() Method
 
class Main {
    public static void main(String args[]) {
        // Define a string
        String s = "Java String charAt() example";
 
        // Retrieve and print the character at index 8
        char ch = s.charAt(8);
        System.out.println(ch);
 
        // Retrieve and print the character at index 24
        ch = s.charAt(24);
        System.out.println(ch);
    }
}
```
**Вывод:**
<p style="background-color: navy; color: yellow">
i<br>
m</p>

#### Обрезка строки с помощью trim() ####

Класс Java String содержит метод, называемый trim(), который может обрезать объект string. Под обрезкой подразумевается удаление пробельных символов в начале и конце строки. Символы пробела включают пробел, табуляцию и новые строки. Вот пример Java String trim():
```java
String text    = "  And he ran across the field   ";
String trimmed = text.trim();
```
После выполнения этого кода обрезанная переменная будет указывать на экземпляр строки со значением:
<p style="background-color: navy; color: yellow">
And he ran across the field</p>

Символы пробела в начале и конце объекта String были удалены. Символ пробела внутри строки не был затронут. Под "внутри" подразумевается расстояние между первым и последним символом, не являющимся пробелом. 

Метод trim() не изменяет экземпляр String. Вместо этого он возвращает новый объект Java String, который равен объекту String, из которого он был создан, но с удаленным пробелом в начале и конце строки. 

Метод trim() может быть очень полезен для обрезки текста, введенного пользователем в поля ввода. Например, пользователь может ввести свое имя и случайно поставить дополнительный пробел после последнего слова или перед первым словом. Метод trim() - это простой способ удалить такие лишние пробельные символы.
#### Сложение строк ####

Сложить две строки в Java довольно просто, воспользовавшись оператором `+`. Java позволяет складывать друг с другом и переменные, и строковые литералы:
```java
public static void main(String[] args) {
    String day = "День";
    String and = "и";
    String night = "Ночь";

    String dayAndNight = day + " " + and + " " + night;
}
```
Складывая объекты класса String с объектами других классов, мы приводим последние к строковому виду. Преобразование объектов других классов к строковому представлению выполняется через неявный вызов метода `toString` у объекта. Продемонстрируем это на следующем примере:
```java
public class StringExamples {
    public static void main(String[] args) {
        Human max = new Human("Макс");
        String out = "Java объект: " + max;
        System.out.println(out); // Вывод: Java объект: Человек с именем Макс
    }

    static class Human {
        private String name;

        public Human(String name) {
            this.name = name;
        }

        @Override
        public String toString() {
            return "Человек с именем " + name;
        }
    }
}
```
#### Замена символов в строках с помощью функции replace() ####

Класс Java String содержит метод с именем replace(), который может заменять символы в строке. Метод replace() фактически не заменяет символы в существующей строке. Скорее, он возвращает новый экземпляр String, который равен экземпляру String, из которого он был создан, но с заменой заданных символов. Вот пример Java String replace():
```java
String source   = "123abc";
String replaced = source.replace('a', '@');
```
После выполнения этого кода заменяемая переменная будет указывать на строку с текстом:
<p style="background-color: navy; color: yellow">
123@bc</p>

Метод replace() заменит все символы, соответствующие символу, переданному в качестве первого параметра методу, на второй символ, переданный в качестве параметра методу replace().
##### replaceFirst() #####

Метод Java String replaceFirst() возвращает новую строку с первым совпадением [регулярного выражения](Regex), переданного в качестве первого параметра, со строковым значением второго параметра. Вот пример replaceFirst():
```java
String text = "one two three two one";

String s = text.replaceFirst("two", "five");
cd```
В этом примере будет возвращена строка: 
<p style="background-color: navy; color: yellow">
one five three two one</p>

##### replaceAll() #####

Метод Java String replaceAll() возвращает новую строку со всеми совпадениями [регулярного выражения](Regex), переданного в качестве первого параметра, со строковым значением второго параметра. Вот пример replaceAll():
```java
String text = "one two three two one";

String t = text.replaceAll("two", "five");
```
В этом примере будет возвращена строка: 
<p style="background-color: navy; color: yellow">
one five three five one</p>

#### Сравнение строк ####

Для сравнения строк можно воспользоваться методом `equals()`:
```java
public static void main(String[] args) {
    String x = "Test String";
    System.out.println("Test String".equals(x)); // true
}
```
Когда при сравнении строк нам не важен регистр, нужно использовать метод `equalsIgnoreCase()`:
```java
public static void main(String[] args) {
       String x = "Test String";
       System.out.println("test string".equalsIgnoreCase(x)); // true
}
```
#### Перевод объекта/примитива в строку ####

Для перевода экземпляра любого Java-класса или любого примитивного типа данных к строковому представлению, можно использовать метод `String.valueOf()`:
```java
public class StringExamples {
    public static void main(String[] args) {
        String a = String.valueOf(1);
        String b = String.valueOf(12.0D);
        String c = String.valueOf(123.4F);
        String d = String.valueOf(123456L);
        String s = String.valueOf(true);
        String human = String.valueOf(new Human("Alex"));

        System.out.println(a);
        System.out.println(b);
        System.out.println(c);
        System.out.println(d);
        System.out.println(s);
        System.out.println(human);
        /*
        Вывод:
        1
        12.0
        123.4
        123456
        true
        Человек с именем Alex
         */
    }

    static class Human {
        private String name;

        public Human(String name) {
            this.name = name;
        }

        @Override
        public String toString() {
            return "Человек с именем " + name;
        }
    }
}
```
#### Перевод строки в число ####

Часто бывает нужно перевести строку в число. У классов [оберток примитивных типов](WrapperClasses) есть методы, которые служат как раз для этой цели. Все эти методы начинаются со слова parse. Рассмотрим ниже перевод строки в целочисленное (`Integer`) и дробное (`Double`) числа:
```java
public static void main(String[] args) {
    Integer i = Integer.parseInt("12");
    Double d = Double.parseDouble("12.65D");

    System.out.println(i); // 12
    System.out.println(d); // 12.65
}
```
#### Перевод коллекции строк к строковому представлению ####

Если нужно преобразовать все элементы некоторой коллекции строк к строковому представлению через произвольный разделитель, можно использовать такие методы класса String Java:
```java
- join(CharSequence delimiter, CharSequence... elements)
- join(CharSequence delimiter, Iterable<? extends CharSequence> elements)
```
Где `delimiter` — разделитель элементов, а `elements` — массив строк / экземпляр коллекции строк. Рассмотрим пример, в котором мы преобразуем список строк в строку, разделяя каждую точкой с запятой:
```java
public static void main(String[] args) {
    List<String> people = Arrays.asList(
            "Philip J. Fry",
            "Turanga Leela",
            "Bender Bending Rodriguez",
            "Hubert Farnsworth",
            "Hermes Conrad",
            "John D. Zoidberg",
            "Amy Wong"
    );

    String peopleString = String.join("; ", people);
    System.out.println(peopleString);
    /*
    Вывод:
    Philip J. Fry; Turanga Leela; Bender Bending Rodriguez; Hubert Farnsworth; Hermes Conrad; John D. Zoidberg; Amy Wong
     */
}
```
#### Разбиение строки на массив строк ####

Эту операцию выполняет метод `split(String regex)` В качестве разделителя выступает строковое [регулярное выражение `regex`](Regex). В примере ниже произведем операцию, обратную той, что мы выполняли в предыдущем примере:
```java
public static void main(String[] args) {
    String people = "Philip J. Fry; Turanga Leela; Bender Bending Rodriguez; Hubert Farnsworth; Hermes Conrad; John D. Zoidberg; Amy Wong";

    String[] peopleArray = people.split("; ");
    for (String human : peopleArray) {
        System.out.println(human);
    }
    /*
    Вывод:
    Philip J. Fry
    Turanga Leela
    Bender Bending Rodriguez
    Hubert Farnsworth
    Hermes Conrad
    John D. Zoidberg
    Amy Wong
     */
}
```

Но иногда такой подход избыточен. Если разделителей много, например, «пробел», «enter», «таб», «точка», приходится конструировать достаточно сложное регулярное выражение. Его сложно читать, а значит, в него сложно вносить изменения.

В Java есть специальный класс [StringTokenizer](StringTokenizer), вся работа которого — разделять строку на подстроки.

Этот класс не использует [регулярные выражения](Regex): вместо этого в него просто передается строка, состоящая из символов-разделителей. Преимущества этого подхода в том, что он не разбивает сразу всю строку на кусочки, а потихоньку идет от начала к концу.

#### Метод matches() в Java ####

Метод **matches()** определяет, соответствует ли строка [регулярному выражению](Regex).
**Синтаксис метода:**
```java
public boolean matches(String regexp);
```
**Вызов:**
```java
boolean match = str1.matches(regexp);
```
Пример:
```java
public class Test {
    public static void main(String[] args) {
        String MyString = "I love Java";
        System.out.println(MyString.matches("(.*)Java(.*)"));
        System.out.println(MyString.matches("(.*)Ruby(.*)"));
    }
}
```
**Если Вы запустите данный код на своем компьютере, в консоли Вы увидите следующее:**
<p style="background-color: navy; color: yellow">true<br>
false</p>
**Комментарии к коду:**
У нас есть строка **"I love Java"**. С помощью метода **matches()** мы проверяем, соответствует ли строка двум регулярным выражениям - "(.*)Java(.*)" и "(.*)Ruby(.*)".
- Первое выражение означает, что мы ищем слово "Java", после которого может стоять любое количество символов, и перед которым может стоять любое количество символов. У нас в строке встречается слово "Java", поэтому в консоли получаем **true**.
- Во второй строке мы так же ищем слово "Ruby". Строка **"I love Java"** не соответствует этому регулярному выражению, поэтому у нас консоли **false**.

#### Определение позиции элемента в строке ####

В языке Java String предоставляет набор методов для определения позиции символа/подстроки в строке:
1. `indexOf(int ch)`
2. `indexOf(int ch, int fromIndex)`
3. `indexOf(String str)`
4. `indexOf(String str, int fromIndex)`
5. `lastIndexOf(int ch)`
6. `lastIndexOf(int ch, int fromIndex)`
7. `lastIndexOf(String str)`
8. `lastIndexOf(String str, int fromIndex)`
Где:
1. `ch` — искомый символ (`char`)
2. `str` — искомая строка
3. `fromIndex` — позиция с которой нужно искать элемент
4. методы `indexOf` — возвращают позицию первого найденного элемента
5. методы `lastIndexOf` — возвращают позицию последнего найденного элемента

Если искомый элемент не найден, методы вернут в строке -1. Попробуем найти порядковый номер букв `A`, `K`, `Z`, `Я` в английском алфавите, но будем иметь ввиду, что индексация символов в строке в Java начинается с нуля:
```java
public static void main(String[] args) {
    String alphabet = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
    System.out.println(alphabet.indexOf('A')); // 0
    System.out.println(alphabet.indexOf('K')); // 10
    System.out.println(alphabet.indexOf('Z')); // 25
    System.out.println(alphabet.indexOf('Я')); // -1
}
```
#### Извлечение подстроки из строки ####

Для извлечения подстроки из строки класс String в Java предоставляет методы:
- `substring(int beginIndex)`
- `substring(int beginIndex, int endIndex)`
Рассмотрим, как с помощью методов определения позиции элемента и извлечения подстроки мы можем получить имя файла из его пути:
```java
public static void main(String[] args) {
    String filePath = "D:\\Movies\\Futurama.mp4";
    int lastFileSeparatorIndex = filePath.lastIndexOf('\\');
    String fileName = filePath.substring(lastFileSeparatorIndex + 1);
    System.out.println(fileName); //9
}
```
#### Перевод строки в верхний/нижний регистр ####

Класс String предоставляет методы для перевода строки в верхний и нижний регистры:
- `toLowerCase()`
- `toUpperCase()`

Рассмотрим работу данных методов на примере:
```java
public static void main(String[] args) {
    String fry = "Philip J. Fry";

    String lowerCaseFry = fry.toLowerCase();
    String upperCaseFry = fry.toUpperCase();

    System.out.println(lowerCaseFry); // philip j. fry
    System.out.println(upperCaseFry); // PHILIP J. FRY
}
```
#### Получение символов и байтов ####

Можно получить символ с определенным индексом в строке, используя метод charAt(). Вот пример:
```java
String theString = "This is a good day to code";

System.out.println( theString.charAt(0) );
System.out.println( theString.charAt(3) );
```
Вывод:
<p style="background-color: navy; color: yellow">
T<br>
s</p>

поскольку это символы, расположенные в строке с индексами 0 и 3. 

Вы также можете получить байтовое представление метода String, используя метод getBytes(). Вот два примера:
```java
String theString = "This is a good day to code";

byte[] bytes1 = theString.getBytes();
byte[] bytes2 = theString.getBytes(Charset.forName("UTF-8");
```
символов по умолчанию на компьютере. Какой набор символов используется по умолчанию, зависит от компьютера, на котором выполняется код. Поэтому, как правило, лучше явно указать набор символов, который будет использоваться для создания байтового представления (как в следующей строке). 

Второй вызов `getBytes()` возвращает представление строки в формате UTF-8 байт.

[Компактные строки в Java 9](CompactString)
[Методы класса String, появившиеся в Java 11](StringJava11)

