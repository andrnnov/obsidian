#Java #Generics 

## [Ограничения обобщений](https://metanit.com/java/tutorial/3.17.php)

2024-07-30 16:59

Когда мы указываем универсальный параметр у обобщений, то по умолчанию он может представлять любой тип. Однако иногда необходимо, чтобы параметр соответствовал только некоторому ограниченному набору типов. В этом случае применяются ограничения, которые позволяют указать базовый класс, которому должен соответствовать параметр.

Для установки ограничения после универсального параметра ставится слово extends, после которого указывается базовый класс ограничения:
```java
class Account{ }
class Transaction<T extends Account>{ }
```
К примеру, в данном случае для параметра T в Transaction ограничением является класс Account. То есть на место параметра T мы можем передать либо класс Account, либо один из его классов-наследников.

Например, рассмотрим следующую программу:
```java
public class Program{
      
    public static void main(String[] args) {
          
        Account acc1 = new Account("1876", 4500);
        Account acc2 = new Account("3476", 1500);
              
        Transaction<Account> tran1 = new Transaction<Account>(acc1,acc2, 4000);
        tran1.execute();
        tran1 = new Transaction<Account>(acc1,acc2, 4000);
        tran1.execute();
    }
}
class Transaction<T extends Account>{
     
    private T from;     // с какого счета перевод
    private T to;       // на какой счет перевод
    private int sum;    // сумма перевода
     
    Transaction(T from, T to, int sum){
        this.from = from;
        this.to = to;
        this.sum = sum;
    }
    public void execute(){
         
        if (from.getSum() > sum)
        {
            from.setSum(from.getSum() - sum);
            to.setSum(to.getSum() + sum);
            System.out.printf("Account %s: %d \nAccount %s: %d \n", 
                from.getId(), from.getSum(),to.getId(), to.getSum());
        }
        else{
            System.out.printf("Operation is invalid");
        }
    }
}
class Account{
     
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
В данном случае класс Transaction, который представляет операцию перевода средств между двумя счетами, типизирован параметром T, у которого в качестве ограничения установлен класс Account. При создании объекта Transaction в его конструктор передаются два объекта Account - два счета, между которыми надо осуществить перевод, и сумма перевода.

При этом важно понимать, что поскольку мы установили подобное ограничение, то компилятор будет распознавать объекты типа T как объекты типа Account. И в этом случае мы можем вызывать у объектов типа T методы класса Account. И мы бы не смогли бы это сделать, если бы мы не задали подобного ограничения:
```java
class Transaction<T>{
    // остальное содержимое
}
```
В этом случае была бы ошибка.

### Обобщенные типы в качестве ограничений

В качестве ограничений могут выступать и другие обобщения, которые сами могут иметь ограничения:
```java
public class Program{
      
    public static void main(String[] args) {
          
        Account<String> acc1 = new Account<String>("1876", 4500);
        Account<String> acc2 = new Account<String>("3476", 1500);
              
        Transaction<Account<String>> tran1 = new Transaction<Account<String>>(acc1,acc2, 4000);
        tran1.execute();
        tran1 = new Transaction<Account<String>>(acc1,acc2, 4000);
        tran1.execute();
    }
}
class Transaction<T extends Account<String>>{
     
    private T from;     // с какого счета перевод
    private T to;       // на какой счет перевод
    private int sum;    // сумма перевода
     
