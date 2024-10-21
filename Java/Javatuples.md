#Java #Tuple #Javatuples

## [Введение в Java-кортежи](https://www.studytonight.com/java-examples/introduction-to-java-tuples)

2024-10-21 10:34

Кортеж — это структура данных, которая хранит данные в **упорядоченной последовательности, как массивы или списки**. Но в отличие от массивов или списков, **кортежи могут хранить данные разных типов**.

**Например,** мы можем сохранить `["строку", 123, 123,321, 'c']` в кортеже, но не можем использовать для этого массивы или списки. Единственный способ сделать это с помощью массивов или списков — создать массив строк и сохранить их в виде строк, но это может быть очень неудобно.
```java
String[] arr = {"string", "123", "123.321", "c"};
```
Мы также можем создавать собственные классы с элементами данных необходимых типов, но это тоже может привести к путанице и задержкам.

В Java нет структуры данных или коллекции, реализующей кортежи, но мы можем добавить в наш проект внешнюю библиотеку **[Java tuples](https://www.javatuples.org)**, чтобы использовать её классы кортежей. Это простая библиотека, которая предоставляет различные методы для работы с кортежами.

## Библиотека Java-кортежей

Библиотека Java-кортежей предоставляет десять различных классов, которые можно использовать для работы с кортежами. Разница между этими классами заключается в количестве элементов, которые можно в них хранить. **В классе Java-кортежей нельзя хранить более 10 элементов**. Названия этих классов следующие:
- **Unit`<A>`** для хранения **одного** элемента.
- **Pair`<A, B>`** для хранения **двух** элементов.
- **Triplet`<A, B, C>`** для хранения **трёх** элементов.
- **Quartet`<A, B, C, D>`** для хранения **четырёх** элементов.
- **Quintet`<A, B, C, D, E>`** для хранения **пяти** элементов.
- **Sextet`<A, B, C, D, E, F>`** для хранения **шести** элементов.
- **Septet`<A, B, C, D, E, F, G>`** для хранения **семи** элементов.
- **Octet`<A, B, C, D, E, F, G, H>`** для хранения **восьми** элементов.
- **Enneade`<A, B, C, D, E, F, G, H, I>`** для хранения **девяти** элементов.
- **Decade`<A, B, C, D, E, F, G, H, I, J>`** для хранения **десяти** элементов.

У нас также есть еще два класса, которые называются **KeyValue`<A, B>`** и **LabelValue`<A, B>`**. Они похожи на класс Pair`<A, B>`. Алфавиты A, B, C и т.д. представляют типы данных различных элементов, которые будут храниться в кортеже.

Все классы кортежей в этой библиотеке **типобезопасны** и **неизменяемы**. Мы не можем изменить данные или структуру кортежей после создания объекта. Все эти классы реализуют интерфейсы [Iterable](Iterable), [Serializable](Serializable) и [Comparable](Comparable).

### Создание кортежа в Java

Создать кортеж довольно просто. Нам нужно лишь указать типы данных элементов и их значения в конструкторе класса.

```java
import org.javatuples.*;

public class TupleDemo {
	public static void main(String[] args) {
		Triplet<String, Double, Integer> tuple1 = new Triplet<String, Double, Integer>("Str", 5.0, 5);
		System.out.println(tuple1);
	}
}
```
**Вывод:**
<p style="background-color:navy; color: yellow">
[Str, 5.0, 5]</p>

Мы также можем использовать метод **with()** для создания нового кортежа.
```java
import org.javatuples.*;

public class TupleDemo {
	public static void main(String[] args)	{
		Triplet<String, Double, Integer> tuple2 = Triplet.with("Str", 5.0, 5);
		System.out.println(tuple2);
	}
}
```
**Вывод:**
<p style="background-color:navy; color: yellow">
[Str, 5.0, 5]</p>

Мы также можем использовать методы **fromCollection()** и **fromIterable()** для создания нового кортежа из коллекции. При использовании метода fromCollection() убедитесь, что вы используете правильный класс кортежа в соответствии с размером коллекции. Метод fromIterable() можно использовать для создания кортежа меньшего размера, указав индекс, с которого следует выбирать элементы.
```java
import java.util.Arrays;
import java.util.List;
import org.javatuples.*;

public class TupleDemo {
	public static void main(String[] args)	{
		List<String> list = Arrays.asList("unit","pair", "triplet");
		Triplet<String, String, String> tuple1 = Triplet.fromCollection(list);
		System.out.println(tuple1);
		
		Pair<String, String> tuple2 = Pair.fromIterable(list, 1);//two elements to be fetched from index 1
		System.out.println(tuple2);
	}
}
```
**Вывод:**
<p style="background-color:navy; color: yellow">
[unit, pair, triplet]<br>
[pair, triplet]</p>

### Извлечение значений кортежа в Java

Мы можем использовать метод **getValue(X)** или **getValueX()** для получения элемента, находящегося по индексу X в кортеже. Как и массивы, кортежи также используют **нулевую индексацию**. Обратите внимание, что **метод getValue() небезопасен с точки зрения типов**. При использовании этого метода необходимо выполнять приведение типов. Однако **метод getValueX() безопасен с точки зрения типов и не требует приведения типов**.
```java
import org.javatuples.*;

public class TupleDemo {
	public static void main(String[] args) {
		Triplet<String, Integer, Double> tuple = Triplet.with("Str", 5, 5.0);
		Integer i = (Integer)tuple.getValue(1);//casting
		Integer j = tuple.getValue1();
		
		System.out.println("Value fetched by getValue(): " + i);
		System.out.println("Value fetched by getValueX(): " + j);
	}
}
```
**Вывод:**
<p style="background-color:navy; color: yellow">
Value fetched by getValue(): 5<br>
Value fetched by getValueX(): 5</p>

### Настройка значений кортежа в Java

Мы можем изменить значение элемента в кортеже с помощью метода **setAtX()**, где X — это индекс. Это вернёт кортеж того же класса, что и исходный кортеж. **Поскольку кортежи неизменяемы, исходный кортеж не будет изменён.**
```java
import org.javatuples.*;

public class TupleDemo {
	public static void main(String[] args)	{
		Triplet<String, Integer, Double> tuple1 = Triplet.with("Str", 5, 5.0);
		Triplet<String, Integer, Double> tuple2 = tuple1.setAt2(5.1);
		
		System.out.println("Original Tuple: " + tuple1);
		System.out.println("New Tuple with changes: " + tuple2);
	}
}
```
**Вывод:**
<p style="background-color:navy; color: yellow">
Original Tuple: [Str, 5, 5.0]<br>
New Tuple with changes: [Str, 5, 5.1]</p>

### Добавление элементов в Tuple

Мы можем добавлять значения в существующий кортеж, но для размещения нового элемента нам нужно создать новый кортеж большего размера.

**Например**, если мы добавим элемент в кортеж класса «Septet», то получим кортеж класса «Octet».

Мы можем добавить элемент в конец кортежа с помощью метода **add()**. Или мы можем использовать метод **addAtX()** для добавления элемента по индексу X. При этом остальные элементы сдвинутся на одну позицию вправо. Прежде чем вставлять новый элемент, убедитесь, что типы данных совпадают.
```java
import org.javatuples.*;

public class TupleDemo {
	public static void main(String[] args)	{
		Triplet<String, String, String> tuple1 = Triplet.with("str1", "str2", "str3");
		Quartet<String, String, String, String> tuple2 = tuple1.add("str4");
		Quartet<String, String, String, String> tuple3 = tuple1.addAt0("str0");
		
		System.out.println("Original Tuple: " + tuple1);
		System.out.println("Adding using add(): " + tuple2);
		System.out.println("Adding using addAtX(): " + tuple3);
	}
}
```
**Вывод:**
<p style="background-color:navy; color: yellow">
Original Tuple: [str1, str2, str3]<br>
Adding using add(): [str1, str2, str3, str4]<br>
Adding using addAtX(): [str0, str1, str2, str3]</p>

Эти два метода также можно использовать для добавления одного кортежа к другому. Нужно следить за размером нового кортежа. **Например,** если кортеж класса Pair добавить к кортежу класса Triplet, то получится кортеж класса Quintet. Убедитесь, что суммарный размер двух кортежей не превышает 10.
```java
import org.javatuples.*;

public class TupleDemo {
	public static void main(String[] args)	{
		Triplet<String, String, String> tuple1 = Triplet.with("str1", "str2", "str3");
		Pair<String, String> tuple2 = Pair.with("str4", "str5");
		Quintet<String, String, String, String, String> tuple3 = tuple1.add(tuple2);
		Quintet<String, String, String, String, String> tuple4 = tuple1.addAt1(tuple2);
		
		System.out.println("Adding tuples using add(): " + tuple3);
		System.out.println("Adding tuples using addAtX(): " + tuple4);
	}
}
```
**Вывод:**
<p style="background-color:navy; color: yellow">
Adding tuples using add(): [str1, str2, str3, str4, str5]<br>
Adding tuples using addAtX(): [str1, str4, str5, str2, str3]</p>

### Удаление элементов

Метод **removeFromX()** можно использовать для удаления элемента из индекса X. В результате будет возвращён кортеж на один элемент меньше исходного массива. **Например**, если метод removeFromX() используется для кортежа Quartet, то возвращается кортеж Triplet.
```java
import org.javatuples.*;

public class TupleDemo {
	public static void main(String[] args)	{
		Triplet<String, String, String> tuple1 = Triplet.with("str1", "str2", "str3");
		Pair<String, String> tuple2 = tuple1.removeFrom0();
		Pair<String, String> tuple3 = tuple1.removeFrom1();
		
		System.out.println("Original Tuple: " + tuple1);
		System.out.println("Removing element at index 0: " + tuple2);
		System.out.println("Removing element at index 1: " + tuple3);
	}
}
```
**Вывод:**
<p style="background-color:navy; color: yellow">
Original Tuple: [str1, str2, str3]<br>
Removing element at index 0: [str2, str3]<br>
Removing element at index 1: [str1, str3]</p>

### Итерация по кортежу

Поскольку **кортежи реализуют интерфейс Iterable**, мы можем легко перебирать кортежи с помощью простого цикла **for-each**.
```java
import org.javatuples.*;

public class TupleDemo {
	public static void main(String[] args) {
		Triplet<String, String, String> tuple = Triplet.with("str1", "str2", "str3");
		
		for(Object o : tuple)
			System.out.print(o + " ");
	}
}
```
**Вывод:**
<p style="background-color:navy; color: yellow">
str1 str2 str3 </p>

### Методы contains() и containsAll()

Метод contains(), как следует из названия, **возвращает логическое значение в зависимости от наличия элемента в кортеже**.
```java
import org.javatuples.*;

public class TupleDemo {
	public static void main(String[] args)	{
		Triplet<String, String, String> tuple = Triplet.with("str1", "str2", "str3");	
		boolean containsStr1 = tuple.contains("Str1");
		boolean containsstr1 = tuple.contains("str1");
		
		System.out.println("Tuple contains Str1: " + containsStr1);
		System.out.println("Tuple contains str1: " + containsstr1);
	}
}
```
**Вывод:**
<p style="background-color:navy; color: yellow">
Tuple contains Str1: false<br>
Tuple contains str1: true</p>

Метод containsAll() можно использовать, чтобы **проверить, присутствуют ли все элементы коллекции в кортеже**. Этот метод также **возвращает логическое значение**.
```java
import java.util.Arrays;
import java.util.List;
import org.javatuples.*;

public class TupleDemo {
	public static void main(String[] args)	{
		Triplet<String, String, String> tuple = Triplet.with("str1", "str2", "str3");
		List<String> list1 = Arrays.asList("str1", "str3", "str2");
		List<String> list2 = Arrays.asList("str1", "str5", "str2");
		
		System.out.println("Tuple contains list1: " + tuple.containsAll(list1));
		System.out.println("Tuple contains list2: " + tuple.containsAll(list2));
	}
}
```
**Вывод:**
<p style="background-color:navy; color: yellow">
Tuple contains list1: true<br>
Tuple contains list2: false</p>

### Методы Java-кортежей indexOf() и lastIndexOf()

Метод indexOf() **возвращает индекс первого вхождения элемента** в кортеж.
Метод lastIndexOf() **возвращает индекс последнего вхождения элемента** в кортеж.
```java
import org.javatuples.Quartet;

public class Main {
    public static void main(String[] args)	{
        Quartet<String, String, String, String> tuple = Quartet.with("str1", "str2", "str1", "str3");

        System.out.println("Tuple: " + tuple);
        System.out.println("First index of str1:" + tuple.indexOf("str1"));
        System.out.println("Last index of str1: " + tuple.lastIndexOf("str1"));
    }
}
```
**Вывод:**
<p style="background-color:navy; color: yellow">
Tuple: [str1, str2, str1, str3]<br>
First index of str1:0<br>
Last index of str1: 2</p>

### Преобразование кортежей в массивы или списки

Мы можем легко преобразовать кортеж в массив, используя метод **toArray()**. Аналогичным образом мы можем использовать метод **ToList()** для преобразования кортежа в список. Обратите внимание, что **эти два метода будут возвращать массивы и списки объектного типа `(Object[] arr, List<Object> list`)** даже если все элементы кортежа имеют одинаковый тип данных.
```java
import java.util.Arrays;
import java.util.List;
import org.javatuples.*;

public class TupleDemo
{
	public static void main(String[] args)
	{
		Quartet<String, String, String, String> tuple = Quartet.with("str1", "str2", "str1", "str3");
		Object[] arrFromTuple = tuple.toArray();
		List<Object> listFromTuple = tuple.toList();
		
		System.out.println("Tuple: " + tuple);
		System.out.println("Array: " + Arrays.toString(arrFromTuple));
		System.out.println("List: " + listFromTuple);
	}
}
```
**Вывод:**
<p style="background-color:navy; color: yellow">
Tuple: [str1, str2, str1, str3]<br>
Array: [str1, str2, str1, str3]<br>
List: [str1, str2, str1, str3]</p>

