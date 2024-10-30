#Java #Object 
#### Класс Object  ####

2024-01-15 11:45

#### [Object: глобальный суперкласс](http://wiki.asistech.org/index.php/Object:_%D0%B3%D0%BB%D0%BE%D0%B1%D0%B0%D0%BB%D1%8C%D0%BD%D1%8B%D0%B9_%D1%81%D1%83%D0%BF%D0%B5%D1%80%D0%BA%D0%BB%D0%B0%D1%81%D1%81) ####

Класс Object является предком для всех классов Java:
```java
class Employee extends Object  // явно отражать факт наследования от Object не обязательно
```
Если суперкласс явно не указан, то им считается класс Object. Поскольку в Java _каждый_ класс расширяет Object, очень важно знать, какими возможностями обладает сам класс Object.

Переменную типа Object можно использовать в качестве ссылки на объект любого типа:
```java
Object obj = new Employee("Harry Hacker", 35000);
```
Разумеется, переменная этого класса полезна лишь как средство для хранения значений произвольного типа. Чтобы сделать с этим значением что-то конкретное, нужно знать его исходный тип, а затем выполнить приведение типов:
```java
Employee e = (Employee) obj;
```
В Java объектами не являются лишь _простые типы_: числа, символы и логические значения.
Все массивы, независимо от того, содержатся ли в его элементах объекты или простые типы, являются объектами, расширяющими класс Object.
```java
Employee[] staff = new Employee[10];
obj = staff;  // OK
obj = new int[10];  // OK
```
>В C++ аналогичного глобального базового класса нет, хотя любой указатель можно преобразовать в указатель типа void*.

#### Методы класса Object ####

У класса есть несколько важных методов:
- Object clone() - создаёт новый объект, не отличающий от клонируемого;
- boolean equals(Object obj) - определяет, равен ли один объект другому;
- void finalize() - вызывается перед удалением неиспользуемого объекта;
- **`Class<?> getClass()`** - получает класс объекта во время выполнения;
- int hashCode() - возвращает хеш-код, связанный с вызывающим объектом;
- void notify() - возобновляет выполнение потока, который ожидает вызывающего объекта;
- void notifyAll() - возобновляет выполнение всех потоков, которые ожидают вызывающего объекта;
- String toString() - возвращает строку, описывающий объект;
- void wait() - ожидает другого потока выполнения;
- void wait(long millis) - ожидает другого потока выполнения;
- void wait(long millis, int nanos) - ожидает другого потока выполнения.

Методы **getClass()**, **notify()**, **notifyAll()**, **wait()** являются финальными и их нельзя переопределять.

#### Метод equals() ####

Метод equals() класса Object проверяет, эквивалентны ли два объекта. Поскольку метод equals() реализован в классе Object, он определяет лишь, ссылаются ли переменные на один и тот же объект. В качестве проверки по умолчанию эти действия вполне оправданы: всякий объект эквивалентен самому себе. Для некоторых классов большего и не требуется. Например, вряд ли кому-то потребуется анализировать два объекта PrintStream и выяснять, отличаются ли они друг от друга. Однако в ряде случаев эквивалентными должны считаться объекты одного типа, имеющие одинаковые состояния.

Рассмотрим в качестве примера объекты, описывающие сотрудников. Очевидно, что они одинаковы, если совпадают имена, размеры заработной платы и даты приема на работу. Строго говоря, в реальных системах учета информации о сотрудниках более оправдано сравнение идентификационных номеров. Здесь же мы лишь демонстрируем принцип реализации метода equals().
```java
class Employee {
    ...
    public boolean equals(Object otherObject) { 
        // Быстрая проверка идентичности объектов
        if (this == otherObject) {
            return true;
        }
        // Если явный параметр - null, возвращается значение false
        if (otherObject == null) {
            return false;
        }
        // Если классы не совпадают, они не эквивалентны
        if (getClass() != otherObject.getClass()) {
            return false;
        }
        // Теперь мы знаем, что объект otherObject
        // имеет тип Employee и не является нулевым
        Employee other = (Employee) otherObject;
        // Проверим, хранятся ли в полях объектов идентичные значения
        return name.equals(other.name)
                && salary = other.salary
                && hireDay.equals(other.hireDay);
    }
}
```
Метод getClass() определяет тип объекта. Чтобы объекты были эквивалентны, они как минимум должны быть объектами одного и того же класса.

