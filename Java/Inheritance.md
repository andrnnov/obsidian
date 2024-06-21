#Java #Inheritance

## # Java – Наследование классов, интерфейсов, методов и конструкторов с помощью ключевых слов super, extends, instanceof и отношений IS-A и HAS-A

2024-06-21 11:48

**Наследование** – это процесс перенимания классом свойств (методов и полей) другого класса. С использованием в Java наследования информация становится управляемой в иерархическом порядке.

Класс, который наследует свойства другого класса, называется подклассом (производным классом, наследующим классом), а класс, свойства которого наследуются, известен как суперкласс (базовый класс, родительский класс). 

### Ключевое слово extends

**extends** – это кодовое слово, используемое для наследования свойств класса. Взглянем на синтаксис этого ключевого слова.
```java
class Super {
   ...
}
class Sub extends Super {
   ...
}
```

#### Пример кода

Дальше приведён пример процесса наследования на Java. На этом примере Вы можете рассмотреть два класса с именами Calculator и My_Calculator.

Используя ключевое слово extends в Java, My_Calculator перенимает методы addition() и subtraction() класса Calculator.
```java
class Calculator {
   int c;
	
   public void addition(int a, int b) {
      c = a + b;
      System.out.println("Сумма чисел: " + c);
   }
	
   public void subtraction(int a, int b) {
      c = a - b;
      System.out.println("Разность чисел: " + c);
   }
}

public class My_Calculator extends Calculator {
   public void multiplication(int a, int b) {
      c = a * b;
      System.out.println("Произведение чисел: " + c);
   }
	
   public static void main(String args[]) {
      int a = 10, b = 20;
      My_Calculator cal = new My_Calculator();
      cal.addition(a, b);
      cal.subtraction(a, b);
      cal.multiplication(a, b);
   }
}
```
**Вывод:**
<p style="background-color: navy; color: yellow">
Сумма чисел: 30<br>
Разность чисел: -10<br>
Произведение чисел: 200</p>
В данной программе, при создании объекта классу **My_Calculator**, копия содержимого суперкласса создаётся в нём же. Поэтому, используя объект подкласса, Вы можете получить доступ к членам суперкласса.

Ссылочная переменная суперкласса может содержать объект подкласса, но, используя эту переменную, Вы можете иметь доступ только к членам суперкласса, поэтому, чтобы иметь доступ к членам обоих классов, рекомендуется всегда создавать ссылочную переменную к подклассу.

Обращаясь к программе выше, Вы можете создать экземпляр класса, как в примере ниже. Но, используя ссылочную переменную суперкласса, Вы не можете вызвать метод **multiplication()**, который принадлежит подклассу My_Calculator.
```java
Calculator cal = new My_Calculator();
cal.addition(a, b);
cal.subtraction(a, b);
```

>Примечание: подкласс наследует все члены (поля, методы, вложенные классы) из суперкласса. В Java конструкторы не являются членами, поэтому они не наследуются подклассом, но конструктор суперкласса может быть вызван из подкласса.

### Ключевое слово super

Ключевое слово **super** схоже с ключевым словом **this**. Ниже приведены случаи, где используется **super** в Java.
- Для **дифференциации членов** суперкласса от членов подкласса, если у них есть одинаковые имена.
- Для **вызова конструктора суперкласса** из подкласса.

### Дифференциация членов

Если класс перенимает свойства другого класса, и члены суперкласса имеют те же имена, что и в подклассе, для их разделения мы используем ключевое слово super, как показано ниже.
```java
super.variable;
super.method();
```

#### Пример кода

Этот раздел содержит программу, которая демонстрирует использование ключевого слова **super** в Java.

В предложенной программе у вас есть два класса с именами Sub_class и Super_class, оба имеющие метод display() с разными реализациями и переменную с именем num с разными значениями. Вы можете увидеть, что мы использовали ключевое слово **super** для дифференциации членов суперкласса из подкласса.
```java
// Интерфейс
class Super_class {
   int num = 88;

   // Метод display() суперкласса
   public void display() {
      System.out.println("Это метод display() суперкласса");
   }
}

public class Sub_class extends Super_class {
   int num = 77;

   // Метод display() субкласса
   public void display() {
      System.out.println("Это метод display() подкласса");
   }

   public void my_method() {
      // Инициализация подкласса
      Sub_class sub = new Sub_class();

      // Вызываем метод display() подкласса
      sub.display();

      // Вызываем метод display() суперкласса
      super.display();

      // Выводим значение переменной num подкласса
      System.out.println("Значение переменной num в подклассе: " + sub.num);

      // Выводим значение переменной num суперкласса
      System.out.println("Значение переменной num в суперклассе: " + super.num);
   }

   public static void main(String args[]) {
      Sub_class obj = new Sub_class();
      obj.my_method();
   }
}
```
**Вывод:**
<p style="background-color: navy; color: yellow">
Это метод display() подкласса<br>
Это метод display() суперкласса<br>
Значение переменной num в подклассе: 77<br>
Значение переменной num в суперклассе: 88</p>

### Вызов конструктора суперкласса

Если класс перенимает свойства другого класса, подкласс автоматически получается стандартный конструктор суперкласса. Но если Вы хотите вызвать параметризованный конструктор суперкласса, Вам нужно использовать ключевое слово super, как показано ниже.

#### Пример кода

