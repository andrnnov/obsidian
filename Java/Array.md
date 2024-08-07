#Java #Array 
#### [Java Arrays](https://www.jenkov.com/tutorials/java/arrays.html) ####

2023-11-01 17:05

Массив Java - это набор переменных одного и того же типа. Например, массив int - это набор переменных типа int. Переменные в массиве упорядочены, и каждая из них имеет индекс
#### Объявление массива в Java ####

Переменная массива Java объявляется точно так же, как вы бы объявили переменную желаемого типа, за исключением того, что вы добавляете [ ] после типа. Вот простой пример объявления массива Java:
```java
int[] intArray;
```
Вы можете использовать массив Java в качестве поля, статического поля, локальной переменной или параметра, как и любую другую переменную. Массив - это просто разновидность типа данных. Вместо того, чтобы быть единственной переменной этого типа, это набор переменных этого типа. Вот еще несколько примеров объявления массива Java:
```java
String[]  stringArray;

MyClass[] myClassArray;
```
В первой строке объявляется массив ссылок на строки. Во второй строке объявляется массив ссылок на объекты класса MyClass, который символизирует класс, созданный вами самостоятельно. На самом деле у вас есть выбор относительно того, где поместить квадратные скобки [], когда вы объявляете массив в Java. Первую локацию вы уже видели. Это стоит за именем типа данных (например, String[]). 

Второе местоположение находится после имени переменной. Все следующие объявления массива Java на самом деле допустимы:
```java
int[] intArray;
int   intArray[];

String[] stringArray;
String   stringArray[];

MyClass[] myClassArray;
MyClass   myClassArray[];
```
#### Создание экземпляра массива в Java ####

Когда вы объявляете переменную массива Java, вы объявляете только переменную (ссылку) на сам массив. Объявление на самом деле не создает массив. Вы создаете массив, подобный этому:
```java
int[] intArray;
intArray = new int[10];
```
В этом примере создается массив типа int с пространством для 10 переменных int внутри. В предыдущем примере Java array был создан массив int, который является примитивным типом данных. Вы также можете создать массив ссылок на объекты. Например:
```java
String[] stringArray = new String[10];
```
Java позволяет создавать массив ссылок на объекты любого типа (на экземпляры любого класса).
#### Литералы массива Java ####

Язык программирования Java содержит ярлык для создания экземпляров массивов примитивных типов и строк. Если вы уже знаете, какие значения вставлять в массив, вы можете использовать литерал массива. Вот как выглядит литерал массива в Java-коде:
```java
int[]   ints2 = new int[]{ 1,2,3,4,5,6,7,8,9,10 };
```
Обратите внимание, что значения, которые должны быть вставлены в массив, перечислены внутри { ... }. Длина этого списка также определяет длину созданного массива. На самом деле, вам не нужно писать новую часть int[] в последних версиях Java. Вы можете просто написать:
```java
int[]   ints2 = { 1,2,3,4,5,6,7,8,9,10 };
```
Это часть внутри фигурных скобок, которая называется литералом массива. Этот стиль работает для массивов всех примитивных типов, а также для массивов строк. Вот пример строкового массива:
```java
 String[] strings = {"one", "two", "three"};
```
#### Длина массива Java не может быть изменена ####

Как только массив создан, его размер не может быть изменен. В некоторых языках программирования (например, JavaScript) массивы могут изменять свой размер после создания, но в Java массив не может изменить свой размер после создания. Если вам нужна структура данных, подобная массиву, которая может изменять свой размер, вам следует использовать список List или вы можете создать изменяемый размер Java-массива. В некоторых случаях вы также можете использовать Java RingBuffer, который, кстати, реализован с использованием Java array внутренне.
#### Доступ к элементам массива Java ####

Каждая переменная в массиве Java также называется "элементом". Таким образом, в примере, показанном ранее, был создан массив с пространством для 10 элементов, и каждый элемент является переменной типа int. Каждый элемент в массиве имеет индекс (число). Вы можете получить доступ к каждому элементу массива через его индекс. Вот пример:
```java
intArray[0] = 0;

int firstInt = intArray[0];
```
Этот пример сначала устанавливает значение элемента (int) с индексом 0, а во-вторых, считывает значение элемента с индексом 0 в переменную int. 

