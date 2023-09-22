#Java #Varargs
### Varargs — аргументы переменной длины ###

2023-09-21 15:24

Varargs позволяют нам создавать методы с произвольным количеством аргументов. По большому счету, создавать такие методы можно было и раньше. Правда, делать это было не очень удобно.  Допустим, нам необходимо написать метод, который будет принимать произвольное количество целочисленных аргументов и складывать их вместе.
У нас есть два варианта.
__Вариант 1 — перегрузка:__
```java
class Calculator {
    int sum(int a, int b){...};
    int sum(int a, int b, int c){...};
    int sum(int a, int b, int c, int d){...};
    int sum(int a, int b, int c, int d, int e){...};
}
```
Но с перегрузкой возникают две проблемы. Во-первых, не всегда понятно, когда пора остановиться, а во-вторых, это громоздко. Лучше уж массивы.
__Вариант 2 — массивы:__
```java
class Calculator {
    int sum(int[] numbers){...};
}
```
```java
int[] arguments = {1,10,123,234,6234,12,8};
int sum = calculator.sum(arguments);
```
Мы все равно не избавимся излишнего количества кода.
Однако с выходом Java 5 для решения этих проблем появилась фича Varargs. Она позволила передавать в методы произвольное количество аргументов. Выглядит это примерно так:
```java
public class Calculator {
    public static void main(String... sss) {
        Calculator calculator = new Calculator();
        int sum = calculator.sum(1,10,123,234,6234,12,8);
    }
    int sum(int... numbers){
       return Arrays.stream(numbers).sum();
    }
}
```
Varargs — это аргументы переменной длины, фича, которая появилась с выходом Java 5. Далее более подробно рассмотрим некоторые правила работы с Varargs.
### 5 правил varargs ###

- **Правило 1.** Vararg аргумент (или же аргумент переменной/произвольной длины) обозначается через троеточие следующим образом:
```java
String... words
Integer... numbers
Person... people
Cat... cats
```
- **Правило 2.** Аргумент произвольной длины может быть указан только как аргумент некоторого метода:
```java
void print(String... words)
int sum(Integer... numbers)
void save(Person... people)
void feed(Cat... cats)
```
- **Правило 3.** Каждый такой аргумент переменной длины в теле метода является массивом:
```java
void print(String... words){
    for (int i = 0; i < words.length; i++) {
        System.out.println(words[i]);
    }
}
```
- **Правило 4.** Vararg аргумент должен быть последним в списке аргументов метода:
```java
void print(String... words, String anotherWord) // - Так нельзя!
void print(String... words, int someNumber) // - Так нельзя!

void print(String anotherWord, String... words) // - Так можно
void print(int someNumber, String... words) // - Так можно
```
- **Правило 5.** Несмотря на то, что varargs являются массивами, при вызове метода, который принимает аргументы переменной длины, не обязательно создавать массив. Достаточно и даже желательно просто перечислить необходимые аргументы через запятую:
```java
public class Main {
    public static void main(String... sss) {
        print("Как","же","прекрасно","изучать","Java");
    }

    static void print(String... words){
        for (int i = 0; i < words.length; i++) {
            System.out.println(words[i]);
        }
    }
}
```
### Примеры varargs ###

В примере ниже мы напишем метод, который принимает varargs состоящий из целых чисел и выводит на экран количество переданных элементов и их сумму. Передадим в этот метод и массив, и ряд целых чисел (оба варианта допустимы):
```java
public static void main(String... sss) {
    int[] a = new int[100];
    for (int i = 0; i < a.length; i++) {
        a[i] = i;
    }

    sum(a);
    sum(1,2,3,4,5,6,7,8,9,10);
}

static void sum(int... numbers){
    final int length = numbers.length;
    final int sum = Arrays.stream(numbers).sum();
    final String lineSeparator = System.lineSeparator();

    System.out.printf("Кол-во элементов для сложения - %d, сумма - %d%s", length, sum, lineSeparator);
}
```
После запуска программа выведет:
```
Кол-во элементов для сложения - 100, сумма - 4950 
Кол-во элементов для сложения - 10, сумма - 55 
```
Стоит сказать, что метод `System.out.printf` также принимает varargs. Если мы взглянем на код этого метода, то убедимся в этом:
```java
public PrintStream printf(String format, Object ... args) {
    return format(format, args);
}
```
Еще один широко используемый метод, принимающий varags — `String.format`. Его код приведен ниже:
```java
public static String format(String format, Object... args) {
    return new Formatter().format(format, args).toString();
}
```
### Когда использовать varargs? ###

Ответ на этот вопрос зависит от того, кто спрашивает. 

Если подобный вопрос задает клиент некоторого API, в котором есть методы с varargs, то ответ будет “использовать такие методы как можно чаще”. Для клиента кода varargs существенно упрощает жизнь, облегчая написание кода и повышая его читаемость. 

Однако в случае, если данный вопрос задает разработчик API, который интересуется, как часто стоит создавать методы с varargs, то ответ будет “не следует часто использовать varargs”. Varargs следует использовать только тогда, когда выгода от его использования очевидна. Также не следует перегружать методы с varargs, так как это вызовет у клиентов вашего кода затруднения в понимании, какой из перегруженных методов в действительности вызывается.