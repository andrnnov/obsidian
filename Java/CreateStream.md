#Java #StreamAPI 
## Создание потока данных

2024-04-03 14:49

Для создания потока данных можно применять различные методы. В качестве источника потока мы можем использовать коллекции. В частности, в JDK 8 в интерфейс [[Collections#Типы коллекций. Интерфейс Collection|Collection]], который реализуется всеми классами коллекций, были добавлены два метода для работы с потоками:
- `default Stream<E> stream`: возвращается поток данных из коллекции;
- `default Stream<E> parallelStream`: возвращается параллельный поток данных из коллекции.

Так, рассмотрим пример с [ArrayList](Class-ArrayList):
```java
import java.util.stream.Stream;
import java.util.*;
public class Program {
 
    public static void main(String[] args) {
         
        ArrayList<String> cities = new ArrayList<String>();
        Collections.addAll(cities, "Париж", "Лондон", "Мадрид");
        cities.stream() // получаем поток
            .filter(s->s.length()==6) // применяем фильтрацию по длине строки
            .forEach(s->System.out.println(s)); // выводим отфильтрованные строки на консоль
    }
}
```
Здесь с помощью вызова `cities.stream()` получаем поток, который использует данные из списка cities. С помощью каждой промежуточной операции, которая применяется к потоку, мы также можем получить поток с учетом модификаций. Например, мы можем изменить предыдущий пример следующим образом:
```java
ArrayList<String> cities = new ArrayList<String>();
Collections.addAll(cities, "Париж", "Лондон", "Мадрид");
 
Stream<String> citiesStream = cities.stream(); // получаем поток
citiesStream = citiesStream.filter(s->s.length()==6); // применяем фильтрацию по длине строки
citiesStream.forEach(s->System.out.println(s)); // выводим отфильтрованные строки на консоль
```

Важно, что после использования терминальных операций другие терминальные или промежуточные операции к этому же потоку не могут быть применены, поток уже употреблен. Например, в следующем случае мы получим ошибку:
```java
citiesStream.forEach(s->System.out.println(s)); // терминальная операция употребляет поток
long number = citiesStream.count(); // здесь ошибка, так как поток уже употреблен
System.out.println(number);
citiesStream = citiesStream.filter(s->s.length()>5); // тоже нельзя, так как поток уже употреблен
```
Фактически жизненный цикл потока проходит следующие три стадии:
1. Создание потока
2. Применение к потоку ряда промежуточных операций
3. Применение к потоку терминальной операции и получение результата

#### Создание пустого потока с помощью метода Stream.empty()

Можно создать пустой поток для использования на более поздних этапах кода. Если использовать метод Stream.empty(), то будет сгенерирован пустой поток, не содержащий значений. Этот пустой поток может пригодиться, если мы хотим пропустить исключение нулевого указателя во время выполнения. Для этого можно использовать следующую команду:
```java
Stream<String> str = Stream.empty();
```
Приведенный выше оператор сгенерирует пустой поток с именем str без каких-либо элементов внутри него. Чтобы убедиться в этом достаточно проверить количество или размер потока с помощью термина str.count(). Например,
```java
System.out.println(str.count());
```
В результате получим на выводе 0.

#### Создание потока с использованием метода Stream.builder() с экземпляром Stream.Builder

Мы также можем использовать Stream Builder для создания потока с помощью шаблона проектирования builder. Он предназначен для пошагового построения объектов. Давайте посмотрим, как мы можем создать экземпляр потока с помощью Stream Builder.
```java
Stream.Builder<Integer> numBuilder = Stream.builder();
numBuilder.add(1).add(2).add( 3);
Stream<Integer> numStream = numBuilder.build();
```
Используя этот код, можно создать поток с именем numStream, содержащий элементы int. Все выполняется достаточно быстро благодаря экземпляру Stream.Builder под именем numBuilder, который создается первым.

#### Создание потока из существующего массива с использованием метода Arrays.stream()

Кроме выше рассмотренных методов мы можем использовать еще ряд способов для создания потока данных. Один из таких способов представляет метод Arrays.stream(T[] array), который создает поток данных из массива:
```java
Stream<String> citiesStream = Arrays.stream(new String[]{"Париж", "Лондон", "Мадрид"}) ;
citiesStream.forEach(s->System.out.println(s)); // выводим все элементы массива
```
Для создания потоков IntStream, DoubleStream, LongStream можно использовать соответствующие перегруженные версии этого метода:
```java
IntStream intStream = Arrays.stream(new int[]{1,2,4,5,7});
intStream.forEach(i->System.out.println(i));
 
LongStream longStream = Arrays.stream(new long[]{100,250,400,5843787,237});
longStream.forEach(l->System.out.println(l));
 
DoubleStream doubleStream = Arrays.stream(new double[] {3.4, 6.7, 9.5, 8.2345, 121});
doubleStream.forEach(d->System.out.println(d));
```

#### Создание потока с указанными значениями с помощью метода Stream.of()

Еще один способ создания потока представляет статический метод of(T..values) класса Stream:
```java
Stream<String> citiesStream =Stream.of("Париж", "Лондон", "Мадрид");
citiesStream.forEach(s->System.out.println(s));
 
// можно передать массив
String[] cities = {"Париж", "Лондон", "Мадрид"};
Stream<String> citiesStream2 =Stream.of(cities);
        
IntStream intStream = IntStream.of(1,2,4,5,7);
intStream.forEach(i->System.out.println(i));
 
LongStream longStream = LongStream.of(100,250,400,5843787,237);
longStream.forEach(l->System.out.println(l));
 
DoubleStream doubleStream = DoubleStream.of(3.4, 6.7, 9.5, 8.2345, 121);
doubleStream.forEach(d->System.out.println(d));
```