Определяя метод equals() для подкласса, надо сначала вызывать тот же метод суперкласса. Если проверка даст отрицательный результат, объекты не могут быть идентичными. Если же поля суперкласса совпадают, можно приступать к сравнению полей подкласса:
```java
class Manager extends Employee {    
    ...
    public boolean equals(Object otherObject) {
        if (!super.equals(otherObject)) {
            return false;
        }
        // При выполнении super.equals() проверяется,
        // принадлежит ли otherObject тому же классу
        Manager other = (Manager) otherObject;
        return bonus == other.bonus;
    }
}
```

#### Проверка эквивалентности объектов и наследование ####

Как должен работать метод equals(), если неявные и явные параметры не принадлежат одному и тому же классу? Рекомендуется составлять код так, чтобы метод equals() возвращал значение false, если классы не совпадают. Однако многие программисты используют следующую проверку:
```java
if (!(otherObject instanceof Employee)) {
    return false;
}
```
При этом остается возможность, что otherObject принадлежит подклассу. Данный подход может привести к возникновению проблем. Спецификация Java требует, чтобы метод equals() обладал следующими характеристиками:
- _Рефлексивность_. Для любой ненулевой ссылки x вызов x.equals(x) должен возвращать true.
- _Симметричность_. Для любых ссылок x и y вызов x.equals(y) должен возвращать true только тогда, когда y.equals(x) возвращает true.
- _Транзитивность_. Для любых ссылок x, y и z, если вызовы x.equals(y) и y.equals(z) возвращают true, то вызов x.equals(z) возвращает true.
- _Непротиворечивость_. Если объекты, на которые ссылались переменные x и y не изменяются, то повторный вызов x.equals(y) должен возвращать то же значение.
- Для любой ненулевой ссылки x вызов x.equals(null) должен возвращать false.
Например, очевидно, что результаты проверки должны зависеть от того, вызывается ли в программе x.equals(y) или y.equals(x).

Однако требование симметрии имеет свои особенности в случае, если явный и неявный параметры принадлежать разным классам. Рассмотрим следующий вызов:
```java
e.equals(m)
```
Объект e принадлежит классу Employee, а объект m - классу Manager, причем каждый из них содержит одинаковые имена, зарплату и дату приема на работу. Если не выполнить проверку эквивалентности классов, которым принадлежат объекты m и e, метод вернет true. Однако это значит, что и обратный вызов, m.equals(e), также должен возвращать true, - правило 2 не позволяет ему возвращать false или генерировать исключение.

В результате оказывается, что класс Manager неоправданно тесно связан с другими классами. Если метод equals() используется для сравнения с объектом Employee, он не должен принимать во внимание информацию, отличающую менеджера от обычного сотрудника. В данной ситуации оператор [instanceof](Instanceof) выглядит достаточно привлекательно.

Некоторые специалисты считают, что проверка с использованием метода getClass() некорректна, поскольку при этом нарушается принцип подстановки. В пользу данного мнения приводят метод equals() класса AbstractSet, который проверяет, содержат ли два множества одинаковые элементы и расположены ли они в одинаковом порядке. Класс AbstractSet выступает в роли суперкласса для классов TreeSet и HashSet, которые не являются абстрактными. Эти классы используют различные алгоритмы для работы с элементами множества. На практике разработчику необходимо иметь возможность сравнивать любые два множества, независимо от того, как они реализованы.

Следует признать, что данный пример слишком специфичен. В данном случае имело бы смысл объявить метод AbstractSet.equals() как терминальный, чтобы невозможно было изменить семантику проверки на эквивалентность множеств. На самом деле при объявлении метода ключевое слово final не указано. Разработчики класса оставили возможность для реализации более эффективного алгоритма проверки на эквивалентность.

