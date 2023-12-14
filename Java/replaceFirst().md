#Java #Regex #replaceFirst
### Метод replaceFirst() ###

2023-12-14 11:26
#### Описание ####

**Метод replaceFirst()** – заменяет первую подстроку данной строки, которая соответствует заданному регулярному выражению, с данной заменой, другими словами – метод в Java позволяет заменить первое вхождение слова или словосочетания в строке.
#### Синтаксис ####

Синтаксис метода:
```java
public String replaceFirst(String regex, String replacement)
```
#### Параметры ####

Подробная информация о параметрах:
- regex – регулярное выражение, которому данная строка должна соответствовать;
- replacement – строка, которая заменит найденное выражение.
#### Возвращаемое значение ####

- В Java replaceFirst() возвращает результирующую строку.
#### Пример ####
```java
import java.io.*;

public class Test{
   public static void main(String args[]){
      String Str1 = new String("Добро пожаловать на ProgLang.su");

      System.out.print("Возвращаемое значение: ");
      System.out.println(Str1.replaceFirst("(.*)ProgLang(.*)", "IAMGROOT" ));

      System.out.print("Возвращаемое значение: ");
      System.out.println(Str1.replaceFirst("ProgLang.su", "IAMGROOT"));
      
      String Str2 = new String("Добро пожаловать на ProgLang.su! Добро пожаловать на ProgLang.su!");
      
      System.out.print("Возвращаемое значение: " );
      System.out.println(Str2.replaceFirst("Добро пожаловать на ProgLang.su!", "IAMGROOT!"));
   }
}
```
Получим следующий результат:
<p style="background-color: navy; color: yellow">Возвращаемое значение: IAMGROOT<br>
Возвращаемое значение: Добро пожаловать на IAMGROOT<br>
Возвращаемое значение: IAMGROOT! Добро пожаловать на ProgLang.su!</p>
