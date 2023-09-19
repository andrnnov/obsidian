#Java #Random #nextBytes

### Метод nextBytes(). Получить массив случайных чисел типа byte[] ###

2023-09-18 17:21

Метод nextBytes() заполняет входной массив случайными числами, имеющими тип byte. Согласно документации синтаксис объявления метода следующий

`void nextBytes(byte[] bytes);`

здесь

bytes – заданный массив некоторой длины. Заполняются все элементы массива. Значения элементов массива лежат в пределах `[-128; 127]`.

**Пример**.
```java
import java.util.Random;

public class MathFunctions {

	public static void main(String[] args) {
	    // 1. Создать поток на основе произвольного начального значения
	    Random rnd = new Random();
	    // 2. Создать массив AB из 10 элементов типа byte
	    byte[] AB = new byte[10];
	    // 3. Заполнить массив AB случайными числами
	    rnd.nextBytes(AB);
	    // 4. Вывести массив на экран
	    System.out.println("Array AB:");
	    for (int i=0; i<AB.length; i++) {
		    System.out.println(AB[i]+" ");
		}
	}
}
```
Вывод:
==Array AB:
-67
-86
98
-61
16
-44
-73
96
-40
-80==