Вы можете использовать элементы в массиве Java точно так же, как если бы они были обычными переменными. Вы можете считывать их значение, присваивать им значения, использовать элементы в вычислениях и передавать определенные элементы в качестве параметров вызовам методов. Индексы элементов в массиве Java всегда начинаются с 0 и продолжаются до числа 1, которое находится ниже размера массива. 

Таким образом, в приведенном выше примере с массивом из 10 элементов индексы изменяются от 0 до 9.
#### Array Length ####

Вы можете получить доступ к длине массива через его поле длины length . Вот пример:
```java
int[] intArray = new int[10];

int arrayLength = intArray.length;
```
В этом примере переменная с именем arrayLength будет содержать значение 10 после выполнения второй строки кода.
#### Итерация массива ####

Вы можете выполнить цикл по всем элементам массива, используя цикл Java for. Вот пример итерации массива с помощью цикла for в Java:
```java
String[] stringArray = new String[10];

for(int i=0; i < stringArray.length; i++) {
    stringArray[i] = "String no " + i;
}

for(int i=0; i < stringArray.length; i++) {
    System.out.println( stringArray[i] );
}
```
В этом примере сначала создается массив ссылок на строки. Когда вы впервые создаете массив ссылок на объекты, каждая из ячеек в массиве указывает на null - отсутствие объекта. Первый из двух циклов for выполняет итерацию по массиву String, создает строку и заставляет ячейку ссылаться на эту строку. Второй из двух циклов for выполняет итерацию по массиву строк и выводит все строки, на которые ссылаются ячейки. Если бы это был массив int (примитивных значений), это могло бы выглядеть следующим образом: 
```java
int[] intArray = new int[10];

for(int i=0; i < intArray.length; i++) {
    intArray[i] = i;
}

for(int i=0; i < intArray.length; i++) {
    System.out.println( intArray[i] );
}
```
Переменная i инициализируется значением 0 и выполняется до тех пор, пока длина массива не станет минус 1. В этом случае я принимаю значения от 0 до 9, каждый раз повторяя код внутри цикла for один раз, и для каждой итерации у меня есть другое значение. 

Вы также можете выполнить итерацию массива, используя цикл "for-each" в Java. Вот как это выглядит:
```java
int[] intArray = new int[10];

for(int theInt : intArray) {
    System.out.println(theInt);
}
```
Цикл for-each предоставляет вам доступ к каждому элементу массива по одному за раз, но не дает вам никакой информации об индексе каждого элемента. Кроме того, у вас есть доступ только к этому значению. Вы не можете изменить значение элемента в этой позиции. Если вам это нужно, используйте обычный цикл for, как показано ранее. 
For-each цикл также работает с массивами объектов. Вот пример, показывающий вам, как выполнить итерацию массива строковых объектов:
```java
String[] stringArray = {"one", "two", "three"};

for(String theString : stringArray) {
    System.out.println(theString);
}
```
#### Многомерные массивы Java ####

В приведенных выше примерах все созданные массивы имеют одно измерение, что означает элементы с индексами от 0 и выше. Однако возможно создавать массивы, в которых каждый элемент имеет два или более индексов, которые идентифицируют (локализуют) его в массиве. 

Вы создаете многомерный массив в Java, добавляя по одному набору квадратных скобок ([]) для каждого измерения, которое вы хотите добавить. Вот пример, который создает двумерный массив:
```java
int[][] intArray = new int[10][20];
```
В этом примере создается двумерный массив элементов int. Массив содержит 10 элементов в первом измерении и 20 элементов во втором измерении. Другими словами, в этом примере создается массив массивов элементов int. В массиве массивов есть место для 10 массивов int, и в каждом массиве int есть место для 20 элементов int. Вы получаете доступ к элементам в многомерном массиве с одним индексом на измерение. В приведенном выше примере вам пришлось бы использовать два индекса. Вот пример:
```java
int[][] intArray = new int[10][20];

intArray[0][2] = 129;

int oneInt = intArray[0][2];
```
Переменная с именем oneInt будет содержать значение 129 после выполнения последней строки Java-кода.
#### Итерация многомерных массивов ####

