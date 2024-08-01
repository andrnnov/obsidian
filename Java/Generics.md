#Java #Generics

2023-09-22 14:39
### Java – Дженерики (обобщения) ###


Было бы неплохо, если бы мы могли написать один метод сортировки, который мог бы сортировать элементы в массиве Integer, массиве String или массиве любого типа, поддерживающего упорядочение.

Java методы обобщения и общие классы позволяют программистам указывать с объявлением одного метода набор связанных методов или с объявлением одного класса набор связанных типов, соответственно.

В Java дженерики также обеспечивают безопасность типа компиляции, которая позволяет программистам ловить недопустимые типы во время компиляции.

Используя концепцию Java Generic, мы можем написать общий метод для сортировки массива объектов, а затем вызвать общий метод с массивами Integer, Double, String и т.д., чтобы отсортировать элементы массива.
### Общие методы ###

Вы можете написать одно обобщенное объявление метода, которое можно вызвать с помощью аргументов разных типов. Основываясь на типах аргументов, переданных на общий метод, компилятор обрабатывает каждый вызов метода соответствующим образом. Ниже приведены правила определения общих методов:

- Все объявления обобщенного метода имеют раздел параметров типа, разделенный угловыми скобками (), который предшествует возвращаемому типу метода ( в следующем примере).
- Раздел параметров каждого типа содержит один или несколько параметров типа, разделенных запятыми. Параметр типа, также известный как переменная типа, является идентификатором, который указывает общее имя типа.
- Параметры типа могут использоваться для объявления возвращаемого типа и действуют как заполнители для типов аргументов, переданных в общий метод, которые известны как аргументы фактического типа.
- Тело общего метода объявлено как тело любого другого метода. Обратите внимание, что параметры типа могут представлять только ссылочные типы, а не примитивные типы (например, int, double и char).

>_Для обозначения дженерик-типа в классе Box мы использовали латинскую букву T. Это необязательно, то есть можно было бы использовать любую другую букву или даже слово — `Box<MyType>`. Тем не менее есть набор рекомендаций от Oracle о том, когда какие обозначения лучше использовать в дженериках. Вот они:
 E — element, для элементов параметризованных коллекций;
 K — key, для ключей map-структур;
 V — value, для значений map-структур;
 N — number, для чисел;
 T — type, для обозначения типа параметра в произвольных классах;
 S, U, V и так далее — применяются, когда в дженерик-классе несколько параметров.`
#### Пример 

Следующий пример показывает, как мы можем выводить массив различного типа, используя один общий:
```java
public class GenericMethodTest {
   // Общий метод printArray
   public static < E > void printArray( E[] inputArray ) {
      // Отображаем элементы массива
      for(E element : inputArray) {
         System.out.printf("%s ", element);
      }
      System.out.println();
   }

   public static void main(String args[]) {
      // Создание массивов типа Integer, Double и Character
      Integer[] intArray = { 1, 2, 3, 4, 5 };
      Double[] doubleArray = { 1.1, 2.2, 3.3, 4.4 };
      Character[] charArray = { 'П', 'Р', 'И', 'В', 'Е', 'Т'};

      System.out.println("Массив integerArray содержит:");
      printArray(intArray);   // передать массив Integer

      System.out.println("\nМассив doubleArray содержит:");
      printArray(doubleArray);   // передать массив Double

      System.out.println("\nМассив characterArray содержит:");
      printArray(charArray);   // передать массив Character
   }
}
```
Получим следующий результат:
<p style="background-color: navy; color: yellow">
Массив integerArray содержит:<br>
1 2 3 4 5 <br>
Массив doubleArray содержит:<br>
1.1 2.2 3.3 4.4 <br>
Массив characterArray содержит:<br>
П Р И В Е Т</p>

### [Параметры ограниченного типа](BorderedGeneric)

Могут быть случаи, когда вы захотите ограничить виды типов, которым разрешено быть переданными типу параметра. Например, метод, который работает с числами, может только принимать экземпляры Number или его подклассов. Для этого используются параметры ограниченного типа.

Чтобы объявить параметр ограниченного типа, введите имя параметра типа, за которым следует ключевое слово extends, а затем его верхняя граница.
#### Пример

Следующий пример иллюстрирует, как extends используется в общем смысле для обозначения либо «extends» (как в классах), либо «implements» (как в интерфейсах). Это пример общего метода для возврата самого большого из трех объектов [Comparable](Comparable):
```java
public class MaximumTest {
   // determines the largest of three Comparable objects
   
