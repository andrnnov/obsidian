#Java #interface #Functional-Interface #Function 

## Функциональный интерфейс Function

2024-09-25 11:45

**java.util.function.Function**  - это встроенный [функциональный интерфейс](Functional-Interface), добавленный в Java SE 8 в пакет java.util.function. Интерфейс Function принимает входные данные и возвращает определенный тип, подобно функции с параметрами и возвращаемым типом. Первый параметр в объявлении интерфейса определяет тип входного аргумента, а второй - тип возвращаемого значения. Часто используется для преобразования одного значения в другое:
```java
@FunctionalInterface
public interface Function<T, R> {
    R apply(T t);
}
```

**Функциональный дескриптор интерфейса**:
```markup
T -> R
```

Рассмотрим пример использования **интерфейса Function**:
```java
import java.util.function.Function;

public class FunctionExample1 {
    public static void main(String[] args) {
        Function<Double, Long> function = d -> Math.round(d);
        System.out.println(function.apply(5.7));
    }
}
```
**Вывод:**
<p style="background-color: navy; color: yellow">
6</p>

### Методы интерфейса Function<T, R>

```java
R apply(T t);
default <V> Function<T, V> andThen(Function<? super R, ? extends V> after);
default <V> Function<V, R> compose(Function<? super V, ? extends T> before);
static <T> Function<T, T> identity();
```

#### Метод apply()

**Параметры:** Этот метод принимает только один параметр *t*, который является аргументом функции.

**Тип возвращаемого значения:** этот метод возвращает **результат функции**, имеющий тип R.

**Пример:**
```java
// Java Program to Illustrate Functional Interface
// Via apply() method
// Importing interface
import java.util.function.Function;

public class Maim {
    // Main driver method
    public static void main(String args[]) {
        // Function which takes in a number
        // and returns half of it
        Function<Integer, Double> half = a -> a / 2.0;
        // Applying the function to get the result
        System.out.println(half.apply(10));
    }
}
```
**Вывод:**
<p style="background-color: navy; color: yellow">
5.0</p>

#### Методы andThen() и compose()

Если несколько функций объединены в цепочку с использованием метода **_andThen_**, они будут выполнены по порядку слева направо. Метод **_compose_** позволяет выполнить функции в обратном порядке - справа налево.

Эти методы выдают исключение NullPointerException, если предыдущая функция имеет значение null.

Следующий пример показывает разницу между этими методами:
```java
import java.util.function.Function;

public class FunctionExample2 {
    public static void main(String[] args) {
        Function<String, String> f1 = s -> s + "1";
        Function<String, String> f2 = s -> s + "2";
        Function<String, String> f3 = s -> s + "3";
        Function<String, String> f4 = s -> s + "4";
        System.out.println(f4.andThen(f3).compose(f2).compose(f1).apply("Compose: "));
        System.out.println(f3.andThen(f2).andThen(f1).apply("AndThen: "));
    }
}
```
**Вывод:**
<p style="background-color: navy; color: yellow">
Compose: 1243<br>
AndThen: 321</p>

**Пример**.  Сначала применяет текущую функцию half(), а затем функцию andThen():
```java
// Java Program to illustrate addThen() method

// Importing interface
import java.util.function.Function;

// Main class
public class Main {

    // main driver method
    public static void main(String args[]) {
        // Function which takes in a number and
        // returns half of it
        Function<Integer, Double> half = a -> a / 2.0;

        // Now triple the output of half function
        half = half.andThen(a -> 3 * a);

        // Applying the function to get the result
        // and printing on console
        System.out.println(half.apply(10));
    }
}
```
**Вывод:**
<p style="background-color: navy; color: yellow">
15.0</p>

**Пример.** Сначала применяет функцию compose(), а затем текущую функцию half()
```java
// Java Program to illustrate compose() method
// Importing Function interface
import java.util.function.Function;

// Main class
public class Main {
    // Main driver method
    public static void main(String args[]) {
        // Function which takes in a number and
        // returns half of it
        Function<Integer, Double> half = a -> a / 2.0;

        // Triple the value given to half function
        half = half.compose(a -> 3 * a);

        // Applying the function to get the result
        System.out.println(half.apply(5));
    }
}
```
**Вывод:**
<p style="background-color: navy; color: yellow">
7,5
</p>

#### Метод **identity**()

