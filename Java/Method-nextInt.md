#Java #Random #nextInt #ScannerClass 

### Метод nextInt()

Метод nextInt() возвращает целое случайное число типа int. Число может быть как положительным, так и отрицательным. Согласно документации объявление метода следующее
```java
public int nextInt();
```

#### Параметры

NA

#### Возвращаемое значение

Этот метод возвращает значение int, сканированное из входных данных

#### Исключение

- **Исключение InputMismatchException** − если следующий токен не соответствует целочисленному регулярному выражению или находится вне диапазона
- **Исключение NoSuchElementException** − если входные данные исчерпаны
- **Исключение IllegalStateException** − если этот сканер закрыт

#### Пример

В примере с помощью метода nextInt() формируется массив случайных чисел. Каждое число имеет значение в пределах `[min; max]`. Для формирования числа выведена формула. В конце массив сформированных чисел выводится на экран. Для ввода цифр с клавиатуры используются средства класса [Scanner](ScannerClass).
```java
import java.util.Random;   // нужно для использования класса Random
import java.util.Scanner;   // нужно для использования класса Scanner

public class MathFunctions {

	public static void main(String[] args) {
	    // 1. Создать поток на основе произвольного исходного значения
	    Random rnd = new Random();
	    // 2. Создать массив из 10 элементов типа int
	    int[] AI = new int[10];
	    // 3. Задать с клавиатуры нижний и верхний предел случайных чисел
	    int min, max;
	    Scanner input = new Scanner(System.in);
	    // 3.1. Ввести нижнюю границу
	    System.out.print("min = ");
	    min = input.nextInt();
	    // 3.2. Ввести верхнюю границу
	    System.out.print("max = ");
	    max = input.nextInt();
	    // 4. Заполнить массив AI случайными числами в пределах [min; max]
	    for (int i=0; i<AI.length; i++)
		    AI[i] = min + Math.abs(rnd.nextInt()) % (max - min + 1);
	    // 5. Вывести массив
	    System.out.println("\nAI:");
	    for (int i=0; i<10; i++)
		    System.out.println(AI[i]);
	}
}
```
**Ввод:**
```
min = 1
max = 10
```
**Вывод:**
<p style="background-color: navy; color: yellow">
AI:<br>
7<br>
10<br>
5<br>
5<br>
8<br>
2<br>
1<br>
4<br>
9<br>
5</p>

### Метод Java Scanner nextInt(int radix)

#### Описание

Метод **java.util.Scanner.nextInt(int radix)** сканирует следующий токен входных данных как int. Этот метод вызовет исключение InputMismatchException, если токен next не может быть преобразован в допустимое значение int, как описано ниже. Если преобразование выполнено успешно, сканер проходит мимо соответствующих входных данных.

#### Объявление

Ниже приводится объявление для **java.util.Scanner.nextInt(int radix)** метод
```java
public int nextInt(int radix)
```

#### Параметры

функция принимает один параметр счисления, который не является обязательным. Он определяет систему счисления, используемую для интерпретации токена как значения типа Int.

#### Возвращаемое значение

Этот метод возвращает значение int, сканированное из входных данных

#### Исключение

- Исключение InputMismatchException − если следующий токен не соответствует целочисленному регулярному выражению или находится вне диапазона
- Исключение NoSuchElementException − если входные данные исчерпаны
- Исключение IllegalStateException − если этот сканер закрыт

#### Пример

В следующем примере показано использование метода Java Scanner nextInt() для сканирования следующего токена как Int с исходным кодом по умолчанию. Мы создали объект scanner, используя заданную строку. Затем мы проверили, чтобы каждый токен был Int, и напечатали, в противном случае "Not Found:", печатается вместе с отсканированным токеном. В конце сканер закрывается с помощью метода close().
```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        String s = "Hello World! 3 + 3.0 = 6";
        // create a new scanner with the specified String Object
        Scanner scanner = new Scanner(s);
        while (scanner.hasNext()) {
            // check if the scanner's next token is a Int
            if(scanner.hasNextInt(4)){
                // print what is scanned
                System.out.println("Found: " + scanner.nextInt());
            } else {
                System.out.println("Not Found: " + scanner.next());
            }
        }
        // close the scanner
        scanner.close();
    }
}
```
**Вывод:**
<p style="background-color: navy; color: yellow">
Not Found: Hello<br>
Not Found: World!<br>
Found: 3<br>
Not Found: +<br>
Not Found: 3.0<br>
Not Found: =<br>
Not Found: 6</p>


