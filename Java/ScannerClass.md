## Java Scanner Class 

#Java #ScannerClass

2023-09-04 15:13

### Метод Java [Scanner](ScannerClassJava).close()

#### Описание

Метод **java Scanner close()** закрывает этот сканер. Если этот сканер еще не был закрыт, то, если его базовый readable также реализует интерфейс [Closeable](Closeable), будет вызван метод close readable. Если этот сканер уже закрыт, то вызов этого метода не будет иметь никакого эффекта.

#### Объявление

Ниже приводится объявление для **java.util.Scanner.close()** метод
```java
public void close()
```

#### Параметры

NA

#### Возвращаемое значение

Этот метод не возвращает никакого значения.

#### Исключение

NA

#### Закрытие сканера на примере строки

В следующем примере показано использование метода Java Scanner close() для закрытия сканера. Мы создали объект scanner, используя заданную строку. Затем мы напечатали строку с помощью метода nextLine(), а затем сканер закрывается с помощью метода close().
```java
import java.util.Scanner;

public class ScannerDemo {
   public static void main(String[] args) {
      String s = "Hello World! 3 + 3.0 = 6";
      // create a new scanner with the specified String Object
      Scanner scanner = new Scanner(s);
      // print the next line of the string
      System.out.println(scanner.nextLine());
      // close the scanner
      System.out.println("Closing Scanner...");  
      scanner.close();
      System.out.println("Scanner Closed.");
   }
}
```
**Вывод:**
<p style="background-color: navy; color: yellow">
Hello World! 3 + 3.0 = 6<br>
Closing Scanner...<br>
Scanner Closed.</p>

#### Примера. Закрытие сканера при вводе пользователем.

В следующем примере показано использование метода Java Scanner close() для закрытия сканера. Мы создали объект scanner с помощью System.in. Затем мы напечатали строку с помощью метода nextLine(), а затем сканер закрывается с помощью метода close().
```java
import java.util.Scanner;
public class ScannerDemo {
    public static void main(String[] args) {
		// create a new scanner with the system input
		Scanner scanner = new Scanner(System.in);
	    // print the next line of the string
	    System.out.println(scanner.nextLine());
	    // close the scanner
	    System.out.println("Closing Scanner...");  
	    scanner.close();
	    System.out.println("Scanner Closed.");
   }
}
```
**Ввод:**
<p style="background-color: navy; color: yellow">
Hello World</p>
**Вывод:**
<p style="background-color: navy; color: yellow">
Hello World<br>
Closing Scanner...<br>
Scanner Closed.</p>

#### Пример. Закрытие сканера в файле свойств.

В следующем примере показано использование метода Java Scanner close() для закрытия сканера. Мы создали объект scanner с помощью файла properties.txt. Затем мы распечатали содержимое с помощью метода nextLine (), а затем сканер закрывается с помощью метода close ().
```java
import java.io.File;
import java.io.FileNotFoundException;
importjava.util.Scanner;

public class ScannerDemo {
	public static void main(String[] args) throws FileNotFoundException {
		// create a new scanner with a file as input
	    Scanner = new Scanner(new File("properties.txt"));
	    // print the next line of the string
	    System.out.println(scanner.nextLine());
	    // close the scanner
	    System.out.println("Closing Scanner...");  
	    scanner.close();
	    System.out.println("Scanner Closed.");
   }
}
```
Содержимое файла properties.txt:
```
Height=200
Width=120
```
**Вывод:**
<p style="background-color: navy; color: yellow">
Height=200<br>
Closing Scanner...<br>
Scanner Closed.</p>

### Метод Java Scanner.delimiter()

#### Описание

Метод **java Scanner delimiter()** возвращает шаблон, который в данный момент использует этот сканер для сопоставления разделителей.

#### Объявление

Ниже приводится объявление для java.util.Scanner.delimiter() метод
```java
public Pattern delimiter()
```

#### Параметры

NA

#### Возвращаемое значение

Этот метод возвращает шаблон разделения данного сканера.

#### Исключение

NA

#### Получение разделителя, используемого Scanner, на примере строки

