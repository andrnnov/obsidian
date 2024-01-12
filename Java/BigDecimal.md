#Java #BigDecimal
### Класс BigDecimal ###

2024-01-11 16:50

Класс BigDecimal расположен в пакете java.math. Этот класс расширяет класс [Number](Number). Каждый объект этого класса хранит два целочисленных значения: мантиссу вещественного числа в виде объекта класса [BigInteger](BigInteger) и неотрицательный десятичный порядок числа типа int. Например, для числа 76,34862 будет храниться мантисса 7 634 862 в объекте класса BigInteger и порядок 5 как целое число типа int. Таким образом, мантисса может содержать любое количество цифр, а порядок ограничен значением константы [[WrapperInteger#Константы класса Integer|Integer.MAX_VALUE]].

Результат операции над объектами класса BigDecimal округляется по одному из восьми правил, определяемых следующими статическими целыми константами:
- ROUND_CEILING — округление в сторону большего целого;
- ROUND_DOWN — округление к нулю, к меньшему по модулю целому значению;
- ROUND_FLOOR — округление к меньшему целому;
- ROUND_HALF_DOWN — округление к ближайшему целому, среднее значение округляется к меньшему целому;
- ROUND_HALF_EVEN — округление к ближайшему целому, среднее значение округляется к четному числу;
- ROUND_HALF_UP — округление к ближайшему целому, среднее значение округляется к большему целому;
- ROUND_UNNECESSARY — предполагается, что результат будет целым, и округление не понадобится;
- ROUND_UP — округление от нуля, к большему по модулю целому значению.

Три константы — ZERO, ONE и TEN — моделируют вещественные нуль, единицу и вещественное число десять в операциях с объектами класса BigDecimal.

В классе BigDecimal около двадцати конструкторов. Четыре из которых были введены еще в Java 2:
- BigDecimal(BigInteger bi) — объект будет хранить большое целое bi, порядок равен нулю;
- BigDecimal(BigInteger mantissa, int scale) — задается мантисса mantissa и неотрицательный порядок scale объекта; если порядок scale отрицателен, возникает исключительная ситуация;
- BigDecimal(double d) — объект будет содержать вещественное число удвоенной точности d; если значение d бесконечно или NaN, то возникает исключительная ситуация;
- BigDecimal(String val) — число задается строкой символов val, которая должна содержать запись числа по правилам языка Java.

При использовании третьего из перечисленных конструкторов возникает неприятная особенность, отмеченная в документации. Поскольку вещественное число при переводе в двоичную форму представляется, как правило, бесконечной двоичной дробью, то при создании объекта, например BigDecimal(0.1), мантисса, хранящаяся в объекте, окажется очень большой. Она показана на рис. 4.5. Но при создании такого же объекта четвертым конструктором, BigDecimal("0.1"), мантисса будет равна просто 1.

Остальные конструкторы определяют точность представления числового значения объекта и правила его округления с помощью объекта класса MathContext или непосредственно.

В классе переопределены методы doubleValue(), floatValue(), intValue(), longValue().

Большинство методов этого класса моделируют операции с вещественными числами. Они возвращают объект класса BigDecimal. Ниже в описании методов буква x обозначает объект класса BigDecimal, буква n — целое значение типа int, буква r — способ округления, одну из восьми перечисленных ранее констант:
- abs() — абсолютное значение объекта this;
- add(x) — операция сложения this + x;
- divide(x, r) — операция деления this / x с округлением по способу r;
- divide(x, n, r) — операция деления this / x с изменением порядка и округлением по способу r;
- max(x) — наибольшее из this и x;
- min(x) — наименьшее из this и x;
- movePointLeft(n) — сдвиг влево на n разрядов;
- movePointRight(n) — сдвиг вправо на n разрядов;
- multiply(x) — операция умножения this * x;
- negate() — возвращает объект с обратным знаком;
- scale() — возвращает порядок числа;
- setScale(n) — устанавливает новый порядок n;
- setScale(n, r) — устанавливает новый порядок n и округляет число при необходимости по способу r;
- signum() — знак числа, хранящегося в объекте;
- subtract(x) — операция вычитания this — x;
- toBigInteger() — округление числа, хранящегося в объекте;
- unscaledValue() — возвращает мантиссу числа;
- upl() — возвращает расстояние до следующего числа.

**Примеры использования этих методов**

```java
import java.math.*;

class BigDecimalTest{
	public static void main(String[] args){
		BigDecimal x = new BigDecimal("-12345.67890123456789"); 
		BigDecimal y = new BigDecimal("345.7896e-4");
		BigDecimal z = new BigDecimal(new BigInteger("123456789"), 8); 
		
		System.out.println("|x| = " + x.abs());
		System.out.println("x + y = " + x.add(y));
		System.out.println("x / y = " + x.divide(y, BigDecimal.ROUND_DOWN));
		System.out.println("x / y = " + x.divide(y, 6, BigDecimal.ROUND_HALF_EVEN)); 
		System.out.println("max(x, y) = " + x.max(y));
		System.out.println("min(x, y) = " + x.min(y));
		System.out.println("x << 3 = " + x.movePointLeft(3)); 
		System.out.println("x >> 3 = " + x.movePointRight(3)); 
		System.out.println("x * y = " + x.multiply(y)); 
		System.out.println("-x = " + x.negate()); 
		System.out.println("scale of x = " + x.scale());
		System.out.println("increase scale of x to 20 = " + x.setScale(20)); 
		System.out.println("decrease scale of x to 10 = " +
						x.setScale(10, BigDecimal.ROUND_HALF_UP)); 			
		System.out.println("sign(x) = " + x.signum()); 
		System.out.println("x — y = " + x.subtract(y)); 
		System.out.println("round x = " + x.toBigInteger()); 
		System.out.println("mantissa of x = " + x.unscaledValue()); 
		System.out.println("mantissa of 0.1 =\n= " + 
						new BigDecimal(0.1).unscaledValue());
	}
}
```
Вывод:
<p style="background-color: navy; color: yellow">
|x| = 12345.67890123456789<br>
x + y = -12345.64432227456789<br>
x / y = -357028.63536770822170<br>
x / y = -357028.635368<br>
max(x, y) = 0.03457896<br>
min(x, y) = -12345.67890123456789<br>
x << 3 = -12.34567890123456789<br>
x >> 3 = -12345678.90123456789<br>
x * y = -426.9007368986340736855944<br>
-x = 12345.67890123456789<br>
scale of x = 14<br>
increase scale of x to 20 = -12345.67890123456789000000<br>
decrease scale of x to 10 = -12345.6789012346<br>
sign(x) = -1<br>
x — y = -12345.71348019456789<br>
round x = -12345<br>
mantissa of x = -1234567890123456789<br>
mantissa of 0.1 =
= 1000000000000000055511151231257827021181583404541015625</p>

#### Метод compareTo() ###

Этот метод сравнивает BigDecimal с заданным BigDecimal и возвращает -1, 0 или 1, поскольку этот BigDecimal численно меньше, равен или больше заданного значения. Если значения экземпляров BigDecimal равны, но масштабы различны, они считаются равными для метода compareTo().
```java
import java.math.BigDecimal;
public class CompareToDemo {
	public static void main(String[] args) {
		System.out.println(new BigDecimal("300.43").compareTo(new igDecimal("150.12")));
		System.out.println(new BigDecimal("200.42").compareTo(new igDecimal("350.56")));
		System.out.println(new BigDecimal("140.56").compareTo(new igDecimal("140.21")));
	}
}
```
Вывод:
<p style="background-color: navy; color: yellow">
1<br>
-1<br>
1</p>

#### Метод equals() ####

Этот метод проверяет равенство BigDecimal с заданным BigDecimal. Если значения экземпляров BigDecimal равны, но масштабы различны, они не рассматриваются как равные методом equals().
```java
import java.math.BigDecimal;
public class EqualsDemo {
	public static void main(String[] args) {
		System.out.println(new BigDecimal("300.34").equals(new BigDecimal("150.67")));
		System.out.println(new BigDecimal("140.78").equals(new BigDecimal("140.78")));
	}
}
```
Вывод:
<p style="background-color: navy; color: yellow">
false<br>
true</p>
