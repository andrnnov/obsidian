
#Java #StreamAPI 

## Параллельные операции над массивами

2024-04-04 11:05

В JDK 8 к классу [Arrays](Array) было добавлено ряд методов, которые позволяют в параллельном режиме совершать обработку элементов массива. И хотя данные методы формально не входят в [Stream API](StreamAPI), но реализуют схожую функциональность, что и параллельные потоки:
- parallelPrefix(): вычисляет некоторое значение для элементов массива (например, сумму элементов)
- parallelSetAll(): устанавливает элементы массива с помощью [лямбда-выражения](Lambda)
- parallelSort(): сортирует массив

### Установка элементов массива с помощью [лямбда-выражения](app://obsidian.md/Lambda)

Используем метод `parallelSetAll()` для установки элементов массива:
```java
import java.util.Arrays;

public class Program { 
    public static void main(String[] args) {
         
        int[] numbers = initializeArray(6);
        for(int i: numbers)
            System.out.println(i);
         
    } 
    public static int[] initializeArray(int size) {
        int[] values = new int[size];
        Arrays.parallelSetAll(values, i -> i*10);
        return values;
    }
}
```
В метод `Arrays.parallelSetAll` передается два параметра: изменяемый массив и функция, которая устанавливает элементы массива. Эта функция перебирает все элементы и в качестве параметра получает индекс текущего перебираемого элемента. Выражение `i -> i*10` означает, что по каждому индексу в массиве будет храниться число, равное i * 10. В итоге мы получим следующий вывод:
<p style="background-color: navy; color: yellow">
0<br>
10<br>
20<br>
30<br>
40<br>
50</p>

Рассмотрим более сложный пример. Пусть у нас есть следующий класс Phone:
```java
class Phone{
     
    private String name;
    private int price;
     
    public Phone(String name, int price){
        this.name=name;
        this.price = price;
    }
     
    public String getName() {
        return name;
    }
    public void setName(String val) {
        this.name=val;
    }
    public int getPrice() {
        return price;
    }
    public void setPrice(int val) {
        this.price=val;
    }
}
```
Теперь произведем манипуляции с массивом объектов Phone:
```java
Phone[] phones = new Phone[]{new Phone("iPhone 8", 54000), 
    new Phone("Pixel 2", 45000),
    new Phone("Samsung Galaxy S9", 40000),
    new Phone("Nokia 9", 32000)};
         
Arrays.parallelSetAll(phones, i -> {
    phones[i].setPrice(phones[i].getPrice()-10000); 
    return phones[i];
});
         
for(Phone p: phones)
    System.out.printf("%s - %d \n", p.getName(), p.getPrice());
```
Теперь [лямбда-выражение](Lambda) в методе `Arrays.parallelSetAll` представляет блок кода. И так как лямбда-выражение должно возвращать объект, то нам надо явным образом использовать оператор return. В этом лямбда-выражении опять же функция получает индексы перебираемых элементов, и по этим индексам мы можем обратиться к элементам массива и их изменить. Конкретно в данном случае происходит уменьшение цены смартфонов на 10000 единиц. В итоге мы получим следующий консольный вывод:
<p style="background-color: navy; color: yellow">
iPhone 8 - 44000 <br>
Pixel 2 - 35000 <br>
Samsung Galaxy S9 - 30000 <br>
Nokia 9 - 22000 </p>

### Сортировка

Отсортируем массив чисел в параллельном режиме:
```java
int[] nums = {30, -4, 5, 29, 7, -8};
Arrays.parallelSort(nums);
for(int i: nums)
    System.out.println(i);
```
Метод `Arrays.parallelSort()` в качестве параметра принимает массив и сортирует его по возрастанию:
<p style="background-color: navy; color: yellow">
-8<br>
-4<br>
5<br>
7<br>
29<br>
30</p>

Если же нам надо как-то по-другому отсортировать объекты, например, по модулю числа, или у нас более сложные объекты, то мы можем создать свой [компаратор](Comparator) и передать его в качестве второго параметра в `Arrays.parallelSort()`. Например, возьмем выше определенный класс Phone и создадим для него компаратор:
```java
import java.util.Arrays;
import java.util.Comparator;

public class Program {
    public static void main(String[] args) {
          
        Phone[] phones = new Phone[]{new Phone("iPhone 8", 54000), 
        new Phone("Pixel 2", 45000),
        new Phone("Samsung Galaxy S9", 40000),
        new Phone("Nokia 9", 32000)};
         
        Arrays.parallelSort(phones,new PhoneComparator());
         
        for(Phone p: phones)
            System.out.println(p.getName());
    }
}
class PhoneComparator implements Comparator<Phone>{
    public int compare(Phone a, Phone b){
	    return a.getName().toUpperCase().compareTo(b.getName().toUpperCase());
    }
}
```

### Метод parallelPrefix

Метод `parallelPrefix()` походит для тех случаев, когда надо получить элемент массива или объект того же типа, что и элементы массива, который обладает некоторыми признаками. Например, в массиве чисел это может быть максимальное, минимальное значения и т.д. Например, найдем произведение чисел:
```java
int[] numbers = {1, 2, 3, 4, 5, 6};
Arrays.parallelPrefix(numbers, (x, y) -> x * y);
 
for(int i: numbers)
    System.out.println(i);
```
Мы получим следующий результат:
<p style="background-color: navy; color: yellow">
1<br>
2<br>
6<br>
24<br>
120<br>
720</p>
То есть, как мы видим из консольного вывода, лямбда-выражение из `Arrays.parallelPrefix`, которое представляет бинарную функцию, получает два элемента и выполняет над ними операцию. Результат операции сохраняется и передается в следующий вызов бинарной функции.