Таким образом, вырисовываются два сценария:
- Если проверка эквивалентности реализована в подклассе, правило симметричности требует использования метода getClass().
- Если проверка производится средствами суперкласса, можно применять оператор [instanceof](Instanceof); при этом становится возможной ситуация, когда два объекта разных классов будут признаны эквивалентными.

В примере с сотрудниками и менеджерами мы считаем два объекта эквивалентными, если их поля совпадают. Если в нашем распоряжении есть два объекта Manager с одинаковыми именами, заработной платой и датой приема на работу, но с различными суммами премии, мы должны признать объекты разными. Следовательно, мы должны использовать проверку с помощью метода getClass().

Теперь предположим, что для проверки эквивалентности используется идентификационный номер сотрудника. Такая проверка имеет смысл для всех подклассов. В этом случае мы можем применять оператор [instanceof](Instanceof) и объявить метод Employee.equals() как final.

Ниже приведены рекомендации для создания метода equals():
1. Предположим, что явный параметр называется otherObject, — впоследствии его тип нужно будет привести к типу другой переменной, которую назовем other.
2. Проверить, идентичны ли ссылки this и otherObject:
``` java
    if (this == otherObject) {
        return true;
    }
```
Это выражение используется для оптимизации проверки. Гораздо быстрее проверить идентичность ссылок, чем сравнивать поля объектов.    
3. Выяснить, является ли ссылка otherObject нулевой (null). Если да, вернуть значение false (делать обязательно!)
```java
    if (otherObject == null) {
        return false;
    }
```
Сравнить классы this и otherObject. Если семантика проверки может измениться в подклассе, использовать метод getClass():
```   java
    if (getClass() != otherObject.getClass()) {
        return false;
    }
```
Если принцип проверки остается справедливым для всех подклассов, использовать оператор [instanceof](Instanceof):
```   java
    if (!(otherObject instanceof ClassName)) {
        return false;
    }
```
Преобразовать объект otherObject в переменную требуемого класса:
```java
    Имя_класса other = (Имя_класса) otherObject;
```
Теперь нужно сравнить между собой все поля. Для полей простых типов используется оператор `==`, для объектных полей - метод equals(). Если все поля двух объектов совпадают друг с другом, возвращается значение true, в противном случае - значение false:
```java
    return поле_1 == other.поле_1
        && поле_2.equals(other.поле_2)
        && ... ;
```
Если в подклассе вы переопределяете метод equals(), в него надо включить вызов super.equals(other).

Стандартная библиотека Java содержит более 150 реализаций метода equals(). Некоторые из них включают множество операторов instanceof, вызовов метода getClass() и фрагментов кода, предназначенных для обработки исключения ClassCastException, другие не выполняют практически никаких действий. Создается впечатление, что многие программисты не представляют себе всех особенностей метода equals(). Например, класс Rectangle представляет собой подкласс Rectangle2D. В обоих классах реализован метод equals(), причем для проверки используется оператор instanceof. Сравнивая Rectangle2D с Rectangle при условии равенства координат, мы получим значение true, если же поменяем параметры местами, проверка даст значение false.

Реализуя метод equals(), многие программисты допускают стандартную ошибку. Сможете ли вы сказать, какая проблема возникает при выполнении следующего фрагмента кода: 
```java
public class Employee {
    public boolean equals(Employee other) {
        return name.equals(other.name)
                && salary == other.salary
                && hireDay.equals(other.hireDay);
    }
    ...
}
```
При определении метода явный параметр объявлен как Employee. В результате он не переопределяет метод equals() класса Object.

Начиная с JDK 5.0, появилась возможность застраховаться от возникновения подобной ошибки, специальным образом указывая, что разрабатываемый метод призван заместить соответствующий метод суперкласса. Для этой цели используется дескриптор @Override.
```java
@Override
public boolean equals(Object other)
```
Если при этом вы случайно определите новый метод, компилятор вернет сообщение об ошибке. Предположим, что в классе Employee присутствует приведенная ниже строка кода.
```java
@Override
public boolean equals(Employee other)
```
Поскольку данный метод не переопределяет метод, определенный в суперклассе Object, будет обнаружена ошибка.

