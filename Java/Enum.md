#Java #Enum
## Перечисления (enumeration). Ключевое слово enum 

2023-11-21 15:47

### Понятие перечисления. Общая форма объявления перечисления. Ключевое слово enum 

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

### Объявление и использование простейшего перечисления. Определение названия месяца года 

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
**Вывод**
<p style="background-color: navy; color: yellow">
month = 8<br>
Aug</p>

### Использование имени перечисления в операторе switch

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
**Вывод**
<p style="background-color: navy; color: yellow">
Season (1..4) = 2<br>
season = Summer<br>
Number of days = 92</p>

### К Enum можно применять методы:

- name() - возвращает имя
- ordinal() - возвращает порядковый номер
- equals()
- hashCode()
- toString()
- finalize()
- clone()
- values()
- valueOf()
Enum реализовывает интерфейс [Comparable](Comparable)
Enum реализовывает интерфейс [Serializable](Serializable)

#### Методы name() и ordinal()

У каждого **enum** есть имя и порядковый номер. Получить их можно с помощью методов **name()** и **ordinal()**
```java
System.out.println(Color.RED.name()); //output: RED
System.out.println(Color.RED.ordinal()); //output: 0
```
Посмотрим как это реализовано в классе **Enum**
```java
public abstract class Enum<E extends java.lang.Enum<E>>
        implements Comparable<E>, Serializable {
 
    private final String name;
 
    public final String name() {
        return name;
    }
 
    private final int ordinal;
 
    public final int ordinal() {
        return ordinal;
    }
 
    protected Enum(String name, int ordinal) {
        this.name = name;
        this.ordinal = ordinal;
    }
....
}
```
Пояснения:
- Конструктор невидим для разработчиков, но используется самой Java для корректной работы перечислений.

Возникает вопрос, а где же ключевое слово **extends** возле декларации перечисления **Color?** Все дело в ключевом слове **enum**, именно оно даёт понять программе, что вы хотите _**не просто класс, а именно перечисление**_.

#### Методы equals(), hashcode(), toString(), finalize() и clone()

**Enum** переопределяет базовые методы класса **Object.** Так что их можно использовать сразу же в наших перечислениях.

**Пример 1: equals()**
```java
boolean isEqualToItself = Color.RED.equals(Color.RED);
boolean isEqualToDifferentColor = Color.RED.equals(Color.GREEN);

System.out.println(isEqualToItself); //output: true
System.out.println(isEqualToDifferentColor);//output: false
```
**Пример 2: hashCode()**
```java
int hashOfRed = Color.RED.hashCode();
int hashOfGreen = Color.GREEN.hashCode();

System.out.println(hashOfRed); //output would be different every time: 366712642
System.out.println(hashOfGreen); //output would be different every time: 1829164700
```
Поскольку мы использовали hashCode(), каждый раз будет выводиться разное значение, сгенерированное автоматически. Когда мы запускали код, получили числа 366712642 и 1829164700. Вы наверняка получите другие числа.

