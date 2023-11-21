#Java #Enum
### Перечисления (enumeration). Ключевое слово enum ###

2023-11-21 15:47
#### Понятие перечисления. Общая форма объявления перечисления. Ключевое слово enum ####

Перечисления появились в Java начиная с версии JDK 5. В наиболее общем случае, перечисления – это список именованных констант. Для объявления перечисления используется ключевое слово enum.

Работа с перечислениями в Java имеет свои особенности, не характерные для некоторых других языков программирования, в частности C++. В языке Java перечисления являются классами. Поэтому для них свойственны все возможности классов. Это означает, что перечисления могут иметь конструкторы, методы, переменные экземпляра и реализации интерфейса. Общая форма объявления перечисления следующая:
```java
enum EnumName {
  constant1, constant2, ..., constantN
}
```
здесь
    EnumName – имя перечисления, которое является типом данных. EnumName – это также имя класса;
    constant1, constant2, …, constantN – список именуемых констант, составляющих множество значений перечисления EnumName. Именуемые константы являются открытыми статическими конечными членами класса EnumName. Эти константы еще называются самотипизированными.

На основе типа вычисления EnumName можно объявлять переменные данного типа по следующему образцу
```java
EnumName obj;
```
Здесь obj – имя экземпляра типа EnumName. Создание экземпляра типа перечисления obj производится без использования оператора new. Это означает, что переменная типа перечисления объявляется и используется так же, как и переменная любого примитивного типа (int, float, char, …).

Переменная obj может получать значения из множества констант, объявленных в перечислении EnumName, например
```java
obj = EnumName.constant1;
```
В языке Java перечисление может оперировать константами типов с плавающей запятой (float, double).
#### Объявление и использование простейшего перечисления. Определение названия месяца года ####

**Условие задачи**. Объявить перечисление Months, содержащее перечень констант, соответствующих сокращенному названию месяца года. В демонстрационной программе обеспечить ввод номер месяца (1..12) и вывод соответствующей константы из экземпляра перечисления.

**Решение**. Для ввода номера месяца с клавиатуры в программе используются возможности класса Scanner.

Листинг программы, решающей данную задачу, следующий
```java
import java.util.Scanner;

// Перечисление, содержащее константы, которые связаны с месяцами года
enum Months {
  Jan, Feb, Mar, Apr, May, Jun,
  Jul, Aug, Sep, Oct, Nov, Dec
}

public class TrainEnumerations {
	public static void main(String[] args) {
	    // Перечисление
	    // 1. Объявить переменную типа Months
	    Months mn = Months.Jan;
	    // 2. Ввести номер месяца с клавиатуры
	    System.out.print("month = ");
	    Scanner input = new Scanner(System.in);
	    int numMonth = input.nextInt();
	    // 3. По номеру месяца присвоить
	    //   соответствующее значение экземпляру mn
	    switch (numMonth) {
		    case 1: mn = Months.Jan; break;
		    case 2: mn = Months.Feb; break;
		    case 3: mn = Months.Mar; break;
		    case 4: mn = Months.Apr; break;
		    case 5: mn = Months.May; break;
			case 6: mn = Months.Jun; break;
		    case 7: mn = Months.Jul; break;
		    case 8: mn = Months.Aug; break;
		    case 9: mn = Months.Sep; break;
		    case 10: mn = Months.Oct; break;
		    case 11: mn = Months.Nov; break;
		    case 12: mn = Months.Dec; break;
		    default: System.out.println("Incorrect input"); return;
		}
    // 4. Вывести название константы, которая соответствует введенному номеру месяца
    System.out.println(mn);
	}
}

```
Вывод
==month = 8
Aug==
#### Использование имени перечисления в операторе switch ####

Данный пример демонстрирует использование экземпляра перечисления для управления оператором switch.

**Условие задачи**. Задано перечисление Seasons, которое описывает четыре времена года. Реализовать ввод с клавиатуры номера времени года (1..4). На основе номера времени года вычислить продолжительность времени года в днях. Считать, что год не высокосный.

**Решение**.
```java
import java.util.Scanner;

// Перечисление, описывающее времена года
enum Seasons {
  Spring, Summer, Autumn, Winter
}

public class TrainEnumerations {
	public static void main(String[] args) {
	    // Использование перечисления в операторе switch
	    // 1. Объявить экземпляр типа Seasons
	    Seasons season;
	    // 2. Ввести номер времени года
	    System.out.print("Season (1..4) = ");
	    Scanner inStr = new Scanner(System.in);
	    int numSeason = inStr.nextInt();
	    // 3. Получить значение константы на основе номера времени года
	    switch (numSeason) {
		    case 1: season = Seasons.Spring; // весна
			    break;
		    case 2: season = Seasons.Summer; // лето
			    break;
		    case 3: season = Seasons.Autumn; // осень
			    break;
		    case 4: season = Seasons.Winter; // зима
			    break;
		    default:
			    System.out.println("Incorrect input.");
			    return;
		}
	    // 4. Вычислить количество дней во времени года на основе значения season.
	    //    Использовать оператор switch.
	    System.out.println("season = " + season);
	    int nDays = 0;
		    switch (season) {
		    case Spring: nDays = 92; break;
		    case Summer: nDays = 92; break;
		    case Autumn: nDays = 91; break;
		    case Winter: nDays = 90; break;
	    }

	    // 5. Вывести результат
	    System.out.println("Number of days = " + nDays);
	}
}
```
Вывод
==Season (1..4) = 2
season = Summer
Number of days = 92==
#### Метод values(). Получить константы перечисления в виде массива ####

Метод values() позволяет конвертировать список именованных констант из перечисления в массив. Общая форма метода следующая
```java
public static enum_type [] values()
```
здесь enum_type – тип перечисления, константы которого нужно конвертировать в массив.

**Пример**. В примере с помощью функции values() формируется массив значений констант из перечисления Days, описывающий дни недели.
```java
import java.util.Scanner;

// Перечисление.
// Перечень дней недели
enum Days {
  Sun, Mon, Tue, Wed, Thu, Fri, Sat
}

public class TrainEnumerations {
	public static void main(String[] args) {
	    // Метод values()
	    // 1. Получить значение констант в виде массива
	    Days arrayDays[] = Days.values();
	    // 2. Вывести элементы массива arrayDays
	    for (int i=0; i<arrayDays.length; i++) {
		    System.out.println(arrayDays[i]);
	    }
	}
}
```
Результат выполнения программы
==Sun
Mon
Tue
Wed
Thu
Fri
Sat==

#### Метод valueOf(). Конвертировать строковое представление константы в значение из перечисления ####

Метод valueOf() позволяет получить представление константы по перечислению в виде строки. Общая форма метода следующая
```java
public static enum_type valueOf(String str)
```
здесь
    enum_type – тип перечисления;
    str – строковое представление константы из перечисления enum_type.

**Пример**. В примере демонстрируется использование метода valueOf() для получения значения константы из перечисления Days.
```java
import java.util.Scanner;

// Перечисление.
// Перечень дней недели
enum Days {
  Sun, Mon, Tue, Wed, Thu, Fri, Sat
}

public class TrainEnumerations {
	public static void main(String[] args) {
	    // Метод valueOf()
	    // Ввести строку названия дня
	    System.out.print("Day = ");
	    Scanner inStr = new Scanner(System.in);
	    String strDay = inStr.next(); // строка с названием дня
	    // Получить значение константы
	    Days day;
	    day = Days.valueOf(strDay);
	    // Вывести полученное значение константы из перечисления day
	    System.out.println(day);
	}
}
```
Вывод
==Day = Fri
Fri==