## Вопросы и ответы

### Вопрос: Как можно реализовать кортежи с помощью классов в Java?

Кортежи имеют фиксированный размер и используются для совместного хранения данных разных типов. **Например,** если мы хотим сохранить строку, целое число и число с плавающей точкой, то мы можем создать класс с этими тремя элементами данных и написать соответствующие конструкторы для создания нового объекта этого типа. Но предпочтительнее использовать внешние библиотеки, такие как кортежи Java.

### Вопрос: Кортежи быстрее списков?

Да, кортежи работают быстрее, чем списки, потому что они имеют фиксированный размер и являются неизменяемыми, поэтому мы можем выделить для них один блок памяти и не нужно добавлять дополнительное пространство для дополнительных элементов. Перебор кортежей также выполняется быстрее, чем перебор списков.

## Краткие сведения

Кортежи — это важная структура данных, если мы хотим присвоить данные только один раз и больше никогда их не менять. Их можно использовать для хранения записей, содержащих поля разных типов данных, например `[101, «Шоколад», 5,99]`. Библиотека Java-кортежей предоставляет различные классы для работы с кортежами. Максимальное количество элементов, которые может хранить класс кортежа, — 10. Следует отметить, что при установке, добавлении или удалении значений мы не изменяем исходный кортеж, а создаём новый кортеж с внесёнными изменениями. Это происходит потому, что кортежи неизменяемы.
