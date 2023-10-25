#java #inctanceof

2023-10-25 15:42
### Оператор instanceof. Определение типа объекта. ###

#### 1. Назначение оператора instanceof. Общая форма ####

Оператор instanceof используется для определения типа объекта во время выполнения программы. Определив тип объекта можно реализовать корректное приведение типов в случае, когда классы образуют иерархию. Если выполнить некорректное приведение к некоторому типу, то на этапе выполнения будет сгенерирована исключительная ситуация, что неприемлемо.

Общая форма оператора instanceof следующая

_reference_ **instanceof** _type_

здесь

- reference – ссылка на объект (экземляр) класса;
- type – тип класса.

Результатом работы оператора instanceof есть значение true или false. Результат true возвращается в случаях:

- если ссылка reference относится к указанному типу;
- если ссылка reference может быть приведена к указанному типу.

В других случаях возвращается значение false.

#### 2. Применение instanceof для классов, образующих иерархию.  ####

В примере демонстрируется корректное определение типа, к которому принадлежит объект класса. Реализовано два класса A и B, которые образуют иерархию. С целью демонстрации определяется тип соответствующего объекта с учетом того, что унаследованный класс расширяет возможности суперкласса.
```java
// Оператор instanceof
// Суперкласс A
class A {
  int a;
}

// Класс B – наследует класс A
class B extends A {
  int b;
}

public class TestInstanceOf {

  public static void main(String[] args) {
    A objA = new A();
    B objB = new B();

    if (objA instanceof A)
      System.out.println("objA is a instance of A");
    else
      System.out.println("objA is not an instance of A");

    if (objA instanceof B)
      System.out.println("objA can be cast to type B");
    else
      System.out.println("objA can not be cast to type B");

    if (objB instanceof A)
      System.out.println("objB can be cast to type A");
    else
      System.out.println("objB can not be cast to type A");

    if (objB instanceof B)
      System.out.println("objB is a instance of B");
    else
      System.out.println("objB is not an instance of B");
  }
}
```
Результат выполнения программы:
==objA is a instance of A
objA can not be cast to type B
objB can be cast to type A
objB is a instance of B==

Как видно из результата, экземпляр унаследованного класса B может быть корректно приведен к суперклассу A. А вот экземпляр суперкласса A не может быть расширен к возможностям унаследованного класса B.

#### 3. Применение instanceof для типа Object. ####

В объектной модели языка Java все создаваемые классы унаследованы от класса Object. В следующем примере приходится это утверждение.
```java
// Оператор instanceof
// Суперкласс A
class A {
  int a;
}

// Подкласс
class B extends A {
  int b;
}

public class TestInstanceOf {

  public static void main(String[] args) {
    A objA = new A(); // экземпляр класса A
    B objB = new B(); // экземпляр класса B

    // Проверка на наследование от Object
    if (objA instanceof Object)
      System.out.println("objA can be cast to type Object");
    else
      System.out.println("objA can not be cast to type Object");

    if (objB instanceof Object)
      System.out.println("objB can be cast to type Object");
    else
      System.out.println("objB can not be cast to type Object");
  }
}
```
Результат работы программы
==objA can be cast to type Object
objB can be cast to type Object==
#### 4. Применение instanceof для ссылки на базовый класс. ####

Если классы образуют иерархию наследования, то ссылка на суперкласс может получать значение экземпляров любого производного класса. В примере ниже демонстрируется определение того, может ли ссылка на суперкласс быть приведена к типу производного класса.
```java
// Оператор instanceof
// Суперкласс A
class A {
  int a;
}

// Подкласс B
class B extends A {
  int b;
}

// Подкласс C
class C extends B {
  int c;
}

// Подкласс D
class D extends C {
  int d;
}

public class TestInstanceOf {

  public static void main(String[] args) {
    // экземпляры классов A, B, C, D
    A objA = new A();
    B objB = new B();
    C objC = new C();
    D objD = new D();

    // ссылка на суперкласс A
    A refA;

    // Ссылке на суперкласс можно присваивать значения
    // экземпляров (ссылок на экземпляры) производных классов
    refA = objA;

    if (refA instanceof A)
      System.out.println("refA is an instance of A");
    else
      System.out.println("refA is not an instance of A");

    // Перенаправить ссылку на экземпляр objB
    refA = objB;
    if (refA instanceof B)
      System.out.println("refA can be cast to type B");
    else
      System.out.println("refA can not be cast to type B");

    if (refA instanceof D)
      System.out.println("refA can be cast to type D");
    else
      System.out.println("refA can not be cast to type D");

    // Ссылка на objC
    refA = objC;
    if (refA instanceof B)
      System.out.println("refA can be cast to type B");
    else
      System.out.println("refA can not be cast to type B");
  }
}
```
Результат выполнения программы
==refA is an instance of A
refA can be cast to type B
refA can not be cast to type D
refA can be cast to type B==