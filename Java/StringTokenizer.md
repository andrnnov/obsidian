#Java #String #StringTokenizer

## Класс StringTokenizer

2024-05-03 14:18

Класс **_StringTokenizer_** пакета java.util предназначен для разложения строки на составляющие. Под токенацией понимается процесс разделения последовательности строки на части.

Будучи удобным в использовании, **_StringTokenizer_** имеет серьезные функциональные ограничения. Так _StringTokenizer_ раскладывает входную строку на части согласно переданных ему списка разделителей. Он не выполняет проверку на наличие разделителя внутри подстроки и не возвращает пустую строку нулевой длины, если во входном потоке обнаружена последовательность разделителей.

### Конструкторы класса StringTokenizer

Для создания экземпляра **_StringTokenizer_** можно использовать один из следующих конструкторов:

| Конструктор                                                     | Описание                                                                                                                                         |
| --------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| StringTokenizer(String str)                                     | Раскладывает строку на части, используя в качестве разделителя символы пробела " ", табуляции "\t", перевода строки "\n" и возврата каретки "\r" |
| StringTokenizer(String str, String delim)                       | Раскладывает строку на части, используя в качестве разделителя строку delim                                                                      |
| StringTokenizer(String str, String delim, boolean returnDelims) | Тоже что и предыдущий, но если returnDelims установлен в true, разделители также возвращаются в качестве части строки                            |
_**str**_ — разделяемая на лексемы строка, _**delim**_ — набор разделителей, _**returnDelims**_ — возвращать ли символы разделители в виде отдельных лексем (по умолчанию не возвращаются).
Если строка "str" не определена, т.е. равна null, то вызывается исключение **NullPointerException**.

Пример использования класса _StringTokenizer_
```java
String s;
s = "Тестовая строка, используемая для разложения на слова";
StringTokenizer st = new StringTokenizer(s, " \t\n\r,.");
while (st.hasMoreTokens()) {
    // Выводим лексемы в консоль
    System.out.println(st.nextToken());
}
```

### Методы класса StringTokenizer, countTokens, hasMoreTokens, nextToken

| Метод                          | Описание                                                                                                                     |
| ------------------------------ | ---------------------------------------------------------------------------------------------------------------------------- |
| int countTokens()              | Определение количества лексем, прежде, чем будет сгенеририровано исключение в результате вызова метода nextToken             |
| boolean hasMoreElements()      | Функция определения наличия лексем (элементов)                                                                               |
| boolean hasMoreTokens()        | Функция определения наличия лексем (элементов). Возвращает true, если в строке еще есть слова, и false, если слов больше нет |
| Object nextElement()           | Возвращает лексему в виде объекта типа [Object](Object), на который указывает токенайзер                                     |
| String nextToken()             | Возвращает лексему в виде объекта типа [String](String), на который указывает токенайзер                                     |
| String nextToken(String delim) | Возвращает лексему в виде объекта типа [String](String), на который указывает токенайзер согласно разделителя delim          |

## Особенности использования класса StringTokenizer

Первый конструктор с одним параметром str не выполняет проверку наличия в строке подстроки. Поэтому строка "Привет. Завтра \"21 сентября \" мы идем в театр." разбивается на следующие части:
```
[Привет., Завтра, "21, сентября, ", мы, идем, в, театр.]
// вместо
[Привет., Завтра, "21 сентября "  , мы, идем, в, театр.]
```
Второй конструктор не отслеживает последовательное появление разделителя во входном потоке. Поэтому если строку "book, author, publication,,,date published" разложить на части, используя в качестве разделителя символ запятой ",", то получим набор из 4-x слов
```
book, author, publication, date published 
```
вместо шести значений
```
book, author, publication, "", "", date published
```
, где "" означает строку нулевой длины.

Чтобы получить все шесть частей, необходимо использовать третий конструктор и установить параметр _returnDelims_ в true.

