
#Java #BigInteger
### Класс BigInteger ###

2024-01-11 14:22

Все примитивные целые типы имеют ограниченный диапазон значений. В целочисленной арифметике Java нет переполнения, целые числа приводятся по модулю, равному диапазону значений.

Для того чтобы было можно производить целочисленные вычисления с любой разрядностью, в состав Java API введен класс BigInteger, хранящийся в пакете java.math. 

BigInteger предназначен для обработки очень больших целых чисел (которые больше 64-разрядных значений). Этот класс может обрабатывать очень большие целые числа, и размер целого числа ограничен только доступной памятью [JVM](JVM). Однако BigInteger следует использовать только в том случае, если это абсолютно необходимо, поскольку использование BigInteger менее интуитивно понятно по сравнению со встроенными типами (поскольку Java не поддерживает перегрузку операторов), и с его использованием всегда связано снижение производительности. Операции с BigInteger выполняются существенно медленнее, чем со встроенными целочисленными типами. Кроме того, объем памяти, занимаемый одним BigInteger, существенно велик (в среднем около 80 байт на 64-разрядной [JVM](JVM)) по сравнению со встроенными типами.

[В официальной документации BigInteger](https://docs.oracle.com/javase/8/docs/api/java/math/BigInteger.html) говорится, что реализации BigInteger должны поддерживать все целые числа от $-2^{2147483647}$ до $2^{2147483647}$ (эксклюзивные). Это означает, что BigInteger s может иметь более 2 _миллиардов_ бит!

Другим важным аспектом класса BigInteger является то, что он неизменяем. Это означает, что вы не можете изменить сохраненное значение объекта BigInteger, вместо этого вам нужно присвоить измененное значение новой переменной.

Например, следующее не будет работать, поскольку `sum` не будет обновляться из-за неизменности.
```java
BigInteger sum = BigInteger.ZERO;
for(int i = 1; i < 5000; i++) {
   sum.add(BigInteger.valueOf(i));  
}
```
Назначьте результат переменной `sum` чтобы она работала.
```java
sum = sum.add(BigInteger.valueOf(i));
```

Этот класс расширяет класс [Number](Number), следовательно, в нем переопределены методы
doubleValue(), floatValue(), intValue(), longValue(). Методы byteValue() и shortValue() не
переопределены, а прямо наследуются от класса [Number](Number).

Действия с объектами класса BigInteger не приводят ни к переполнению, ни к приведению по модулю. Если результат операции велик, то число разрядов просто наращивается. Числа хранятся в двоичной форме с дополнительным кодом.

Перед выполнением операции числа выравниваются по длине распространением знакового разряда.

Шесть конструкторов класса создают объект класса BigInteger из строки символов (знака числа и цифр), массива байтов или задают случайное число. Чаще всего используются три конструктора:
- BigInteger(String value) — объект будет хранить большое целое число, заданное строкой цифр, перед которыми может стоять знак минус;
- BigInteger(String value, int radix) — задается строка цифр со знаком value, записанная в системе счисления с основанием radix;
- BigInteger(byte[] value) — объект будет хранить большое целое число, заданное массивом value, содержащим двоичное представление числа в дополнительном коде.

Три константы — ZERO, ONE и TEN — моделируют нуль, единицу и число десять в операциях с объектами класса BigInteger.

#### Методы класса BigInteger ####
##### Метод toByteArray() преобразует объект в массив байтов #####

```java
  public class BigIntegerMethodsExample {
    public static void main(String[] args) {
        BigIntegerMethodsExample example = new BigIntegerMethodsExample();
        example.toByteArrayMethod();
    }
    
    public void toByteArrayMethod() {
        // create and assign value to byte array b3
        byte b3[] = {
            0x1,
            0x00,
            0x00
        };
        BigInteger bi1 = new BigInteger("10");
        BigInteger bi2 = new BigInteger(b3); // using byte[] constructor of BigInteger

        // assign byte array representation of bi1, bi2 to b1, b2
        byte[] b1 = bi1.toByteArray();
        byte[] b2 = bi2.toByteArray();
        String str1 = "Byte array representation of " + bi1 + " is: ";
        System.out.println(str1);
        // print byte array b1 using for loop
        for (int i = 0; i < b1.length; i++) {
            System.out.format("0x%02X\n", b1[i]);
        }

        String str2 = "Byte array representation of " + bi2 + " is: ";
        System.out.println(str2);
        // print byte array b2 using for loop
        for (int j = 0; j < b2.length; j++) {
            System.out.format("0x%02X ", b2[j]);
        }
    }
}
```
Вывод:
<p style="background-color: navy; color: yellow">
Byte array representation of 10 is: <br>
0x0A<br>
Byte array representation of 65536 is: <br>
0x01 0x00 0x00</p>

Большинство методов класса BigInteger моделируют целочисленные операции и функции, возвращая объект класса BigInteger:
- abs() — возвращает объект, содержащий абсолютное значение числа, хранящегося в данном объекте this;
- add(x) — операция сложения this + x;
- and(x) — операция побитовой конъюнкции this & x;
- andNot(x) — операция побитовой дизъюнкции с дополнением this & (~x);
- divide(x) — операция деления this / x;
- divideAndRemainder(x) — возвращает массив из двух объектов класса BigInteger, содержащих частное и остаток от деления this на x;
- gcd(x) — наибольший общий делитель абсолютных значений объекта this и аргумента x;
- max(x) — наибольшее из значений объекта this и аргумента x;
- min(x) — наименьшее из значений объекта this и аргумента x;
- mod(x) — остаток от деления объекта this на аргумент метода x;
- modInverse(x) — остаток от деления числа, обратного объекту this, на аргумент x;
- modPow(n, m) — остаток от деления объекта this, возведенного в степень n, на m;
- multiply(x) — операция умножения this * x;
- negate() — перемена знака числа, хранящегося в объекте;
- not() — операция отрицания ~this;
- or(x) — операция побитовой дизъюнкции this | x;
- pow(n) — операция возведения числа, хранящегося в объекте, в степень n;
- remainder(x) — операция взятия остатка от деления this % x;
- shiftLeft(n) — операция сдвига влево this << n;
- shiftRight(n) — операция арифметического сдвига вправо this >> n;
- signum() — для отрицательных значений равно -1, для 0 равно 0, для положительного значения равно +1;
- subtract(x) — операция вычитания this — x;
- xor(x) — операция "исключающее ИЛИ" this ^ x.

##### Пример использования signum() #####

```java
package com.concretepage;
import java.math.BigInteger;
public class SignumDemo {
	public static void main(String[] args) {
		//-1 for values < 0
		System.out.println("signum for -15: "+ new BigInteger("-15").signum());
		//0 for value 0
		System.out.println("signum for   0: "+ new BigInteger("0").signum());
		//1 for values > 0
		System.out.println("signum for  25: "+ new BigInteger("25").signum());
	}
}
```
Вывод:
<p style="background-color: navy; color: yellow">
signum for -15: -1<br>
signum for   0: 0<br>
signum for  25: 1</p>

##### Сравнение BigInteger #####

Вы можете сравнить `BigIntegers` же, как вы сравниваете `String` или другие объекты в Java.

Например:
```java
BigInteger one = BigInteger.valueOf(1);
BigInteger two = BigInteger.valueOf(2);

if(one.equals(two)){
    System.out.println("Equal");
}
else{
    System.out.println("Not Equal");
}
```
**Выход:**
<p style="background-color: navy; color: yellow">
Not Equal</p>

**Замечания:**
В общем, **не** используйте использование оператора `==` для сравнения BigIntegers
- `==` operator: сравнивает ссылки; т.е. имеют ли два значения один и тот же объект
- Метод `equals()` : сравнивает содержимое двух BigIntegers.

Например, BigIntegers **не** следует сравнивать следующим образом:
```java
if (firstBigInteger == secondBigInteger) {
  // Only checks for reference equality, not content equality!
}
```
Это может привести к неожиданному поведению, поскольку оператор `==` проверяет только ссылочное равенство. Если оба BigIntegers содержат один и тот же контент, но не относятся к одному и тому же объекту, **это не сработает.** Вместо этого сравните BigIntegers, используя методы `equals`, как описано выше.

Вы также можете сравнить свой `BigInteger` с постоянными значениями, такими как 0,1,10.

Например:
```java
BigInteger reallyBig = BigInteger.valueOf(1);
if(BigInteger.ONE.equals(reallyBig)){
    //code when they are equal.
}    
```

Вы также можете сравнить два BigInteger с помощью метода `compareTo()`, как `compareTo()` ниже: `compareTo()` возвращает 3 значения.
- **0:** Когда оба **равны**.
- **1:** Когда первое **больше** второго (одно в скобках).
- **-1:** Когда первое **меньше** второго.
```java
BigInteger reallyBig = BigInteger.valueOf(10);
BigInteger reallyBig1 = BigInteger.valueOf(100);

if(reallyBig.compareTo(reallyBig1) == 0){
    //code when both are equal.
}
else if(reallyBig.compareTo(reallyBig1) == 1){
    //code when reallyBig is greater than reallyBig1.
}
else if(reallyBig.compareTo(reallyBig1) == -1){
    //code when reallyBig is less than reallyBig1.
}
```

#### Примеры использования методов класса BigInteger ####

##### Пример 1. Следующий пример BigInteger показывает, как можно создать Java BigInteger и как с ним можно выполнять различные арифметические операции #####

```java
import java.math.BigInteger;
 
public class BigIntegerDemo {
 
    public static void main(String[] args) {
         
        BigInteger b1 = new BigInteger("987654321987654321000000000");
        BigInteger b2 = new BigInteger("987654321987654321000000000");
         
        BigInteger product = b1.multiply(b2);
        BigInteger division = b1.divide(b2);
         
        System.out.println("product = " + product);
        System.out.println("division = " + division);  // prints 1
    }
}
```
Вывод:
<p style="background-color: navy; color: yellow">
product = 975461059740893157555403139789971041000000000000000000<br>
division = 1</p>

##### Пример 2. Вычисление факториала с помощью BigInteger #####

Вычисление факториала - хороший пример того, как числа становятся очень большими даже при небольших входных данных. Мы можем использовать BigInteger для вычисления факториала даже для больших чисел!
```java
import java.math.BigInteger;
public class BigIntegerFactorial {
     public static void main(String[] args) {
        calculateFactorial(50);
    }
    public static void calculateFactorial(int n) {      
        BigInteger result = BigInteger.ONE;
        for (int i=1; i<=n; i++) {
            result = result.multiply(BigInteger.valueOf(i));
        }
        System.out.println(n + "! = " + result);
    }
}
```
Вывод:
<p style="background-color: navy; color: yellow">
50! = 30414093201713378043612608166064768844377641568960512000000000000</p>

##### Пример3. Использования методов класса BigInteger в программе BigIntegerTest #####

```java
import java.math.BigInteger; 

class BigIntegerTest{
	public static void main(String[] args){
		BigInteger a = new BigInteger("99999999999999999"); 
		BigInteger b = new BigInteger("88888888888888888888"); 
		
		System.out.println("bits in a = " + a.bitLength()); 
		System.out.println("bits in b = " + b.bitLength()); 
		System.out.println("a + b = " + a.add(b)); 
		System.out.println("a & b = " + a.and(b)); 
		System.out.println("a & ~b = " + a.andNot(b)); 
		System.out.println("a / b = " + a.divide(b)); 
		
		BigInteger[] r = a.divideAndRemainder(b);
		
		System.out.println("a / b: q = " + r[0] + ", r = " + r[1]); 
		System.out.println("gcd(a, b) = " + a.gcd(b)); 
		System.out.println("max(a, b) = " + a.max(b)); 
		System.out.println("min(a, b) = " + a.min(b)); 
		System.out.println("a mod b = " + a.mod(b)); 
		System.out.println("1/a mod b = " + a.modInverse(b)); 
		System.out.println("a^n mod b = " + a.modPow(a, b));
		System.out.println("a * b = " + a.multiply(b)); 
		System.out.println("-a = " + a.negate()); 
		System.out.println("~a = " + a.not()); 
		System.out.println("a | b = " + a.or(b)); 
		System.out.println("a ^ 3 = " + a.pow(3)); 
		System.out.println("a % b = " + a.remainder(b)); 
		System.out.println("a << 3 = " + a.shiftLeft(3)); 
		System.out.println("a >> 3 = " + a.shiftRight(3)); 
		System.out.println("sign(a) = " + a.signum()); 
		System.out.println("a — b = " + a.subtract(b)); 
		System.out.println("a ^ b = " + a.xor(b));
	}
}
```
Вывод:
<p style="background-color: navy; color: yellow">
bits in a = 57<br>
bits in b = 67<br>
a + b = 88988888888888888887<br>
a & b = 72133975954525752<br>
a & ~b = 27866024045474247<br>
a / b = 0<br>
a / b: q = 0, r = 99999999999999999<br>
gcd(a, b) = 1<br>
max(a, b) = 88888888888888888888<br>
min(a, b) = 99999999999999999<br>
a mod b = 99999999999999999<br>
1/a mod b = 87543098654209765319<br>
a^n mod b = 36948590717373350119<br>
a * b = 8888888888888888799911111111111111112<br>
-a = -99999999999999999<br>
~a = -100000000000000000<br>
a | b = 88916754912934363135<br>
a ^ 3 = 999999999999999970000000000000000299999999999999999<br>
a % b = 99999999999999999<br>
a << 3 = 799999999999999992<br>
a >> 3 = 12499999999999999<br>
sign(a) = 1<br>
a — b = -88788888888888888889<br>
a ^ b = 88844620936979837383</p>