В следующем примере показано использование метода Java Scanner delimiter() для печати разделителя, используемого объектом Scanner. Мы создали объект Scanner, используя заданную строку. Затем мы напечатали строку с помощью метода scanner.nextLine(), а затем разделитель, используемый сканером, печатается с помощью метода delimiter().
```java
import java.util.Scanner;

public class ScannerDemo {
	public static void main(String[] args) {
    String s = "Hello World! 3 + 3.0 = 6";
    // create a new scanner with the specified String Object
    Scanner scanner = new Scanner(s);
    // print the next line of the string
    System.out.println(scanner.nextLine());
    // print the delimiter this scanner is using
    System.out.println(scanner.delimiter());
	// close the scanner  
	scanner.close();
	}
}
```
**Вывод:**
<p style="background-color: navy; color: yellow">
Hello World! 3 + 3.0 = 6<br>
\p{javaWhitespace}+</p>

#### Получение пользовательского разделителя, используемого Scanner, на примере строки

В следующем примере показано использование метода Java Scanner delimiter() для печати разделителя, используемого объектом Scanner. Мы создали объект Scanner, используя заданную строку и заданный разделитель. Затем мы напечатали строку с помощью метода scanner.nextLine(), а затем разделитель, используемый сканером, печатается с помощью метода delimiter().
```java
import java.util.Scanner;

public class ScannerDemo {
	public static void main(String[] args) {
    String input = "1 abc 2 abc";
    Scanner scanner = new Scanner(input).useDelimiter("\\s*abc\\s*");
    System.out.println(scanner.nextInt());
    System.out.println(scanner.nextInt());
    // print the delimiter this scanner is using
    System.out.println(scanner.delimiter());
    // close the scanner
    scanner.close();
   }
}
```
**Вывод:**
<p style="background-color: navy; color: yellow">
1<br>
2<br>
\s*abc\s*</p>

#### Получение разделителя, используемого сканером, в примере пользовательского ввода

В следующем примере показано использование метода Java Scanner delimiter() для печати разделителя, используемого объектом scanner . Мы создали объект scanner с помощью System.in. Затем мы напечатали строку с помощью метода scanner.nextLine(), а затем разделитель, используемый сканером, печатается с помощью метода delimiter().
```java
import java.util.Scanner;  

public class ScannerDemo {  
    public static void main(String[] args) {  
        String s = "Hello World! 3 + 3.0 = 6";  
        // create a new scanner with the specified String Object  
        Scanner scanner = new Scanner(System.in);  
        // print the next line of the string  
        System.out.println(scanner.nextLine());  
        // print the delimiter this scanner is using  
        System.out.println(scanner.delimiter());  
        // close the scanner  scanner.close();  
    }  
}
```
**Ввод:**
```
Hello World
```
**Вывод:**
<p style="background-color: navy; color: yellow">
Hello World<br>
\p{javaWhitespace}+</p>

#### Метод boolean hasNext() - возвращает true, если во входных данных присутствует другой токен

```java
Scanner scanner = new Scanner(System.in);  
if (scanner.hasNext()) {  
    String input = scanner.next();  
    System.out.println("Input: " + input);  
}
```

#### Метод boolean hasNextLine() - возвращает true, если во входных данных есть другая строка

```java
Scanner scanner = new Scanner("Hello,\nworld!");  
if (scanner.hasNextLine()) {  
    System.out.println("Found next line: " + scanner.nextLine()); // Output: Found next line: Hello,  
}
```

#### Метод String next() - возвращает следующий токен во входных данных в виде строки

```java
Scanner scanner = new Scanner("Hello, world!");  
String word = scanner.next();  
System.out.println(word); // Output: Hello,
```

#### Метод useLocale(Locale locale) - Устанавливает локаль сканера в указанную локаль

```java
Scanner scanner = new Scanner("1.234,56");  
scanner.useLocale(Locale.GERMAN);  
double num = scanner.nextDouble(); // num = 1234.56
```

#### Метод useRadix(int radix) - устанавливает систему счисления сканера

```java
Scanner scanner = new Scanner("FF");  
scanner.useRadix(16);  
int num = scanner.nextInt(); // num = 255
```

#### Метод `Stream<MatchResult>` findAll(Pattern pattern) - возвращает поток результатов сопоставления, соответствующих указанному шаблону регулярных выражений.

```java
Scanner scanner = new Scanner("Hello, World!");  
Pattern pattern = Pattern.compile("\\w+");  
scanner.findAll(pattern).forEach(matchResult -> System.out.println(matchResult.group()));  
// Output: Hello World
```

#### Метод String nextLine() in Java - возвращает следующую строку входных данных в виде строки

```java
Scanner scanner = new Scanner("Hello,\nworld!");  
String line = scanner.nextLine();  
System.out.println(line); // Output: Hello,
```

#### Метод Double nextDouble() - возвращает следующий токен во входных данных как double

