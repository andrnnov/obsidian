#Java #System

## Работа с классом Java System (java.lang.System)

2024-06-19 14:41

Класс `Java System` является одним из базовых классов в Java и принадлежит пакету java.lang. Класс System является финальным и не предоставляет общедоступных конструкторов. Из-за этого все члены и методы, содержащиеся в этом классе, являются статическими по природе.

Таким образом, вы не можете наследовать этот класс для переопределения его методов. Поскольку класс System  имеет множество ограничений, существуют различные предварительно созданные поля и методы класса. Ниже я перечислил несколько важных функций, поддерживаемых этим классом:
- Стандартный ввод и вывод.
- Ошибка вывода потоков.
- Доступ к внешним свойствам и переменным среды.
- Встроенная утилита для копирования части массива.
- Предоставляет средства для загрузки файлов и библиотек.

### Объявление

```java
public final class System extends Object
```

### Поля класса

Класс java.lang.System поставляется с тремя полями:
- **public static final InputStream in**: Это стандартный поток ввода в Java-программировании. Этот поток уже открыт и доступен для ввода входных данных. Этот поток ввода в основном соответствует вводу с клавиатуры или другим источникам ввода, которые указываются хост-средой или пользователем.
- **public static final PrintStream out**: Это стандартный поток вывода в Java-программировании. Этот поток уже открыт и доступен для принятия выходных данных. Этот выходной поток в основном соответствует отображению выходного или другого выходного пункта назначения, который указан хост-средой или пользователем.
- **public static final PrintStream err**: Это стандартный поток вывода ошибок в Java-программировании. Этот поток уже открыт и доступен для принятия выходных данных. Этот выходной поток в основном соответствует отображению выходного или другого выходного пункта назначения, который указан хост-средой или пользователем. Технически этот выходной поток используется для отображения сообщений об ошибках или другой информации, которая требует немедленного внимания пользователя.

### Методы класса System

| Метод                                                                               | Описание                                                                                                                                                                                                                                            |
| ----------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| static void arraycopy(Object src, int srcPos, Object dest, int destPos, int length) | Копирует массив из указанного исходного массива, начиная с указанной позиции, в указанную позицию целевого массива.                                                                                                                                 |
| static String clearProperty(String key)                                             | Удаляет системное свойство, указанное указанным ключом.                                                                                                                                                                                             |
| static Console	console()                                                            | Возвращает уникальный Console объект, связанный с текущей виртуальной машиной Java, если таковой имеется.                                                                                                                                           |
| static long	currentTimeMillis()                                                     | Возвращает текущее время в миллисекундах.                                                                                                                                                                                                           |
| static void	exit(int status)                                                        | Завершает работу текущей виртуальной машины Java.                                                                                                                                                                                                   |
| static void	gc()                                                                    | Запускает сборщик мусора.                                                                                                                                                                                                                           |
| static Map<String,String>	getenv()                                                  | Возвращает неизменяемое представление строковой карты текущей системной среды.                                                                                                                                                                      |
| static String	getenv(String name)                                                   | Получает значение указанной переменной окружения.                                                                                                                                                                                                   |
| static Properties	getProperties()                                                   | Определяет текущие свойства системы.                                                                                                                                                                                                                |
| static String	getProperty(String key)                                               | Получает системное свойство, указанное указанным ключом.                                                                                                                                                                                            |
| static String	getProperty(String key, String def)                                   | Получает системное свойство, указанное указанным ключом.                                                                                                                                                                                            |
| static SecurityManager	getSecurityManager()                                         | Получает интерфейс безопасности системы.                                                                                                                                                                                                            |
| static int	identityHashCode(Object x)                                               | Возвращает тот же хэш-код для данного объекта, который был бы возвращен методом по умолчанию hashCode(), независимо от того, переопределяет ли класс данного объекта hashCode().                                                                    |
| static Channel	inheritedChannel()                                                   | Возвращает канал, унаследованный от объекта, создавшего эту виртуальную машину Java.                                                                                                                                                                |
| static String	lineSeparator()                                                       | Возвращает строку разделителя строк, зависящую от системы.                                                                                                                                                                                          |
| static void	load(String filename)                                                   | Загружает встроенную библиотеку, указанную в аргументе filename.                                                                                                                                                                                    |
| static void	loadLibrary(String libname)                                             | Загружает встроенную библиотеку, указанную в аргументе libname.                                                                                                                                                                                     |
| static String	mapLibraryName(String libname)                                        | Преобразует имя библиотеки в строку для конкретной платформы, представляющую собственную библиотеку.                                                                                                                                                |
| static long	nanoTime()                                                              | Возвращает текущее значение источника времени с высоким разрешением для запущенной виртуальной машины Java в наносекундах.                                                                                                                          |
| static void	runFinalization()                                                       | Запускает методы завершения любых объектов, ожидающих завершения.                                                                                                                                                                                   |
| static void	runFinalizersOnExit(boolean value)                                      | Устарело. Этот метод по своей сути небезопасен. Это может привести к вызову финализаторов для живых объектов, в то время как другие потоки одновременно манипулируют этими объектами, что приводит к неустойчивому поведению или взаимоблокировке.  |
| static void	setErr(PrintStream err)                                                 | Переназначает "стандартный" поток вывода ошибок.                                                                                                                                                                                                    |
| static void	setIn(InputStream in)                                                   | Переназначает "стандартный" поток ввода.                                                                                                                                                                                                            |
| static void	setOut(PrintStream out)                                                 | Переназначает "стандартный" выходной поток.                                                                                                                                                                                                         |
| static void	setProperties(Properties props)                                         | Присваивает системным свойствам значение Properties аргумент.                                                                                                                                                                                       |
| static String	setProperty(String key, String value)                                 | Устанавливает системное свойство, указанное указанным ключом.                                                                                                                                                                                       |
| static void	setSecurityManager(SecurityManager s)                                   | <br>Устарел, подлежит удалению: Этот элемент API подлежит удалению в будущей версии.<br>Этот метод полезен только в сочетании с менеджером безопасности, который устарел и подлежит удалению в будущем выпуске. Устанавливает безопасность системы. |

