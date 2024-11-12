#Java #Comparable
### [Java Comparable](https://www.jenkov.com/tutorials/java-collections/comparable.html) ###

2023-11-02 12:09

Интерфейс Java Comparable, java.lang.Comparable, представляет объект, который можно сравнить с другими объектами. Например, можно сравнивать числа, строки можно сравнивать с помощью алфавитного сравнения и т.д. Несколько встроенных классов в Java реализуют Java Comparable interface. Вы также можете самостоятельно реализовать Java Comparable interface, чтобы сделать ваши собственные классы сопоставимыми.

Когда класс реализует Java Comparable interface, это означает, что экземпляры (объекты) этого класса можно сравнивать друг с другом, как упоминалось выше. Когда объекты можно сравнить, их можно отсортировать с помощью встроенной функции сортировки в Java. Эта функция сортировки может быть использована для сортировки коллекций объектов Java.

Пожалуйста, имейте в виду, что интерфейс Comparable предназначен для сравнения объектов одного и того же класса. Другими словами, сравнивая яблоки с яблоками и апельсины с апельсинами. Он не предназначен для сравнения яблок с апельсинами, строк с цифрами, дат с номерными знаками и т.д.
#### Определение интерфейса Comparable ####

Comparable интерфейс Java находится в пакете java.lang. Определение Comparable интерфейса Java выглядит следующим образом:
```java
package java.lang;
    
public interface Comparable<T> {
 
    int compareTo(T);
}
```
Как вы можете видеть, Java Comparable interfaces содержит только один метод.
#### compareTo() ####

Метод Java Comparable compareTo() принимает один объект в качестве параметра и возвращает значение int. Возвращаемый int сигнализирует о том, является ли объект, для которого вызывается метод compareTo(), больше, равен или меньше параметра object. Более конкретно:
- Положительное значение (1 или больше) сигнализирует о том, что объект, для которого вызывается функция compareTo(), больше объекта-параметра. 
- Нулевое значение (0) сигнализирует о том, что два объекта равны. 
- Отрицательное значение (-1 или меньше) сигнализирует о том, что объект, для которого вызываются методы compareTo(), меньше объекта-параметра.
##### Переходное сравнение #####

Обратите внимание, что при реализации Comparable интерфейса Java требуется, чтобы реализация учитывала следующие характеристики транзитивного сравнения: 
Если A больше, чем B, а B больше, чем C, то A также должно быть больше, чем C.
#### Java Comparable Example ####

чтобы лучше проиллюстрировать, как работает Java Comparable interface, позвольте мне показать вам простой пример. Класс Java Integer реализует интерфейс Comparable, поэтому вы можете вызвать compareTo().  Вот пример:
```java
public class ComparableExample {

    public static void main(String[] args) {

        Integer valA = Integer.valueOf(45);
        Integer valB = Integer.valueOf(99);

        int comparisonA = valA.compareTo(valB);
        int comparisonB = valB.compareTo(valA);

        System.out.println(comparisonA);
        System.out.println(comparisonB);
    }
}
```
В этом примере будут выведены следующие строки:
<p style="background-color: navy; color: yellow">
-1<br>
1</p>

Поскольку значение 45 меньше 99 - первое сравнение ( valA.compareTo(valB) = 45.compareTo(99)) приводит к возвращению значения -1. 
Во втором сравнении, когда 99 сравнивается с 45 (valB.compareTo(valA) = 99.compareTo(45)), результат равен 1 - потому что 99 больше, чем 45.
#### Реализация Comparable интерфейса Java ####

Вы можете самостоятельно реализовать Comparable интерфейс Java, если вам это нужно. Вот пример класса Spaceship, который может сравнивать себя с другими экземплярами Spaceship:
```java
public class Spaceship implements Comparable<Spaceship> {

    private String spaceshipClass = null;
    private String registrationNo = null;

    public Spaceship(String spaceshipClass, String registrationNo) {
        this.spaceshipClass = spaceshipClass;
        this.registrationNo = registrationNo;
    }

    @Override
    public int compareTo(Spaceship other) {
        int spaceshipClassComparison =
                this.spaceshipClass.compareTo(other.spaceshipClass);

        if(spaceshipClassComparison != 0) {
            return spaceshipClassComparison;
        }
        
        return this.registrationNo.compareTo(other.registrationNo);
    }
}
```
Обратите внимание, как в этом примере реализации сначала сравнивается spaceShipClass и, если они совпадают, продолжается сравнение по registrationNo. Таким образом, вы можете реализовать compareTo() для сравнения базы по нескольким факторам.

Обратите также внимание, как реализация указывает, что она реализует Comparable`<Spaceship>`, а не просто Comparable. При указании параметра type при реализации интерфейса Comparable параметр метода compareTo() изменяется с [Object](Object) на любой указанный вами тип. В этом случае параметром типа является Spaceship - и, таким образом, тип параметра тоже становится Spaceship.

Реализация без параметра type выглядела бы примерно так:
```java
public class Spaceship implements Comparable {

    private String spaceshipClass = null;
    private String registrationNo = null;

    public Spaceship(String spaceshipClass, String registrationNo) {
        this.spaceshipClass = spaceshipClass;
        this.registrationNo = registrationNo;
    }

    @Override
    public int compareTo(Object o) {
        Spaceship other = (Spaceship) o;

        int spaceshipClassComparison =
                this.spaceshipClass.compareTo(other.spaceshipClass);

        if(spaceshipClassComparison != 0) {
            return spaceshipClassComparison;
        }

        return this.registrationNo.compareTo(other.registrationNo);
    }
}
```
Обратите внимание, что в объявлении класса после интерфейса "implements Comparable" не указан параметр type. Обратите также внимание, что тип параметра объекта compareTo() больше не является Spaceship, а [Object](Object). Наконец, также обратите внимание, что теперь необходимо явно привести параметр метода compareTo() к Spaceship.

