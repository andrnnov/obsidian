### Java Scanner Class ###

#Java #ScannerClass

2023-09-04 15:13

Класс `java.util.Scanner`

 [Java Scanner Class](ScannerClassJava) cчитывает данные из источника, который ты для него укажешь. Например, из строки, из файла, из консоли. Далее он распознает эту информацию и обрабатывает нужным образом.

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