Особенность установки параметра _returnDelims_ в true, является очень важной. Особенно когда текстовые данные поступают динамически и их необходимо раскладывать на составляющие и записывать в базу данных. В этом случае необходимо получить значения для всех полей таблицы.

Третий конструктор не будет работать также и в том случае, когда информационная часть строки соответствует разделителю и находится внутри подстроки. Так, например после токенации следующей строки:
```
"book, author, publication,\",\",date published"
```
мы получим шесть частей
```
book, author, publication, ", ", date published
```
вместо пяти
```
book, author, publication, ',', date published.
```
В этом случае использование третьего конструктора с установленным в true значением returnDelims также не поможет.

**ПРИМЕР 1**

```java
import java.util.StringTokenizer;

public class StringTokenizerExample_1 {

	static String str = "Пример использования StringTokenizer для разбора строки на лексемы.";
	
	public static void main(String[] args) {
		StringTokenizer st = new StringTokenizer(str, " .");
		
		int i = 1;
		while(st.hasMoreTokens()) {
			System.out.println((i++)+" "+st.nextToken());
		}
	}

}
```
**Результат работы**
<p style="background-color: navy; color: yellow">
1 Пример<br>
2 использования<br>
3 StringTokenizer<br>
4 для<br>
5 разбора<br>
6 строки<br>
7 на<br>
8 лексемы</p>
**ПРИМЕР 2**

```java
import java.util.StringTokenizer;

public class StringTokenizerExample_2 {

	static String str = "Имя:Иван|Фамилия:Иванов|E-Mail:Ivanov@mail.ru";
	
	public static void main(String[] args) {
		StringTokenizer st = new StringTokenizer(str, ":|");
		
		while(st.hasMoreTokens()) {
			System.out.println(st.nextToken()+" - "+st.nextToken());
		}
	}

}
```
**Результат работы**
<p style="background-color: navy; color: yellow">
Имя - Иван<br>
Фамилия - Иванов<br>
E-Mail - Ivanov@mail.ru</p>

### Адаптивный токенайзер, CustomTokenizer

Создать свой токенайзер на все случаи жизни - дело очень затратное по временным ресурсам, и не очень благодарное. Можно получить очень сложный код, бизнес-логика которого в скором времени забудется, и внесение дополнительных изменений потребует серьезных усилий.

Ниже предложен подход решения одной из рассмотренных выше проблем - как исключить из анализа/разложения текст, обрамленный кавычками (двойными, одинарными) или разного рода скобками.

Решение проблемы простое. Необходимо в токенайзер передать модифицированную строку для анализа, где проблемные участки текста заменены заглушками. А при извлечении токенов, вместо заглушек вернуть их исходное значение. То есть текст предварительно, перед передачей токенайзеру для разложения, обрабатывается и значение токена восстанавливается, перед возвращением.