Когда вы выполняете итерацию многомерного массива в Java, вам нужно выполнять итерацию каждого измерения массива отдельно. Вот как выглядит многомерное повторение в Java:
```java
int[][] intArray = new int[10][20];

for(int i=0; i < intArrays.length; i++){
    for(int j=0; j < intArrays[i].length; j++){
        System.out.println("i: " + i + ", j: " + j);
    }
}
```
#### Вставка элементов в массив ####

Иногда вам нужно куда-то вставить элементы в массив Java. Вот как вы вставляете новое значение в массив в Java:
```java
int[] ints   = new int[20];

int insertIndex = 10;
int newValue    = 123;

//move elements below insertion point.
for(int i=ints.length-1; i > insertIndex; i--){
    ints[i] = ints[i-1];
}

//insert new value
ints[insertIndex] = newValue;

System.out.println(Arrays.toString(ints));
```
В примере сначала создается массив. Затем он определяет индекс вставки и новое значение для вставки. Затем все элементы от индекса вставки и до конца массива сдвигаются на один индекс вниз в массиве. Обратите внимание, что это приведет к смещению последнего значения в массиве за пределы массива (оно будет просто удалено).

Приведенный выше код вставки массива может быть встроен в метод Java. Вот как это могло бы выглядеть:
```java
public void insertIntoArray(int[] array, int insertIndex, int newValue){
    //move elements below insertion point.
    for(int i=array.length-1; i > insertIndex; i--){
        array[i] = array[i-1];
    }
    //insert new value
    array[insertIndex] = newValue;
}
```
Этот метод принимает массив int[] в качестве параметра, а также индекс для вставки нового значения и само новое значение. Вы можете вставить элементы в массив, вызвав этот метод следующим образом:
```java
int[] ints   = new int[20];

insertIntoArray(ints, 0, 10);
insertIntoArray(ints, 1, 23);
insertIntoArray(ints, 9, 67);
```
Конечно, если метод insertIntoArray() находится в классе, отличном от приведенного выше кода, вам понадобится объект этого класса, чтобы иметь возможность вызывать метод. Или, если метод insertIntoArray() был статическим, вам нужно было бы поместить имя класса и точку перед именем метода.
#### Удаление элементов из массива ####

Иногда вы хотите удалить элемент из массива Java. Вот код для удаления элемента из массива в Java:
```java
int[] ints   = new int[20];

ints[10] = 123;

int removeIndex = 10;

for(int i = removeIndex; i < ints.length -1; i++){
    ints[i] = ints[i + 1];
}
```
В этом примере сначала создается массив int. Затем он устанавливает значение элемента с индексом от 10 до 123. Затем в примере удаляется элемент с индексом 10. Он удаляет элемент, сдвигая все элементы ниже индекса 10 на одну позицию вверх в массиве. После удаления последний элемент в массиве будет существовать дважды. Как в последнем, так и в предпоследнем элементе. Приведенный выше код может быть встроен в метод Java. Вот как мог бы выглядеть такой Java-метод удаления массива:
```java
public void removeFromArray(
    int[] array, int removeIndex){

    for(int i = removeIndex; i < array.length -1; i++){
        array[i] = array[i + 1];
    }
}
```
Этот метод removeFromArray() принимает два параметра: массив, из которого нужно удалить элемент, и индекс удаляемого элемента. Конечно, если метод removeFromArray() находится в классе, отличном от приведенного выше кода, вам понадобится объект этого класса, чтобы иметь возможность вызывать метод. Или, если метод removeFromArray() был статическим, вам нужно было бы указать имя класса и точку перед именем метода.
#### Поиск минимального и максимального значений в массивах ####