**Пример 3: toString()**
```java
String red = Color.RED.toString();
System.out.println(red); //output: RED
```
Посмотрим как они реализованы в классе Enum
```java
public String toString() {
    return name;
}

public final boolean equals(Object other) {
    return this==other;
}

public final int hashCode() {
    return super.hashCode();
}
```
**Пояснения:**
метод toString() возвращает имя значения перечисления. Назвали значение WHITE, это же значение и получим при вызове toString() или name();
метод equals() сравнивает значения перечислений по ссылкам. Почему? Потому, что значения в перечислениях являются константными (уникальными), существует всего один экземпляр цвета RED, один цвета GREEN и один BLUE, значит ссылка на этот экземпляр будет всего одна, значит их можно сравнивать с помощью `==`. Вы можете сами убедиться в этом, написав `Color.RED == Color.RED` или `Color.GREEN == COLOR.BLUE`;
метод [[Object#Метод hashCode()|hashCode()]] использует стандартную реализацию из класса [Object](Object).

**Пример 4: finalize(), clone()**
```java
protected final void finalize() { }

protected final Object clone() throws CloneNotSupportedException {
    throw new CloneNotSupportedException();
}
```
**Пояснения:**
- метод finalize() пустой, а это значит, что не нужно закрывать "ресурсы" перед сборщиком мусора.  Мы говорим о тех "ресурсах", которые используются в [try-with-resources](try-with-resources). Да и вообще метод finalize() пережиток прошлых лет и в Java 9 данный метод уже помечен как @Deprecated (устаревший метод, который уберут в последующих реализациях);
- метод clone() мы можем вызвать только внутри самого перечисления т.к. он помечен ключевым словом protected. Но даже если мы попытаемся сделать это, то ничего мы не получим, кроме CloneNotSupportedException. Нужно это для того, чтобы нельзя было создать несколько экземпляров одного и того же перечисления. Ведь в реальной жизни у нас нет двух цифр "1", нет двух значений скорости света, так и с перечислениями.

#### Метод values(). Получить константы перечисления в виде массива

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
**Результат выполнения программы**
<p style="background-color: navy; color: yellow">
Sun<br>
Mon<br>
Tue<br>
Wed<br>
Thu<br>
Fri<br>
Sat</p>
Посмотрим на реализацию метода values() в классе Enum
```java
public static E[] values();
```
**Пояснения:**
- полной реализации метода в классе Enum нет, так как он синтетический (искусственно добавляется во время компиляции). Из документации узнаем, что метод просто возвращает массив всех значений перечисления в порядке их объявления.

#### Метод valueOf(). Конвертировать строковое представление константы в значение из перечисления

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
**Вывод**
<p style="background-color: navy; color: yellow">
Day = Fri<br>
Fri</p>
Посмотрим на реализацию метода valueOf() в классе Enum
```java
public static E valueOf(String name);
```
**Пояснения:**
- как и в случае с values() этот метод тоже синтетический и поэтому полной реализации данного метода в классе Enum нет. В официальной документации написано, что метод просто возвращает значение перечисления по его строковому представлению. Проверка строгая, поэтому никаких пробелов вначале, в конце или между буквами не должно быть.


**Есть еще один способ получить значение перечисления**
```java
System.out.println(Enum.valueOf(Color.class, "BLUE").ordinal()); //output: 2
```
но он является менее распространённым.

Рассмотрим его подробнее:
```java
public static <T extends Enum<T>> T valueOf(Class<T> enumType, String name) {
    T result = enumType.enumConstantDirectory().get(name);
    if (result != null)
        return result;
    if (name == null)
        throw new NullPointerException("Name is null");
    throw new IllegalArgumentException(
        "No enum constant " + enumType.getCanonicalName() + "." + name);
}
```
**Пояснения:**
- метод enumConstantDirectory() возвращает Map, где ключ - строковое значение перечисления, а значение - реальное значение перечисления;
- если мы нашли нужное значение в Map - возвращаем его;
- если мы передали null в метод valueOf() - обратно получим NullPointerException;
- если же значения, которое мы указали в valueOf() нет - мы получим IllegalArgumentException.

### Enum реализовывает интерфейс [Comparable](Comparable)

Зачем же Enum реализовывает интерфейс [Comparable](Comparable)? Сделано это для того, чтобы перечисления можно было сравнивать друг с другом при сортировке. При этом сравнение происходит по ordinal() перечисления. Вспомним порядок объявления значений в Color
```java
enum Color {
    RED, GREEN, BLUE
}
```
Теперь посмотрим на сравнение элементов перечисления с помощью метода compareTo()
```java
System.out.println(Color.GREEN.compareTo(Color.RED)); //output: 1
System.out.println(Color.GREEN.compareTo(Color.GREEN)); //output: 0
System.out.println(Color.GREEN.compareTo(Color.BLUE)); //output: -1
System.out.println(Color.RED.compareTo(Color.BLUE)); //output: -2
```
Результат показывает как располагаются значения перечисления относительно друг друга:
- Число 1 означает, что значение GREEN находится правее на одну позицию от значения RED
- Число 0 означает, что значение GREEN равно само себе
- Число -1 означает, что значение GREEN находится левее от значения BLUE на одну позицию
- Число -2 означает, что значение RED находится левее от значения BLUE на две позиции
А теперь посмотрим на использование в коллекции [List](List)
```java
List<ColorEnum> colors = new ArrayList<>(List.of(Color.GREEN, Color.RED, Color.BLUE));
System.out.println(colors); //output: [GREEN, RED, BLUE]

Collections.sort(colors);
System.out.println(colors); //output: [RED, GREEN, BLUE]
```
Метод Collections.sort(colors) отсортировал список colors благодаря тому, что Enum реализовывают интерфейс [Comparable](Comparable). Посмотрим на реализацию метода compareTo() в классе Enum
```java
public final int compareTo(E o) {
    Enum<?> other = (Enum<?>)o;
    Enum<E> self = this;
    if (self.getClass() != other.getClass() &&
        self.getDeclaringClass() != other.getDeclaringClass())
        throw new ClassCastException();
    return self.ordinal - other.ordinal;
}
```
**Пояснения:**
- сравнивать перечисления можно только между своими типами. Нельзя сравнивать перечисления типа Color с перечислением типа Car. Мало того, что компилятор не даст вам это сделать с помощью своих подсказок так еще и в самом методе есть проверка на тип класса перечислений.

### Enum реализовывает интерфейс [Serializable](Serializable)

Но как и в случае с clone() воспользоваться мы им не можем
```java
private void readObject(ObjectInputStream in) throws IOException,
    ClassNotFoundException {
    throw new InvalidObjectException("can't deserialize enum");
}

private void readObjectNoData() throws ObjectStreamException {
    throw new InvalidObjectException("can't deserialize enum");
}
```
**Пояснения:**
- причина того, что эти методы приватные да и к тому же бросают исключения при их вызове так же, что и в случае с clone(). Если бы эта возможность была открыта, тогда легко можно было бы сохранить перечисление в файл, затем считать его обратно и получить на выходе два экземпляра одного значения перечисления. Этот как два значения числа "1".