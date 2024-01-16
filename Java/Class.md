
#Java #Class 
### Класс Class ###

2024-01-15 15:29

В запущенной программе Java каждому классу соответствует объект типа Class. Этот объект содержит информацию, необходимую для описания класса – поля, методы и т.д.

Экземпляры класса `Class` представляют классы и интерфейсы в работающем приложении Java. Класс перечисления и класс записи — это разновидности класса; интерфейс аннотаций — это своего рода интерфейс. Каждый массив также принадлежит классу, который отображается как объект `Class`, который используется всеми массивами с одинаковым типом элемента и количеством измерений. Примитивные типы Java ( `boolean`, `byte`, `char`, `short`, `int`, `long`, `float` и `double`) и ключевое слово `void` также представлены как объекты `Class`.

Класс Class не имеет открытого конструктора – объекты этого класса создаются автоматически Java-машиной по мере загрузки описания классов из class-файлов и предоставляется методом `getClass()` класса [Object](Object). 

#### Методы класса Class ####

- `getSuperclass()` **_-_** возвращает супер класс объекта ссылочного типа.
- `getPackage()` - возвращает пакет.
- `getModifiers()` - возвращает модификаторы класса.

Логические методы позволяющие уточнить, является ли объект массивом, интерфейсом или примитивным типом.

- `isArray()`
- `isInterface()`
- `isPrimitive()`

Если объект ссылочного типа, то можно извлечь сведения о вложенных классах, конструкторах, методах в виде массива:

- `getDeclaredClasses()`
- `getDeclaredConstructors()`
- `getDeclaredMethods()`
- `getDeclaredFields()`

Методы возвращают такие же массивы, но не всех, а только открытых членов класса.

- `getClasses()`
- `getConstructors()`
- `getMethods()`
- `getFields()`

Получить экземпляр Class для конкретного класса можно с помощью метода forName(): **`public static Class forName(String name, boolean initialize, ClassLoader loader)`** – возвращает объект Class, соответствующий классу, или интерфейсу, с названием, указанным в name необходимо указывать полное название класса или интерфейса, используя переданный загрузчик классов. Если в качестве загрузчика классов loader передано значение null, будет взят ClassLoader, который применялся для загрузки вызывающего класса. При этом класс будет инициализирован, только если значение initialize равно true и класс не был инициализирован ранее.

Зачастую проще и удобнее воспользоваться методом forName(), передав только название класса: **`public static Class forName(String className)`**, – при этом будет использоваться загрузчик вызывающего класса и класс будет инициализирован (если до этого не был).

**`public Object newInstance()`** – создает и возвращает объект класса, который представляется данным экземпляром Class. Создание будет происходить с использованием конструктора без параметров. Если такового в классе нет, будет брошено исключение InstantiationException. Это же исключение будет брошено, если объект Class соответствует абстрактному классу, интерфейсу, или какая-то другая причина помешала созданию нового объекта.

Каждому методу, полю, конструктору класса также соответствуют объекты, список которых можно получить вызовом соответствующих методов объекта Class: getMethods(), getFields(), getConstructors(), getDeclaredMethods() и т.д. В результате будут получены объекты, которые отвечают за поля, методы, конструкторы объекта. Их можно использовать для формирования динамических вызовов Java – этот механизм называется reflection. Необходимые классы содержатся в пакете java.lang.reflection.

Рассмотрим пример использования этой технологии:
```java
interface Vehicle {
   void go();
}
class Automobile implements Vehicle {
   public void go() {
      System.out.println("Automobile go!");
   }
}
class Truck implements Vehicle {
   public Truck(int i) {
      super();
   }
   public void go() {
      System.out.println("Truck go!");
   }
}
public class VehicleStarter {
   public static void main(String[] args) {
      Vehicle vehicle;
      String[] vehicleNames = {"demo.lang.Automobile", 
         "demo.lang.Truck", "demo.lang.Tank"};
      for(int i=0; i<vehicleNames.length; i++) {
         try {
            String name = vehicleNames[i];
            System.out.println("look for class for: " + name);
            Class aClass = Class.forName(name);
            System.out.println("creating vehicle...");
            vehicle = (Vehicle)aClass.newInstance();
            System.out.println("create vehicle: " + vehicle.getClass());
            vehicle.go();
         } catch(ClassNotFoundException e) {
            System.out.println("Exception: " + e);
         } catch(InstantiationException e) {
            System.out.println("Exception: " + e);
         }
      }
   }
}
```
Если запустить эту программу, на экран будет выведено следующее:
<p style="background-color: navy; color: yellow">
look for class for: demo.lang.Automobile <br>
creating vehicle...<br>
create vehicle: class demo.lang.Automobile<br>
Automobile go!<br>
look for class for: demo.lang.Truck<br>
creating vehicle...<br>
Exception: java.lang.InstantiationException<br>
look for class for: demo.lang.Tank<br>
Class not found: java.lang.ClassNotFoundException: demo.lang.Tank</p>
В этом примере делается попытка создать с помощью reflection три объекта. Имена классов, от которых они должны быть порождены, записаны в массив vehicleNames. Объект класса Automobile был успешно создан, причем, дальнейшая работа с ним велась через интерфейс Vehicle. Класс Truck был найден, но при попытке создания объекта было брошено, а затем обработано исключение java.lang.InstantiationException, поскольку конструктор без параметров отсутствует. Класс java.lang.Tank определен не был и поэтому при попытке получить соответствующий ему объект Class было выброшено исключение java.lang.ClassNotFoundException.

