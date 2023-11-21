#Java #Enum #EnumClass
### Класс [Enum](EnumClass). Методы класса Enum ###

2023-11-21 16:29
#### Класс Enum. Общие сведения. Обзор методов класса Enum ####

В языке Java все перечисления, объявляемые с помощью ключевого слова enum автоматически наследуются от обобщенного класса Enum. Согласно документации, общая форма объявления класса Enum следующая:
```java
class Enum<E extends Enum<E>>
```
здесь
    E – перечислительный тип.

У класса Enum нет открытых конструкторов.

Ниже приведен сокращенный перечень методов класса Enum, доступных во всех перечислениях:
    clone() – вызов метода предотвращает клонирование перечислений;
    compareTo() – сравнивает порядковые значения двух именуемых констант одного и того же перечисления;
    getDeclaringClass() – возвращает тип перечисления, членом которого является вызывающая константа;
    hashCode() – возвращает хэш-код объекта;
    name() – возвращает имя именуемой константы;
    ordinal() – возвращает позицию константы в списке констант перечисления;
    toString() – возвращает имя именуемой константы.
#### Метод clone(). Предотвращение клонирования ####

В классе Enum метод clone() предназначен для предотвращения выполнения операции клонирования перечислений. Этот метод скрыт, поэтому вызвать его для перечисления не удастся. Объявление метода clone() в классе Enum следующее
```java
protected final Object clone() throws CloneNotSupportedException
```
При объявлении перечисления и присвоении ему значения константы каждый раз создается новый объект. Каждая присваиваемая константа является отдельным независимым объектом, поэтому не имеет смысла клонировать этот объект, поскольку он и так уже клонируется. Следующий пример объясняет эту особенность.

**Пример**.
```java
// Перечисление, определяющее общеизвестные временные интервалы
enum TimeIntervals {
	secondsInMinute(60), // количество секунд в одной минуте
	hoursInDay(24),       // количество часов в сутке
	daysPerWeek(7),       // количество дней в неделе
	daysInYear(365);     // количество дней в году

	// Конструктор
	TimeIntervals(int interval) {
	    this.interval = interval;
	}
	// Внутренняя переменная, сохраняющая значение интервала времени
	private int interval;
	// Метод доступа к значению interval
	public int get() { return interval; }
}

public class TrainEnumerations {
	public static void main(String[] args) {
	    // Метод clone() - сделать копию перечисления
	    // 1. Создать экземпляр типа перечисления TimeIntervals
	    TimeIntervals t1;
	    // 2. Инициализировать перечисление t1 значением
	    t1 = TimeIntervals.hoursInDay;
	    // 3. Создать экземпляр другого перечисления и инициализировать его значением t1
	    TimeIntervals t2 = t1;
	    // 4. Вывести значение перечисления t2
	    System.out.println(t2); // hoursInDay
	    // 5. Изменить экземпляр перечисления t1 другим значением
	    t1 = TimeIntervals.daysPerWeek;
		// 6. Повторно вывести значение перечисления t2
	    System.out.println(t2); // hoursInDay - значение не изменилось
	}
}
```
Результат выполнения программы
==hoursInDay
hoursInDay==

Как видно из результата, при присвоении перечислений
```java
// 3. Создать экземпляр другого перечисления и инициализировать его значением t1
TimeIntervals t2 = t1;
```
перечисления t1 и t2 указывают на разные участки памяти. То есть, не состоялось присваивание ссылок, как в случае с экземплярами классов. Этот факт доказывает результат вывода значения t2 после изменения значения в перечислении t1
```java
// 5. Изменить экземпляр перечисления t1 другим значением
t1 = TimeIntervals.daysPerWeek;
// 6. Повторно вывести значение перечисления t2
System.out.println(t2); // hoursInDay - значение не изменилось
```
Как видно из результата, значение перечисления t2 не изменилось, то есть клонирование выполняется автоматически. Поэтому нет смысла определять метод clone() для работы с перечислениями.

#### Метод compareTo(). Сравнить значения двух объектов перечисления ####

Метод compareTo() позволяет сравнить значения двух объектов одинакового типа перечисления. Согласно документации, метод имеет следующее объявление
```java
public final int compareTo(E obj)
```
здесь
    E – тип перечисления, имеющий текущее перечисление (объект) и перечисление (объект) obj. Текущее перечисление и перечисление obj должны быть одинакового типа E;
    obj – перечисление (объект), которое сравнивается с текущим перечислением.

Метод сравнивает текущее перечисление с определенным перечислением, которое передается как параметр метода. Метод возвращает:
    отрицательное число, если текущий объект меньше заданного объекта obj. Термин «меньше» означает, что значение текущей константы (объекта) следует перед значением константы obj в перечислении;
    ноль (0), если значения текущей константы и константы obj равны между собой;
    положительное число, если значение константы в текущем перечислении следует после значения константы в перечислении obj.