Иногда вам может понадобиться найти минимальное или максимальное значение в массиве Java. Java не имеет никаких встроенных функций для нахождения минимального и максимального значения, поэтому я покажу вам, как закодировать это самостоятельно. Вот, во-первых, как вы находите минимальное значение в массиве:
```java
int[] ints = {0,2,4,6,8,10};

int minVal = Integer.MAX_VALUE;

for(int i=0; i < ints.length; i++){
    if(ints[i] < minVal){
        minVal = ints[i];
    }
}
System.out.println("minVal = " + minVal);
```
В примере сначала задается значение minVal равным целому числу.MAX_VALUE, которое является максимально возможным значением, которое может принимать int. Это делается для того, чтобы убедиться, что начальное значение случайно не меньше наименьшего значения в массиве. Во-вторых, в примере выполняется итерация по массиву и сравнивается каждое значение с MinValue. Если элемент в массиве меньше minVal, то minVal присваивается значение элемента. Наконец, выводится минимальное значение, найденное в массиве. В приведенном выше примере минимальное значение равно 0.

Вот как вы находите максимальное значение в массиве. Это очень похоже на поиск минимального значения.
```java
int[] ints = {0,2,4,6,8,10};

int maxVal = Integer.MIN_VALUE;
for(int i=0; i < ints.length; i++){
    if(ints[i] > maxVal){
        maxVal = ints[i];
    }
}
System.out.println("maxVal = " + maxVal);
```
В этом примере будет выведено значение 10. 

Основными отличиями поиска минимального значения является инициализация maxVal и сравнение maxVal с элементами массива.
#### The Arrays Class ####

Java содержит специальный служебный класс, который упрощает вам выполнение многих часто используемых операций с массивами, таких как копирование и сортировка массивов, заполнение данных, поиск в массивах и т.д. Служебный класс называется Arrays и находится в стандартном Java-пакете java.util. Таким образом, полное имя класса является:
```java
java.util.Arrays
```
Помните, что для того, чтобы использовать java.util.Arrays в ваших классах Java, которые вы должны импортировать. Вот как выполняется импорт java.util.Arrays можно было бы искать в вашем собственном классе Java:
```java
package myjavaapp;

import java.util.Arrays;

public class MyClass{
    public static void main(String[] args) {
    }
}
```
#### Копирование массивов ####

Вы можете скопировать массив в другой массив в Java несколькими способами.
##### Копирование массива путем итерации массива #####

Первый способ скопировать массив в Java - это выполнить итерацию по массиву и скопировать каждое значение исходного массива в целевой массив. Вот как выглядит копирование массива с использованием этого метода:
```java
int[] source = new int[10];
int[] dest   = new int[10];

for(int i=0; i < source.length; i++) {
    source[i] = i;
}

for(int i=0; i < source.length; i++) {
    dest[i] = source[i];
}
```
Создаются первые два массива int. Во-вторых, исходный массив инициализируется значениями от 0 до 9 (от 0 до длины массива минус 1). В-третьих, каждый элемент в исходном массиве копируется в целевой массив.
##### Копирование массива с использованием Arrays.copyOf() #####

Второй способ скопировать массив Java - это использовать метод Arrays.copyOf(). Вот как выглядит копирование массива с помощью Arrays.copyOf():
```java
int[] source = new int[10];

for(int i=0; i < source.length; i++) {
    source[i] = i;
}

int[] dest = Arrays.copyOf(source, source.length);
```
Метод Arrays.copyOf() принимает 2 параметра. Первый параметр - это массив для копирования. Второй параметр - это длина нового массива. Этот параметр можно использовать для указания количества элементов из исходного массива для копирования.
##### Копирование массива с использованием Arrays.copyOfRange() #####

Третий способ скопировать массив Java - это использовать метод Arrays.copyOfRange(). Метод Arrays.copyOfRange() копирует диапазон массива, не обязательно полный массив. Вот как выглядит копирование полного массива с помощью Arrays.copyOfRange() в Java:
```java
int[] source = new int[10];

for(int i=0; i < source.length; i++) {
    source[i] = i;
}
int[] dest = Arrays.copyOfRange(source, 0, source.length);
```
Метод Arrays.copyOfRange() принимает 3 параметра. Первый параметр - это массив для копирования. Второй параметр - это первый индекс в исходном массиве, который необходимо включить в копию. Третий параметр - это последний индекс в исходном массиве, который нужно включить в копию (исключен - поэтому передача 10 приведет к копированию до тех пор, пока не будет включен индекс 9). 
#### Преобразование массивов в строки с помощью Arrays.toString() ####

