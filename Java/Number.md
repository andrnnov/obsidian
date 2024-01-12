#Java #Number
### [Class Number](https://www.javaguides.net/2018/12/java-number-class-methods-with-examples.html) ###

2024-01-10 16:26

Класс java.lang.Number является суперклассом классов [BigDecimal](BigDecimal), [BigInteger](BigInteger), Byte, Double, Float, [[WrapperInteger#Класс Integer|Integer]], Long и Short. Подклассы Number должны предоставлять методы для преобразования представленного числового значения в byte, double, float, int, long и short.

#### Методы класса Number ####

| Модификатор и тип | Метод | Описание |
| ---- | ---- | ---- |
| byte | byteValue() | Возвращает значение указанного числа в виде byte |
| abstract double | doubleValue() | Возвращает значение указанного числа в виде double |
| abstract float | floatValue() | Возвращает значение указанного числа в виде float |
| abstract int | intValue() | Возвращает значение указанного числа в виде int |
| abstract long | longValue() | Возвращает значение указанного числа в виде long |
| short | shortValue() | Возвращает значение указанного числа в виде short |

##### Метод byte byteValue() #####

Этот метод возвращает значение указанного числа в виде байта, что может включать округление или усечение.
```java
public void byteValueMethod() {
 // get a number as integer
 Number x = new Integer(123456);

 // get a number as float
 Number y = new Float(9876f);

 // print their value as byte
 System.out.println("x as integer:" + x + ", x as byte:" + x.byteValue());
 System.out.println("y as float:" + y + ", y as byte:" + y.byteValue());
}
```
Вывод:
<p style="background-color: navy; color: yellow">
x as integer:123456, x as byte:64<br>
y as float:9876.0, y as byte:-108</p>
##### Метод abstract double doubleValue() #####

Этот метод возвращает значение указанного числа в виде двойного значения, которое может включать округление.
```java
public void doubleValueMethod() {
 // get a number as integer
 Number x = new Integer(123456);

 // get a number as float
 Number y = new Float(9876f);

 // print their value as double
 System.out.println("x as integer :" + x + ", x as double:" + x.doubleValue());
 System.out.println("y as float::" + y + ", y as double:" + y.doubleValue());
}
```
Вывод:
<p style="background-color: navy; color: yellow">
x as integer :123456, x as double:123456.0<br>
y as float::9876.0, y as double:9876.0</p>

##### Метод abstract float floatValue() #####

Этот метод возвращает значение указанного числа в виде числа с плавающей точкой, что может включать округление.
```java
public void floatValueMethod() {
 // get a number as integer
 Number x = new Integer(123456);

 // get a number as double
 Number y = new Double(9876);

 // print their value as float
 System.out.println("x as integer:" + x + ", x as float:" + x.floatValue());
 System.out.println("y as double:" + y + ", y as float:" + y.floatValue());
}
```
Вывод:
<p style="background-color: navy; color: yellow">
x as integer:123456, x as float:123456.0<br>
y as double:9876.0, y as float:9876.0</p>

##### Методcd  abstract int intValue() #####

Этот метод возвращает значение указанного числа в виде int, которое может включать округление или усечение.
```java
public void intValueMethod() {
 // get a number as float
 Number x = new Float(123456f);

 // get a number as double
 Number y = new Double(9876);

 // print their value as int
 System.out.println("x as float:" + x + ", x as Integer:" + x.intValue());
 System.out.println("y as double:" + y + ", y as Integer:" + y.intValue());
}
```
Вывод:
<p style="background-color: navy; color: yellow">
x as float:123456.0, x as Integer:123456<br>
y as double:9876.0, y as Integer:9876</p>

##### Метод abstract long longValue() #####

Этот метод возвращает значение указанного числа в виде long, что может включать округление или усечение.
```java
public void longValueMethod() {
 // get a number as float
 Number x = new Float(123456f);

 // get a number as double
 Number y = new Double(9876);

 // print their value as long
 System.out.println("x as float:" + x + ", x as long:" + x.longValue());
 System.out.println("y as double:" + y + ", y as long:" + y.longValue());
}
```
Вывод:
<p style="background-color: navy; color: yellow">
x as float:123456.0, x as long:123456<br>
y as double:9876.0, y as long:9876</p>

##### Метод short shortValue() #####

Этот метод возвращает значение указанного числа в виде краткого значения, которое может включать округление или усечение.
```java
public void shortValueMethod() {
 // get a number as float
 Number x = new Float(123456f);

 // get a number as double
 Number y = new Double(9876);

 // print their value as short
 System.out.println("x as float :" + x + ", x as short:" + x.shortValue());
 System.out.println("y as double:" + y + ", y as short:" + y.shortValue());
}
```
Вывод:
<p style="background-color: navy; color: yellow">
x as float :123456.0, x as short:-7616<br>
y as double:9876.0, y as short:9876</p>

##### Полный пример #####

```java
package net.javaguides.lang;

/**
 * Class demonstrates the usage of Random class methods with examples
 * 
 * @author Ramesh Fadatare
 *
 */
public class NumberClassMethods {

    public static void main(String[] args) {
        NumberClassMethods classMethods = new NumberClassMethods();
        classMethods.shortValueMethod();
        classMethods.longValueMethod();
        classMethods.intValueMethod();
        classMethods.floatValueMethod();
        classMethods.doubleValueMethod();
        classMethods.byteValueMethod();
    }

    public void shortValueMethod() {
        // get a number as float
        Number x = new Float(123456 f);

        // get a number as double
        Number y = new Double(9876);

        // print their value as short
        System.out.println("x as float :" + x + ", x as short:" + x.shortValue());
        System.out.println("y as double:" + y + ", y as short:" + y.shortValue());
    }

    public void longValueMethod() {
        // get a number as float
        Number x = new Float(123456 f);

        // get a number as double
        Number y = new Double(9876);

        // print their value as long
        System.out.println("x as float:" + x + ", x as long:" + x.longValue());
        System.out.println("y as double:" + y + ", y as long:" + y.longValue());
    }

    public void intValueMethod() {
        // get a number as float
        Number x = new Float(123456 f);

        // get a number as double
        Number y = new Double(9876);

        // print their value as int
        System.out.println("x as float:" + x + ", x as Integer:" + x.intValue());
        System.out.println("y as double:" + y + ", y as Integer:" + y.intValue());
    }

    public void floatValueMethod() {
        // get a number as integer
        Number x = new Integer(123456);

        // get a number as double
        Number y = new Double(9876);

        // print their value as float
        System.out.println("x as integer:" + x + ", x as float:" + x.floatValue());
        System.out.println("y as double:" + y + ", y as float:" + y.floatValue());
    }

    public void doubleValueMethod() {
        // get a number as integer
        Number x = new Integer(123456);

        // get a number as float
        Number y = new Float(9876 f);

        // print their value as double
        System.out.println("x as integer :" + x + ", x as double:" + x.doubleValue());
        System.out.println("y as float::" + y + ", y as double:" + y.doubleValue());
    }

    public void byteValueMethod() {
        // get a number as integer
        Number x = new Integer(123456);

        // get a number as float
        Number y = new Float(9876 f);

        // print their value as byte
        System.out.println("x as integer:" + x + ", x as byte:" + x.byteValue());
        System.out.println("y as float:" + y + ", y as byte:" + y.byteValue());
    }
}
```
Вывод:
<p style="background-color: navy; color: yellow">
x as float :123456.0, x as short:-7616<br>
y as double:9876.0, y as short:9876<br>
x as float:123456.0, x as long:123456<br>
y as double:9876.0, y as long:9876<br>
x as float:123456.0, x as Integer:123456<br>
y as double:9876.0, y as Integer:9876<br>
x as integer:123456, x as float:123456.0<br>
y as double:9876.0, y as float:9876.0<br>
x as integer :123456, x as double:123456.0<br>
y as float:9876.0, y as double:9876.0<br>
x as integer:123456, x as byte:64<br>
y as float:9876.0, y as byte:-108</p>
