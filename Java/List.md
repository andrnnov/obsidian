#Java #Collections #List 
#### [Java List](https://www.jenkov.com/tutorials/java-collections/list.html) 

2023-10-31 12:45

Интерфейс Java List, java.util. Список, представляющий собой упорядоченную последовательность объектов. Элементы, содержащиеся в списке Java, могут быть вставлены, доступны, повторены и удалены в соответствии с порядком, в котором они отображаются внутри списка Java. Порядок расположения элементов - вот почему эта структура данных называется списком.

Каждый элемент в Java List имеет индекс. Первый элемент в List имеет индекс 0, второй элемент имеет индекс 1 и т.д. Индекс означает "на сколько элементов больше от начала списка". Таким образом, первый элемент находится на расстоянии 0 элементов от начала списка - потому что он находится в начале списка.

Вы можете добавить любой объект Java в список List . Если список не типизирован, используя Java Generics, то вы даже можете смешивать объекты разных типов (классов) в одном списке. Однако на практике смешивание объектов разных типов в одном и том же списке не часто выполняется.

Интерфейс Java List - это стандартный интерфейс Java, и он является подтипом интерфейса Java [Collection](Collections), что означает, что List наследуется от Collection.

#### List и Set 

Интерфейсы Java List и Java [Set](Set) очень похожи в том смысле, что оба они представляют собой набор элементов. Однако есть некоторые существенные различия. Эти различия отражены в методах, предлагаемых интерфейсами List и Set. 

Первое различие между Java List и Java Set interface заключается в том, что один и тот же элемент может встречаться в Java List более одного раза. Это отличается от множества Set  Java, где каждый элемент может встречаться только один раз. 

Второе различие между интерфейсами Java List и Java Set заключается в том, что элементы в списке List имеют определенный порядок, и элементы могут повторяться в этом порядке. Множество Set Java не дает никаких обещаний относительно порядка элементов, хранящихся внутри.

#### Реализация списка 

