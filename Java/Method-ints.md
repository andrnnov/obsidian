#Java #Random #ints
### Метод ints(). Получить данные типа int в виде потока случайных чисел###

2023-09-18 17:23

Метод ints() создает поток случайных чисел типа IntStream. Наиболее распространенные реализации метода выглядят следующим образом

`IntStream ints();`
`IntStream ints(**long** streamSize);`

здесь
`streamSize` – количество элементов в потоке данных типа int.

Первая реализация метода (без параметров) создает поток случайных чисел типа int неограниченного размера. Вторая реализация позволяет установить ограничение в потоке размером streamSize.

Чтобы использовать тип IntStream и подобные ему в начале модуля нужно включить строку
import java.util.stream.*;

**Пример**.

В примере методом ints() без параметров создается поток неограниченного размера. Затем выводятся первые 5 элементов потока.

```java
import java.util.Iterator; // нужно для использования класса Iterator<>
import java.util.Random;   // нужно для использования класса Random
import java.util.stream.*; // нужно для использования класса IntStream

public class MathFunctions {
	public static void main(String[] args) {
	    // 1. Создать поток на основе произвольного исходного значения 
	    Random r1 = new Random();
	    // 2. Получить поток с неограниченным количеством чисел типа int 
	    IntStream rndInt = r1.ints();
	    // 3. Получить итератор на поток rndInt 
	    Iterator<Integer> it1 = rndInt.iterator();
	    // 4. Вывести в цикле 5 случайных чисел из потока rndInt 
	    int value;
	    System.out.println("Stream rndInt:");
	    for (int i=0; i<5; i++) {
	      // Получить случайное число 
	      value = it1.next();
	      System.out.println(value);
	    }
	}
}
```
Вывод:
==Stream rndInt:
2119189406
-15495572
-2068391741
271674312
742325160==