    Transaction(T from, T to, int sum){
        this.from = from;
        this.to = to;
        this.sum = sum;
    }
    public void execute(){
         
        if (from.getSum() > sum)
        {
            from.setSum(from.getSum() - sum);
            to.setSum(to.getSum() + sum);
            System.out.printf("Account %s: %d \nAccount %s: %d \n", 
                from.getId(), from.getSum(),to.getId(), to.getSum());
        }
        else{
            System.out.printf("Operation is invalid");
        }
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
В данном случае ограничением для Transaction является тип Account, который типизирован типом String.

### Интерфейсы в качестве ограничений

В качестве ограничений могут выступать также интерфейсы. В этом случае передаваемый на место универсального параметра тип должен реализовать данный интерфейс:
```java
public class Program{
      
    public static void main(String[] args) {
          
        Account acc1 = new Account("1235rwr", 5000);
        Account acc2 = new Account("2373", 4300);
        Transaction<Account> tran1 = new Transaction<Account>(acc1, acc2, 1560);
        tran1.execute();
    }
}
interface Accountable{
    String getId();
    int getSum();
    void setSum(int sum);
}
class Account implements Accountable{
     
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
class Transaction<T extends Accountable>{
     
    private T from;     // с какого счета перевод
    private T to;       // на какой счет перевод
    private int sum;    // сумма перевода
     
    Transaction(T from, T to, int sum){
        this.from = from;
        this.to = to;
        this.sum = sum;
    }
    public void execute(){
         
        if (from.getSum() > sum)
        {
            from.setSum(from.getSum() - sum);
            to.setSum(to.getSum() + sum);
            System.out.printf("Account %s: %d \nAccount %s: %d \n", 
                from.getId(), from.getSum(),to.getId(), to.getSum());
        }
        else{
            System.out.printf("Operation is invalid");
        }
    }
}
```

### Множественные ограничения

Также можно установить сразу несколько ограничений. Например, пусть класс Transaction может работать только с объектами, которые одновременно реализуют интерфейс Accountable и являются наследниками класса Person:
```java
class Person{}
interface Accountable{}
 
class Transaction<T extends Person & Accountable>{}
```

#### Пример. [Методы обобщений и ограничение параметров](https://docs.oracle.com/javase/tutorial/java/generics/boundedTypeParams.html)

Рассмотрим метод, который подсчитывает количество элементов в массиве. 
```java
public static <T> int countGreaterThan(T[] anArray, T elem) {
 int count = 0;
 for (T e : anArray)
 if (e > elem) // compiler error
 ++count;
 return count;
}
```
Реализация метода проста, но он не компилируется, поскольку оператор  (>) применяется только к примитивным типам, таким как short, int, double, long, float, byte и char. Вы не можете использовать оператор > для сравнения объектов. Чтобы устранить проблему, используйте параметр типа, ограниченный интерфейсом [Comparable](Comparable):
```java
public interface Comparable<T> {
 public int compareTo(T o);
}
```
Результирующий код будет иметь вид:
```java
public static <T extends Comparable<T>> int countGreaterThan(T[] anArray, T elem) {
 int count = 0;
 for (T e : anArray)
 if (e.compareTo(elem) > 0)
 ++count;
 return count;
}
```

#### Пример. [Как реализовать ограниченные типы (расширить суперкласс) с помощью обобщений.]()

Ограничение по верхней границе (которая в приведенном ниже примере c является **A**):
```java
// This class only accepts type parameters as any class
// which extends class A or class A itself.
// Passing any other type will cause compiler time error
 
class Bound<T extends A> {
     
    private T objRef;
     
    public Bound(T obj){
        this.objRef = obj;
    }
     
    public void doRunTest(){
        this.objRef.displayClass();
    }
}
 
class A {
    public void displayClass()
    {
        System.out.println("Inside super class A");
    }
}
 
class B extends A {
    public void displayClass()
    {
        System.out.println("Inside sub class B");
    }
}
 
class C extends A {
    public void displayClass()
    {
        System.out.println("Inside sub class C");
    }
}
 
public class BoundedClass {
    public static void main(String a[]) {
         
        // Creating object of sub class C and
        // passing it to Bound as a type parameter.
        Bound<C> bec = new Bound<C>(new C());
        bec.doRunTest();
         
        // Creating object of sub class B and
        // passing it to Bound as a type parameter.
        Bound<B> beb = new Bound<B>(new B());
        beb.doRunTest();
         
        // similarly passing super class A
        Bound<A> bea = new Bound<A>(new A());
        bea.doRunTest();
         
    }
}
```
**Вывод:**
<p style="background-color: navy; color: yellow">
Inside sub class C<br>
Inside sub class B<br>
Inside super class A</p>
Теперь мы ограничены только типом A и его подклассами, поэтому он выдаст ошибку для любого другого типа.

#### Пример. Множественные границы

Параметры ограниченного типа могут использоваться как с методами, так и с классами и интерфейсами.

Обобщения Java также поддерживают несколько границ. В этом случае A может быть интерфейсом или классом. Если A - класс, то B и C должны быть интерфейсами. У нас не может быть более одного класса в нескольких границах.
```java
class Bound<T extends A & B>{
     
    private T objRef;
     
    public Bound(T obj) {
        this.objRef = obj;
    }
     
    public void doRunTest(){
        this.objRef.displayClass();
    }
}
 
interface B {
    public void displayClass();
}
 
class A implements B {
    public void displayClass() {
        System.out.println("Inside super class A");
    }
}
 
public class BoundedClass {
    public static void main(String a[]) {
        //Creating object of sub class A and
        //passing it to Bound as a type parameter.
        Bound<A> bea = new Bound<A>(new A());
        bea.doRunTest();
    }
}
```
**Вывод:**
<p style="background-color: navy; color: yellow">
Inside super class A</p>