### Пример использования метода ArrayCopy() класса Java System

Класс System обеспечивает нативный метод для копирования данных из одного массива в другой. Это встроенный метод, поэтому должен работать быстрее, чем другие способы копирования массива.

**static void arraycopy(Object src, int srcPos, Object dest, int destPos, int length)** - 
копирует массив из указанного исходного массива, начиная с указанной позиции, в указанную позицию целевого массива.

Метод System.arraycopy() бросает [исключение](Exceptions) _IndexOutOfBoundsException_ если копирование обратится к данным за пределами границ массива.

Также он бросает _ArrayStoreException_ если элемент в исходном массиве не может быть сохранен в массиве назначения из-за несоответствия типа.

Еще может быть выброшен _NullPointerException_, если массив источник или массив назначения null.

Пример программы с примером использования этого метода:
```java
// Java code illustrating arraycopy() method
import java.lang.*;
import java.util.Arrays;
class SystemDemo {
    public static void main(String args[]) {
        int[] a = {1, 2, 3, 4, 5};
        int[] b = {6, 7, 8, 9, 10};
         
        System.arraycopy(a, 0, b, 2, 2);
        // array b after arraycopy operation
        System.out.println(Arrays.toString(b));
    }
}
```
**Вывод:**
<p style="background-color: navy; color: yellow">
[6, 7, 1, 2, 10]</p>

### Пример использования System Properties

Класс System содержит очень полезный метод для получения System properties и дальнейшей работы с ними. По этой [ссылке](Properties) приведен пример использования различных методов System properties.

### Читаем с консоли/пишем в консоль с помощью класса Java System

Класс System предоставляет удобный способ получить уникальный объект Console, связанный с управлением JVM. Класс Console был введен в Java IO версии Java SE 1.6 c полезным методом для печати отформатированных данных и безопасного считывания пароля. Если у вас консоль не связан с текущей JVM или работает в качестве фоновой программы, то на попытку получить объект Console возвращается значение null.

**public static Console console()** - возвращает уникальный объект консоли, связанный с текущей виртуальной машиной Java, если таковая имеется.

```java
// Java code illustrating console() method
import java.io.Console;
import java.lang.*;
import java.util.Currency;
import java.util.Locale;

class SystemDemo {
    public static void main(String args[]) throws NullPointerException {
        Console c = System.console();
        if(c != null) {
	        Currency currency = Currency.getInstance(Locale.ITALY);
	        c.printf(currency.getSymbol());
	        c.flush();
        }
        else
            System.out.println("No console attached");
    }
}
```
**Вывод:**
<p style="background-color: navy; color: yellow">
No console attached</p>

### Получаем текущее время с помощью класса System

Класс System предоставляет два метода получения текущего времени в миллисекундах и наносекундах. Мы можем использовать время в миллисекундах, чтобы создать объект [Date](Date). Время в наносекундах используется в основном в научных экспериментах или тестировании производительности программ.

**static long currentTimeMillis()** - возвращает текущее время в миллисекундах. Обратите внимание: хотя единицей времени возвращаемого значения является миллисекунда, степень детализации значения зависит от базовой операционной системы и может быть больше.

