#Java #String #StringBuilder
### StringBuilder в Java ###

#### 1. Изменения строк ####

[Строки в Java](String) — это неизменяемые объекты (immutable). Так было сделано для того, чтобы класс-строку можно было сильно оптимизировать и использовать повсеместно. Например, [в качестве ключей у коллекции HashMap](https://javarush.com/groups/posts/1940-klass-hashmap-) рекомендуется использовать только immutable-типы.

Однако часто возникают ситуации, когда программисту все же было бы удобнее иметь `String`-класс, который можно менять. Который не создает новую подстроку при каждом вызове его метода.

Например, у нас есть очень большая строка и мы часто дописываем что-то в ее конец. В этом случае даже коллекция символов (`ArrayList<Character>`) может быть эффективнее, чем постоянное пересоздание строк и конкатенации объектов типа `String`.

Именно поэтому в язык Java все же добавили тип String, который можно менять. Называется он `StringBuilder`.
##### Создание объекта #####

Чтобы создать объект `StringBuilder` на основе существующей строки, нужно выполнить команду вида:
```java
StringBuilder имя = new StringBuilder(строка);
```
Чтобы создать пустую изменяемую строку, нужно воспользоваться командой вида:
```java
StringBuilder имя = new StringBuilder();
```

Пример далее импортирует java.lang.StringBuilder. Мы создаем StringBuilder. Зацикливаем и добавляем к нему пять строк и конвертируем данные в объект String. Затем отображаем полученную строку в консоли с помощью метода System.out.println.
```java
import java.lang.StringBuilder;

public class Program {
	public static void main(String[] args) {
		// Create a new StringBuilder.
		StringBuilder builder = new StringBuilder();
		// Loop and append values.
		for (int i = 0; i < 5; i++) {
			builder.append("abc ");
		}
		// Convert to string.
		String result = builder.toString();
		// Print result.
		System.out.println(result);
	}
}
```
Вывод:
<p style="background-color: navy; color: yellow">abc abc abc abc abc</p>
##### Список методов #####

Класс `StringBuilder` имеет два десятка полезных методов, вот самые важные из них:

|Метод|Описание|
|---|---|
|```StringBuilder append(obj)```|Преобразовывает переданный объект в строку и добавляет к текущей строке|
|```StringBuilder insert(int index, obj)```|Преобразовывает переданный объект в строку и вставляет в текущую строку|
|```StringBuilder replace(int start, int end, String str)```|Заменяет часть строки, заданную интервалом start..end на переданную строку|
|```StringBuilder deleteCharAt(int index)```|Удаляет из строки символ под номером index|
|```StringBuilder delete(int start, int end)```|Удаляет из строки символы, заданные интервалом|
|```int indexOf(String str, int index)```|Ищет подстроку в текущей строке|
|```int lastIndexOf(String str, int index)```|Ищет подстроку в текущей строке с конца|
|```char charAt(int index)```|Возвращает символ строки по его индексу|
|```String substring(int start, int end)```|Возвращает подстроку, заданную интервалом|
|```StringBuilder reverse()```|Разворачивает строку задом наперед.|
|```void setCharAt(int index, char)```|Изменяет символ строки, заданный индексом на переданный|
|```int length()```|Возвращает длину строки в символах|
Часто мы используем StringBuilders в циклах. Здесь у нас часто неизвестное количество итераций. А StringBuilder оптимизирует случаи, когда происходит много вызовов append().

Следовательно, использование StringBuilder в цикле может предотвратить возникновение проблемы с производительностью генерации.

StringBuilder может добавлять данные многих типов. Мы не ограничены строками. С помощью метода append () мы можем добавлять целые числа, двойные числа, символы - любой числовой тип.

В этом примере мы вызываем append() для результата предыдущего вызова append() и он возвращает исходный StringBuilder.
```java
import java.lang.StringBuilder;

public class Program {
	public static void main(String[] args) {
		int value1 = 300;
		double value2 = 3.14;
		short value3 = 5;
		char value4 = 'A';
		// Create StringBuilder and add four values to it.
		StringBuilder builder = new StringBuilder();
		builder.append(value1).append("\n");
		builder.append(value2).append("\n");
		builder.append(value3).append("\n");
		builder.append(value4);
		// Display results.
		String result = builder.toString();
		System.out.println(result);
	}
}
```
Вывод:
<p style="background: navy; color: yellow">300<br>
3.14<br>
5<br>
A</p>
StringBuilder имеет изменяемый буфер. Таким образом, мы можем быстро добавлять или вставлять данные. Он получает два аргумента: индекс и значение, которое мы хотим вставить.

Индекс: это первый аргумент. Чтобы вставить после второго символа, используйте значение 2. А для вставки в начале используйте ноль.
Строка: мы передаем строку (или другое значение) в качестве второго аргумента. Это данные, которые помещаются в StringBuilder.
```java
import java.lang.StringBuilder;

public class Program {
	public static void main(String[] args) {
		// Initialize StringBuilder with this value.
		StringBuilder builder = new StringBuilder("abc");
		// Insert this substring at position 2.
		builder.insert(2, "xyz");
		System.out.println(builder);
	}
}
```
Вывод
<p style="background-color: navy; color: yellow">abxyzc</p>

Мы используем метод indexOf для поиска подстроки в данных. Если подстрока найдена, первый индекс, в котором она встречается, возвращается как int.
Если подходящая подстрока не найдена, возвращается отрицательное значение. Мы должны часто проверять -1 при использовании indexOf.
```java
import java.lang.StringBuilder;
public class Program {
	public static void main(String[] args) {
		StringBuilder builder = new StringBuilder("abc");
		// Try to find this substring.
		int result = builder.indexOf("bc");
		System.out.println(result);
		// This substring does not exist.
		int result2 = builder.indexOf("de");
		System.out.println(result2);
	}
}
```
Вывод
==1
-1==

Удаление. Мы передаем ему два аргумента типа int. Первый аргумент - это начальный индекс, с которого должно начинаться удаление. И второй аргумент - это конечный индекс.
```java
import java.lang.StringBuilder;

public class Program {
	public static void main(String[] args) {
		StringBuilder builder = new StringBuilder("carrot");
		// Delete characters from index 2 to index 5.
		builder.delete(2, 5);
		System.out.println(builder);
	}
}
```
Вывод
<p style="background-color: navy; color: yellow">cat</p>

Замена. Этот метод принимает два индекса и заменяет символы в этом диапазоне указанной строкой. Replace в StringBuilder работает иначе, чем replace() в Strings.
```java
import java.lang.StringBuilder;

public class Program {
	public static void main(String[] args) {
		// Create new StringBuilder.
		StringBuilder b = new StringBuilder("abc");
		// Replace second character with "xyz".
		b.replace(1, 2, "xyz");
		System.out.println(b);
	}
}
```
Вывод
<p style="background-color: navy; color: yellow">axyzc</p>

Объединение. Мы можем добавить один StringBuilder к другому. Мы просто вызываем append() и передаем второй StringBuilder в качестве аргумента.
```java
public class Program {
	public static void main(String[] args) {
		StringBuilder builder = new StringBuilder("cat");
		StringBuilder builder2 = new StringBuilder("dog");
		// Combine two StringBuilders.
		builder.append(builder2);
		System.out.println(builder);
	}
}
```
Вывод
<p style="background-color: navy; color: yellow">catdog</p>

Подстрока или [Substring в Java](https://hr-vector.com/java/substring). Этот метод находится в классе AbstractStringBuilder. Он предоставляет полезную возможность извлекать диапазон символов в новую строку.
Аргументы: первый аргумент - это начальный индекс желаемой подстроки. Второй аргумент - это последний индекс (а не количество символов).
```java
import java.lang.StringBuilder;

public class Program {
	public static void main(String[] args) {
		StringBuilder builder = new StringBuilder();
		builder.append("Forest");
		// Get substring after the first two characters.
		String omitFirstTwo = builder.substring(2);
		System.out.println(omitFirstTwo);
		// Get only the first two characters in a substring.
		String firstTwo = builder.substring(0, 2);
		System.out.println(firstTwo);
	}
}
```
Вывод
<p style="background-color: navy; color: yellow">rest<br>
Fo</p>

Перебор символов. Цикл for может перебирать символы. Мы обращаемся к методу length(), чтобы получить размер StringBuilder, а затем используем charAt() для доступа к символам.
```java
import java.lang.StringBuilder;

public class Program {
	public static void main(String[] args) {
		StringBuilder builder = new StringBuilder("magic");
		// Loop over the characters in this StringBuilder.
		for (int i = 0; i < builder.length(); i++) {
			System.out.println(builder.charAt(i));
		}
	}
}
```
Вывод
<p style="background-color: navy; color: yellow">m<br>
a<br>
g<br>
i<br>
c</p>

SetLength. Мы можем изменить длину StringBuilder с помощью setLength. Это часто бывает полезно, когда мы хотим сократить или уменьшить количество символов в объекте.
```java
import java.lang.StringBuilder;

public class Program {
	public static void main(String[] args) {
		StringBuilder builder = new StringBuilder("carrot");
		// Use setLength to remove characters from the end.
		builder.setLength(3);
		System.out.println(builder);
	}
}
```
Вывод
<p style="background-color: navy; color: yellow">car</p>

Reverse. В этом примере выполняется обратное преобразование. Он вызывает метод reverse(). Обратить строку легко - сначала мы должны поместить ее содержимое в StringBuilder.
```java
import java.lang.StringBuilder;

public class Program {
	public static void main(String[] args) {
		// A StringBuilder can be reversed.
		StringBuilder builder = new StringBuilder();
		builder.append("abc");
		builder.reverse();
		System.out.println(builder);
	}
}
```
Вывод
<p style="background-color: navy; color: yellow">cba</p>

StringBuilder намного быстрее делает добавление, чем String. Для добавления String требуется значительное время(251 мс), а для добавления StringBuilder требуется менее 1 мс.
```java
import java.lang.StringBuilder;

public class Program {
	public static void main(String[] args) {
		long t1 = System.currentTimeMillis();
		// Version 1: add to string.
		String value = "";
		for (int i = 0; i < 10000; i++) {
			value += Integer.toString(i) + ' ';
		}
		long t2 = System.currentTimeMillis();
		// Version 2: append to StringBuilder.
		StringBuilder builder = new StringBuilder();
		for (int i = 0; i < 10000; i++) {
			builder.append(i).append(' ');
		}
		long t3 = System.currentTimeMillis();
		// ... Lengths are equal.
		System.out.println(value.length());
		System.out.println(builder.length());
		// ... Times.
		System.out.println(t2 - t1);
		System.out.println(t3 - t2);
	}
}
```
Результат
<p style="background-color: navy; color: yellow">48890<br>
48890<br>
251 ms, String + operator (20000 adds)<br>
0 ms, StringBuilder append (20000 calls)</p>

**Класс StringBuffer**

Есть еще один класс — `StringBuffer` — это аналог класса `StringBuilder`, только его методы имеют модификатор `synchronized`. А это значит, что к объекту `StringBuffer` можно одновременно обращаться из нескольких потоков.
Зато он работает гораздо медленнее, чем `StringBuilder`. 