```java
Scanner scanner = new Scanner(System.in);  
System.out.print("Enter a double value: ");  
double input = scanner.nextDouble();  
System.out.println("Input value: " + input);
```

#### Метод boolean nextBoolean() - возвращает следующий токен во входных данных как логическое значение

```java
Scanner scanner = new Scanner(System.in);  
System.out.print("Enter a boolean value (true/false): ");  
boolean input = scanner.nextBoolean();  
System.out.println("Input value: " + input);
```

#### Метод byte nextByte() - возвращает следующий токен во входных данных в виде байта

```java
Scanner scanner = new Scanner(System.in);  
System.out.print("Enter a byte value: ");  
byte input = scanner.nextByte();  
System.out.println("Input value: " + input);
```

#### Метод short nextShort() - возвращает следующий токен во входных данных как short

```java
Scanner scanner = new Scanner(System.in);  
System.out.println("Enter a short value: ");  
short num = scanner.nextShort();  
System.out.println("The entered short value is " + num);
```
#### Метод long nextLong() - возвращает следующий токен во входных данных как long

```java
Scanner scanner = new Scanner(System.in);  
System.out.println("Enter a long value: ");  
long num = scanner.nextLong();  
System.out.println("The entered long value is " + num);
```
#### Метод float nextFloat() - возвращает следующий токен во входных данных в виде числа с плавающей точкой

```java
Scanner scanner = new Scanner(System.in);  
System.out.print("Enter a float value: ");  
float input = scanner.nextFloat();  
System.out.println("Input value: " + input);
```
#### Метод Scanner useDelimiter() - устанавливает разделитель для синтаксического анализа входных данных.

```java
Scanner scanner = new Scanner("Hello,world!");  
scanner.useDelimiter(",");  
System.out.println(scanner.next()); // Output: Hello  
System.out.println(scanner.next()); // Output: world!
```

#### Метод Scanner skip() - пропускает входные данные, соответствующие указанному шаблону

```java
Scanner scanner = new Scanner("1,2,3,4,5");  
scanner.useDelimiter(",");  
while (scanner.hasNext()) {  
    if (scanner.hasNextInt()) {  
        int num = scanner.nextInt();  
        System.out.println(num);  
    } else {  
        scanner.skip(",");  
    }  
}
```

#### Метод findInLine() - выполняет поиск следующего вхождения указанного шаблона в текущей строке ввода

```java
Scanner scanner = new Scanner("Hello, 123, world!");  
String match = scanner.findInLine("\\d+");  
System.out.println(match); // Output: 123  
Scanner scanner = new Scanner("The quick brown fox jumps over the lazy dog.");  
String result = scanner.findInLine("fox");  
System.out.println(result); // Output: fox
```

#### Метод findWithinHorizon(String pattern, int horizon) - выполняет поиск следующего появления указанного шаблона во входных данных до указанного горизонта

```java
Scanner scanner = new Scanner("abc123def456");  
System.out.println(scanner.findWithinHorizon("\\d+", 3));  
// Output: null (pattern not found within horizon of 3 characters)
```
#### Метод hasNextByte() - возвращает true, если у сканера есть другой токен, представляющий собой байт.

```java
Scanner scanner = new Scanner(System.in);  
if (scanner.hasNextByte()) {  
    byte b = scanner.nextByte();  
    System.out.println("Byte: " + b);  
}
```

#### Метод MatchResult match() - возвращает MatchResult для последней операции сопоставления

```java
Scanner scanner = new Scanner(System.in);  
System.out.print("Enter a string: ");  
String input = scanner.next();  
scanner.useDelimiter("[aeiou]");  
scanner.next();  
MatchResult result = scanner.match();  
System.out.println("Last match: " + result.group());
```

#### Метод ioException() - возвращает исключение IOException, последнее вызванное базовым Readable сканера

```java
Scanner scanner = new Scanner(new java.io.FileReader("nonexistent.txt"));  
try {  
    while (scanner.hasNextLine()) {  
        System.out.println(scanner.nextLine());  
    }  
} catch (java.util.NoSuchElementException e) {  
    if (scanner.ioException() == null) {  
        System.out.println("Scanner is still valid, but there is no more input");  
    } else {  
        System.out.println("Scanner is invalid due to an IOException: " + scanner.ioException().getMessage());  
    }  
}  
// Output: Scanner is invalid due to an IOException: null (file not found)
```

#### Метод delimiter() - возвращает шаблон, который в данный момент использует этот сканер для сопоставления разделителей

