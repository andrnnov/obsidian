#Java #ArrayList #Constructor-ArrayList
### Конструкторы класса ArrayList. Создание массива.

2023-09-20 16:16

В классе [ArrayList](Class-ArrayList) определены следующие конструкторы:

`ArrayList()`
`ArrayList(Collection<? extends E>)`
`ArrayList(int size)`

здесь
- E – тип элементов коллекции;
- size – текущий размер массива.

Первый конструктор создает пустой динамический массив. 
Второй конструктор создает динамический массив на основе другого массива.
Третий конструктор создает пустой массив с зарезервированным объемом размера size. Если при наращивании количество элементов в таком массиве превысит size, то зарезервированный объем (максимальная емкость) будет увеличен на некоторую величину.

**Пример**. В примере создаются разные виды динамических массивов.
```java
import java.util.*;

public class TrainCollections {
	public static void main(String[] args) {
	    // 1. Конструктор ArrayList()
	    //    Создать пустой массив целых чисел
	    ArrayList<Integer> AL = new ArrayList();
	    // Прибавить к массиву числа от 0 до 9
	    for (int i=0; i<10; i++)
		    AL.add(i);
	    System.out.println(AL); // [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
	    // 2. Создать массив строк на основе другого массива строк,
	    //    конструктор ArrayList(Collection<? extends E>)
	    // 2.1. Создать исходный массив
	    ArrayList<String> AS1 = new ArrayList();
	    AS1.add("Winter");
	    AS1.add("Spring");
	    AS1.add("Autumn");
	    AS1.add("Summer");
	    System.out.println(AS1);  // [Winter, Spring, Autumn, Summer]
	    // 2.2. Использовать конструктор ArrayList(Collection<? extends E>)
	    ArrayList<String> AS2 = new ArrayList(AS1);
	    System.out.println(AS2);  // [Winter, Spring, Autumn, Summer]
	    // 3. Конструктор ArrayList(int)
	    // 3.1. Создать пустой массив з зарезервированным размером 8 элементов
	    ArrayList<Character> AC = new ArrayList(8);
	    // 3.2. Вывести размер массива
	    System.out.println(AC.size()); // 0 - это есть текущий размер массива
	}
}
```
Результат выполнения программы

==[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
[Winter, Spring, Autumn, Summer]
[Winter, Spring, Autumn, Summer]
0==