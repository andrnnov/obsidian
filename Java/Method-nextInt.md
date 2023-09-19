#Java #Random #nextInt #ScannerClass 

Метод nextInt(). Получить случайное число типа int. Получить целое число в заданных пределах

Метод nextInt() возвращает целое случайное число типа int. Число может быть как положительным, так и отрицательным. Согласно документации объявление метода следующее
```java
public int nextInt();
```
**Пример.**

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
Результат
min = 1
max = 10

==AI:
7
10
5
5
8
2
1
4
9
5==