   public static <T extends Comparable<T>> T maximum(T x, T y, T z) {
      T max = x;   // assume x is initially the largest
      
      if(y.compareTo(max) > 0) {
         max = y;   // y is the largest so far
      }
      
      if(z.compareTo(max) > 0) {
         max = z;   // z is the largest now                 
      }
      return max;   // returns the largest object   
   }
   
   public static void main(String args[]) {
      System.out.printf("Max of %d, %d and %d is %d\n\n", 
         3, 4, 5, maximum( 3, 4, 5 ));

      System.out.printf("Max of %.1f,%.1f and %.1f is %.1f\n\n",
         6.6, 8.8, 7.7, maximum( 6.6, 8.8, 7.7 ));

      System.out.printf("Max of %s, %s and %s is %s\n","pear",
         "apple", "orange", maximum("pear", "apple", "orange"));
   }
}
```
Получим следующий результат:
<p style="background-color: navy; color: yellow">
Max of 3, 4 and 5 is 5<br>
Max of 6.6,8.8 and 7.7 is 8.8<br>
Max of pear,apple and orange is pear</p>

### Общие классы

Объявление общего класса выглядит как объявление не общего класса, за исключением того, что за именем класса следует раздел параметров типа.

Как и в случае с общими методами, раздел параметров типа универсального класса может иметь один или несколько параметров типа, разделенных запятыми. Эти классы известны как параметризованные классы или параметризованные типы, поскольку они принимают один или несколько параметров.
#### Пример 1

Следующий пример показывает, как мы можем определить общий класс:
```java
public class Box {
   private T t;

   public void add(T t) {
      this.t = t;
   }

   public T get() {
      return t;
   }

   public static void main(String[] args) {
      Box integerBox = new Box();
      Box stringBox = new Box();
    
      integerBox.add(new Integer(10));
      stringBox.add(new String("Привет Мир"));

      System.out.printf("Значение Integer :%d\n\n", integerBox.get());
      System.out.printf("Значение String :%s\n", stringBox.get());
   }
}
```
Получим следующий результат:
<p style="background-color: navy; color: yellow">
Значение Integer :10<br>
Значение String :Привет Мир</p>

#### Пример 2

```java
public class Program{
      
    public static void main(String[] args) {
          
        Account<String> acc1 = new Account<String>("2345", 5000);
        String acc1Id = acc1.getId();
        System.out.println(acc1Id);
         
        Account<Integer> acc2 = new Account<Integer>(2345, 5000);
        Integer acc2Id = acc2.getId();
        System.out.println(acc2Id);
    }
}
class Account<T>{
     
    private T id;
    private int sum;
     
    Account(T id, int sum){
        this.id = id;
        this.sum = sum;
    }
     
    public T getId() { return id; }
    public int getSum() { return sum; }
    public void setSum(int sum) { this.sum = sum; }
}
```

При определении переменной данного класса и создании объекта после имени класса в угловых скобках нужно указать, какой именно тип будет использоваться вместо универсального параметра. При этом надо учитывать, что они работают только с объектами, но не работают с примитивными типами. То есть мы можем написать `Account<Integer>`, но не можем использовать тип int или double, например, `Account<int>`. Вместо примитивных типов надо использовать [классы-обертки](WrapperClasses): [Integer](WrapperInteger) вместо int, Double вместо double и т.д.

Например, первый объект будет использовать тип [String](String), то есть вместо T будет подставляться [String](String):
```java
Account<String> acc1 = new Account<String>("2345", 5000);
```
В этом случае в качестве первого параметра в конструктор передается строка.

А второй объект использует тип int ([Integer](WrapperInteger)):
```java
Account<Integer> acc2 = new Account<Integer>(2345, 5000);
```

### [Обобщенные интерфейсы](https://metanit.com/java/tutorial/3.11.php)

[Интерфейсы](Interface), как и классы, также могут быть обобщенными. Создадим обобщенный интерфейс Accountable и используем его в программе:
```java
public class Program{
      
