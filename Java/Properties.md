#Java #Properties
## Класс Properties

2024-04-15 15:43

**_Properties_** – это подкласс [_Hashtable_](Hashtable). Он используется для хранения списков значений, в которых ключ является [_String_](String), а значение также является [_String_](String).

Класс _Properties_ в Java используется множеством других классов. Например, это тип объекта, возвращаемый System.getProperties(), когда тот получает внешние значения.

_Properties_ определяет следующие переменную экземпляра. Эта переменная содержит список свойств по умолчанию, связанный с объектом _Properties_.

Следующая программа показывает несколько методов, поддерживаемых этой структурой данных:
```java
Properties defaults;
```

### Конструкторы

Вот список конструкторов, предоставляемые классом Properties.

|     |                                                                                                                                                                    |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| №   | Конструктор и описание                                                                                                                                             |
| 1   | **Properties()**  <br>Этот конструктор создает объёкт _Properties_, который не имеет значений по умолчанию.                                                        |
| 2   | **Properties(Properties propDefault)**  <br>Создаёт объект, который использует propDefault для своих значений по умолчанию. В обоих случаях список свойств пустой. |

### Методы 

| МЕТОД                                                  | ОПИСАНИЕ                                                                                                                                     |
| ------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------- |
| String getProperty(String key)                         | Возвращает значение, связанное с ключом. Возвращается нулевой объект, если ключ не находится ни в списке, ни в списке свойств по умолчанию.  |
| String getProperty(String key, String defaultProperty) | Возвращает значение, связанное с ключом; Возвращается defaultProperty, если ключ не находится ни в списке, ни в списке свойств по умолчанию. |
| void list(PrintStream streamOut)                       | Отправляет список свойств в выходной поток, связанный с streamOut.                                                                           |
| void list(PrintWriter streamOut)                       | Отправляет список свойств в выходной поток, связанный с streamOut.                                                                           |
| void load(InputStream streamIn) throws IOException     | Вводит список свойств из входного потока, связанного с streamIn.                                                                             |
| Enumeration propertyNames()                            | Вводит список свойств из входного потока, связанного с streamIn.                                                                             |
| Enumeration propertyNames()                            | Возвращает перечисление ключей, включая ключи, найденные в списке свойств по умолчанию.                                                      |
| Object setProperty(String key, String value)           | Связывает значение с ключом. Возвращает предыдущее значение, связанное с ключом, или возвращает ноль, если такой связи не существует.        |
| void store(OutputStream streamOut, String description) | После записи строки, указанной в описании, список свойств записывается в выходной поток, связанный с streamOut.                              |

#### Пример 1

Следующая программа показывает несколько методов, поддерживаемых этой структурой данных:
```java
import java.util.*;

public class PropDemo {
   public static void main(String args[]) {
      Properties capitals = new Properties();
      Set states;
      String str;
      
      capitals.put("Иллинойс", "Спрингфилд");
      capitals.put("Миссури", "Джефферсон-Сити");
      capitals.put("Вашингтона", "Олимпия");
      capitals.put("Калифорнии", "Сакраменто");
      capitals.put("Индианы", "Индианаполис");

      // Показывает все штаты и столицы в хэш-таблицы.
      states = capitals.keySet();   // Получить набор ключей
      Iterator itr = states.iterator();
      
      while(itr.hasNext()) {
         str = (String) itr.next();
         System.out.println("Столицей " + str + " является " + 
            capitals.getProperty(str) + ".");
      }     
      System.out.println();

      // При нахождении штата вне списка –– указать значение по умолчания.
      str = capitals.getProperty("Флорида", "Не Найдена");
      System.out.println("Столица Флориды " + str + ".");
   }
}
```
**Получим следующее:**
<p style="background-color: navy; color: yellow">
Столицей Миссури является Джефферсон-Сити.<br>
Столицей Иллинойс является Спрингфилд.<br>
Столицей Индианы является Индиана полис.<br>
Столицей Калифорнии является Сакраменто.<br>
Столицей Вашингтона является Олимпия.<br>
<br>
Столица Флориды Не Найдена.</p>

#### Пример 2. 

В приведенной ниже программе показано, как использовать класс Properties для получения информации из файла свойств. Давайте создадим файл свойств и назовем его db.properties.

db.properties:

`username = coder
`password = geeksforgeeks
`
```java
// Java program to demonstrate Properties class to get 
// information from the properties file 
import java.util.*; 
import java.io.*; 

public class GFG { 
    public static void main(String[] args) throws Exception { 
        // create a reader object on the properties file 
        FileReader reader = new FileReader("db.properties"); 
        // create properties object 
        Properties p = new Properties(); 
        // Add a wrapper around reader object 
        p.load(reader); 
        // access properties data 
        System.out.println(p.getProperty("username")); 
        System.out.println(p.getProperty("password")); 
    } 
}
```
**Выход**
<p style="background-color: navy; color: yellow">
coder<br>
geeksforgeeks</p>

#### Пример 3.

В приведенной ниже программе показано, как использовать класс _Properties_ для получения всех свойств системы. Используя метод System.getProperties(), мы можем получить все свойства системы.
```java
// Java program to demonstrate Properties class to get all 
// the system properties 
import java.util.*; 
import java.io.*; 
  
