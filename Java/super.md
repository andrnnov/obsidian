#Java #super 

## [Ключевое слово super](https://www.geeksforgeeks.org/super-keyword/)

2024-09-13 10:14

**Ключевое слово super в Java** - это ссылочная переменная, которая используется для ссылки на родительский класс, когда мы работаем с объектами. 

### Характеристики ключевого слова super в Java

В Java ключевое слово super используется для обозначения родительского класса подкласса. Вот некоторые из его ключевых характеристик:
- **super используется для вызова конструктора суперкласса:** При создании подкласса его конструктор должен вызывать конструктор своего родительского класса. Это делается с помощью ключевого слова super(), которое вызывает конструктор родительского класса.
- **super используется для вызова метода суперкласса:** подкласс может вызывать метод, определенный в его родительском классе, используя ключевое слово super. Это полезно, когда подкласс хочет вызвать реализацию метода родительского класса в дополнение к своей собственной.
- **super используется для доступа к полю суперкласса:** подкласс может получить доступ к полю, определенному в его родительском классе, используя ключевое слово super. Это полезно, когда подкласс хочет ссылаться на версию поля родительского класса.
- **super должен быть первым оператором в конструкторе:** При вызове конструктора суперкласса оператор super() должен быть первым оператором в конструкторе подкласса.
- **super нельзя использовать в статическом контексте:** ключевое слово super нельзя использовать в статическом контексте, например, в статическом методе или инициализаторе статической переменной.
- **для вызова метода суперкласса не требуется super:** Хотя ключевое слово super можно использовать для вызова метода в родительском классе, оно не является обязательным. Если метод не переопределен в подклассе, то его вызов без ключевого слова super вызовет реализацию родительского класса.

> В целом, **ключевое слово super** - это мощный инструмент для создания подклассов в Java, позволяющий подклассам наследовать функциональность своих родительских классов и развивать ее.

### Использование ключевого слова super в Java

Оно чаще всего используется в следующих контекстах, как указано ниже:
- **Использование super с переменными**
- **Использование super с методами**
- **Использование super с конструкторами**

#### 1. Использование super с переменными

Этот сценарий возникает, когда производный класс и базовый класс имеют одинаковые элементы данных. В этом случае существует вероятность неоднозначности в [JVM](https://www.geeksforgeeks.org/jvm-works-jvm-architecture/).
```java
// super keyword in java example 
  
// Base class vehicle 
class Vehicle { 
    int maxSpeed = 120; 
} 
  
// sub class Car extending vehicle 
class Car extends Vehicle { 
    int maxSpeed = 180; 
  
    void display() { 
        // print maxSpeed of base class (vehicle) 
        System.out.println("Maximum Speed: " + super.maxSpeed); 
    } 
} 
  
// Driver Program 
class Test { 
    public static void main(String[] args) { 
        Car small = new Car(); 
        small.display(); 
    } 
}
```
**Вывод:**
<p style="background-color: navy; color: yellow">
Maximum Speed: 120</p>

#### 2. Использование super с методами

Это используется, когда мы хотим вызвать метод родительского класса. Поэтому всякий раз, когда родительский и дочерний классы имеют методы с одинаковыми именами, для устранения неоднозначности мы используем ключевое слово super .
```java
// super keyword in java example 
  
// superclass Person 
class Person { 
    void message() { 
        System.out.println("This is person class\n"); 
    } 
} 
// Subclass Student 
class Student extends Person { 
    void message() { 
        System.out.println("This is student class"); 
    } 
    // Note that display() is 
    // only in Student class 
    void display() { 
        // will invoke or call current 
        // class message() method 
        message(); 
  
        // will invoke or call parent 
        // class message() method 
        super.message(); 
    } 
} 
// Driver Program 
class Test { 
    public static void main(String args[]) { 
        Student s = new Student(); 
  
        // calling display() of Student 
        s.display(); 
    } 
}
```
**Вывод:**
<p style="background-color: navy; color: yellow">
This is student class<br>
This is person class</p>
В приведенном выше примере мы увидели, что если мы вызываем только метод message(), то вызывается текущий класс message(), но с использованием ключевого слова super также может быть вызвано message() суперкласса.

#### 3. Использование super с конструкторами

Ключевое слово super также можно использовать для доступа к конструктору родительского класса. Еще одна важная вещь заключается в том, что ‘super’ может вызывать как параметрические, так и непараметрические конструкторы в зависимости от ситуации.

#### Пример 1

```java
// Java Code to show use of 
// super keyword with constructor 
  
// superclass Person 
class Person { 
    Person() { 
        System.out.println("Person class Constructor"); 
    } 
} 
  
// subclass Student extending the Person class 
class Student extends Person { 
    Student() { 
        // invoke or call parent class constructor 
        super(); 
  
        System.out.println("Student class Constructor"); 
    } 
} 
  
// Driver Program 
class Test { 
    public static void main(String[] args) { 
        Student s = new Student(); 
    } 
}
```
**Вывод:**
<p style="background-color: navy; color: yellow">
Person class Constructor<br>
Student class Constructor</p>
В приведенном выше примере мы вызвали конструктор суперкласса, используя ключевое слово ‘super’ через конструктор подкласса.

#### Пример 2

```java
class ParentClass { 
    public boolean isTrue() { return true; } 
} 
  
class ChildClass extends ParentClass { 
    public boolean isTrue() { 
        // calls parent implementation of isTrue() 
        boolean parentResult = super.isTrue(); 
        // negates the parent result 
        return !parentResult; 
    } 
} 
  
public class Main { 
    public static void main(String[] args) { 
        ChildClass child = new ChildClass(); 
        // calls child implementation 
        // of isTrue() 
        boolean result = child.isTrue(); 
  
        // prints "false" 
        System.out.println(result); 
    } 
}
```
**Вывод:**
<p style="background-color: navy; color: yellow">
false</p>

### Преимущества использования ключевого слова Java Super

**Ключевое слово super в Java** предоставляет множество преимуществ в объектно-ориентированном программировании, а именно:
- **Позволяет повторно использовать код**: Использование ключевого слова super позволяет подклассам наследовать функциональность от своих родительских классов, что способствует повторному использованию кода и уменьшает дублирование.
- **Поддерживает полиморфизм*: поскольку подклассы могут переопределять методы и обращаться к полям из своих родительских классов с помощью super, полиморфизм возможен. Это обеспечивает более гибкий и расширяемый код.
- **Предоставляет доступ к поведению родительского класса**: Подклассы могут получать доступ к методам и полям, определенным в их родительских классах, и использовать их с помощью ключевого слова super, что позволяет им использовать преимущества существующего поведения без необходимости его переопределения.
- **Позволяет настраивать поведение:** Переопределяя методы и используя super для вызова родительской реализации, подклассы могут настраивать и расширять поведение своих родительских классов.
- **Облегчает абстракцию и инкапсуляцию:** Использование super способствует инкапсуляции и абстракции, позволяя подклассам сосредоточиться на своем поведении, полагаясь при этом на родительский класс для обработки деталей более низкого уровня.

> В целом, ключевое слово super является ключевой особенностью [наследования](https://www.geeksforgeeks.org/inheritance-in-java/) и [полиморфизма](https://www.geeksforgeeks.org/polymorphism-in-java/) в Java, и оно предоставляет ряд преимуществ разработчикам, стремящимся писать повторно используемый, расширяемый и хорошо организованный код.

