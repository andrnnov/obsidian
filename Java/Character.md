#Java #Character

## Класс Character в Java

2024-07-08 14:43

В Java **_Character_** – это специальный "контейнер" для хранения одного символа, например, буквы или цифры. Он помогает работать с текстом, используя мощь Юникода, чтобы понимать и представлять символы со всего мира.

**_Character_** решает проблему представления и манипуляции символами в программировании. Он позволяет не только хранить символы, но и проводить с ними различные операции: проверять, является ли символ буквой или цифрой, изменять регистр и многое другое. Это делает работу с текстом гибкой и мощной.

Это упрощает написание программ, делая их более универсальными и международными. Понимание того, как работать с **_Character_** и Юникодом, позволяет создавать программы, способные обрабатывать текст на любом языке. Это открывает двери для глобальных проектов и приложений, доступных пользователям по всему миру.

Создание объекта **_Character_**:
```java
Character ch = new Character('a');
```

### Методы класса Character

**1. boolean isLetter(char ch):** Этот метод используется для определения того, является ли указанное значение символа (ch) буквой или нет. Метод вернет true, если это буква `([AZ],[az])`, в противном случае вернет false. Вместо символа мы также можем передать значение ASCII в качестве аргумента.

**Синтаксис:** 
```java
boolean isLetter(char ch);
```
**Пример:**
```java
// Java program to demonstrate isLetter() method 
  
public class Test { 
    public static void main(String[] args) { 
        System.out.println(Character.isLetter('A')); 
        System.out.println(Character.isLetter('0')); 
    } 
}
```
**Вывод:**
<p style="background-color: navy; color: yellow>">
true<br>
false</p>

**2. boolean isDigit(char ch):** этот метод используется для определения того, является ли указанное значение char (ch) цифрой или нет. Здесь мы также можем передать значение ASCII в качестве аргумента.

**Синтаксис:**
```java
boolean isDigit(char ch);
```
**Пример:**
```java
// Java program to demonstrate isDigit() method 
  
public class Test { 
    public static void main(String[] args) { 
        // print false as A is character 
        System.out.println(Character.isDigit('A')); 
        System.out.println(Character.isDigit('0')); 
    } 
}
```
**Вывод:**
<p style="background-color: navy; color: yellow>">
false<br>
true</p>

**3. boolean isWhitespace(char ch):** определяет, является ли указанное значение char (ch) пробелом. Пробелы включают пробел, табуляцию или новую строку.

**Синтаксис:** 
```java
boolean isWhitespace(char ch);
```
**Пример:**
```java
// Java program to demonstrate isWhitespace() method 
  
public class Test { 
    public static void main(String[] args) { 
        System.out.println(Character.isWhitespace('A')); 
        System.out.println(Character.isWhitespace(' ')); 
        System.out.println(Character.isWhitespace('\n')); 
        System.out.println(Character.isWhitespace('\t')); 
        // ASCII value of tab 
        System.out.println(Character.isWhitespace(9)); 
        System.out.println(Character.isWhitespace('9')); 
    } 
}
```
**Вывод:**
<p style="background-color: navy; color: yellow>">
false<br>
true<br>
true<br>
true<br>
true<br>
false</p>

**4. boolean isUpperCase(char ch):** определяет, является ли указанное значение char (ch) прописными буквами или нет.

**Синтаксис:** 
```java
boolean isUpperCase(char ch);
```
**Пример:**
```java
// Java program to demonstrate isUpperCase() method 
  
public class Test { 
    public static void main(String[] args) { 
        System.out.println(Character.isUpperCase('A')); 
        System.out.println(Character.isUpperCase('a')); 
        System.out.println(Character.isUpperCase(65)); 
    } 
}
```
**Вывод:**
<p style="background-color: navy; color: yellow>">
true<br>
false<br>
true</p>

**5. boolean isLowerCase(char ch):** определяет, является ли указанное значение char (ch) строчной буквой или нет.

**Синтаксис:**
```java
boolean isLowerCase(char ch);
```
**Пример:**
```java
// Java program to demonstrate isLowerCase() method 
  
public class Test { 
    public static void main(String[] args) { 
        System.out.println(Character.isLowerCase('A')); 
        System.out.println(Character.isLowerCase('a')); 
        System.out.println(Character.isLowerCase(97)); 
    } 
}
```
**Вывод:**
<p style="background-color: navy; color: yellow>">
false<br>
true<br>
true</p>

**6. char toUpperCase(char ch):** возвращает верхний регистр указанного значения char (ch). Если передается значение ASCII, то будет возвращено значение ASCII в верхнем регистре.