##### Примеры1. Использования класса Class: #####
```java
public class ClassDemo1 {
    public static void main(String[] args) {
        getClassName1();
        getClassName2();
        getClassName3();
    }

    private static void getClassName1() {
        String s = "Это строка";
        Class aClass = s.getClass();
        System.out.println(aClass);
    }

    private static void getClassName2() {
        try {
            Class aClass = Class.forName("java.lang.String");
            System.out.println(aClass);
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        }
    }

    private static void getClassName3() {
        Class aClass = String.class;
        System.out.println(aClass);
    }
}
```
Вывод:
<p style="background-color: navy; color: yellow">
class java.lang.String<br>
class java.lang.String<br>
class java.lang.String</p>

##### Пример 2. Использования класса Class: #####

```java
import java.io.Serializable;

public class ClassDemo2 {
       public static void main(String[] args) {
        int[] array = new int[4];

        printInfo(array.getClass());
        printInfo(Serializable.class);
        printInfo(Integer.class);
        printInfo(double.class);
    }

    private static void printInfo(Class arrayClass) {
        System.out.println("Class name " + arrayClass.getName());
        System.out.println("Is Array? " + arrayClass.isArray());
        System.out.println("Is Interface? " + arrayClass.isInterface());
        System.out.println("Is Primitive? " + arrayClass.isPrimitive());
        System.out.println();
    }
}
```
Вывод:
<p style="background-color: navy; color: yellow">
Class name [I<br>
Is Array? true<br>
Is Interface? false<br>
Is Primitive? false<br>
<br>
Class name java.io.Serializable<br>
Is Array? false<br>
Is Interface? true<br>
Is Primitive? false<br>
<br>
Class name java.lang.Integer<br>
Is Array? false<br>
Is Interface? false<br>
Is Primitive? false<br>
<br>
Class name double<br>
Is Array? false<br>
Is Interface? false<br>
Is Primitive? true</p>

##### Пример 3. Использования класса Class: #####

```java
import java.util.Arrays;

public class ClassDemo3 {
    public static void main(String[] args) {
        Class heavyBoxClass = Number.class;

        System.out.println("Declared Constructors: "
                + Arrays.toString(heavyBoxClass.getDeclaredConstructors()));
        System.out.println("Constructors: "
                + Arrays.toString(heavyBoxClass.getConstructors()));

        System.out.println("Declared Methods: "
                + Arrays.toString(heavyBoxClass.getDeclaredMethods()));
        System.out.println("Methods: "
                + Arrays.toString(heavyBoxClass.getMethods()));

        System.out.println("Declared Fields: "
                + Arrays.toString(heavyBoxClass.getDeclaredFields()));
        System.out.println("Fields: "
                + Arrays.toString(heavyBoxClass.getFields()));
    }
}
```
Вывод:
<p style="background-color: navy; color: yellow">
Declared Constructors: [public java.lang.Number()]<br>
Constructors: [public java.lang.Number()]<br>
Declared Methods: [public byte java.lang.Number.byteValue(), public short java.lang.Number.shortValue(), public abstract int java.lang.Number.intValue(), public abstract long java.lang.Number.longValue(), public abstract float java.lang.Number.floatValue(), public abstract double java.lang.Number.doubleValue()]<br>
Methods: [public byte java.lang.Number.byteValue(), public short java.lang.Number.shortValue(), public abstract int java.lang.Number.intValue(), public abstract long java.lang.Number.longValue(), public abstract float java.lang.Number.floatValue(), public abstract double java.lang.Number.doubleValue(), public boolean java.lang.Object.equals(java.lang.Object), public java.lang.String java.lang.Object.toString(), public native int java.lang.Object.hashCode(), public final native java.lang.Class java.lang.Object.getClass(), public final native void java.lang.Object.notify(), public final native void java.lang.Object.notifyAll(), public final void java.lang.Object.wait(long) throws java.lang.InterruptedException, public final void java.lang.Object.wait(long,int) throws java.lang.InterruptedException, public final void java.lang.Object.wait() throws java.lang.InterruptedException]<br>
Declared Fields: [private static final long java.lang.Number.serialVersionUID]<br>
Fields: []</p>

