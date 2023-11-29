#Java #File #Files #Path #Paths
### Работа с файлами ###

2023-11-23 15:51

До появления Java 7 все операции по созданию, переименованию и т.д. проводились с помощью класса [File](File). Но в Java 7 создатели языка решили изменить работу с файлами и каталогами.

Это произошло из-за того, что у класса [File](File) был ряд недостатков. Например, в нем не было метода copy(), который позволил бы скопировать файл из одного места в другое (казалось бы, явно необходимая функция).

Кроме того, в классе [File](File) было достаточно много методов, которые возвращали boolean-значения. При ошибке такой метод возвращает false, а не выбрасывает исключение, что делает диагностику ошибок и установление их причин очень непростым делом.

Вместо единого класса [File](File) появились целых 3 класса: Paths, Path и Files. Ну а если быть точным, Path — это интерфейс, а не класс.
### Paths ###

Paths — это совсем простой класс с единственным статическим методом get(). Его создали исключительно для того, чтобы из переданной строки или URI получить объект типа Path.
Другой функциональности у него нет.

Вот пример его работы:
```java
import java.nio.file.Path;
import java.nio.file.Paths;

public class Main {

   public static void main(String[] args) {

       Path testFilePath = Paths.get("C:\\Users\\Username\\Desktop\\testFile.txt");
   }
}
```
### Path ###

Path, по большому счету, — это переработанный аналог класса [File](File). Работать с ним значительно проще, чем с File. Во-первых, из него убрали многие утилитные (статические) методы, и перенесли их в класс Files. Во-вторых, в Path были упорядочены возвращаемые значения методов. В классе File методы возвращали то String, то boolean, то [File](File) — разобраться было непросто. 

Например, был метод getParent(), который возвращал родительский путь для текущего файла в виде строки. Но при этом был метод getParentFile(), который возвращал то же самое, но в виде объекта File!

Это явно избыточно. Поэтому в интерфейсе Path метод getParent() и другие методы работы с файлами возвращают просто объект Path. Никакой кучи вариантов — все легко и просто.

Некоторые методы Path:
- getFileName() — возвращает имя файла из пути;
- getParent() — возвращает «родительскую» директорию по отношению к текущему пути (то есть ту директорию, которая находится выше по дереву каталогов);
- getRoot() — возвращает «корневую» директорию; то есть ту, которая находится на вершине дерева каталогов;
- startsWith(), endsWith() — проверяют, начинается/заканчивается ли путь с переданного пути:
```java
import java.nio.file.Path;
import java.nio.file.Paths;

public class Main {

   public static void main(String[] args) {

       Path testFilePath = Paths.get("C:\\Users\\Username\\Desktop\\testFile.txt");

       Path fileName = testFilePath.getFileName();
       System.out.println(fileName);

       Path parent = testFilePath.getParent();
       System.out.println(parent);

       Path root = testFilePath.getRoot();
       System.out.println(root);

       boolean endWithTxt = testFilePath.endsWith("Desktop\\testFile.txt");
       System.out.println(endWithTxt);

       boolean startsWithLalala = testFilePath.startsWith("lalalala");
       System.out.println(startsWithLalala);
   }
}
```
Вывод в консоль:
<p style="background-color: navy; color: yellow">
testFile.txt<br>
C:\Users\Username\Desktop<br>
C:\<br>
true<br>
false</p>
Обрати внимание на то, как работает метод endsWith(). Он проверяет, заканчивается ли текущий путь на переданный путь. Именно на путь, а не на набор символов.

Сравни результаты этих двух вызовов:
```java
import java.nio.file.Path;
import java.nio.file.Paths;

public class Main {
   public static void main(String[] args) {
       Path testFilePath = Paths.get("C:\\Users\\Username\\Desktop\\testFile.txt");

       System.out.println(testFilePath.endsWith("estFile.txt"));
       System.out.println(testFilePath.endsWith("Desktop\\testFile.txt"));
   }
}
```
Вывод в консоль:
<p style="background-color: navy; color: yellow">
false<br>
true</p>
В метод endsWith() нужно передавать именно полноценный путь, а не просто набор символов: в противном случае результатом всегда будет false, даже если текущий путь действительно заканчивается такой последовательностью символов (как в случае с “estFile.txt” в примере выше).