**Синтаксис:**
```java
char toUpperCase(char ch);
```
**Пример:**
```java
// Java program to demonstrate toUpperCase() method 
  
public class Test { 
    public static void main(String[] args) { 
        System.out.println(Character.toUpperCase('a')); 
        System.out.println(Character.toUpperCase(97)); 
        System.out.println(Character.toUpperCase(48)); 
    } 
}
```
**Вывод:**
<p style="background-color: navy; color: yellow>">
А<br>
65<br>
48</p>

**7. char toLowerCase(char ch):** возвращает нижний регистр указанного значения char(ch).

**Синтаксис:**
```java
char toLowerCase(char ch);
```
**Пример:**
```java
// Java program to demonstrate toLowerCase() method 
  
public class Test { 
    public static void main(String[] args) { 
        System.out.println(Character.toLowerCase('A')); 
        System.out.println(Character.toLowerCase(65)); 
        System.out.println(Character.toLowerCase(48)); 
    } 
}
```
**Вывод:**
<p style="background-color: navy; color: yellow>">
а<br>
97<br>
48</p>

**8. toString(символ ch):** возвращает объект класса String, представляющий указанное значение символа (ch), т. е. строку из одного символа. Здесь мы **не можем** передать значение ASCII.

**Синтаксис:**
```java
String toString(char ch);
```
**Пример:**
```java
// Java program to demonstrate toLowerCase() method 
  
// Java program to demonstrate toString() method 
  
public class Test { 
    public static void main(String[] args) { 
        System.out.println(Character.toString('x')); 
        System.out.println(Character.toString('Y')); 
    } 
}
```
**Вывод:**
<p style="background-color: navy; color: yellow>">
x<br>
Y</p>

#### Пример

Представьте, что вы разрабатываете программу для обработки текстовых сообщений, и вам нужно убедиться, что все предложения начинаются с заглавной буквы, а остальные символы остаются строчными. В этом случае класс **_Character_** в Java становится вашим надежным помощником.

Давайте рассмотрим простой пример кода, который решает эту задачу:
```java
public class CapitalizeSentence {
    public static void main(String[] args) {
        String message = "привет! как дела? это новая программа.";
        StringBuilder capitalizedMessage = new StringBuilder();

        // Флаг, указывающий, что следующий символ должен быть заглавным
        boolean capitalizeNext = true;

        for (char ch : message.toCharArray()) {
            if (capitalizeNext && Character.isLetter(ch)) {
                capitalizedMessage.append(Character.toUpperCase(ch));
                capitalizeNext = false;
            } else {
                capitalizedMessage.append(Character.toLowerCase(ch));
            }

            // Если текущий символ – точка, восклицательный или вопросительный знак, следующий символ должен быть заглавным
            if (ch == '.' || ch == '!' || ch == '?') {
                capitalizeNext = true;
            }
        }

        System.out.println(capitalizedMessage.toString());
    }
}
```
В этом примере мы используем методы Character.isLetter(ch) для проверки, является ли текущий символ буквой, и Character.toUpperCase(ch) для преобразования буквы в верхний регистр. Это позволяет нам легко и эффективно обрабатывать текст, гарантируя, что каждое предложение начинается с заглавной буквы.

Этот пример демонстрирует, как класс **_Character_** и его методы могут быть использованы для решения реальных задач по обработке текста, делая код более читаемым и удобным в обслуживании.

### Основы работы с символами

В мире Java, **char** и **_Character_** играют ключевые роли в обработке и представлении текстовых данных. **_char_** – это примитивный тип данных, который может хранить одиночный символ, в то время как **_Character_** – это полноценный класс, который обертывает `char` в объект, предоставляя множество полезных методов для работы с символами. Это позволяет не только хранить символы, но и проводить с ними различные операции, такие как проверка на принадлежность к определенной категории (буква, цифра, пробел и т.д.), преобразование регистра и многое другое.

**Автоматическая упаковка и распаковка** упрощает преобразование между `char` и `Character`, позволяя разработчикам сосредоточиться на логике программы, а не на технических деталях преобразования типов.

### Юникод: объединяющий языки мира в Java

**Юникод** играет важную роль в Java, позволяя программам работать с текстом на любом языке мира. Это достигается благодаря тому, что `char` в Java является 16-битным типом данных, что позволяет представлять символы из **Базовой Многоязыковой Плоскости (BMP)** Юникода. Однако, для представления символов за пределами BMP используются **суррогатные пары**, расширяя возможности представления символов до более чем миллиона кодовых точек Юникода.

### За границами BMP: суррогатные пары и кодовые точки

**Суррогатные пары** и **кодовые точки** позволяют Java работать с символами, которые не умещаются в стандартный 16-битный размер `char`. Это особенно важно для работы с историческими текстами, эмодзи и символами, используемыми в различных культурных и языковых контекстах. Использование методов класса `Character` для работы с кодовыми точками обеспечивает поддержку полного спектра символов Юникода, делая Java идеальным выбором для глобальных и многоязычных приложений.


