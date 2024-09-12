#Java #this 

## [Ключевое слово this](https://www.geeksforgeeks.org/this-reference-in-java/)

2024-09-12 16:31

В Java ‘this’ - это ссылочная переменная, которая ссылается на текущий объект, или, можно сказать, “this” в Java - это ключевое слово, которое ссылается на текущий экземпляр объекта. Ее можно использовать для вызова методов и полей текущего класса, для передачи экземпляра текущего класса в качестве параметра и для различения локальных переменных и переменных экземпляра. Использование ссылки “this” может улучшить читаемость кода и уменьшить конфликты именования.

В Java это ссылочная переменная ссылающаяся на текущий объект, для которого вызывается метод или конструктор. Ее можно использовать для доступа к переменным экземпляра и методам текущего объекта.

**Ниже приведена реализация этой ссылки:**

```java
// Java Program to implement
// Java this reference
 
// Driver Class
public class Person {
    // Fields Declared
    String name;
    int age;
    // Constructor
    Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
 
    // Getter for name
    public String get_name() { return name; }
 
    // Setter for name
    public void change_name(String name) {
        this.name = name;
    }
 
    // Method to Print the Details of
    // the person
    public void printDetails() {
        System.out.println("Name: " + this.name);
        System.out.println("Age: " + this.age);
        System.out.println();
    }
 
    // main function
    public static void main(String[] args) {
        // Objects Declared
        Person first = new Person("ABC", 18);
        Person second = new Person("XYZ", 22);
 
        first.printDetails();
        second.printDetails();
 
        first.change_name("PQR");
        System.out.println("Name has been changed to: " + first.get_name());
    }
}
```
**Вывод**
<p style="background-color: navy; color: yellow">
Name: ABC<br>
Age: 18<br>
<br>
Name: XYZ<br>
Age: 22<br>
<br>
Name has been changed to: PQR</p>

В приведенном выше коде мы определили класс Person с двумя закрытыми полями name и age . Мы определили конструктор класса Person для инициализации этих полей с помощью этого ключевого слова. Мы также определили методы получения и установки для этих полей, которые используют это ключевое слово для ссылки на текущий экземпляр объекта.

В методе printDetails() мы использовали это ключевое слово для ссылки на текущий экземпляр объекта и вывода его имени, возраста и ссылки на объект.

В основном классе мы создали два объекта Person и вызвали метод printDetails() для каждого объекта. Выходные данные показывают имя, возраст и ссылку на объект каждого экземпляра объекта.

## Методы использования ‘this’ в Java

Ниже приведены способы использования ключевого слова ‘this’ в Java, упомянутые ниже:
- Использование ключевого слова ‘this’ для ссылки на текущие переменные экземпляра класса.
- Использование this() для вызова конструктора текущего класса
- Использование ключевого слова ‘this’ для возврата текущего экземпляра класса
- Использование ключевого слова ‘this’ в качестве параметра метода
- Использование ключевого слова ‘this’ для вызова текущего метода класса
- Использование ключевого слова ‘this’ в качестве аргумента в вызове конструктора

### 1. Использование ключевого слова ‘this’ для ссылки на текущие переменные экземпляра класса

```java
// Java code for using 'this' keyword to
// refer current class instance variables
class Test {
    int a;
    int b;
 
    // Parameterized constructor
    Test(int a, int b) {
        this.a = a;
        this.b = b;
    }
 
    void display() {
        // Displaying value of variables a and b
        System.out.println("a = " + a + "  b = " + b);
    }
 
    public static void main(String[] args) {
        Test object = new Test(10, 20);
        object.display();
    }
}
```

**Вывод**
<p style="background-color: navy; color: yellow">
a = 10  b = 20</p>

### 2. Использование this() для вызова конструктора текущего класса