[[Static#Модификатор static в Java методы|Статический метод]] интерфейса Function **identity**():
```java
static <T> Function<T, T> identity()
```

Рассмотрим пример использования:
```java
import java.util.function.Function;

public class FunctionExample3 {
    public static void main(String[] args) {
        Function<String, String> f = Function.identity();
        System.out.println(f.apply("Some Value"));
    }
}
```
**Вывод:**
<p style="background-color: navy; color: yellow">
Some Value
</p>

#### Пример использования интерфейса Function

```java
import org.junit.Test;  
import org.junit.jupiter.api.*;  
import java.util.function.*;

@TestMethodOrder(MethodOrderer.OrderAnnotation.class)
public class FunctionInterface {
    //При объявлении Функции сначала указывается тип входного аргумента, затем тип возвращаемого значения
    Function<String, String>  toUpperCase = (text) -> text.toUpperCase(); //Принимает String, возвращает тоже String
    Function<String, String>  toLowerCase = (text) -> text.toLowerCase();
    Function<Integer, Double> log10 = (number) -> Math.log10(number); //Принимает Integer, возвращает Double
    //То же самое, но вместо лямбда-функций применяются ссылки на методы
    Function<String, String>  toUpperCaseUsingMethodReference = String::toUpperCase;
    Function<String, String>  toLowerCaseUsingMethodReference = String::toLowerCase;
    Function<Integer, Double> log10UsingMethodReference = Math::log10;
    //Пример с BiFunction (Тип 1-го входного аргумента, Тип 2-го входного аргумента, Тип возвращаемого значения)
    BiFunction<Integer, Integer, Integer> powerOf = (base, power) -> (int) Math.pow(base, power);
    //Пример с UnaryOperator (Тип входного аргумента и возвращаемого значения - одинаковые)
    UnaryOperator<String> appendText = (text) -> "I am appending: " + text;
   
    @BeforeEach
    public void setup(TestInfo testInfo) {
        System.out.println("Test name: " + testInfo.getDisplayName());
        System.out.println();
    }
  
    @Order(1)
    @Test
    public void functionTest() {
        String upperCaseResult = toUpperCase.apply("Hello world!");
        Double log10Result = log10.apply(5000);
        System.out.println(upperCaseResult);
        System.out.println(log10Result);
    }
 
    @Order(2)
    @Test
    public void functionChainWithAndThen() {
        String chainResult1 = toUpperCase.andThen(toLowerCase).apply("heLLo WorLD!");
        String chainResult2 = toLowerCase.andThen(toUpperCase).apply("heLLo WorLD secOND tiME!");
        System.out.println(chainResult1);
        System.out.println(chainResult2);
    }
 
    @Order(3)
    @Test
    public void functionChainWithCompose() {
        String chainResult1 = toUpperCase.compose(toLowerCase).apply("heLLo WorLD!");
        String chainResult2 = toLowerCase.compose(toUpperCase).apply("heLLo WorLD secOND tiME!");
        System.out.println(chainResult1);
        System.out.println(chainResult2);
    }
 
    @Order(4)
    @Test
    public void biFunctionTest() {
        int result = powerOf.apply(5, 5);
        System.out.println("5-ть в 5-ой степени равно: " + result);
    }
 
    @Order(5)
    @Test
    public void unaryOperatorTest(){
        System.out.println(appendText.apply("Hello world with Unary Operator!"));
    }
}
```
Результат выполнения:
<p style="background-color: navy; color: yellow">
hello world!<br>
HELLO WORLD SECOND TIME!<br>
HELLO WORLD!<br>
3.6989700043360187<br>
I am appending: Hello world with Unary Operator!<br>
HELLO WORLD!<br>
hello world second time!<br>
5-ть в 5-ой степени равно: 3125</p>

- functionChainWithAndThen
		Во время выполнения тестового метода functionChainWithAndThen() два экземпляра функции (toUpperCase и toLowerCase) объединяются с помощью метода andThen(), и результирующая функция применяется к входным значениям. Результатом будет строка "hello world!" и строка "HELLO WORLD SECOND TIME!".	
- functionTest
		HELLO WORLD!
		3.6989700043360187
- unaryOperatorTest
		I am appending: Hello world with Unary Operator!
- functionChainWithCompose
		В тестовом методе functionChainWithCompose() два экземпляра Function (toUpperCase и toLowerCase) объединяются с помощью метода compose(), и полученная функция применяется к входным значениям. Метод compose() похож на andThen(), но он применяет вначале вторую функцию, а затем первую. Поэтому результатом будет строка "HELLO WORLD!" и строка "hello world second time!".
- biFunctionTest
		5-ть в 5-ой степени равно: 3125