Дескриптор @Override относится к языковым конструкциям, применяемым для работы с метаданными. Механизм метаданных достаточно универсальный и допускает расширение. С помощью метаданных компилятор получает возможность отслеживать различные действия.

#### Метод hashCode() ####

Хэш-код - это целое число, генерируемое на основе конкретного объекта. Хэш-код можно рассматривать как некоторый шифр: если x и y - разные объекты, то с высокой степенью вероятности должны различаться результаты вызовов x.hashCode() и y.hashCode(). Ниже приведено несколько примеров хэш-кодов, полученных в результате вызова метода hashCode() класса String.

|Строка|Хэш-код|
|---|---|
|Hello|140207504|
|Harry|140013338|
|Hacker|884756206|

Для вычисления хеш-кода в классе **String** применяется следующий алгоритм.
```java
int hash = 0;
for(int i = 0; i < length(); i++)
	hash = 31 * hash + charAt(i);
```
Метод hashCode() определен в классе Object. Поэтому каждый объект имеет хэш-код, определяемый по умолчанию. В классе Object хэш-код вычисляется на основе адреса памяти, занимаемой объектом. Рассмотрим следующий пример:
```java
String s = "Ok";

StringBuffer sb = new StringBuffer(s);
System.out.println(s.hashCode() + " " + sb.hashCode());

String t = new String("Ok");

StringBuffer tb = new StringBuffer(t);
System.out.println(t.hashCode() + " " + tb.hashCode());
```
Результаты выполнения данного фрагмента кода приведены в таблице:

| Объект | Хэш-код |
| ---- | ---- |
| s | 3030 |
| sb | 20526976 |
| t | 3030 |
| tb | 20527144 |
Строкам s и t соответствуют одинаковые хэш-коды, так как они вычисляются на основе _содержимого_ объекта. Для буферов sb и tb хэш-коды различаются. Причина в том, что в классе StringBuffer метод hashCode() не определен и используется метод hashCode() класса Object, который определяет хэш-код по адресу занимаемой памяти.

Если вы переопределяете метод equals(), вам также следует переопределить и метод hashCode(). Он может быть использован при включении объектов в хэш-таблицу.

Метод hashCode() возвращает целое число (которое может быть отрицательным). Для того чтобы обеспечить различие хэш-кодов для разных объектов, достаточно объединить хэш-коды полей экземпляра.

Ниже приведен пример метода hashCode() для класса Employee:
```java
class Employee {
    public int hashCode() {
        return 7 * name.hashCode()
            + 11 * new Double(salary).hashCode()
            + 13 * hireDay.hashCode();
    }
    ...
}
```
Методы equals() и hashCode() должны быть совместимы: если x.equals(y) возвращает значение true, то результаты выполнения x.hashCode() и y.hashCode() также должны совпадать. Например, если в методе Employee.equals() для определения эквивалентности применяется табельный номер сотрудника, то при вычислении хэш-кода также должен использоваться этот номер, а не имя и не адрес памяти, занимаемый объектом.

[Контракты equals и hashCode](equals_hashCode)

#### Метод toString() ####

Еще одним важным методом класса Object является toString(), возвращающий значение объекта в виде строки. В качестве примера можно привести метод toString() класса Point. Он возвращает строку, подобную приведенной ниже:
<p style="background-color: navy; color: yellow">
java.awt.Point[x=10,y=20]</p>
Большинство (но не все) методы toString() возвращают строку, которая состоит из имени класса, за которым указываются значения его полей в квадратных скобках. Ниже приведена реализация метода toString() для класса Employee.
```java
public String toString() {
    return "Employee[name=" + name
        + ",salary=" + salary
        + ",hireDay=" + hireDay
        + "]";
}
```
Этот метод можно усовершенствовать. Не будем встраивать имя класса в метод toString(), а лишь вызовем метод getClass().getName() и получим строку, содержащую имя класса.
```java
public String toString() {
    return getClass().getName()
        + "[name=" + name
        + ",salary=" + salary
        + ",hireDay=" + hireDay
        + "]";
}
```
Теперь метод toString работает и с подклассами.

