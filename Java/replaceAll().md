#Java #Regex #replaceAll
### Java – Метод replaceAll() ###

2023-12-14 11:34
### Описание ###

**Метод replaceAll()** – заменяет каждую подстроку данной строки, которая соответствует заданному регулярному выражению, с данной заменой, другими словами – метод позволяет заменить слово в строке.
### Синтаксис ###

Синтаксис метода:
```java
public String replaceAll(String regex, String replacement)
```
#### Параметры ####

Подробная информация о параметрах:
- regex – регулярное выражение, которому данная строка должна соответствовать;
- replacement – строка, которая заменит найденное выражение.

#### Возвращаемое значение ####
- В Java replaceAll() возвращает результирующую строку.
#### Пример ####
```java
import java.io.*;

public class Test{
   public static void main(String args[]){
      String Str = new String("Добро пожаловать на ProgLang.su");

      System.out.print("Возвращаемое значение: ");
      System.out.println(Str.replaceAll("(.*)ProgLang(.*)",
                         "IAMGROOT"));
      
      System.out.print("Возвращаемое значение: ");
      System.out.println(Str.replaceAll("ProgLang.su",
                         "сайт посвященный программированию!"));
   }
}
```
Получим следующий результат:
<p style="background-color: navy; color: yellow">Возвращаемое значение: IAMGROOT<br>
Возвращаемое значение: Добро пожаловать на сайт посвященный программированию!</p>