```java
Scanner scanner = new Scanner(System.in);  
System.out.print("Enter a string with multiple words: ");  
String input = scanner.nextLine();  
scanner.useDelimiter("\\s");  
while (scanner.hasNext()) {  
    System.out.println("Word: " + scanner.next());  
}
```

#### Метод Locale locale() - возвращает языковой стандарт данного сканера

```java
Scanner scanner = new Scanner("one deux trois");  
scanner.useLocale(Locale.FRENCH);  
while (scanner.hasNext()) {  
    System.out.println(scanner.next());  
}  
// Output: one  
//         deux  
//         trois  
System.out.println(scanner.locale());  
// Output: fr_FR
```

#### Метод radix() - возвращает radix по умолчанию для синтаксического анализа целых чисел

```java
Scanner scanner = new Scanner(System.in);  
scanner.useRadix(16);  
System.out.println("Enter a hexadecimal number: ");  
int num = scanner.nextInt();  
System.out.println("The entered hexadecimal number is " + num);
```

#### Метод Scanner reset() - возвращает сканер в исходное состояние

```java
Scanner scanner = new Scanner(System.in);  
System.out.print("Enter a string with multiple words: ");  
String input = scanner.nextLine();  
scanner.useDelimiter("\\s");  
while (scanner.hasNext()) {  
    System.out.println("Word: " + scanner.next());  
}  
scanner.reset();  
System.out.println("Original delimiter: " + scanner.delimiter());
```

#### Метод String toString() - возвращает строковое представление объекта scanner

```java
Scanner scanner = new Scanner("hello world");  
System.out.println(scanner.toString());
```

#### Метод tokens() - возвращает итератор по токенам во входных данных


```java
Scanner scanner = new Scanner(System.in);  
System.out.print("Enter a string with multiple words: ");  
String input = scanner.nextLine();  
scanner.useDelimiter("\\s");  
Iterator<String> tokens = scanner.tokens();  
while (tokens.hasNext()) {  
    System.out.println("Token: " + tokens.next());  
}
```

#### Метод void remove() - удаляет текущий токен из входных данных

```java
Scanner scanner = new Scanner("apple orange banana");  
while (scanner.hasNext()) {  
    String fruit = scanner.next();  
    System.out.println(fruit);  
    if (fruit.equals("orange")) {  
        scanner.remove();  
        System.out.println("Removed " + fruit);  
    }  
}
```

#### Метод hasNextBigDecimal() - возвращает true, если во входных данных присутствует другой токен, и он может быть интерпретирован как BigDecimal

```java
Scanner scanner = new Scanner(System.in);  
if (scanner.hasNextBigDecimal()) {  
    BigDecimal decimal = scanner.nextBigDecimal();  
    System.out.println("Decimal: " + decimal);  
}
```

#### Метод nextBigDecimal() - возвращает следующий токен во входных данных в виде BigDecimal

```java
Scanner scanner = new Scanner(System.in);  
System.out.print("Enter a BigDecimal value: ");  
BigDecimal input = scanner.nextBigDecimal();  
System.out.println("Input value: " + input);
```

#### Метод hasNextBigInteger() - возвращает true, если во входных данных присутствует другой токен, и он может быть интерпретирован как [BigInteger](BigInteger)

```java
Scanner scanner = new Scanner(System.in);  
if (scanner.hasNextBigInteger()) {  
    BigInteger integer = scanner.nextBigInteger();  
    System.out.println("Integer: " + integer);  
}
```

#### Метод nextBigInteger() - возвращает следующий токен во входных данных как [BigInteger](BigInteger)

```java
Scanner scanner = new Scanner(System.in);  
System.out.print("Enter a BigInteger value: ");  
BigInteger input = scanner.nextBigInteger();  
System.out.println("Input value: " + input);
```

#### Метод hasNextBoolean() - возвращает true, если у сканера есть другой логический токен

```java
Scanner scanner = new Scanner(System.in);  
if (scanner.hasNextBoolean()) {  
    boolean bool = scanner.nextBoolean();  
    System.out.println("Boolean: " + bool);  
}
```

#### Метод hasNextPattern() - возвращает true, если следующий токен во входных данных соответствует указанному шаблону

```java
Scanner scanner = new Scanner(System.in);  
System.out.print("Enter a string: ");  
String str = scanner.next();  
if (scanner.hasNextPattern("\\d+")) {  
    int num = scanner.nextInt();  
    System.out.println("The entered string is: " + str + " and the number is: " + num);  
} else {  
    System.out.println("The entered string is: " + str);  
}
```

#### Метод nextInt() in Java- возвращает следующий токен во входных данных как int