В предложенной программе демонстрируется использование в Java ключевого слова super для вызова параметризованного конструктора. В этой программе содержится суперкласс и подкласс, где суперкласс содержит параметризованный конструктор, который принимает строковое значение, а мы используем ключевое слово super для вызова параметризованного конструктора суперкласса.
```java
class Superclass {
   int age;

   Superclass(int age) {
      this.age = age; 		 
   }

   public void getAge() {
      System.out.println("Значение переменной age в суперклассе равно: " + age);
   }
}

public class Subclass extends Superclass {
   Subclass(int age) {
      super(age);
   }

   public static void main(String args[]) {
      Subclass s = new Subclass(24);
      s.getAge();
   }
}
```
**Вывод:**
<p style="background-color: navy; color: yellow">
Значение переменной age в суперклассе равно: 24</p>

### [Разница между ключевыми словами this и super в Java](this_super)


### Отношение IS-A

**IS-A** – это способ сказать «Этот объект является типом этого объекта». Давайте посмотрим, как ключевое слово **extends** используется для достижения наследования.
```java
public class Animal {
}

public class Mammal extends Animal {
}

public class Reptile extends Animal {
}

public class Dog extends Mammal {
}
```
Теперь, основываясь на примере выше, в объектно-ориентированных терминах, следующие утверждения верны

- Animal является суперклассом класса Mammal.
- Animal является суперклассом класса Reptile.
- Mammal и Reptile являются подклассами класса Animal.
- Dog одновременно является подклассом классов Mammal и Animal.
- 
Теперь, используя отношение IS-A, мы можем сказать так:

- Mammal IS-A Animal.
- Reptile IS-A Animal.
- Dog IS-A Mammal.
- Таким образом, Dog IS-A тоже Animal.

С использованием ключевого слова extend, подклассы могут наследовать все свойства суперкласса кроме его приватных свойств (private).

Мы можем убедиться, что Mammal на самом деле Animal с использованием оператора экземпляра [instanceof](instanceof).
```java
class Animal {
}

class Mammal extends Animal {
}

class Reptile extends Animal {
}

public class Dog extends Mammal {

   public static void main(String args[]) {
      Animal a = new Animal();
      Mammal m = new Mammal();
      Dog d = new Dog();

      System.out.println(m instanceof Animal);
      System.out.println(d instanceof Mammal);
      System.out.println(d instanceof Animal);
   }
}
```
Мы получим следующий результат:
<p style="background-color: navy; color: yellow">
true<br>
true<br>
true</p>
Так как у нас есть хорошее понимание принципа работы ключевого слова **extends**, давайте рассмотрим, как используется ключевое слово **implements** для получения отношения IS-A.

В общем, ключевое слово **implements** в Java используется с классами для перенятия свойств интерфейса. Интерфейсы никогда не могут быть переняты классом с помощью **extends**.

#### Пример

```java
public interface Animal {
}

public class Mammal implements Animal {
}

public class Dog extends Mammal {
}
```

### Ключевое Слово instanceof

Давайте использует оператор [instanceof](instanceof) в Java с целью проверки, являются ли Mammal и Dog на самом деле Animal.

### Пример

```java
interface Animal{}
class Mammal implements Animal{}

public class Dog extends Mammal {

   public static void main(String args[]) {
      Mammal m = new Mammal();
      Dog d = new Dog();

      System.out.println(m instanceof Animal);
      System.out.println(d instanceof Mammal);
      System.out.println(d instanceof Animal);
   }
}
```
Мы получим следующий результат:
<p style="background-color: navy; color: yellow">
true<br>
true<br>
true</p>

### Отношение HAS-A

Эти отношения в основном основаны на обращении. Они определяют, является ли определенный класс HAS-A определенным случаем. Эта взаимосвязь помогает уменьшить дублирование кода, а также баги. Взглянем на пример.
```java
public class Vehicle{}
public class Speed{}

public class Van extends Vehicle {
   private Speed sp;
}
```
Мы видим, что у класса Van HAS-A (есть) Speed. Имея отдельный класс Speed, нам не нужно вставлять код, принадлежащий Speed в класс Van, что позволяет нам использовать класс Speed в нескольких приложениях.

В особенности объектно-ориентированного программирования, пользователям не нужно волноваться о том, какой объект выполняет текущую работу. Для достижения этого, класс Van скрывает детали реализации от пользователей класса Van. Таким образом, пользователи, должны попросить класс Van выполнить определенное действие, и класс Van либо выполнит работу сам по себе, либо попросит другой класс выполнить действие.

### Виды наследования

Есть различные способы наследования, как показано ниже.

| Вид                         | Схема                                                                                                          | Пример                                                                                                                                        |
| --------------------------- | -------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| Одиночное наследование      | ![Одиночное наследование в Java](https://proglang.su/images/categories/java/single-inheritance.webp)           | <br>public class A { ... }<br>public class B extends A { ... }                                                                                |
| Многоуровневое наследование | ![Многоуровневое наследование в Java](https://proglang.su/images/categories/java/multi-level-inheritance.webp) | <br>public class A { ... }<br>public class B extends A { ... }<br>public class C extends B { ... }<br>                                        |
| Иерархическое наследование  | ![Иерархическое наследование в Java](https://proglang.su/images/categories/java/hierarchical-inheritance.webp) | public class A { ... }<br>public class B extends A { ... }<br>public class C extends A { ... }                                                |
| Множественное наследование  | ![Множественное наследование в Java](https://proglang.su/images/categories/java/multiple-inheritance.webp)     | public class A { ... }<br>public class B { ... }<br>public class C extends A, B { ... }<br>// Java не поддерживает множественное наследование |

Очень важно запомнить, что Java не поддерживает множественное наследование. Это значит, что класс не может продлить более одного класса. Значит, следующее утверждение НЕВЕРНО:
```java
public class extends Animal, Mammal{} 
```

Тем не менее, класс может реализовать один или несколько интерфейсов, что и помогло Java избавиться от невозможности множественного наследования.