Разумеется, программист, создающий подкласс, должен определить свой собственный метод toString() и добавить поля подкласса. Если в суперклассе используется вызов getClass().getName(), подкласс просто вызывает метод super.toString(). Ниже приведен пример метода toString() для класса Manager.
```java
class Manager extends Employee {
    ...
    public String toString() {
        return super.toString()
            + "[bonus=" + bonus
            + "]";
    }
}
```
Теперь состояние объекта Manager выводится следующим образом:
<p style="background-color: navy; color: yellow">
Manager[name...,salary=...,hireDay=...][bonus=...]</p>
Метод toString() универсален. Есть важная причина для реализации его в каждом классе: если объект объединяется со строкой с помощью оператора "+", компилятор Java автоматически вызывает метод toString(), чтобы получить представление о его текущем состоянии.
```java
Point p = new Point(10, 20);
String message = "The current position is = " + p;  // автоматически вызывает метод p.String()
```
Вместо x.toString() можно использовать выражение " " + x. Конкатенация пустой строки с представлением объекта x в виде строки эквивалентна вызову метода x.toString(). Такое выражение будет корректным, даже если переменная принадлежит к одному из простых типов.

Предположим, что x - произвольный объект и в программе имеется следующая строка:
```java
System.out.println(x);
```
В этом случае метод println() вызовет метод x.toString() и выведет строку результата.

Метод toString(), определенный в классе Object, выводит имя класса и адрес объекта. Рассмотрим следующий вызов:
```java
System.out.println(System.out);
```
После выполнения метода println() отображается следующая строка:
<p style="background-color: navy; color: yellow">
java.io.PrintStream@2f6684</p>
Как видите, разработчики класса PrintStream не позаботились о переопределении метода toString().

Данный метод - отличное средство протоколирования. С его помощью можно получать полезную информацию о состоянии объекта. Так, например, для протоколирования можно применить следующее выражение:
```java
System.out.println("Current position = " + position);
```
Мы настоятельно рекомендуем переопределять метод toString() в каждом создаваемом вами классе. Это будет полезно как вам, так и программистам, использующим результаты вашей работы.

