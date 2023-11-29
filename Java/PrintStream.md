#Java #PrintStream
### Класс PrintStream ###

**PrintStream** является именно тем классом, который используется для вывода информации в консоль. Когда мы с помощью вызова System.out.println() пишем в консоль некоторую информацию, то тем самым используется PrintStream, так как переменная _out_ класса System представляет объект класса PrintStream, а метод println() - это метод класса PrintStream.

Но PrintStream можно использовать для записи информации в поток вывода. Например, запишем информацию в файл:
```java
import java.io.*;
...
String text = "Hello, World!"; // строка для записи
FileOutputStream fos = new FileOutputStream("C:/data.txt");
try {
    PrintStream printStream = new PrintStream(fos));
    printStream.println(text);
    System.out.println("Запись в файл выполнена");
} catch(IOException e) {
    System.out.println(e.getMessage());
}
```
В данном примере используется конструктор **PrintStream**, который в качестве параметра принимает поток вывода [FileOutputStream](FileOutputStream). Можно было бы также использовать конструктор с указанием названия файла для записи: PrintStream (String filename).

С помощью метода println() производится запись информации в выходной поток - то есть в объект [FileOutputStream](FileOutputStream). В случае с выводом на консоль с помощью System.out.println() в качестве потока вывода выступает консоль.

Для вывода информации в выходной поток **PrintStream** использует следующие методы:
- println(): вывод строковой информации с переводом строки
- print(): вывод строковой информации без перевода строки
- printf(): форматированный вывод

Следующий код показывает возможности использования форматированного вывода класса **PrintStream** :
```java
int i = 15;
printStream.printf("Квадрат числа %d равен %d \n", i, i*i);
```