Обратите также внимание, что метод compareTo() должен вызывать исключение NullPointerException, если параметр object равен null. Это означает, что вам не нужно выполнять проверку null перед сравнением объектов.

Аналогично, метод compareTo() должен вызывать исключение ClassCastException, если входной параметр не относится к тому же классу, что и класс объекта, для которого вызывается compareTo(). Таким образом, явная проверка типа не требуется. Вы можете просто привести к нужному классу (как в примере выше). Если классы не совпадают, виртуальная машина Java выдаст исключение ClassCastException.
#### [Java Comparable Example 2](https://vertex-academy.com/tutorials/ru/interfejsy-comparable-comparator-java/) ####

Представим, что мы хотим сравнить два дома.
Давайте у нас будет класс **House**:
```java
public class House {
    int area;
    int price;
    String city;
    boolean hasFurniture;
}
```
Как Вы можете видеть, у нас есть четыре параметра - размер дома, цена, город, в котором дом находится, и **boolean** "**hasFurniture**" ("продается ли дом с мебелью"). Мы НЕ сделали эти переменные приватными чтобы не отягощать код и не писать гетеры и сеттеры на каждый параметр. Давайте просто добавим конструктор и метод "вывести все параметры":
```java
public class House {
    int area;
    int price;
    String city;
    boolean hasFurniture;
    public House(int area, int price, String city, boolean hasFurniture) {
        this.area = area;
        this.price = price;
        this.city = city;
        this.hasFurniture = hasFurniture;
    }
    @Override
    public String toString() {
        final StringBuffer sb = new StringBuffer("House{");
            sb.append("area=").append(area);
            sb.append(", price=").append(price);
            sb.append(", city='").append(city).append('\'');
            sb.append(", hasFurniture=").append(hasFurniture);
            sb.append('}');
        return sb.toString();
    }
}
```
Но пока мы не можем сравнить два объекта типа **House**. Например, если мы попробуем создать **TreeSet** из объектов типа **House** (а **TreeSet** всегда сортирует свои элементы) и добавить туда элемент:
```java
public class Test {
    public static void main(String[] args) {
       TreeSet<House> myHouseArrayList = new TreeSet<House>();
        House firstHouse = new House(100, 120000, "Tokyo", true);
        myHouseArrayList.add(firstHouse);
    }
}
```
получим ошибку:
![[Exception.png]]
Как мы уже говорили, **TreeSet** сортирует свои элементы - но в данном случае сортировать у него не получится, поскольку он не знает, по какому критерию нужно сортировать.

Теперь, давайте имплементируем  **Comparable**:
```java
public class House implements Comparable<House>{
    int area;
    int price;
    String city;
    boolean hasFurniture;
    public House(int area, int price, String city, boolean hasFurniture) {
        this.area = area;
        this.price = price;
        this.city = city;
        this.hasFurniture = hasFurniture;
    }
    @Override
    public String toString() {
        final StringBuffer sb = new StringBuffer("House{");
            sb.append("area=").append(area);
            sb.append(", price=").append(price);
            sb.append(", city='").append(city).append('\'');
            sb.append(", hasFurniture=").append(hasFurniture);
            sb.append('}');
        return sb.toString();
    }
    public int compareTo(House anotherHouse) {
        if (this.area == anotherHouse.area) {
            return 0;
        } else if (this.area < anotherHouse.area) {
            return -1;
        } else {
            return 1;
        }
    }
}
```
Как видите, мы решили сортировать дома по площади.
Теперь давайте создадим три объекта **House** и положим их в **TreeSet**:
```java
public class Test {
    public static void main(String[] args) {
       TreeSet<House> myHouseArrayList = new TreeSet<House>();
       
        House firstHouse = new House(100, 120000, "Tokyo", true);
        House secondHouse = new House(40, 70000, "Oxford", true);
        House thirdHouse = new House(70, 180000, "Paris", false);

        myHouseArrayList.add(firstHouse);
        myHouseArrayList.add(secondHouse);
        myHouseArrayList.add(thirdHouse);

        for (House h: myHouseArrayList) {
            System.out.println(h);
        }
    }
}
```
На экране получим:
<p style="background-color: navy; color: yellow">
Area: 40, price: 70000, city: Oxford, hasFurniture: true<br>
Area: 70, price: 180000, city: Paris, hasFurniture: false<br>
Area: 100, price: 120000, city: Tokyo, hasFurniture: true<br>
Process finished with exit code 0</p>

Как видите, наши дома стоят не в порядке добавления (Токио, Оксфорд, Париж), а отсортированы по площади (Оксфорд, Париж, Токио). Ну, и ошибок, естественно, тоже нет.

Кстати, метод **compareTo(T o)**, который требует реализовать интерфейс **Comparable**, часто называют "естественным сравнением" ("_natural comparison method_") - т.е. методом по умолчанию. Основные типы (например, Integer, String, Float) уже имеют свои методы **compareTo(T o)**.

Тем не менее, если Вам нужен "нестандартный" вид сортировки - следует использовать **[Comparator](Comparator)**.