Кроме того, в Path есть группа методов, которая упрощает работу с абсолютными (полными) и относительными путями.

Давай рассмотрим эти методы:
- boolean isAbsolute() — возвращает true, если текущий путь является абсолютным:
```java
import java.nio.file.Path;
import java.nio.file.Paths;

public class Main {
   public static void main(String[] args) {
       Path testFilePath = Paths.get("C:\\Users\\Username\\Desktop\\testFile.txt");
       System.out.println(testFilePath.isAbsolute());
   }
}
```
Вывод в консоль:
<p style="background-color: navy; color: yellow">
true</p>
- Path normalize() — «нормализует» текущий путь, удаляя из него ненужные элементы. Ты, возможно, знаешь, что в популярных операционных системах при обозначении путей часто используются символы “.” (“текущая директория”) и “..” (родительская директория). Например: “./Pictures/dog.jpg” обозначает, что в той директории, в которой мы сейчас находимся, есть папка Pictures, а в ней — файл “dog.jpg”

Так вот. Если в твоей программе появился путь, использующий “.” или “..”, метод normalize() позволит удалить их и получить путь, в котором они не будут содержаться:
```java
import java.nio.file.Path;
import java.nio.file.Paths;

public class Main {
   public static void main(String[] args) {
       Path path5 = Paths.get("C:\\Users\\Java\\.\\examples");
       System.out.println(path5.normalize());

       Path path6 = Paths.get("C:\\Users\\Java\\..\\examples");
       System.out.println(path6.normalize());
   }
}
```
Вывод в консоль:
<p style="background-color: navy; color: yellow">
C:\Users\Java\examples<br>
C:\Users\examples</p>
- Path relativize() — вычисляет относительный путь между текущим и переданным путем.
Например:

