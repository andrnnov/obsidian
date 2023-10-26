#Java #WrapperClasses
### Классы-обёртки в Java ###

2023-10-26 12:07

Класс-обёртки в Java - это класс, объект которого обертывает или содержит примитивные типы данных. Когда мы создаем объект для класса-обёрток, он содержит поле, и в этом поле мы можем хранить примитивные типы данных. Другими словами, мы можем обернуть примитивное значение в объект класса-обёртку.

**Автоупаковка (autoboxing)** — это автоматическая конвертация из примитивных типов в соответствующий этому типу класс-обёртку, вставляемая компилятором Java, например из float во Float , из int в Integer.
Примера автоупаковки:
```java
Character ch = 'a';
Integer i1 = 220;
Double d1 = 300.0;
Boolean b1 = false;
```
Компилятор Java применяет автоупаковку в следующих случаях:
- При передаче примитивного типа в параметр метода, ожидающего соответствующий ему класс-обёртку.
- При присвоении значения примитивного типа переменной соответствующего класса-обёртки.

**Распаковка (unboxing)** — конвертация класса-обёртки в соответствующий ему примитивный тип. В процессе распаковки может произойти исключение java.lang.NullPointerException , если значение переменной равно null.

Компилятор Java автоматически применяет распаковку в следующих случаях:
- При передаче объекта класса-обёртки в метод, ожидающий соответствующий примитивный тип.
- При присвоении экземпляра класса-обёртки переменной соответствующего примитивного типа.
- В выражениях, в которых один или оба аргумента являются экземплярами классов-обёрток (кроме операции == и != ).
Примеры:
```java
class Main {
    public static void method1(int x) {
    }
    public static void main(String[] args) {
        Integer i1 = 100;
        method1(i1); // распаковка
        Double d1 = 2.3;
        Double d2 = 3.3;
        double d3 = i1 + d1 + d2; // распаковка
        System.out.println(d3);
    }
}
```
Соответствие примитивных типов и классов-обёрток

|Примитивный тип|Класс-обёртка|Упаковка|Распаковка|
|---|---|---|---|
|boolean|Boolean|Boolean.valueOf(booleanValue)|booleanObject.booleanValue()|
|byte|Byte|Byte.valueOf(byteValue)|byteObject.byteValue()|
|char|Character|Character.valueOf(charValue)|characterObject.charValue()|
|float|Float|Float.valueOf(floatValue)|floatObject.floatValue()|
|int|Integer|Integer.valueOf(integerValue)|integerObject.integerValue()|
|long|Long|Long.valueOf(longValue)|longObject.longValue()|
|short|Short|Short.valueOf(shortValue)|shortObject.shortValue()|
|double|Double|Double.valueOf(doubleValue)|doubleObject.doubleValue()|

#### Когда нужны классы-обертки ####

Существуют определенные потребности для использования класса-оберток в Java, как указано ниже:
1. Они преобразуют примитивные типы данных в объекты. Объекты необходимы, если мы хотим изменить аргументы, передаваемые в метод (поскольку примитивные типы передаются по значению).
2. Классы в пакете java.util обрабатывают только объекты, и, следовательно, классы-оболочки помогают и в этом случае.
3. Структуры данных в среде Collection framework, такие как [ArrayList](Class-ArrayList) и [Vector](https://translated.turbopages.org/proxy_u/en-ru.ru.818776e1-653a23d7-ba71a0d2-74722d776562/https/www.geeksforgeeks.org/vector-vs-arraylist-java/), хранят только объекты (ссылочные типы), а не примитивные типы.
4. Объект необходим для поддержки синхронизации в многопоточности.
#### Преимущества классов-оберток ####

1. Коллекции допускают только объектные данные.
2. Для объектных данных мы можем вызывать несколько методов compareTo(), equals(), toString()
3. Клонирование обрабатывает только объекты
4. Данные объекта допускают нулевые значения.
5. Сериализация может разрешать только объектные данные.

#### Пример классов-оберток Java ####
```java
// Java program to demonstrate Wrapping and UnWrapping in Classes
import java.io.*;
 
class GFG {
    public static void main(String[] args) {
        // byte data type
        byte a = 1;
 
        // wrapping around Byte object
        Byte byteobj = new Byte(a);
        // Use with Java 9
        // Byte byteobj = Byte.valueOf(a);
 
        // int data type
        int b = 10;
 
        // wrapping around Integer object
        Integer intobj = new Integer(b);
        // Use with Java 9
        // Integer intobj = Integer.valueOf(b);
 
        // float data type
        float c = 18.6f;
 
        // wrapping around Float object
        Float floatobj = new Float(c);
        // Use with Java 9
        // Float floatobj = Float.valueOf(c);
 
        // double data type
        double d = 250.5;
 
        // Wrapping around Double object
        Double doubleobj = new Double(d);
        // Use with Java 9
        // Double doubleobj = Double.valueOf(d);
 
        // char data type
        char e = 'a';
 
        // wrapping around Character object
        Character charobj = e;
 
        // printing the values from objects
        System.out.println("Values of Wrapper objects (printing as objects)");
        System.out.println("\nByte object byteobj: " + byteobj);
        System.out.println("\nInteger object intobj: " + intobj);
        System.out.println("\nFloat object floatobj: " + floatobj);
        System.out.println("\nDouble object doubleobj: " + doubleobj);
        System.out.println("\nCharacter object charobj: " + charobj);
 
        // objects to data types (retrieving data types from
        // objects) unwrapping objects to primitive data
        // types
        byte bv = byteobj;
        int iv = intobj;
        float fv = floatobj;
        double dv = doubleobj;
        char cv = charobj;
 
        // printing the values from data types
        System.out.println(
            "\nUnwrapped values (printing as data types)");
        System.out.println("\nbyte value, bv: " + bv);
        System.out.println("\nint value, iv: " + iv);
        System.out.println("\nfloat value, fv: " + fv);
        System.out.println("\ndouble value, dv: " + dv);
        System.out.println("\nchar value, cv: " + cv);
    }
}
```
**Вывод**
==Values of Wrapper objects (printing as objects)
Byte object byteobj: 1
Integer object intobj: 10
Float object floatobj: 18.6
Double object doubleobj: 250.5
Character object charobj: a
Unwrapped values (printing as data types)
byte value, bv: 1
int value, iv: 10
float value, fv: 18.6
double value, dv: 250.5
char value, cv: a==
#### Пользовательские классы-оболочки в Java ####

Классы-обертки Java обертывают примитивные типы данных. Мы можем создать класс, который обертывает данные внутри него. Итак, давайте проверим, как создать наш собственный пользовательский класс-оболочку в Java. Это может быть реализовано для создания определенных структур, таких как очереди, стеки и т.д.
```java
// Java Program to implement
// Custom wrapper class
import java.io.*;
 
// wrapper class
class Maximum {
    private int maxi = 0;
    private int size = 0;
 
    public void insert(int x) {
        this.size++;
        if (x <= this.maxi)
            return;
        this.maxi = x;
    }
 
    public int top() { return this.maxi; }
 
    public int elementNumber() { return this.size; }
};
 
class GFG {
    public static void main(String[] args) {
        Maximum x = new Maximum();
        x.insert(12);
        x.insert(3);
        x.insert(23);
 
        System.out.println("Maximum element: " + x.top());
        System.out.println("Number of elements inserted: "
                           + x.elementNumber());
    }
}
```
**Вывод**:
==Maximum element: 23
Number of elements inserted: 3==