Вы можете преобразовать массив Java примитивных типов в строку, используя метод Arrays.toString(). Вот пример того, как преобразовать массив int в строку с помощью Arrays.toString():
```java
int[]   ints = new int[10];

for(int i=0; i < ints.length; i++){
    ints[i] = 10 - i;
}
System.out.println(java.util.Arrays.toString(ints));
```
Первая строка создает массив int из 10 элементов. Цикл for инициализирует массив значениями от 10 до 1. В последней строке выводится значение, возвращаемое из Arrays.toString(). Возвращаемая строка (которая печатается) выглядит следующим образом:
==[10, 9, 8, 7, 6, 5, 4, 3, 2, 1]==
#### Сортировка массива ####

Вы можете отсортировать элементы массива, используя метод Arrays.sort(). Сортировка элементов массива изменяет порядок расположения элементов в соответствии с порядком их сортировки. Вот пример Arrays.sort():
```java
int[]   ints = new int[10];

for(int i=0; i < ints.length; i++){
    ints[i] = 10 - i;
}
System.out.println(java.util.Arrays.toString(ints));
java.util.Arrays.sort(ints);
System.out.println(java.util.Arrays.toString(ints));
```
В первой строке объявляется и создается экземпляр массива int длиной 10; 
Цикл for выполняет итерацию по массиву и вставляет значения в каждый элемент. Введенные значения будут варьироваться от 10 до 1 в порядке убывания. После цикла for массив преобразуется в строку с помощью Arrays.toString() и выводится на консоль (командная строка). На данный момент выходные данные, записанные в консоль (строковая версия массива), выглядят следующим образом:
==[10, 9, 8, 7, 6, 5, 4, 3, 2, 1]==
Затем массив сортируется с помощью Arrays.sort(). Теперь элементы будут упорядочены в порядке возрастания. После сортировки массива он снова преобразуется в строку и выводится на консоль. Вывод, напечатанный на этот раз, выглядит следующим образом:
==[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]==
#### Сортировка массивов объектов ####

Пример Arrays.sort(), показанный ранее, работает только для массивов Java примитивных типов данных. Примитивные типы данных Java имеют естественный порядок, либо их числовой порядок, либо порядок символов в таблице ASCII (двоичное число, представляющее символ). 

Если вы хотите отсортировать массив объектов, вам нужно использовать другой метод. Объекты могут не иметь какого-либо естественного порядка сортировки, поэтому вам нужно предоставить другой объект, который способен определять порядок ваших объектов. Такой объект называется компаратором.

Вот первый класс для объектов, которые мы хотим отсортировать:
```java
private static class Employee{
    public String name;
    public int    employeeId;

    public Employee(String name, int employeeId){
        this.name       = name;
        this.employeeId = employeeId;
    }
}
```
Класс Employee - это простая модель сотрудника (я создал класс Employee). У сотрудника есть имя и идентификатор сотрудника. Потенциально вы могли бы отсортировать массив объектов Employee по имени или по их идентификатору сотрудника. Я покажу вам, как сделать и то, и другое. Вот первый пример сортировки массива объектов Employee по их именам с использованием метода Arrays.sort():
```java
Employee[] employeeArray = new Employee[3];

employeeArray[0] = new Employee("Xander", 1);
employeeArray[1] = new Employee("John"  , 3);
employeeArray[2] = new Employee("Anna"  , 2);

java.util.Arrays.sort(employeeArray, new Comparator<Employee>() {
    @Override
    public int compare(Employee e1, Employee e2) {
        return e1.name.compareTo(e2.name);
    }
});
for(int i=0; i < employeeArray.length; i++) {
    System.out.println(employeeArray[i].name);
}
```
Сначала объявляется массив Java. Массив имеет тип Employee - класс, который я показывал вам ранее. Во-вторых, создаются и вставляются в массив три объекта Employee.