**Пример**.
```java
В примере сравниваются значения констант из перечисления Seasons.

// Перечисление, которое описывает времена года
enum Seasons {
	Winter, Spring, Summer, Autumn
}

public class TrainEnumerations {
	public static void main(String[] args) {
	    // Метод compareTo() - сравнить порядковые значения констант
	    // 1. Объявить два перечисления и присвоить им значения
	    Seasons s1, s2;
	    s1 = Seasons.Summer;
	    s2 = Seasons.Spring;
	    // 2. Реализовать сравнение перечислений s1 и s2
	    int result;
	    result = s1.compareTo(s2); // 1
	    System.out.println("Seasons.Summer == Seasons.Spring => " + result);

		s1 = Seasons.Winter;
	    s2 = Seasons.Winter;
	    result = s2.compareTo(s1); // 0
	    System.out.println("Seasons.Winter == Seasons.Winter => " + result);

	    s1 = Seasons.Spring;
	    s2 = Seasons.Autumn;
	    result = s1.compareTo(s2); // -2
	    System.out.println("Seasons.Spring == Seasons.Autumn => " + result);
	}
}
```
Результат выполнения программы
==Seasons.Summer == Seasons.Spring => 1
Seasons.Winter == Seasons.Winter => 0
Seasons.Spring == Seasons.Autumn => -2==

Как показывает результат, метод compareTo() возвращает разницу между порядковыми номерами констант текущего перечисления и перечисления, являющегося входным параметром метода.

#### Метод getDeclaringClass(). Получить информацию о перечислении ####

С помощью метода getDeclaringClass() можно получить исчерпывающую информацию о перечислении (список констант, перечень методов, конструкторов в перечислении и т.п.).

Согласно документации Java, объявление метода следующее
```java
public final Class<E> getDeclaringClass()
```
здесь
    E – тип перечисления.

Метод возвращает объект класса, соответствующий типу перечисления E.

**Пример**.

В примере показано использование метода getDeclaringClass() для определения некоторых характеристик перечислений Days и Seasons.
```java
import java.lang.reflect.Field;

// Перечисление, описывающее дни недели
enum Days {
	Sun, Mon, Tue, Wed, Thu, Fri, Sat
}

// Перечисление, которое описывает времена года
enum Seasons {
	Winter, Spring, Summer, Autumn
}

public class TrainEnumerations {
	public static void main(String[] args) {
	    // Метод getDeclaringClass() - получить задекларированный класс
	    // 1. Объявить экземпляр перечисления типа Days
	    Days day = Days.Mon;
	    // 2. Вывести имя перечисления Days
	    String nameClass = day.getDeclaringClass().getName();
	    System.out.println(nameClass);
	    // 3. Получить данные об экземпляре season1 перечисления Seasons
	    Seasons season1 = Seasons.Summer;
	    Class<Seasons> classSeason1 = season1.getDeclaringClass();
	    // 3.1. Вывести название класса
	    System.out.println(classSeason1.getName());
	    System.out.println(classSeason1.getTypeName());
	    // 3.2. Вывести названия полей из перечисления Seasons
	    System.out.println("-----------------------------------");
	    Field[] fl = classSeason1.getDeclaredFields();
	    for (int i=0; i<fl.length; i++)
			System.out.println(fl[i].getName());
	}
}
```
Результат выполнения программы
==Days
Seasons
Seasons
`-----------------------------------`
Winter
Spring
Summer
Autumn
ENUM$VALUES==
#### Метод hashCode(). Получить хэш-код объекта ####

Метод hashCode() возвращает хэш-код объекта. Метод имеет следующее объявление
```java
public final int hashCode()
```
**Пример**.
```java
// Перечисление, которое описывает дни недели
enum Days {
	Sun, Mon, Tue, Wed, Thu, Fri, Sat
}

public class TrainEnumerations {
	public static void main(String[] args) {
	    // Метод hashCode() - получить хэш-код объекта
	    Days day = Days.Sat;
	    int hCode = day.hashCode(); // 366712642
	    System.out.println(hCode);
	}
}
```
Результат выполнения программы
==366712642==

#### Метод ordinal(). Получить позицию константы в перечислении ####

С помощью метода ordinal() можно получить позицию константы в перечислении. Позиции нумеруются с нуля. Объявление метода следующее:
```java
public final int ordinal()
```
**Пример**.
```java
// Перечисление, описывающее дни недели
enum Days {
	Sun, Mon, Tue, Wed, Thu, Fri, Sat
}

public class TrainEnumerations {
	public static void main(String[] args) {
	    // Метод ordinal() - получить позицию константы
	    Days day = Days.Wed;
	    int ordNum = day.ordinal();
	    System.out.println("Wed = " + ordNum);

	    day = Days.Sat;
	    ordNum = day.ordinal();
	    System.out.println("Sat = " + ordNum);

	    day = Days.Sun;
	    ordNum = day.ordinal();
	    System.out.println("Sun = " + ordNum);
	}
}
```
Результат выполнения программы
==Wed = 3
Sat = 6
Sun = 0==
#### Метод toString(). Получить имя константы в перечислении ####

Метод toString() возвращает имя константы перечисления, которое содержится в объявлении. По желанию, метод может быть переопределен для получения имени константы в более удобной форме.

Согласно документации Java объявление метода следующее
```java
public String toString()
```
**Пример**.
```java
// Перечисление, описывающее дни недели
enum Days {
	Sun, Mon, Tue, Wed, Thu, Fri, Sat
}

public class TrainEnumerations {
	public static void main(String[] args) {
	    // Метод toString() - получить имя константы
	    // 1. Объявить экземпляр перечисления типа Days
	    Days day = Days.Mon;
	    // 2. Вывести имя константы из экземпляра day
	    String name = day.toString();
	    System.out.println(name);   // Mon
	    // 3. Вывести имя константы из типа Days
	    name = Days.Sun.toString();
	    System.out.println(name);   // Sun
	}
}
```
Результат выполнения программы
==Mon
Sun==