Следующий листинг содержит код методов equals() и toString(), реализованных для классов Employee и Manager:
```java
import java.util.*;

public class EqualsTest {
    public static void main(String[] args) {
        Employee alice1 = new Employee("Alice Adams", 75000, 1987, 12, 15);
        Employee alice2 = alice1;
        Employee alice3 = new Employee("Alice Adams", 75000, 1987, 12, 15);
        Employee bob = new Employee("Bob Brandson", 50000, 1989, 10, 1);

        System.out.println("alice1 == alice2: " + (alice1 == alice2));
        System.out.println("alice1 == alice3: " + (alice1 == alice3));
        System.out.println("alice1.equals(alice3): " + alice1.equals(alice3));
        System.out.println("alice1.equals(bob): " + alice1.equals(bob));
        System.out.println("bob.toString(): " + bob);

        Manager carl = new Manager("Carl Cracker", 80000, 1987, 12, 15);
        Manager boss = new Manager("Carl Cracker", 80000, 1987, 12, 15);
        boss.setBonus(5000);
        System.out.println("boss.toString(): " + boss);
        System.out.println("carl.equals(boss): " + carl.equals(boss));
        System.out.println("alice1.hashCode(): " + alice1.hashCode());
        System.out.println("alice3.hashCode(): " + alice3.hashCode());
        System.out.println("bob.hashCode(): " + bob.hashCode());
        System.out.println("carl.hashCode(): " + carl.hashCode());
    }
}

class Employee {
    public Employee(String n, double s, int year, int month, int day) {
        name = n;
        salary = s;
        GregorianCalendar calendar = new GregorianCalendar(year, month - 1, day);
        hireDay = calendar.getTime();
    }

    public String getName() {
        return name;
    }

    public double getSalary() {
        return salary;
    }

    public Date getHireDay() {
        return hireDay;
    }

    public void raiseSalary(double byPercent) {
        double raise = salary * byPercent / 100;
        salary += raise;
    }

    public boolean equals(Object otherObject) {
        // a quick test to see if the objects are identical
        if (this == otherObject) {
            return true;
        }

        // must return false if the explicit parameter is null
        if (otherObject == null) {
            return false;
        }

        // if the classes don't match, they can't be equal
        if (getClass() != otherObject.getClass()) {
            return false;
        }

        // now we know otherObject is a non-null Employee
        Employee other = (Employee) otherObject;

        // test whether the fields have identical values
        return name.equals(other.name)
                && salary == other.salary
                && hireDay.equals(other.hireDay);
    }

    public int hashCode() {
        return 7 * name.hashCode()
                + 11 * new Double(salary).hashCode()
                + 13 * hireDay.hashCode();
    }

    public String toString() {
        return getClass().getName()
                + "[name=" + name
                + ",salary=" + salary
                + ",hireDay=" + hireDay
                + "]";
    }

    private String name;
    private double salary;
    private Date hireDay;
}

class Manager extends Employee {
    public Manager(String n, double s, int year, int month, int day) {
        super(n, s, year, month, day);
        bonus = 0;
    }

    public double getSalary() {
        double baseSalary = super.getSalary();
        return baseSalary + bonus;
    }

    public void setBonus(double b) {
        bonus = b;
    }

    public boolean equals(Object otherObject) {
        if (!super.equals(otherObject)) {
            return false;
        }
        Manager other = (Manager) otherObject;
        // super.equals checked
        // that this and other belong to the same class
        return bonus == other.bonus;
    }

    public int hashCode() {
        return super.hashCode() + 17 * new Double(bonus).hashCode();
    }

    public String toString() {
        return super.toString() + "[bonus=" + bonus + "]";
    }

    private double bonus;
}
```
Вывод:
<p style="background-color: navy; color: yellow">
alice1 == alice2: true<br>
alice1 == alice3: false<br>
alice1.equals(alice3): true<br>
alice1.equals(bob): false<br>
bob.toString(): Employee[name=Bob Brandson,salary=50000.0,hireDay=Sun Oct 01 00:00:00 MSK 1989]<br>
boss.toString(): Manager[name=Carl Cracker,salary=80000.0,hireDay=Tue Dec 15 00:00:00 MSK 1987][bonus=5000.0]<br>
carl.equals(boss): false<br>
alice1.hashCode(): 611776739<br>
alice3.hashCode(): 611776739<br>
bob.hashCode(): 1189281687<br>
carl.hashCode(): 620510272</p>

**Пример:**
```java
package demo.lang;
public class Rectangle {
   public int sideA;
   public int sideB;
   public Rectangle(int x, int y) {
      super();
      sideA = x;
      sideB = y;
   }
   public boolean equals(Object obj) {
      if(!(obj instanceof Rectangle)) 
	     return false;
      Rectangle ref = (Rectangle)obj;
      return (((this.sideA==ref.sideA)&&(this.sideB==ref.sideB))||
              (this.sideA==ref.sideB)&&(this.sideB==ref.sideA));
   }
   public static void main(String[] args) {
      Rectangle r1 = new Rectangle(10,20);
      Rectangle r2 = new Rectangle(10,10);
      Rectangle r3 = new Rectangle(20,10);
      System.out.println("r1.equals(r1) == " + r1.equals(r1));
      System.out.println("r1.equals(r2) == " + r1.equals(r2));
      System.out.println("r1.equals(r3) == " + r1.equals(r3));
      System.out.println("r2.equals(r3) == " + r2.equals(r3));
      System.out.println("r1.equals(null) == " + r1.equals(null));
   }
}
```
Запуск этой программы, очевидно, приведет к выводу на экран следующего:
<p style="background-color: navy; color: yellow">
r1.equals(r1) == true<br>
r1.equals(r2) == false<br>
r1.equals(r3) == true<br>
r2.equals(r3) == false<br>
r1.equals(null) == false</p>
В этом примере метод equals() у класса Rectangle был переопределен таким образом, чтобы прямоугольники были равны, если их можно наложить друг на друга (геометрическое равенство).