Листинг настраиваемого токенайзера :
```java
import java.util.Map;
import java.util.HashMap;
import java.util.StringTokenizer;

public class CustomTokenizer
{
    private  StringTokenizer      tokenizer   = null;
    private  int                  tokenNum    = 0;
    private  int                  totalTokens = 0;
    private  final  String        QUOTE       = "\"";
    private  Map<String, String>  substitutes;  
    // шаблон заглушки
    private  final  String        SUBSTITUTE  = "__SUBSTITUTE__";
    //~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    /**
     * Конструктор
     * @param text текстовая строка
     * @param delim строка разделителей
     */
    public CustomTokenizer(String text, String delim)
    {
        substitutes = new HashMap <String, String>();
        tokenizer = new StringTokenizer(setSubstitute(text), delim, true);
    }
    //~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    /**
     * Конструктор
     * @param text текстовая строка
     * @param delim строка разделителей
     * @param includeDelim флаг включения разделителей 
     *                     как токенов
     */
    public CustomTokenizer(String str, String delim, boolean includeDelim)
    {
        tokenizer = new StringTokenizer(setSubstitute(str), delim, includeDelim);
    }
    //~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    /**
     * Функция замены "проблемного" текста в кавычках 
     * заглушками. Проблемный текст в строке, выделенный 
     * двойными кавычками, заменяется
     * @param text исходный текст
     * @return измененный текст
     */
    private String setSubstitute(final String text)
    {
        String temp = text;
        int id = 0;
        // Определение начала и конца проблемного кода
        int startQuote = temp.indexOf(QUOTE, 0);
        int endQuote = -1;
        if (startQuote >= 0 )
            endQuote = temp.indexOf(QUOTE, startQuote + 1);
        // Цикл перебора текста
        while (((startQuote >= 0) && (endQuote > startQuote))) {
            // Извлечение проблемного текста
            String txt;
            txt = temp.substring(startQuote, endQuote + 1);
            // Определение ключа
            String key = SUBSTITUTE + String.valueOf(id++);
            // Замена проблемного текста заглушкой
            temp = temp.replaceFirst(txt, key);
            // Сохранение проблемного текста с ключом
            substitutes.put(key, txt);
            // Подготовка к следующему циклу
            startQuote = temp.indexOf(QUOTE, 0);
            if (startQuote >= 0)
                endQuote = temp.indexOf(QUOTE,startQuote+1);
        }
        return temp;
    }
    //~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    /**
     * Функция возвращения следующего токена строки
     * @return следующий токен
     */
    public String nextToken()
    {
        String sToken = tokenizer.nextToken();
        if (substitutes.containsKey(sToken.trim()))
            sToken = substitutes.get(sToken.trim());
        tokenNum++;
        return sToken;
    }
    //~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    /**
     * Функция проверки наличия оставшихся токенов	
     * @return логическое значение true, если имеется 
     *  еще токен
     */
    public boolean hasMoreTokens()
    {
        if (totalTokens == 0)
            totalTokens = countTokens();
        return (tokenNum < totalTokens);
    }
    //~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    /**
     * Функция проверки наличия оставшихся токенов
     * @return логическое значение true, если имеется
     * еще токен
     */
    public boolean hasMoreElements()
    {
        return hasMoreTokens();
    }
    //~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    /**
     * Функция получения следующего токена
     * @return текущий токен строки типа Object
     */
    public Object nextElement()
    {
        return nextToken();
    }
    //~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    /**
     * Функция определения количества токенов в строке
     * @return количество токенов
     */
    public int countTokens()
    {
        return tokenizer.countTokens();
    }
    //~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    public static void main(String[] args)
    {
        String string;
//      string = "hi, hello,, \"how, are, qrt, u\", good, "
//                          + "\"fine, hty, great\", data";
//      string = "hi, how, \"are, u\", hello, \"how, are\", u";
        string = "Привет. Завтра \"21 сентября \" " + "мы идем в театр.";
        System.out.println("~~~ Исходная строка ~~~\n" + string);
        CustomTokenizer tokenizer;
        tokenizer = new CustomTokenizer(string, " .", false);
        System.out.println("\nколичество токенов = " + tokenizer.countTokens());
        System.out.println("\n~~~ Список токенов ~~~");
        int i = 0;
        while(tokenizer.hasMoreTokens())
            System.out.println("" + ++i + " = " + tokenizer.nextToken());
    }
}
```
В данном токенайзере имеется две функции, код которых можно модифицировать под разные случаи жизни:
- String setSubstitute(final String text) - функция замены в исходном тексте различного рода проблемных участков заглушками;
- String nextToken() - функция получения токенов, и, при необходимости, восстановления их исходных значений.

Результат выполнения программы выведет в консоль следующую информацию:
<p style="background-color: navy; color: yellow">
~~~ Исходная строка ~~~<br>
Привет. Завтра "21 сентября " мы идем в театр.<br>
<br>
количество токенов = 7<br>
<br>
~~~ Список токенов ~~~<br>
1 = Привет<br>
2 = Завтра<br>
3 = "21 сентября "<br>
4 = мы<br>
5 = идем<br>
6 = в<br>
7 = театр</p>
