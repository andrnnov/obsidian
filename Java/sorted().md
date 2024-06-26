#Java #StreamAPI 
## [Сортировка](https://metanit.com/java/tutorial/10.8.php)

Коллекции, на основе которых нередко создаются потоки, уже имеют специальные методы для сортировки содержимого. Однако класс [Stream](StreamAPI) также включает возможность сортировки. Такую сортировку мы можем задействовать, когда у нас идет набор промежуточных операций с потоком, которые создают новые наборы данных, и нам надо эти наборы отсортировать.

Для простой сортировки по возрастанию применяется метод sorted():
```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;
 
public class Program {
  
    public static void main(String[] args) {
          
        List<String> phones = new ArrayList<String>();
        Collections.addAll(phones, "iPhone X", "Nokia 9", "Huawei Nexus 6P",
                "Samsung Galaxy S8", "LG G6", "Xiaomi MI6",
                "ASUS Zenfone 3", "Sony Xperia Z5", "Meizu Pro 6",
                "Pixel 2");
          
        phones.stream()
                .filter(p->p.length()<12)
                .sorted() // сортировка по возрастанию
                .forEach(s->System.out.println(s));
    } 
}
```
Консольный вывод после сортировки объектов:
<p style="background-color: navy; color: yellow">
LG G6<br>
Meizu Pro 6<br>
Nokia 9<br>
Pixel 2<br>
Xiaomi MI6<br>
iPhone X</p>
Однако данный метод не всегда подходит. Уже по консольному выводу мы видим, что метод сортирует объекты по возрастанию, но при этом заглавные и строчные буквы рассматриваются отдельно.

Кроме того, данный метод подходит только для сортировки тех объектов, которые реализуют интерфейс [Comparable](Comparable).

Если же у нас классы объектов не реализуют этот интерфейс или мы хотим создать какую-то свою логику сортировки, то мы можем использовать другую версию метода `sorted()`, которая в качестве параметра принимает компаратор.

Например, пусть у нас есть следующий класс Phone:
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
Отсортируем поток объектов Phone:
```java
import java.util.Comparator;
import java.util.stream.Stream;
 
public class Program {
 
    public static void main(String[] args) {
 
        Stream<Phone> phoneStream = Stream.of(new Phone("iPhone X", "Apple", 600), 
            new Phone("Pixel 2", "Google", 500),
            new Phone("iPhone 8", "Apple",450),
            new Phone("Nokia 9", "HMD Global",150),
            new Phone("Galaxy S9", "Samsung", 300));
         
        phoneStream.sorted(new PhoneComparator())
                .forEach(p->System.out.printf("%s (%s) - %d \n", 
                        p.getName(), p.getCompany(), p.getPrice()));
         
    } 
}
class PhoneComparator implements Comparator<Phone>{
  
    public int compare(Phone a, Phone b){
      
        return a.getName().toUpperCase().compareTo(b.getName().toUpperCase());
    }
}
```
Здесь определен класс компаратора PhoneComparator, который сортирует объекты по полю name. В итоге мы получим следующий вывод:
<p style="background-color: navy; color: yellow">
Galaxy S9 (Samsung) - 300 <br>
iPhone 8 (Apple) - 450 <br>
iPhone X (Apple) - 600<br>
Nokia 9 (HMD Global) - 150 <br>
Pixel 2 (Google) - 500</p>
