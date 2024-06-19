### Разница между классом Scanner и BufferedReader в Java ###

#Java #ScannerClass #BufferedReader 

2023-09-06 12:52

В Java класс  Scanner и BufferedReader являются исходными текстами, которые служат способами чтения входных данных. [Класс Scanner](ScannerClassJava) - это простой сканер текста, который может анализировать примитивные типы и строки. Он внутренне использует регулярные выражения для чтения различных типов, в то время как, с другой стороны, [класс BufferedReader](BufferedReader) считывает текст из потока ввода символов, буферизуя символы, чтобы обеспечить эффективное чтение последовательности символов

Эксцентричное различие заключается в чтении различных способов приема входных данных с помощью метода next(), который оправдан в приведенных ниже программах, поверх аналогичного набора входных данных.

```java
import java.util.Scanner;

class GFG {
    public static void main(String args[])
    {
        Scanner scn = new Scanner(System.in);
        System.out.println("Enter an integer & a String");
        int a = scn.nextInt();
        String b = scn.nextLine();
        System.out.printf("You have entered:- " + a + " " + "and name as " + b);
    }
}
```
**Вывод:**
==Enter an integer & a String
10 John
You have entered:- 10 and name as  John==

Давайте попробуем то же самое, используя класс BufferedReader и тот же ввод, приведенный ниже, следующим образом:

```java
import java.io.*;
 
class GFG {
    public static void main(String args[])
        throws IOException
    {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        System.out.println("Enter an integer");
        int a = Integer.parseInt(br.readLine());
        System.out.println("Enter a String"); 
        String b = br.readLine();
        System.out.printf("You have entered:- " + a + " and name as " + b);
    }
}
```
**Вывод:**
==Enter an integer  
10
Enter a String
John
You have entered:- 10 and name as  John

В классе Scanner, если мы вызываем nextLine() после любого из семи _методов nextXXX(),_ то nextLine() не считывает значения с консоли, и курсор не попадет в консоль, он пропустит этот шаг. Методами nextXXX() являются nextInt(), nextFloat(), nextByte(), nextShort(), nextDouble(), nextLong(), next().

```java
import java.util.Scanner;
class Differ
 {
     public static void main(String args[])
     {
         Scanner scn = new Scanner(System.in);
         System.out.println("Enter an integer");
         int a = scn.nextInt();
         scn.nextLine();
         System.out.println("Enter a String");
         String b = scn.nextLine();
         System.out.printf("You have entered:- " + a + " " + "and name as " + b);
     }
}
```

В классе BufferReader такого типа проблем нет. Эта проблема возникает только для класса Scanner из-за того, что методы nextXXX() игнорируют символ новой строки, а nextLine() считывает только до первого символа новой строки. Если мы используем еще один вызов метода nextLine() между nextXXX() и nextLine(), то эта проблема не возникнет, потому что nextLine() будет использовать символ новой строки.

**Ниже приведены основные различия между классом Scanner и BufferedReader в Java**

- BufferedReader является синхронным, в то время как Scanner - нет. BufferedReader следует использовать, если мы работаем с несколькими потоками.
- BufferedReader имеет значительно больший объем буферной памяти, чем Scanner.
- У сканера небольшой буфер (1 КБ буфера символов) в отличие от BufferedReader (8 КБ байтового буфера), но этого более чем достаточно.
- BufferedReader работает немного быстрее по сравнению со Scanner, потому что сканер выполняет синтаксический анализ входных данных, а BufferedReader просто считывает последовательность символов.