```java
Scanner scanner = new Scanner(System.in);  
System.out.println("Enter an integer: ");  
int num = scanner.nextInt();  
System.out.println("The entered integer is " + num);
```

#### Метод hasNextDouble() - возвращает true, если во входных данных присутствует другой токен, и он может быть интерпретирован как double

```java
Scanner scanner = new Scanner(System.in);  
if (scanner.hasNextDouble()) {  
    double d = scanner.nextDouble();  
    System.out.println("Double: " + d);  
}
```

#### Метод hasNextFloat() - возвращает true, если во входных данных присутствует другой токен, который может быть интерпретирован как значение с плавающей точкой

```java
Scanner scanner = new Scanner(System.in);  
if (scanner.hasNextFloat()) {  
    float f = scanner.nextFloat();  
    System.out.println("Float: " + f);  
}
```

#### Метод hasNextInt() - возвращает true, если во входных данных присутствует другой токен, и он может быть интерпретирован как int

```java
Scanner scanner = new Scanner(System.in);  
if (scanner.hasNextInt()) {  
    int i = scanner.nextInt();  
    System.out.println("Int: " + i);  
}
```

#### Метод hasNextLong() - возвращает true, если во входных данных присутствует другой токен, который может быть интерпретирован как long

```java
Scanner scanner = new Scanner(System.in);  
System.out.print("Enter a long value: ");  
if (scanner.hasNextLong()) {  
    long value = scanner.nextLong();  
    System.out.println("You entered: " + value);  
} else {  
    System.out.println("Invalid input");  
}
```

#### Метод hasNextShort - возвращает true, если следующий токен во входных данных этого сканера может быть интерпретирован как короткое значение в базе данных по умолчанию с использованием nextShort() метода.

```java
Scanner scanner = new Scanner(System.in);  
if (scanner.hasNextShort()) {  
 short s = scanner.nextShort();  
 System.out.println("Short : " + s);  
}
```


### Методы

Метод **`nextLine()`** обращается к источнику данных, находит там следующую строку, которую он еще не считывал и возвращает ее.

```java
import java.util.Scanner;

public class Main {

   public static void main(String[] args) {

       Scanner scanner = new Scanner("Люблю тебя, Петра творенье,\n" +
               "Люблю твой строгий, стройный вид,\n" +
               "Невы державное теченье,\n" +
               "Береговой ее гранит");
       String s = scanner.nextLine();
       System.out.println(s);
   }
}
```

Метод **`nextInt()`** считывает и возвращает введенное число.

```java
ublic class Main {
   public static void main(String[] args) {
       Scanner sc = new Scanner(System.in);
       System.out.println("Введите число:");
       int number = sc.nextInt();
       System.out.println("Спасибо! Вы ввели число " + number);
   }
}
```
**`hasNextInt()`** — метод проверяет, является ли следующая порция введенных данных числом, или нет (возвращает, соответственно, true или false).
**`hasNextLine()`** — проверяет, является ли следующая порция данных строкой. 
**`hasNextByte()`**, **`hasNextShort()`**, **`hasNextLong()`**, **`hasNextFloat()`**, **`hasNextDouble()`** — все эти методы делают то же для остальных типов данных.

```java
public class Main {

   public static void main(String[] args) {

       Scanner sc = new Scanner(System.in);
       System.out.println("Введите число:");

       if (sc.hasNextInt()) {
           int number = sc.nextInt();
           System.out.println("Спасибо! Вы ввели число " + number);
       } else {
           System.out.println("Извините, но это явно не число. Перезапустите программу и попробуйте снова!");
       }

   }
}
```

В метод **`useDelimiter()`** передается строка, которую вы хотите использовать в качестве разделителя.

```java
public class Main {  
    public static void main(String[] args) {  
        String[] stih = new String[] {"Люблю тебя, Петра творенье,",  
                "Люблю твой строгий, стройный вид,",  
                "Невы державное теченье,",  
                "Береговой ее гранит"};  
                
        List list = new ArrayList<String>();  
        for (String line: stih) {  
            list.add(line);  
        }
	    for (String line: stih) {  
            Scanner sc = new Scanner(line);  
            sc.useDelimiter("\\n");  
            System.out.println(sc.next());  
            sc.close();  
        }  
    }  
}
```

Как и любой объект, работающий с потоками ввода-вывода, сканер должен быть закрыт по завершении своей работы, чтобы больше не потреблять ресурсы нашего компьютера. Никогда не забывай о методе **`close()`**!