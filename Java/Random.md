#Java #Random  #setSeed #doubles #ints #longs #nextBytes 

### Случайные числа в Java ###

2023-09-14 17:30

1. **Метод Math.random()**

В Java у класса `Math` есть специальный метод, который возвращает случайное число. И, как вы возможно догадываетесь, метод называется `random`. Общий вид его вызова выглядит так:
```java
Math.random()
```
Этот метод не принимает никаких параметров, но возвращает результат — псевдослучайное вещественное число в диапазоне от `0` до `1`. Единица при этом в диапазон не входит.

Пример:
```java
public class Main {
	public static void main(String[] args) {
		for (int i = 0; i < 10; i++) {
		    System.out.println(Math.random());
	    }
    }
}
```
Вывод:
==0.9703753971734451
0.09979423801773157
0.994048474709053
0.2852203204171295
0.13551248551226025
0.3128547131272822
0.5342480554101412
0.6817369932044817
0.1840767788961758
0.06969563435451254==
Но что, если вам этот метод не очень подходит, а вы хотите, допустим, написать программу, которая имитирует выбрасывание кубика с шестью гранями. Как получить случайные целые числа в диапазоне 1..6, а не вещественные в диапазоне 0..1?

Это на самом деле довольно просто.

Сначала нужно превратить диапазон `[0,1)` в `[0, 6)`. Для этого нужно просто умножить результат функции `random()` на `6`. Ну а чтобы получить целые числа, нужно это все округлить:
```java
public class Main {
   public static int getRandomDiceNumber() {
	    return (int) (Math.random() * 6);
	}

	public static void main(String[] args) {
	    for (int i = 0; i < 10; i++) {
	    int x = getRandomDiceNumber();
	        System.out.println(x);
	    }
	}
}
```
Вывод:
==5
2
3
3
2
4
1
1
5
0==
Функция `getRandomDiceNumber()` возвращает случайное целое число из диапазона `0..5` включительно. Только это будут не числа из набора `1,2,3,4,5,6`, а числа из набора `0,1,2,3,4,5`.

Если требуются именно числа из набора `1,2,3,4,5,6`, нужно просто ко всем случайным числам добавлять единицу:
```java
public class Main
{
   public static int getRandomDiceNumber()
   {
      return (int) (Math.random() * 6) + 1;
   }

   public static void main(String[] args)
   {
     for (int i = 0; i < 10; i++)
     {
       int x = getRandomDiceNumber();
       System.out.println(x);
     }
   }
}
```
Вывод:
==3
2
1
3
6
5
6
1
6
6==

2. **Класс Random**

В Java есть специальный класс `Random`, который инкапсулирует в себе последовательность псевдослучайных чисел. Можно создать несколько объектов класса `Random`, и каждый из этих объектов будет генерировать свою последовательность псевдослучайных чисел.

Это очень интересный класс, и у него есть много интересных методов. Начнем с самых простых:

**Метод [void setSeed()](Method-setSeed)**

Этот метод устанавливает исходное значение, которое используется в качестве основы для генерирования случайных чисел.

**Метод `double nextDouble()`**

Этот метод возвращает случайное вещественное число в диапазоне `0.0` – `1.0`. Очень похоже на метод `Math.random()`. И ничего удивительного, ведь метод `Math.random()` просто вызывает метод `nextDouble()` у объекта типа `Random`.

**Метод `float nextFloat()`**

Метод очень похож на метод `nextDouble()`, только возвращаемое случайное число типа `float`. Оно также лежит в диапазоне `0.0` – `1.0`. И, как всегда, в Java диапазон не включает число `1.0`.
```java
Random r = new Random();
float f = r.nextFloat();
```
**Метод `int nextInt(int max)`**

Этот метод возвращает случайное целое число в диапазоне `[0, max)`. `0` входит в диапазон, `max` — не входит.

Т.е. если вы хотите получить случайное число из набора `1, 2, 3, 4, 5, 6`, вам нужно будет прибавить к полученному случайному числу единицу:
```java
Random r = new Random();
int x = r.nextInt(6) + 1;
```

**Метод [`int nextInt()`](Method-nextInt)**

Этот метод аналогичен предыдущему, но не принимает никаких параметров. Тогда в каком же диапазоне он выдает числа? От `-2 миллиарда` до `+2 миллиарда`.

Ну или если точнее, от `-2147483648` до `+2147483647`.

**Метод `long nextLong()`**

Этот метод аналогичен методу `nextInt()`, только возвращаемое значение будет из всего возможного диапазона значений типа `long`.

**Метод `boolean nextBoolean()`**

Этот метод возвращает случайное значение типа `boolean`: `false` или `true`. Очень удобно, если нужно получить длинную последовательность случайных логических значений.

**Метод `void nextBytes(byte[] data)`**

Этот метод ничего не возвращает (тип `void`). Вместо этого он заполняет переданный в него массив случайными значениями. Очень удобно, если нужен большой буфер, заполненный случайными данными.

**Метод `double nextGaussian()`**

Этот метод возвращает значение типа double, полученное на основе распределения Гаусса со средним значением 0.0 и стандартным отклонением 1.0.

```java
import java.util.Random;

public class MathFunctions {
	public static void main(String[] args) {
	    // 1. Создать поток на основе произвольного исходного значения
	    Random rnd = new Random();
	    // 2. Создать массив AD из 10 элементов типа double
	    //   в котором элементы получаются на основе распределения Гаусса
	    double[] AD = new double[10];
	    // 3. Заполнить массив AD случайными числами
	    //    с использованием метода nextGaussian()
	    for (int i=0; i<AD.length; i++)
		    AD[i] = rnd.nextGaussian();
	    // 4. Вывести массив AD на экран
	    System.out.println("Array AD:");
	    for (int i=0; i<AD.length; i++)
		    System.out.println(AD[i]+" ");
    }
}
```
Вывод:
==0.8462285437123548
1.1084379848996055
0.5552376880883958
-1.0787586788543444
0.9944069427425211
0.8645907102307332
-1.449023177851094
1.2567221522577043
-1.073685704004384
-0.8709705603926711==

3. **Методы получения наборов случайных чисел**

Метод [doubles()](Method-doubles) cоздает поток данных, содержащий случайные числа типа double.

Метод [ints()](Method-ints) получает данные типа int в виде потока случайных чисел.

Метод [longs()](Method-longs) получает данные типа long в виде потока случайных чисел.

Метод [nextBytes()](Method-bytes) получает массив случайных чисел типа Bytes[].