Будучи подтипом Collection, все методы в интерфейсе [[Collections#Интерфейс Java Collection|Collection]] также доступны в интерфейсе List.

Поскольку List - это интерфейс, вам нужно создать экземпляр конкретной реализации интерфейса, чтобы использовать его. Вы можете выбрать одну из следующих реализаций списка в Java Collections API:
- [java.util.ArrayList](Class-ArrayList)
- [java.util.LinkedList](Class-LinkedList)
- [java.util.Vector](Vector)
- [java.util.Stack](Stack)

Из этих реализаций [ArrayList](Class-ArrayList) является наиболее часто используемой. 
#### Создание списка ####

Из этих реализаций ArrayList является наиболее часто используемой. Вы создаете экземпляр списка, создавая экземпляр одного из классов, реализующих интерфейс списка. Вот несколько примеров того, как создать экземпляр списка:
```java
List listA = new ArrayList();
List listB = new LinkedList();
List listC = new Vector();
List listD = new Stack();
```
Помните, что чаще всего вы будете использовать класс ArrayList, но могут быть случаи, когда использование одной из других реализаций может иметь смысл.

#### Generic Lists 

По умолчанию вы можете поместить любой объект в список, но начиная с Java 5, Java [Generics](Generics) позволяет ограничить типы объектов, которые вы можете вставить в список. Вот пример:
```java
List<MyObject> list = new ArrayList<MyObject>();
```
Теперь в этот список могут быть вставлены только экземпляры MyObject. Затем вы можете получить доступ к его элементам и выполнять их итерацию, не приводя их в действие. Вот как это выглядит:
```java
List<MyObject> list = new ArrayList<MyObject>();

list.add(new MyObject("First MyObject"));

MyObject myObject = list.get(0);

for(MyObject anObject : list){
   //do someting to anObject...
}
```
Без дженериков приведенный выше пример выглядел бы примерно так:
```java
List list = new ArrayList();   //no generic type specified

list.add(new MyObject("First MyObject"));

MyObject myObject = (MyObject) list.get(0);  //cast needed

for(Object anObject : list){
    //cast needed
    MyObject theMyObject = (MyObject) anObject;
   //do someting to anObject...
}
```
Обратите внимание, что необходимо преобразовать экземпляры MyObject, извлеченные из списка, в MyObject. Без универсального типа, заданного в объявлении переменной списка, компилятор Java знает только о том, что список содержит экземпляры объектов. Таким образом, вам нужно привести их к конкретному классу (или интерфейсу), к которому, как вы знаете, относится объект.

Хорошей практикой является указание общего типа для переменных вашего списка всякий раз, когда это возможно. Это поможет вам избежать вставки неправильных типов объектов в список. Это позволяет вам извлекать объекты из списка без необходимости приводить их к их реальному типу. И - это помогает читателю вашего кода увидеть, какой тип объектов должен содержать список. Вы должны опустить универсальный тип только в том случае, если у вас есть для этого очень веские причины.

#### Вставка элементов в список 

Вы можете вставить элементы (объекты) в список Java, используя его метод add(). Вот пример добавления элементов в список Java с помощью метода add():
```java
List<String> listA = new ArrayList<>();

listA.add("element 1");
listA.add("element 2");
listA.add("element 3");
```
Первые три вызова add() добавляют экземпляры String в конец списка.

#### Вставить нулевые значения 

На самом деле можно вставить нулевые значения в список List Java. Вот пример вставки нулевого значения в список Java:
```java
Object element = null;

List<Object> list = new ArrayList<>();

list.add(element);
```

#### Вставлять элементы с определенным индексом 

Можно вставить элемент в список List Java по определенному индексу. Интерфейс списка имеет версию метода add(), который принимает индекс в качестве первого параметра, а элемент для вставки - в качестве второго параметра. Вот пример вставки элемента с индексом 0 в список Java:
```java
list.add(0, "element 4");
```
Если список уже содержал элементы, то теперь эти элементы будут перемещены дальше вниз по внутренней последовательности списка. Элемент, который имел индекс 0 до того, как новый элемент был вставлен с индексом 0, будет перенесен в индекс 1 и т.д.

#### Вставка элементов из одного списка в другой

Можно добавить все элементы из одного списка Java в другой список. Вы делаете это с помощью метода List addAll(). Результирующий список представляет собой объединение двух списков. Вот пример добавления всех элементов из одного списка в другой:
```java
List<String> listSource = new ArrayList<>();

listSource.add("123");
listSource.add("456");

List<String> listDest   = new ArrayList<>();

listDest.addAll(listSource);
```
В этом примере все элементы из listSource добавляются в listDest.

Метод addAll() принимает коллекцию в качестве параметра, поэтому вы можете передать либо список, либо Java [Set](Set) в качестве параметра. Другими словами, вы можете добавить все элементы из списка или установить в список с помощью addAll(). 

#### Получение элементов из списка

Вы можете получить элементы из списка Java, используя индекс элементов. Вы можете сделать это, используя любой метод get(int index). Вот пример доступа к элементам списка Java с использованием индексов элементов:
```java
List<String> listA = new ArrayList<>();

listA.add("element 0");
listA.add("element 1");
listA.add("element 2");

//access via index
String element0 = listA.get(0);
String element1 = listA.get(1);
String element3 = listA.get(2);
```
Также возможно выполнять итерацию элементов списка Java в том порядке, в котором они хранятся внутри.

#### Поиск элементов в списке

Вы можете найти элементы в списке Java, используя один из этих двух методов:
- indexOf()
- lastIndexOf()

Метод indexOf() находит индекс первого вхождения в списке данного элемента. Вот пример нахождения индекса двух элементов в списке Java:
```java
List<String> list = new ArrayList<>();

String element1 = "element 1";
String element2 = "element 2";

list.add(element1);
list.add(element2);

int index1 = list.indexOf(element1);
int index2 = list.indexOf(element2);

System.out.println("index1 = " + index1);
System.out.println("index2 = " + index2);
```
Выполнение этого кода приведет к такому результату:
<p style="background-color: navy; color: yellow">
index1 = 0<br>
index2 = 1</p>

#### Найти последнее вхождение элемента в списке 

Метод lastIndexOf() находит индекс последнего вхождения в списке данного элемента. Вот пример, показывающий, как найти индекс последнего вхождения данного элемента в списке Java:
```java
List<String> list = new ArrayList<>();

String element1 = "element 1";
String element2 = "element 2";

list.add(element1);
list.add(element2);
list.add(element1);

int lastIndex = list.lastIndexOf(element1);
System.out.println("lastIndex = " + lastIndex);
```
Выходные данные, напечатанные в результате выполнения приведенного выше примера Java, будут следующими:
<p style="background-color: navy; color: yellow">
lastIndex = 2</p>

Элемент element 1 встречается в списке 2 раза. Индекс последнего вхождения равен 2.

#### Проверка, содержит ли список элемент

Вы можете проверить, содержит ли список Java данный элемент, используя метод List contains(). Вот пример проверки того, содержит ли список Java элемент, с помощью метода contains():
```java
List<String> list = new ArrayList<>();

String element1 = "element 1";

list.add(element1);
boolean containsElement = list.contains("element 1");
System.out.println(containsElement);
```
Результатом выполнения этого примера будет: 
<p style="background-color: navy; color: yellow">true</p>
... потому что список действительно содержит этот элемент.

Чтобы определить, содержит ли список элемент, список будет внутренне перебирать свои элементы и сравнивать каждый элемент с объектом, переданным в качестве параметра. При сравнении используется метод Java equals элемента, чтобы проверить, равен ли элемент параметру. 

Поскольку в список можно добавлять нулевые значения, на самом деле можно проверить, содержит ли список нулевое значение. Вот как вы проверяете, содержит ли список нулевое значение:
```java
list.add(null);

containsElement = list.contains(null);

System.out.println(containsElement);
```

Очевидно, что если входной параметр contains() равен null, метод contains() не будет использовать метод equals() для сравнения с каждым элементом, а скорее будет использовать оператор `==`.

#### Удаление элементов из списка 

Вы можете удалить элементы из списка Java с помощью этих двух методов: 
1. remove(Object element)
2. remove(int index)

remove(Object element) - удаляет этот элемент из списка, если он присутствует. Затем все последующие элементы в списке перемещаются вверх по списку. Таким образом, их индекс уменьшается на 1. Вот пример удаления элемента из списка Java на основе самого элемента:
```java
List<String> list = new ArrayList<>();

String element = "first element";
list.add(element);

list.remove(element);
```
В этом примере сначала добавляется элемент в список, а затем снова удаляется.

Метод List remove(int index) удаляет элемент с заданным индексом. Затем все последующие элементы в списке перемещаются вверх по списку. Таким образом, их индекс уменьшается на 1. Вот пример удаления элемента из списка Java по его индексу:
```java
List<String> list = new ArrayList<>();

list.add("element 0");
list.add("element 1");
list.add("element 2");

list.remove(0);
```
После запуска этого примера кода Java список будет содержать строковые элементы Java element 1 и element 2 с индексами 0 и 1. Первый элемент (элемент 0) был удален из списка.

#### Удаление всех элементов из списка

Интерфейс Java List содержит метод clear(), который удаляет все элементы из списка при вызове. Удаление всех элементов из списка также называется очисткой списка. Вот простой пример удаления всех элементов из списка с помощью метода clear():
```java
List<String> list = new ArrayList<>();

list.add("object 1");
list.add("object 2");
//etc.

list.clear();
```
Сначала создается новый список. Во-вторых, в список добавляются два элемента. В-третьих, вызывается метод clear(). После вызова метода clear() список будет полностью пуст.

#### Сохранить все элементы из одного списка в другом

Интерфейс Java List имеет метод retainAll(), который способен сохранять все элементы из одного списка, которые также присутствуют в другом списке. Другими словами, метод retain() удаляет все элементы из целевого списка, которые не найдены в другом списке. Результирующий список является пересечением двух списков. Вот Java-пример вызова метода List retainAll():
```java
List<String> list      = new ArrayList<>();
List<String> otherList = new ArrayList<>();

String element1 = "element 1";
String element2 = "element 2";
String element3 = "element 3";
String element4 = "element 4";

list.add(element1);
list.add(element2);
list.add(element3);

otherList.add(element1);
otherList.add(element3);
otherList.add(element4);

list.retainAll(otherList);
```
Создаются первые два списка. Во-вторых, 3 элемента добавляются в список и 3 элемента добавляются в otherList. В-третьих, метод retainAll() вызывается в list, передавая otherList в качестве параметра. После завершения выполнения list.retainAll(otherList) список будет содержать только те элементы, которые присутствовали как в list, так и в otherList до вызова retainAll(). Более конкретно, это element1 и element3.

#### List size() 

Вы можете получить количество элементов в списке, вызвав метод size(). Вот пример:
```java
List<String> list = new ArrayList<>();

list.add("object 1");
list.add("object 2");

int size = list.size();
```

#### Подсписок списка 

Интерфейс Java List имеет метод, называемый subList(), который может создавать новый список с подмножеством элементов из исходного списка. 

Метод subList() принимает 2 параметра: начальный индекс и конечный индекс. Начальный индекс - это индекс первого элемента из исходного списка, включаемого в подсписок. Конечный индекс - это последний индекс подсписка, но элемент с последним индексом не включен в подсписок. Это похоже на то, как работает метод Java String substring. 

Вот пример Java создания подсписка элементов из другого списка с использованием метода subList():
```java
List<String> list      = new ArrayList<>();

list.add("element 1");
list.add("element 2");
list.add("element 3");
list.add("element 4");

List<String> sublist = list.subList(1, 3);
```
После выполнения инструкции list.subList(1,3) подсписок будет содержать элементы с индексами 1 и 2. Помните, что исходный список содержит 4 элемента с индексами от 0 до 3. Вызов list.subList(1,3) будет включать индекс 1, но исключать индекс 3, тем самым сохраняя элементы с индексами 1 и 2.

#### Конвертировать List в [Set](Set) 

Вы можете преобразовать список List Java в множество Set Java, создав новое множество и добавив в него все элементы из списка List. Множество удалит все дубликаты. Таким образом, результирующее множество будет содержать все элементы из списка List, но только один раз. Вот пример преобразования списка Java в множество:
```java
List<String> list      = new ArrayList<>();

list.add("element 1");
list.add("element 2");
list.add("element 3");
list.add("element 3");

Set<String> set = new HashSet<>();
set.addAll(list);
```
Обратите внимание, что список содержит строковый элемент 3 два раза. Множество будет содержать эту строку только один раз. Таким образом, результирующее множество будет содержать строки element 1, element 2 и element 3.

#### Преобразовать список в массив 

Вы можете преобразовать список Java в массив Java, используя метод List toArray(). Вот пример преобразования списка Java в массив Java:
```java
List<String> list = new ArrayList<>();

list.add("element 1");
list.add("element 2");
list.add("element 3");
list.add("element 3");

Object[] objects = list.toArray();
```
Также возможно преобразовать список в массив определенного типа. Вот пример преобразования списка Java в массив определенного типа:
```java
List<String> list = new ArrayList<>();

list.add("element 1");
list.add("element 2");
list.add("element 3");
list.add("element 3");

String[] objects1 = list.toArray(new String[0]);
```
Обратите внимание, что даже если мы передадим массив строк размером 0 в toArray(), возвращаемый массив будет содержать в себе все элементы из списка. В нем будет то же количество элементов, что и в списке.

#### Конвертировать массив в список

Пример преобразования массива Java в список:
```java
String[] values = new String[]{ "one", "two", "three" };

List<String> list = (List<String>) Arrays.asList(values);
```
Это метод Arrays.asList() преобразует массив в список.

#### Сортировка списка

Вы можете отсортировать список Java, используя метод [Collections](Collections) sort().

##### Сортировка списка сопоставимых объектов #####

Если список содержит объекты, реализующие интерфейс [Comparable (java.lang.Comparable)](Comparable), тогда объекты могут сравнивать себя друг с другом. В этом случае вы можете отсортировать список следующим образом:
```java
List<String> list = new ArrayList<>();

list.add("c");
list.add("b");
list.add("a");

Collections.sort(list);
```
Класс Java String реализует интерфейс Comparable, вы можете отсортировать их в их естественном порядке, используя метод Collections sort().

##### Сортировка списка с использованием [Comparator](Comparator)

Если объекты в списке Java не реализуют интерфейс Comparable или если вы хотите отсортировать объекты в другом порядке, чем их реализация compare(), тогда вам нужно использовать реализацию [Comparator](Comparator) (java.util.Comparator). Вот пример сортировки списка объектов Car с помощью компаратора. Вот, во-первых, класс автомобиля:
```java
public class Car{
    public String brand;
    public String numberPlate;
    public int noOfDoors;

    public Car(String brand, String numberPlate, int noOfDoors) {
        this.brand = brand;
        this.numberPlate = numberPlate;
        this.noOfDoors = noOfDoors;
    }
}
```
Вот код, который сортирует Java-список вышеуказанных объектов Car:
```java
List<Car> list = new ArrayList<>();

list.add(new Car("Volvo V40" , "XYZ 201845", 5));
list.add(new Car("Citroen C1", "ABC 164521", 4));
list.add(new Car("Dodge Ram" , "KLM 845990", 2));

Comparator<Car> carBrandComparator = new Comparator<Car>() {
    @Override
    public int compare(Car car1, Car car2) {
        return car1.brand.compareTo(car2.brand);
    }
};

Collections.sort(list, carBrandComparator);
```
Обратите внимание на реализацию компаратора в приведенном выше примере. Эта реализация сравнивает только поле марки объектов Car. Можно создать другую реализацию компаратора, которая сравнивает номерные знаки или даже количество дверей в автомобилях. 

Обратите также внимание, что можно реализовать компаратор, используя Java Lambda. Вот пример, который сортирует список объектов Car, используя три различные реализации Java lambda интерфейса Comparator, каждая из которых сравнивает экземпляры Car по другому полю:
```java
List<Car> list = new ArrayList<>();

list.add(new Car("Volvo V40" , "XYZ 201845", 5));
list.add(new Car("Citroen C1", "ABC 164521", 4));
list.add(new Car("Dodge Ram" , "KLM 845990", 2));


Comparator<Car> carBrandComparatorLambda      =
    (car1, car2) -> car1.brand.compareTo(car2.brand);

Comparator<Car> carNumberPlatComparatorLambda =
    (car1, car2) -> car1.numberPlate.compareTo(car2.numberPlate);

Comparator<Car> carNoOfDoorsComparatorLambda  =
    (car1, car2) -> car1.noOfDoors - car2.noOfDoors;

Collections.sort(list, carBrandComparatorLambda);
Collections.sort(list, carNumberPlatComparatorLambda);
Collections.sort(list, carNoOfDoorsComparatorLambda);
```

#### Итерация списка 

Вы можете выполнить итерацию списка Java несколькими различными способами:
- Используя [Iterator](Iterator)
- Используя цикл for-each 
- Используя цикла for
- Используя Java [Stream API](StreamAPI)
- 
##### Итерация списка с использованием итератора 

Первый способ выполнить итерацию списка - это использовать Java-итератор. Вот пример итерации списка с помощью итератора:
```java
List<String> list = new ArrayList<>();

list.add("first");
list.add("second");
list.add("third");

Iterator<String> iterator = list.iterator();
while(iterator.hasNext()) {
    String next = iterator.next();
}
```
Вы получаете итератор, вызывая метод iterator() интерфейса List. Как только вы получили итератор, вы можете продолжать вызывать его метод hasNext() до тех пор, пока он не вернет значение false. Вызов hasNext() выполняется внутри цикла while, как вы можете видеть. 

Внутри цикла while вы вызываете метод Iterator next() интерфейса [Iterator](Iterator), чтобы получить следующий элемент, на который указывает итератор. 

Если список набран с использованием Java [Generics](Generics), вы можете сохранить некоторое приведение объекта внутри цикла while. Вот пример:
```java
List<String> list = new ArrayList<>();

list.add("first");
list.add("second");
list.add("third");
    
Iterator<String> iterator = list.iterator();
while(iterator.hasNext()){
    String obj = iterator.next();
}
```
##### Итерация списка с использованием цикла for-each #####

Второй способ перебора списка - использовать цикл for-each, добавленный в Java 5 (также называемый циклом "для каждого"). Вот пример итерации списка с использованием цикла for-each:
```java
List list = new ArrayList();

list.add("first");
list.add("second");
list.add("third");

for(Object element : list) {
    System.out.println(element);
}
```
Цикл for выполняется один раз для каждого элемента в списке. Внутри цикла for каждый элемент, в свою очередь, привязан к переменной obj. 

Если список типизирован (общий список), вы можете изменить тип переменной внутри цикла for. Вот пример итерации набранного списка:
```java
List<String> list = new ArrayList<String>();

//add elements to list

for(String element : list) {
    System.out.println(element);
}
```
Обратите внимание, как список преобразуется в строку. Следовательно, вы можете установить тип переменной внутри цикла for равным String.

##### Итерация списка с использованием цикла for

Третий способ перебора списка - использовать стандартный цикл for, подобный этому:
```java
List list = new ArrayList();

list.add("first");
list.add("second");
list.add("third");
    
for(int i=0; i < list.size(); i++) {
    Object element = list.get(i);
}
```
Цикл for создает переменную int и инициализирует ее значением 0. Затем он повторяется до тех пор, пока переменная int i не станет меньше размера списка. Для каждой итерации переменная i увеличивается. 

Внутри цикла for пример обращается к элементам списка с помощью своего метода get(), передавая увеличивающуюся переменную i в качестве параметра. 

Опять же, если список вводится с использованием Java [Generics](Generics), например, в строку, то вы можете использовать общий тип списка в качестве типа для локальной переменной, которая присваивается каждому элементу в списке во время итерации. Пример сделает это более понятным:
```java
List<String> list = new ArrayList<String>();

list.add("first");
list.add("second");
list.add("third");
    
for(int i=0; i < list.size(); i++) {
    String element = list.get(i);
}
```
Обратите внимание, что тип локальной переменной внутри цикла for теперь является String. Поскольку список обычно типизируется как String, он может содержать только строковые объекты. Следовательно, компилятор знает, что из метода get() может быть возвращена только строка. Поэтому вам не нужно приводить элемент, возвращаемый функцией get(), к String.

##### Итерация списка с использованием Java Stream API

Четвертый способ итерации списка Java - через Java [Stream API](StreamAPI). Чтобы выполнить итерацию списка Java, вы должны сначала получить поток из списка. Получение потока из списка в Java осуществляется путем вызова метода List stream(). Вот пример получения потока Java из списка Java:
```java
List<String> stringList = new ArrayList<String>();

stringList.add("abc");
stringList.add("def");

Stream<String> stream = stringList.stream();
```
Именно в последней строке этого примера вызывается метод List stream() для получения потока, представляющего элементы в списке. 

Как только вы получили поток из списка, вы можете выполнить итерацию потока, вызвав его метод forEach(). Вот пример итерации элементов списка с использованием метода Stream forEach():
```java
List<String> stringList = new ArrayList<String>();

stringList.add("one");
stringList.add("two");
stringList.add("three");

Stream<String> stream = stringList.stream();
stream
    .forEach( element -> { System.out.println(element); });
```
Вызов метода forEach() заставит поток выполнить внутреннюю итерацию всего элемента потока и вызовет потребителя, переданного в качестве параметра методу forEach() для каждого элемента в потоке.