**static long nanoTime()** - возвращает текущее значение источника времени с высоким разрешением работающей виртуальной машины Java в наносекундах.

```java
// Java code illustrating currentTimeMillis() method
import java.lang.*;
class SystemDemo {
    public static void main(String args[]) throws NullPointerException {
        System.out.println("difference between the "
                + "current time and midnight,"
                + " January 1, 1970 UTC is: " + 
                System.currentTimeMillis());
        System.out.println("current time in "
                + "nano sec: " + 
                System.nanoTime());
    }
}
```
**Вывод:**
<p style="background-color: navy; color: yellow">
difference between the current time and midnight, January 1, 1970 UTC is: 1718799628246<br>
current time in nano sec: 106136814512600</p>

### Завершение работу текущей виртуальной Java машины

**static void exit(int status)** - завершает работу текущей виртуальной машины Java. Аргумент служит кодом состояния; по соглашению, ненулевой код состояния указывает на ненормальное завершение.

Этот метод вызывает метод выхода в классе Runtime. Этот метод никогда не возвращает нормальный результат. Вызов System.exit(n) фактически эквивалентен вызову Runtime.getRuntime().exit(n).
```java
// Java code illustrating exit() method 
import java.lang.*;

class SystemDemo {
    public static void main(String args[]) throws NullPointerException {
        System.gc();
        System.out.println("Garbage collector executed ");
        System.out.println(System.getProperty("os.name"));
        System.exit(1);
        // this line will not execute as JVM terminated
        System.out.println("JVM terminated");
    }
}
```
**Вывод:**
<p style="background-color: navy; color: yellow">
Garbage collector executed <br>
Windows 11</p>

### Сборщик мусора

**static void gc()** - запускает сборщик мусора. Вызов метода gc() предполагает, что виртуальная машина Java расширит усилия по переработке неиспользуемых объектов, чтобы сделать память, которую они сейчас занимают, доступной для быстрого повторного использования. Когда управление возвращается из вызова метода, виртуальная машина Java приложила все усилия, чтобы освободить место для всех удаленных объектов.
```java
// Java code illustrating gc() method
import java.lang.*;
class SystemDemo {
    public static void main(String args[]) {
        Runtime gfg = Runtime.getRuntime();
        long memory1, memory2;
        Integer integer[] = new Integer[1000];

        // checking the total memory
        System.out.println("Total memory is: " + gfg.totalMemory());

        // checking free memory
        memory1 = gfg.freeMemory();
        System.out.println("Initial free memory: " + memory1);

        // calling the garbage collector on demand
        System.gc();

        memory1 = gfg.freeMemory();

        System.out.println("Free memory after garbage " + "collection: " + 
	        memory1);

        // allocating integers
        for (int i = 0; i < 1000; i++)
            integer[i] = i;

        memory2 = gfg.freeMemory();
        System.out.println("Free memory after allocation: " + memory2);

        System.out.println("Memory used by allocation: " + (memory1 - memory2));

        // discard integers
        for (int i = 0; i < 1000; i++)
            integer[i] = null;

        System.gc();

        memory2 = gfg.freeMemory();
        System.out.println("Free memory after  " + 
	        "collecting discarded Integers: " + memory2);
    }
}
```
**Вывод:**
<p style="background-color: navy; color: yellow">
Total memory is: 266338304<br>
Initial free memory: 263230504<br>
Free memory after garbage collection: 13604648<br>
Free memory after allocation: 12849512<br>
Memory used by allocation: 755136<br>
Free memory after  collecting discarded Integers: 7565608</p>

### Операции File IO с помощью класса System

Класс System содержит три поля — in, out и err. Они используются для чтения данных из [InputStream](InputStream) и записи данных в [OutputStream](OutputStream). Например, мы можем установить [FileOutputStream](FileOutputStream) к полю out и err для того, чтобы результат вывода в консоль записывался в файл.
```java
import java.io.PrintStream;  
import java.lang.*;  

class SystemDemo {  
    public static void main(String args[]) throws IOException {  
        try (FileInputStream fis = new FileInputStream("input.txt");  
             FileOutputStream fos = new FileOutputStream("server.log");) {  
  
            //устанавливаем inputStream  
            System.setIn(fis);  
            char c = (char) System.in.read();  
            System.out.print(c); //печатаем первый считанный знак  
  
            //устанавливаем outputStream            
            System.setOut(new PrintStream(fos));  
            System.out.write("Привет, Java\n".getBytes());  
  
            //устанавливаем errorStream  
            System.setErr(new PrintStream(fos));  
            System.err.write("Сообщение об исключении\n".getBytes());  
        } catch (IOException e) {  
            e.printStackTrace();  
        }  
    }  
}
```