В-третьих, метод Arrays.sort() вызывается для сортировки массива. В качестве параметра методу Arrays.sort() мы передаем массив employee и реализацию компаратора, которая может определять порядок объектов Employee.  Это создает анонимную реализацию интерфейса компаратора.  В реализации также используются [дженерики](Generics) Java.

Что важно уловить в этом примере, так это реализацию метода compare() анонимной внутренней реализации интерфейса [Comparator](Comparator). Этот метод возвращает положительное число, если первый объект "больше" (позже в порядке сортировки), чем второй объект, 0 они "равны" (в порядке сортировки) и отрицательное число, если первый объект "меньше" (раньше в порядке сортировки), чем второй объект. В приведенном выше примере мы просто вызываем метод String.compare(), который выполняет сравнение за нас (сравнивает имена сотрудников).

После сортировки массива мы перебираем его и выводим имена сотрудников. Вот как выглядит напечатанный результат:
==Anna
John
Xander==

Обратите внимание, что порядок был изменен на противоположный по сравнению с тем порядком, в котором они были первоначально вставлены в массив. 

Давайте теперь посмотрим, как выглядит сортировка объектов Employee по их идентификатору сотрудника. Вот пример из предыдущего, с измененной реализацией метода compare() анонимной реализации интерфейса [Comparator](Comparator):
```java
Employee[] employeeArray = new Employee[3];

employeeArray[0] = new Employee("Xander", 1);
employeeArray[1] = new Employee("John"  , 3);
employeeArray[2] = new Employee("Anna"  , 2);

java.util.Arrays.sort(employeeArray, new Comparator<Employee>() {
    @Override
    public int compare(Employee e1, Employee e2) {
        return e1.employeeId - e2.employeeId;
    }
});

for(int i=0; i < employeeArray.length; i++) {
    System.out.println(employeeArray[i].name);
}
```
Обратите внимание, как метод compare() возвращает разницу между идентификаторами сотрудников путем вычитания одного из другого. Это самый простой способ определить естественный порядок числовых переменных. Выходные данные, выведенные из этого кода, будут следующими:
==Xander
Anna
John==

Чтобы сравнить объекты Employee в массиве сначала по их имени, и если это одно и то же, то по их идентификатору сотрудника, реализация compare() будет выглядеть следующим образом:
```java
java.util.Arrays.sort(employeeArray, new Comparator<Employee>() {
    @Override
    public int compare(Employee e1, Employee e2) {
        int nameDiff = e1.name.compareTo(e2.name);
        if(nameDiff != 0) { return nameDiff; }
    
        return e1.employeeId - e2.employeeId;
    }
});
```
#### Заполнение массивов с помощью arrays.fill() ####

Класс Arrays имеет набор методов, называемых fill(). Эти методы Arrays.fill() могут заполнять массив заданным значением. Это проще, чем перебирать массив и вставлять значение самостоятельно. Вот пример использования Arrays.fill() для заполнения массива int:
```java
int[] intArray = new int[10];

Arrays.fill(intArray, 123);

System.out.println(Arrays.toString(intArray));
```
В этом примере создается массив int и заполняется значением 123 во все элементы массива. Последняя строка примера преобразует массив в строку и выводит его на консоль. Вот как выглядел бы результат:

==[123, 123, 123, 123, 123, 123, 123, 123, 123, 123]==

Существует версия метода Arrays.fill(), который принимает значения from и to index, поэтому только элементы с индексами в этом интервале заполняются заданным значением. Вот пример этого метода Arrays.fill():
```java
int[] intArray = new int[10];

Arrays.fill(ints2, 3, 5, 123) ;

System.out.println(Arrays.toString(intArray));
```
В этом примере только элементы с индексами 3 и 4 (от 3 до 5 без 5) заполняются значением 123. Вот выходные данные, распечатанные из этого примера:

==[0, 0, 0, 123, 123, 0, 0, 0, 0, 0]==
#### Поиск массивов с помощью Arrays.BinarySearch() ####

