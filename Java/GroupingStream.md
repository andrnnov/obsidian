#Java #StreamAPI 

## Группировка

2024-04-03 16:49

Чтобы сгруппировать данные по какому-нибудь признаку, нам надо использовать в связке метод [`collect()`](collect()) объекта [Stream](StreamAPI) и метод Collectors.groupingBy() класса [[collect()#Класс Collectors|Collectors]]. Допустим, у нас есть следующий класс:
```java
class Phone{
     
    private String name;
    private String company;
    private int price;
     
    public Phone(String name, String comp, int price){
        this.name=name;
        this.company=comp;
        this.price = price;
    }
     
    public String getName() { return name; }
    public int getPrice() { return price; }
    public String getCompany() { return company; }
}
```
И, к примеру, у нас есть набор объектов Phone, которые мы хотим сгруппировать по компании:
```java
import java.util.List;
import java.util.Map;
import java.util.stream.Stream;
import java.util.stream.Collectors;
 
public class Program {
  
    public static void main(String[] args) {
          
        Stream<Phone> phoneStream = Stream.of(new Phone("iPhone X", "Apple", 600), 
            new Phone("Pixel 2", "Google", 500),
            new Phone("iPhone 8", "Apple",450),
            new Phone("Galaxy S9", "Samsung", 440),
            new Phone("Galaxy S8", "Samsung", 340));
          
        Map<String, List<Phone>> phonesByCompany = phoneStream.collect(
                Collectors.groupingBy(Phone::getCompany));
          
        for(Map.Entry<String, List<Phone>> item : phonesByCompany.entrySet()){
              
            System.out.println(item.getKey());
            for(Phone phone : item.getValue()){
                  
                System.out.println(phone.getName());
            }
            System.out.println();
        } 
    } 
}
```
Консольный вывод:
<p style="background-color: navy; color: yellow">
Google<br>
Pixel 2<br>
<br>
Apple<br>
iPhone X<br>
iPhone 8<br>
<br>
Samsung<br>
Galaxy S9<br>
Galaxy S8</p>
Итак, для создания групп в метод `phoneStream.collect()` передается вызов функции `Collectors.groupingBy()`, которая с помощью выражения `Phone::getCompany` группирует объекты по компании. В итоге будет создан объект [Map](Map), в котором ключами являются названия компаний, а значениями - список связанных с компаниями телефонов.

### Метод Collectors.partitioningBy

Метод Collectors.partitioningBy() имеет похожее действие, только он делит элементы на группы по принципу, соответствует ли элемент определенному условию. Например:
```java
Map<Boolean, List<Phone>> phonesByCompany = phoneStream.collect(
                Collectors.partitioningBy(p->p.getCompany()=="Apple"));
         
for(Map.Entry<Boolean, List<Phone>> item : phonesByCompany.entrySet()){
             
    System.out.println(item.getKey());
    for(Phone phone : item.getValue()){
                 
        System.out.println(phone.getName());
    }
    System.out.println();
}
```
В данном случае с помощью условия `p->p.getCompany()=="Apple"` мы смотрим, принадлежит ли телефон компании Apple. Если телефон принадлежит этой компании, то он попадает в одну группу, если нет, то в другую.

### Метод Coollectors.counting

Метод Collectors.counting применяется в `Collectors.groupingBy()` для вычисления количества элементов в каждой группе:
```java
Map<String, Long> phonesByCompany = phoneStream.collect(
        Collectors.groupingBy(Phone::getCompany, Collectors.counting()));
         
for(Map.Entry<String, Long> item : phonesByCompany.entrySet()){
 
    System.out.println(item.getKey() + " - " + item.getValue());
}
```
Консольный вывод:
<p style="background-color: navy; color: yellow">
Google -1<br>
Apple - 2<br>
Samsung - 2</p>

### Методы maxBy и minBy

Методы maxBy и minBy применяются для подсчета минимального и максимального значения в каждой группе. В качестве параметра эти методы принимают функцию компаратора, которая нужна для сравнения значений. Например, найдем для каждой компании телефон с минимальной ценой:
```java
Map<String, Optional<Phone>> phonesByCompany = phoneStream.collect(
        Collectors.groupingBy(Phone::getCompany, 
                Collectors.minBy(Comparator.comparing(Phone::getPrice))));
         
for(Map.Entry<String, Optional<Phone>> item : phonesByCompany.entrySet()){
 
    System.out.println(item.getKey() + " - " + item.getValue().get().getName());
}
```
Консольный вывод:
<p style="background-color: navy; color: yellow">
Google - Pixel 2<br>
Apple - iPhone 8<br>
Samsung - Galaxy S8</p>
В качестве возвращаемого значения операции группировки используется объект `Map<String, Optional<Phone>>`. Опять же поскольку группируем по компаниям, то ключом будет выступать строка, а значением - объект [Optional](Optional) `Optional<Phone>`.

### Метод summarizing

Методы `summarizingInt() / summarizingLong() / summarizingDouble()` позволяют объединить в набор значения соответствующих типов:
```java
import java.util.IntSummaryStatistics;
//....................................
 
 Map<String, IntSummaryStatistics> priceSummary = phoneStream.collect(
    Collectors.groupingBy(Phone::getCompany,
        Collectors.summarizingInt(Phone::getPrice)));
         
for(Map.Entry<String, IntSummaryStatistics> item : priceSummary.entrySet()){
 
    System.out.println(item.getKey() + " - " + item.getValue().getAverage());
}
```
Метод `Collectors.summarizingInt(Phone::getPrice))` создает набор, в который помещаются цены для всех телефонов каждой из групп. Данный набор инкапсулируется в объекте IntSummaryStatistics. Соответственно если бы мы применяли методы `summarizingLong()` или `summarizingDouble()`, то соответственно бы получали объекты LongSummaryStatistics или DoubleSummaryStatistics.

У этих объектов есть ряд методов, который позволяют выполнить различные атомарные операции над набором:
- getAverage(): возвращает среднее значение 
- getCount(): возвращает количество элементов в наборе
- getMax(): возвращает максимальное значение
- getMin(): возвращает минимальное значение
- getSum(): возвращает сумму элементов
- accept(): добавляет в набор новый элемент

В данном случае мы получаем среднюю цену смартфонов для каждой группы.
Консольный вывод:
<p style="background-color: navy; color: yellow">
Google - 500.0<br>
Apple - 525.0<br>
Samsung - 390.0</p>

### Метод mapping

Метод mapping позволяет дополнительно обработать данные и задать функцию отображения объектов из потока на какой-нибудь другой тип данных. Например:
```java
Map<String, List<String>> phonesByCompany = phoneStream.collect(
    Collectors.groupingBy(Phone::getCompany,
        Collectors.mapping(Phone::getName, Collectors.toList())));
         
for(Map.Entry<String, List<String>> item : phonesByCompany.entrySet()){
 
    System.out.println(item.getKey());
    for(String name : item.getValue()){
        System.out.println(name);
    }
}
```
Выражение `Collectors.mapping(Phone::getName, Collectors.toList())` указывает, что в группу будут выделиться названия смартфонов, причем группа будет представлять объект [List](List).