public class GFG { 
    public static void main(String[] args) throws Exception { 
        // get all the system properties 
        Properties p = System.getProperties(); 
        // stores set of properties information 
        Set set = p.entrySet(); 
        // iterate over the set 
        Iterator itr = set.iterator(); 
        while (itr.hasNext()) { 
            // print each property 
            Map.Entry entry = (Map.Entry)itr.next(); 
            System.out.println(entry.getKey() + " = " + entry.getValue()); 
        } 
    } 
}
```
**Выход**
<p style="background-color: navy; color: yellow">
C:\Users\minipc\.jdks\openjdk-19.0.1\bin\java.exe "-javaagent:C:\Program Files\JetBrains\IntelliJ IDEA Community Edition 2022.2.3\lib\idea_rt.jar=50595:C:\Program Files\JetBrains\IntelliJ IDEA Community Edition 2022.2.3\bin" -Dfile.encoding=UTF-8 -Dsun.stdout.encoding=UTF-8 -Dsun.stderr.encoding=UTF-8 -classpath C:\Users\minipc\IdeaProjects\Example\out\production\Example Main<br>
java.specification.version = 19<br>
sun.cpu.isalist = amd64<br>
sun.jnu.encoding = Cp1251<br>
java.class.path = C:\Users\minipc\IdeaProjects\Example\out\production\Example<br>
java.vm.vendor = Oracle Corporation<br>
sun.arch.data.model = 64<br>
user.variant = <br>
java.vendor.url = https://java.oracle.com/<br>
java.vm.specification.version = 19<br>
os.name = Windows 11<br>
sun.java.launcher = SUN_STANDARD<br>
user.country = RU<br>
sun.boot.library.path = C:\Users\minipc\.jdks\openjdk-19.0.1\bin<br>
sun.java.command = Main<br>
jdk.debug = release<br>
sun.cpu.endian = little<br>
user.home = C:\Users\minipc<br>
user.language = ru<br>
sun.stderr.encoding = UTF-8<br>
java.specification.vendor = Oracle Corporation<br>
java.version.date = 2022-10-18<br>
java.home = C:\Users\minipc\.jdks\openjdk-19.0.1<br>
file.separator = \<br>
java.vm.compressedOopsMode = Zero based<br>
sun.stdout.encoding = UTF-8<br>
line.separator = <br>
<br>
java.vm.specification.vendor = Oracle Corporation<br>
java.specification.name = Java Platform API Specification<br>
user.script = <br>
sun.management.compiler = HotSpot 64-Bit Tiered Compilers<br>
java.runtime.version = 19.0.1+10-21<br>
user.name = minipc<br>
stdout.encoding = UTF-8<br>
path.separator = ;<br>
os.version = 10.0<br>
java.runtime.name = OpenJDK Runtime Environment<br>
file.encoding = UTF-8<br>
java.vm.name = OpenJDK 64-Bit Server VM<br>
java.vendor.url.bug = https://bugreport.java.com/bugreport/<br>
java.io.tmpdir = C:\Users\minipc\AppData\Local\Temp\<br>
java.version = 19.0.1<br>
user.dir = C:\Users\minipc\IdeaProjects\Example<br>
os.arch = amd64<br>
java.vm.specification.name = Java Virtual Machine Specification<br>
sun.os.patch.level = <br>
native.encoding = Cp1251<br>
java.library.path = C:\Users\minipc\.jdks\openjdk-19.0.1\bin;C:\WINDOWS\Sun\Java\bin;C:\WINDOWS\system32;C:\WINDOWS;C:\Program Files\Common Files\Oracle\Java\javapath;C:\WINDOWS\system32;C:\WINDOWS;C:\WINDOWS\System32\Wbem;C:\WINDOWS\System32\WindowsPowerShell\v1.0\;C:\WINDOWS\System32\OpenSSH\;C:\Program Files\Git\cmd;c:\msys64\ucrt64\bin;c:\ProgramFiles (x86)\vim\vim90;C:\Users\minipc\AppData\Local\Microsoft\WindowsApps;c:\msys64\ucrt64\bin;c:\Program Files\Git\bin;c:\Program Files (x86)\vim\vim90;;.<br>
java.vm.info = mixed mode, sharing<br>
stderr.encoding = UTF-8<br>
java.vendor = Oracle Corporation<br>
java.vm.version = 19.0.1+10-21<br>
sun.io.unicode.encoding = UnicodeLittle<br>
java.class.version = 63.0</p>

#### Пример 4.

В приведенной ниже программе показано, как использовать класс Properties для создания файла свойств.
```java
// Java program to demonstrate Properties class to create 
// the properties file 
import java.util.*; 
import java.io.*; 
  
public class GFG { 
    public static void main(String[] args) throws Exception { 
        // create an instance of Properties 
        Properties p = new Properties(); 
  
        // add properties to it 
        p.setProperty("name", "Ganesh Chowdhary Sadanala"); 
        p.setProperty("email", 
                      "ganeshs.gfg@gmail.com"); 
  
        // store the properties to a file 
        p.store(new FileWriter("info.properties"), 
                "GeeksforGeeks Properties Example"); 
    } 
}
```
**Выход в info.properties**
<p style="background-color: navy; color: yellow">
#GeeksforGeeks Properties Example<br>
#Mon Apr 15 16:38:38 MSK 2024<br>
email=ganeshs.gfg@gmail.com<br>
name=Ganesh Chowdhary Sadanala</p>