    public static void main(String[] args) {
          
        Accountable<String> acc1 = new Account("1235rwr", 5000);
        Account acc2 = new Account("2373", 4300);
        System.out.println(acc1.getId());
        System.out.println(acc2.getId());
    }
}
interface Accountable<T>{
    T getId();
    int getSum();
    void setSum(int sum);
}
class Account implements Accountable<String>{
     
    private String id;
    private int sum;
     
    Account(String id, int sum){
        this.id = id;
        this.sum = sum;
    }
     
    public String getId() { return id; }
    public int getSum() { return sum; }
    public void setSum(int sum) { this.sum = sum; }
}
```
При реализации подобного интерфейса есть две стратегии. В данном случае реализована первая стратегия, когда при реализации для универсального параметра интерфейса задается конкретный тип, как например, в данном случае это тип [String](String). Тогда класс, реализующий интерфейс, жестко привязан к этому типу.

Вторая стратегия представляет определение обобщенного класса, который также использует тот же универсальный параметр:
```java
public class Program{
      
    public static void main(String[] args) {
          
        Account<String> acc1 = new Account<String>("1235rwr", 5000);
        Account<String> acc2 = new Account<String>("2373", 4300);
        System.out.println(acc1.getId());
        System.out.println(acc2.getId());
    }
}
interface Accountable<T>{
    T getId();
    int getSum();
    void setSum(int sum);
}
class Account<T> implements Accountable<T>{
     
    private T id;
    private int sum;
     
    Account(T id, int sum){
        this.id = id;
        this.sum = sum;
    }
     
    public T getId() { return id; }
    public int getSum() { return sum; }
    public void setSum(int sum) { this.sum = sum; }
```

### Обобщенные методы

Кроме обобщенных типов можно также создавать обобщенные методы, которые точно также будут использовать универсальные параметры. Например:
```java
public class Program{
      
    public static void main(String[] args) {
          
        Printer printer = new Printer();
        String[] people = {"Tom", "Alice", "Sam", "Kate", "Bob", "Helen"};
        Integer[] numbers = {23, 4, 5, 2, 13, 456, 4};
        printer.<String>print(people);
        printer.<Integer>print(numbers);
    }
}
 
class Printer{
     
    public <T> void print(T[] items){
        for(T item: items){
            System.out.println(item);
        }
    }
}
```
Особенностью обобщенного метода является использование универсального параметра в объявлении метода после всех модификаторов и перед типом возвращаемого значения.
```java
public <T> void print(T[] items)
```
Затем внутри метода все значения типа T будут представлять данный универсальный параметр.

При вызове подобного метода перед его именем в угловых скобках указывается, какой тип будет передаваться на место универсального параметра:
```java
printer.<String>print(people);
printer.<Integer>print(numbers);
```

### Использование нескольких универсальных параметров

Мы можем также задать сразу несколько универсальных параметров:
```java
public class Program{
      
    public static void main(String[] args) {
          
        Account<String, Double> acc1 = new Account<String, Double>("354", 5000.87);
        String id = acc1.getId();
        Double sum = acc1.getSum();
        System.out.printf("Id: %s  Sum: %f \n", id, sum);
    }
}
class Account<T, S>{
     
    private T id;
    private S sum;
     
    Account(T id, S sum){
        this.id = id;
        this.sum = sum;
    }
     
    public T getId() { return id; }
    public S getSum() { return sum; }
    public void setSum(S sum) { this.sum = sum; }
}
```
В данном случае тип [String](String) будет передаваться на место параметра T, а тип Double - на место параметра S.

### Обобщенные конструкторы

Конструкторы, как и методы также могут быть обобщенными. В этом случае перед конструктором также указываются в угловых скобках универсальные параметры:
```java
public class Program{
      
    public static void main(String[] args) {
          
        Account acc1 = new Account("cid2373", 5000);
        Account acc2 = new Account(53757, 4000);
        System.out.println(acc1.getId());
        System.out.println(acc2.getId());
    }
}
 
class Account{
     
    private String id;
    private int sum;
     
    <T>Account(T id, int sum){
        this.id = id.toString();
        this.sum = sum;
    }
     
    public String getId() { return id; }
    public int getSum() { return sum; }
    public void setSum(int sum) { this.sum = sum; }
}
```
В данном случае конструктор принимает параметр id, который представляет тип T. В конструкторе его значение превращается в строку и сохраняется в локальную переменную.