```java
// Java code for using this() to
// invoke current class constructor
class Test {
    int a;
    int b;
 
    // Default constructor
    Test() {
        this(10, 20);
        System.out.println("Inside  default constructor \n");
    }
 
    // Parameterized constructor
    Test(int a, int b) {
        this.a = a;
        this.b = b;
        System.out.println("Inside parameterized constructor");
    }
 
    public static void main(String[] args) {
        Test object = new Test();
    }
}
```
**Вывод**
<p style="background-color: navy; color: yellow">
Inside parameterized constructor<br>
Inside  default constructor</p>

### 3. Использование ключевого слова ‘this’ для возврата текущего экземпляра класса

```java
// Java code for using 'this' keyword
// to return the current class instance
class Test {
    int a;
    int b;
 
    // Default constructor
    Test() {
        a = 10;
        b = 20;
    }
 
    // Method that returns current class instance
    Test get() { return this; }
 
    // Displaying value of variables a and b
    void display() {
        System.out.println("a = " + a + "  b = " + b);
    }
 
    public static void main(String[] args) {
        Test object = new Test();
        object.get().display();
    }
}
```
**Вывод**
<p style="background-color: navy; color: yellow">
a = 10  b = 20</p>

### 4. Использование ключевого слова ‘this’ в качестве параметра метода

```java
// Java code for using 'this'
// keyword as method parameter
class Test {
    int a;
    int b;
 
    // Default constructor
    Test() {
        a = 10;
        b = 20;
    }
 
    // Method that receives 'this' keyword as parameter
    void display(Test obj) {
        System.out.println("a = " + obj.a
                           + "  b = " + obj.b);
    }
 
    // Method that returns current class instance
    void get() { display(this); }
 
    // main function
    public static void main(String[] args) {
        Test object = new Test();
        object.get();
    }
}
```
**Вывод**
<p style="background-color: navy; color: yellow">
a = 10  b = 20</p>

### 5. Использование ключевого слова ‘this’ для вызова текущего метода класса

```java
// Java code for using this to invoke current
// class method
class Test {
 
    void display() {
        // calling function show()
        this.show();
 
        System.out.println("Inside display function");
    }
 
    void show() {
        System.out.println("Inside show function");
    }
 
    public static void main(String args[]) {
        Test t1 = new Test();
        t1.display();
    }
}
```
**Вывод**
<p style="background-color: navy; color: yellow">
Inside show function<br>
Inside display function</p>

### 6. Использование ключевого слова ‘this’ в качестве аргумента в вызове конструктора

```java
// Java code for using this as an argument in constructor
// call
// Class with object of Class B as its data member
class A {
    B obj;
 
    // Parameterized constructor with object of B
    // as a parameter
    A(B obj) {
        this.obj = obj;
 
        // calling display method of class B
        obj.display();
    }
}
 
class B {
    int x = 5;
 
    // Default Constructor that create an object of A
    // with passing this as an argument in the
    // constructor
    B() { A obj = new A(this); }
 
    // method to show value of x
    void display() {
        System.out.println("Value of x in Class B : " + x);
    }
 
    public static void main(String[] args) {
        B obj = new B();
    }
}
```
**Вывод**
<p style="background-color: navy; color: yellow">
Value of x in Class B : 5</p>

### Преимущества использования ссылки ‘this’

Использование ссылки "this" в Java имеет определенные преимущества, как указано ниже:
1. Это помогает различать переменные экземпляра и локальные переменные с тем же именем.
2. Ее можно использовать для передачи текущего объекта в качестве аргумента другому методу.
3. Ее можно использовать для возврата текущего объекта из метода.
4. Ее можно использовать для вызова конструктора из другого перегруженного конструктора в том же классе.

### Недостатки использования ссылки ‘this’

Хотя ссылка ‘this’ имеет много преимуществ, у нее также есть определенные недостатки:
1. Чрезмерное использование этого может затруднить чтение и понимание кода.
2. Использование этого без необходимости может добавить ненужные накладные расходы программе.
3. Использование этого в статическом контексте приводит к ошибке времени компиляции.
4. В целом, это ключевое слово является полезным инструментом для работы с объектами в Java, но его следует использовать разумно и только при необходимости.