```java
import java.nio.file.Path;
import java.nio.file.Paths;

public class Main {
	public static void main(String[] args) {
	    Path testFilePath1 = Paths.get("C:\\Users\\Users");
	    Path testFilePath2 = 
		       Paths.get("C:\\Users\\Users\\Username\\Desktop\\testFile.txt");
		System.out.println(testFilePath1.relativize(testFilePath2));
	}
}
```
Вывод в консоль:
<p style="background-color: navy; color: yellow">
Username\Desktop\testFile.txt</p>
Полный список методов Path довольно велик. Найти их все можено в [документации Oracle](https://docs.oracle.com/javase/7/docs/api/java/nio/file/Path.html).

### Files ###

Files — это утилитный класс, куда были вынесены статические методы из класса [File](File). Files — это примерно то же, что и `Arrays` или `Collections`, только работает он с файлами, а не с массивами и коллекциями. Он сосредоточен на управлении файлами и директориями. Используя статические методы `Files`, мы можем создавать, удалять и перемещать файлы и директории. Для этих операций используются методы createFile() (для директорий — createDirectory()), move() и delete(). Вот как ими пользоваться:
```java
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;

import static java.nio.file.StandardCopyOption.REPLACE_EXISTING;

public class Main {
   public static void main(String[] args) throws IOException {
       //создание файла
       Path testFile1 = Files.createFile(Paths.get("C:\\Users\\Username\\Desktop\\testFile111.txt"));
       System.out.println("Был ли файл успешно создан?");
       System.out.println(Files.exists(Paths.get("C:\\Users\\Username\\Desktop\\testFile111.txt")));

       //создание директории
       Path testDirectory = Files.createDirectory(Paths.get("C:\\Users\\Username\\Desktop\\testDirectory"));
       System.out.println("Была ли директория успешно создана?");
       System.out.println(Files.exists(Paths.get("C:\\Users\\Username\\Desktop\\testDirectory")));

       //перемещаем файл с рабочего стола в директорию testDirectory. Перемещать надо с указанием имени файла в папке!
       testFile1 = Files.move(testFile1, Paths.get("C:\\Users\\Username\\Desktop\\testDirectory\\testFile111.txt"), REPLACE_EXISTING);

       System.out.println("Остался ли наш файл на рабочем столе?");
       System.out.println(Files.exists(Paths.get("C:\\Users\\Username\\Desktop\\testFile111.txt")));

       System.out.println("Был ли наш файл перемещен в testDirectory?");
       System.out.println(Files.exists(Paths.get("C:\\Users\\Username\\Desktop\\testDirectory\\testFile111.txt")));

       //удаление файла
       Files.delete(testFile1);
       System.out.println("Файл все еще существует?");
       System.out.println(Files.exists(Paths.get("C:\\Users\\Username\\Desktop\\testDirectory\\testFile111.txt")));
   }
}
```
Здесь мы сначала создаем файл (метод Files.createFile()) на рабочем столе, далее создаем там же папку (метод Files.createDirectory()). После этого мы перемещаем файл (метод Files.move()) с рабочего стола в эту новую папку, а в конце — удаляем файл (метод Files.delete()).
Вывод в консоль:
<p style="background-color: navy; color: yellow">
Был ли файл успешно создан?<br>
true<br>
Была ли директория успешно создана?<br>
true<br>
Остался ли наш файл на рабочем столе?<br>
false<br>
Был ли наш файл перемещен в testDirectory?<br>
true<br>
Файл все еще существует?<br>
false</p>

<p style="background-color: orange; color: white">Обрати внимание:</p> так же, как и методы интерфейса Path, многие методы Files возвращают объект Path.

Большинство методов класса Files принимают на вход также объекты Path. Тут твоим верным помощником станет метод Paths.get() — активно им пользуйся.

Что еще интересного есть в Files? То, чего очень не хватало старому классу [File](File) — метод copy()! Мы говорили о нем в начале лекции, самое время с ним познакомиться!
```java
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;

import static java.nio.file.StandardCopyOption.REPLACE_EXISTING;

public class Main {
   public static void main(String[] args) throws IOException {
       //создание файла
       Path testFile1 = Files.createFile(Paths.get("C:\\Users\\Username\\Desktop\\testFile111.txt"));
       System.out.println("Был ли файл успешно создан?");
       System.out.println(Files.exists(Paths.get("C:\\Users\\Username\\Desktop\\testFile111.txt")));

       //создание директории
       Path testDirectory2 = Files.createDirectory(Paths.get("C:\\Users\\Username\\Desktop\\testDirectory2"));
       System.out.println("Была ли директория успешно создана?");
       System.out.println(Files.exists(Paths.get("C:\\Users\\Username\\Desktop\\testDirectory2")));

       //копируем файл с рабочего стола в директорию testDirectory2.
       testFile1 = Files.copy(testFile1, Paths.get("C:\\Users\\Username\\Desktop\\testDirectory2\\testFile111.txt"), REPLACE_EXISTING);

       System.out.println("Остался ли наш файл на рабочем столе?");
       System.out.println(Files.exists(Paths.get("C:\\Users\\Username\\Desktop\\testFile111.txt")));

       System.out.println("Был ли наш файл скопирован в testDirectory?");
       System.out.println(Files.exists(Paths.get("C:\\Users\\Username\\Desktop\\testDirectory2\\testFile111.txt")));
   }
}
```
Вывод в консоль:
<p style="background-color: navy; color: yellow">
Был ли файл успешно создан?<br>
true<br>
Была ли директория успешно создана?<br>
true<br>
Остался ли наш файл на рабочем столе?<br>
true<br>
Был ли наш файл скопирован в testDirectory?<br>
true</p>
Но класс Files позволяет не только управлять самими файлами, но и работать с его содержимым. 

Для записи данных в файл у него есть метод write(), а для чтения — целых 3: read(), readAllBytes() и readAllLines()

Мы подробно остановимся на последнем. Почему именно на нем?

Потому что у него есть очень интересный тип возвращаемого значения — **``List<String>``**! То есть он возвращает нам список строк файла. Конечно, это делает работу с содержимым очень удобной, ведь весь файл, строку за строкой, можно, например, вывести в консоль в обычном цикле for:
```java
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Paths;
import java.util.List;

import static java.nio.charset.StandardCharsets.UTF_8;

public class Main {
   public static void main(String[] args) throws IOException {

	    List<String> lines = Files.readAllLines(Paths.get("C:\\Users\\Username\\Desktop\\pushkin.txt"), UTF_8);

	    for (String s: lines) {
	        System.out.println(s);
	    }
	}
}
```
Вывод в консоль:
<p style="background-color: navy; color: yellow">
Я помню чудное мгновенье:<br>
Передо мной явилась ты,<br>
Как мимолетное виденье,<br>
Как гений чистой красоты.</p>