Класс Arrays содержит набор методов, называемых BinarySearch(). Этот метод поможет вам выполнить двоичный поиск в массиве. Сначала массив должен быть отсортирован. Вы можете сделать это самостоятельно или с помощью метода Arrays.sort(), описанного ранее в этом тексте. Вот пример Arrays.BinarySearch():
```java
int[] ints = {0,2,4,6,8,10};

int index = Arrays.binarySearch(ints, 6);

System.out.println(index);
```
Вторая строка этого примера выполняет поиск в массиве значения 6. Метод BinarySearch() вернет индекс в массиве, в котором был найден элемент. В приведенном выше примере метод BinarySearch() вернул бы значение 3. 

Если в массиве существует более одного элемента с искомым значением, нет никакой гарантии относительно того, какой элемент будет найден. Если ни один элемент с заданным значением не найден, будет возвращено отрицательное число. Отрицательное число будет индексом, по которому будет вставлен искомый элемент, а затем минус единица. Посмотрите на этот пример:
```java
int[] ints = {0,2,4,6,8,10};

int index = Arrays.binarySearch(ints, 7);

System.out.println(index);
```
Число 7 не найдено в массиве. Число 7 должно было быть вставлено в массив с индексом 4, если в массив должно было быть вставлено 7 (и сохранен порядок сортировки). Следовательно, функция BinarySearch() возвращает -4 - 1 = -5 .

Если все элементы в массиве меньше искомого значения, то функция BinarySearch() вернет - длина массива - 1. Посмотрите на этот пример:
```java
int[] ints = {0,2,4,6,8,10};

int index = Arrays.binarySearch(ints, 12);

System.out.println(index);
```
В этом примере мы ищем 12 в массиве, но все элементы в массиве меньше 12. Поэтому функция BinarySearch() вернет значение -length (-6) - 1 = -6 -1 = -7.

Метод Arrays.BinarySearch() также существует в версии, в которой вы просто выполняете поиск по части массива. Вот как это выглядит:
```java
int[] ints = {0,2,4,6,8,10};

int index = Arrays.binarySearch(ints, 0, 4, 2);

System.out.println(index);
```
В этом примере выполняется поиск в массиве значения 2, но только между индексами от 0 до 4 (без 4).

Эта версия BinarySearch() работает точно так же, как и другая версия, за исключением случаев, когда соответствующий элемент не найден. Если ни один элемент не найден соответствующим в пределах интервала индекса, то функция BinarySearch() все равно вернет индекс того места, куда должно было быть вставлено значение. Но, если все значения в интервале меньше искомого значения, функция BinarySearch() вернет -toIndex -1 , а не -array length - 1. Таким образом, этот пример BinarySearch()
```java
int[] ints = {0,2,4,6,8,10};

int index = Arrays.binarySearch(ints, 0, 4, 12);
```
вернет -5, а не -7, как это было бы при BinarySearch(ints, 12).
#### Проверка равенства массивов с помощью Arrays.equals() ####

Java.util.Arrays содержит набор методов, называемых equals(), которые можно использовать для проверки равенства двух массивов Java. Два массива считаются равными, если массивы имеют одинаковую длину, а элементы равны друг другу в том порядке, в котором они находятся в массиве. Посмотрите на этот пример Arrays.equals():
```java
int[] ints1 = {0,2,4,6,8,10};
int[] ints2 = {0,2,4,6,8,10};
int[] ints3 = {10,8,6,4,2,0};

boolean ints1EqualsInts2 = Arrays.equals(ints1, ints2);
boolean ints1EqualsInts3 = Arrays.equals(ints1, ints3);

System.out.println(ints1EqualsInts2);
System.out.println(ints1EqualsInts3);
```
В этом примере массив ints1 сравнивается с массивами ints2 и ints3. Первое сравнение приведет к значению true, поскольку ints1 и ints2 содержат одни и те же элементы в одном и том же порядке. Второе сравнение приведет к значению false. Массив ints1 содержит те же элементы, что и ints3, но не в том же порядке. Поэтому два массива не считаются равными.
