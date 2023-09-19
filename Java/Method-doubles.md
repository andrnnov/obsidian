#Java #Random #doubles
### Метод doubles(). Создать поток данных, содержащий случайные числа типа double.

2023-09-18 17:23

Метод doubles() создает поток данных, состоящий из случайных чисел типа double. Числа имеют значение от 0 до 1. Метод имеет несколько реализаций. Наиболее распространенные реализации метода выглядят следующим образом:

`DoubleStream doubles();`
`DoubleStream doubles(long streamSize);'

`streamSize` – количество чисел, которые необходимо сгенерировать в потоке данных.

Первая реализация (без параметров) позволяет создавать неограниченный поток данных. Вторая реализация метода doubles() генерирует поток данных фиксированного размера.

Чтобы использовать класс DoubleStream, нужно подключить модуль:
`import java.util.stream.DoubleStream;`

**Пример**
```java
import java.util.Iterator; // нужно для использования класса Iterator<>
import java.util.Random;   // нужно для использования класса Random
import java.util.stream.DoubleStream; // нужно для использования класса DoubleStream

public class MathFunctions {
	public static void main(String[] args) {
	    // 1. Создать поток на основе произвольного начального значения
	    Random r1 = new Random(); //
	    // 2. Получить поток из 10 чисел типа double
	    DoubleStream ds1 = r1.doubles(10);
	    // 3. Получить итератор на поток ds1
	    Iterator<Double> it1 = ds1.iterator();
	    // 4. Вывести в цикле 10 случайных чисел из потока ds1
	    System.out.println("Stream ds1:");
	    while (it1.hasNext()) {
			System.out.println(it1.next());
	    }
	}
}

```
Вывод:
==Stream ds1:
0.03296957043047
0.5816373543355657
0.6067884839512304
0.3600735235508934
0.5041601996294538
0.8372554459494158
0.7894095095554403
0.23663204256820447
0.5334022228843057
0.5142652199413285==
