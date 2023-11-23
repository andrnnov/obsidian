#Java #File
### Работа с файлами в Java. Класс File ###

2023-11-22 11:48

Класс Java File, java.io.Файл в Java IO API предоставляет вам доступ к базовой файловой системе. Используя класс Java File, вы можете: 
- [[File#Метод exists(). Определение наличия файла (каталога)|Метод exists(). Определение наличия файла (каталога)]] 
- Создать каталог, если он не существует. 
- [[File#Метод getName(). Получить имя файла или каталога|Метод getName(). Получить имя файла или каталога]]
- [[File#Метод length(). Определить размер в байтах файла, который связан с файловым объектом|Метод length(). Определить размер в байтах файла, который связан с файловым объектом]]
- Переименовать или переместить файл. 
- [[File#]]Метод delete(). Удалить файл. 
- Проверить, является ли путь файлом или каталогом. 
- [[File#Чтение списка файлов в директории|Методы list() и listFiles(). Прочитайть список файлов в каталоге]].

#### Создание экземпляра класса File. Конструкторы класса ####

В классе File реализованы несколько конструкторов, каждый из которых позволяет формировать имя файла или каталога разными способами. 

Наиболее распространенным есть конструктор, который получает строку типа String. В этой строке задается полное (абсолютное) или сокращенное (относительное) имя файла или каталога, который рассматривается (создается, определяется и т.п.).

Также существуют конструкторы, формирующие имя файла из нескольких частей.
```java
import java.io.*;

public static void main(String[] args) throws IOException
{
	// Конструкторы класса File
	// 1. Конструктор, который получает одну строку типа String,
	//     создается файловый объект (переменная) с именем f1
	File f1 = new File("output.txt"); // задан сокращенный путь
	String path1 = f1.getPath();
	System.out.println(path1);
	// 2. Конструктор, который получает две строки:
	//     - первая строка задает абсолютный путь к файловому элементу,
	//     - вторая строка задает имя файлового элемента.
	File f2 = new File("C:\\", "Program Files");
	String path2 = f2.getPath(); // path2 = "C:\\Program Files"
	System.out.println("path2 = " + path2);
	// 3. Конструктор типа File(File, String)
	File f3 = new File("C:\\Programs\\Java\\Project22");
	File f4 = new File(f3,"output.txt");
	String path3 = f3.getPath();
	String path4 = f4.getPath();
	System.out.println("path3 = " + path3); // path3 = C:\Programs\Java\Project22
	System.out.println("path4 = " + path4); // path4 = C:\Programs\Java\Project22\output.txt
	}
```
Результат выполнения программы
<p style="background-color: navy; color: yellow">
output.txt<br>
path2 = C:\Program Files<br>
path3 = C:\Program Files\Java\Project22<br>
path4 = C:\Program Files\Java\Project22\output.txt</p>
#### Метод getName(). Получить имя файла или каталога ####

Метод getName() возвращает имя файла или каталога, с которым связана файловая переменная. Если абсолютный путь к имени файла (каталога) содержит несколько уровней вложения, то возвращается непосредственно имя этого файла (каталога). Общая форма использования метода следующая 
```java
name = fileObj.getName();
```
здесь
    name – переменная типа String, которая есть результатом выполнения метода;
    fileObj – файловый объект, связанный с файлом или каталогом.
```java
import java.io.*;

public static void main(String[] args) throws IOException
{
	 // Метод getName() - получить имя файла
	// Объявить файловый объект и связать его с именем файла
	f = new File("C:\\Program Files");
	String name = f.getName(); // name = "Program Files"
	System.out.println("name = " + name);
}
```
Результат выполнения программы
<p style="background-color: navy; color: yellow">name = Program Files</p>
#### Метод getPath(). Получить имя файла ####

Метод getPath() возвращает имя файла (каталога), которое было задано в конструкторе при создании файлового объекта типа File. Общая форма использования метода следующая
```java
path = fileObj.getPath();
```
здесь
    path – строка типа String, что есть именем файла (каталога), которое было задано при создании файловой переменной fileObj.
```java
import java.io.*;

public static void main(String[] args) throws IOException
{
	 // Метод getPath() - получить полный путь к файлу
	// Объявить файловый объект и связать его с именем файла
	File f = new File("output.txt"); // имя текстового файла
	String Path = f.getPath();
	System.out.println("Path = " + Path);

	// Указать полное имя при создании файлового объекта
	f = new File("C:\\Program Files");
	Path = f.getPath();
	System.out.println("Path = " + Path); // Path = C:\Program Files
}
```
#### Метод isAbsolute(). Определить, указан ли полный путь к файлу ####

Метод isAbsolute() позволяет определить, указан ли полный путь к файлу при создании файлового объекта в конструкторе класса File. Общая форма использования метода следующая
```java
res = fileObj.isAbsolute();
```
здесь
    res – результат, который равен true, если при создании файловой переменной fileObj был задан абсолютный путь.
```java
import java.io.*;

public static void main(String[] args) throws IOException
{
	// Метод isAbsolute() - задан ли полный путь к файлу (каталогу)
	// Объявить файловый объект и связать его с именем файла
	File f1 = new File("output.txt"); // задан сокращенный путь
	boolean res1;
	res1 = f1.isAbsolute();
	System.out.println("res1 = " + res1); // res1 = false

	// Задать полное имя при создании файлового объекта
	File f2 = new File("C:\\Program Files");
	boolean res2 = f2.isAbsolute();
	System.out.println("res2 = " + res2); // res2 = true
}
```
#### Метод getAbsolutePath(). Получить полный путь к файлу ####

Метод getAbsolutePath() возвращает полный путь к файлу. Общая форма использования метода следующая
```java
path = fileObj.getAbsolutePath();
```
здесь
    path – строка типа String, которая есть результатом;
    fileObj – файловый объект, который связан с файлом, для которого нужно определить абсолютный путь.
```java
import java.io.*;

public static void main(String[] args) throws IOException
{
	// Метод getAbsolutePath() - получить полный путь к файлу
	// Объявить файловый объект и связать его с именем файла
	File f = new File("output.txt"); // имя текстового файла
	String absPath = f.getAbsolutePath();
	System.out.println("Path = " + absPath);
}
```
Результат выполнения программы
<p style="background-color: navy; color: yellow">Path = C:\Programs\Java\Project22\output.txt</p>

#### Методы canRead(), canWrite(). Определение того, допускает ли файловый объект чтение и запись ####

Методы canRead() и canWrite() предназначены для определения того, допускает ли файловый объект чтение или запись. В случае положительного результата методы возвращают true.
```java
import java.io.*;

public static void main(String[] args) throws IOException
{
	File f = new File("output.txt");

	if (f.canRead())
	    System.out.println("The result of canRead() is true.");
	else
	    System.out.println("The result of canRead() is false");

	if (f.canWrite())
	    System.out.println("The result of canWrite() is true.");
	else
	    System.out.println("The result of canWrite() is false");
}
```
Результат работы программы
<p style="background-color: navy; color: yellow">The result of canRead() is true.<br>
The result of canWrite() is true.</p>
#### Метод exists(). Определение наличия файла (каталога) ####

Метод exists() предназначен для определения существования файла, ассоциированного с файловым объектом. Общая форма использования метода следующая
```java
res = fileObj.exists();
```
здесь
    res – результат работы метода. Если res = true, то заданный файл существует;
    fileObj – объект, который проверяется.
```java
import java.io.*;

public static void main(String[] args) throws IOException
{
	// Метод exists() - определить, существует ли файл (директорий)
	// Объявить файловый объект и связать его с именем файла
	File f = new File("output.txt"); // имя текстового файла

	// Если файл f существует, то вывести соответствующее сообщение
	if (f.exists())
		System.out.println("File is present.");
	else
		System.out.println("File is not present"); // файл отсутствует
	// Определить, существует ли каталог
	File f2 = new File("C:\\Program Files");

	if (f2.exists())
	    System.out.println("The directory is present.");
	else
	    System.out.println("The directory is not present.");
}
```
#### Метод isDirectory(). Определить, связан ли файловый объект с директорией ####

Метод isDirectory() предназначен для определения того, есть ли файл директорием (папкой). Общая форма использования метода следующая
```java
res = fileObj.isDirectory();
```
здесь
    res – значение типа bool. Если res=true, то файл есть директорием;
    fileObj – файловый объект, который проверяется.
```java
import java.io.*;

public static void main(String[] args) throws IOException
{
	// Метод isDirectory - определить, есть ли файл директорием (папкой)
	// 1. Объявить файловую переменную и связать ее именем файла или папки
	File f = new File("C:\\Program Files"); // имя папки, которую нужно проверить

	// Если файл f существует, то определить его тип
	if (f.exists()) {
	    if (f.isDirectory()) {
		    System.out.println("Directory.");
	    }
	    else
		    System.out.println("File.");
	}
	else
	    System.out.println("The file is not present"); // файл отсутствует
}
```
#### Метод isFile(). Определить, связан ли файловый объект с файлом ####

Метод isFile() возвращает true, если файловый объект связан с файлом. Общая форма использования метода следующая
```java
res = fileObj.isFile();
```
здесь
    res – результат вычисления. Если файловый объект есть файлом, то res = true;
    fileObj – файловый объект.
```java
import java.io.*;

public static void main(String[] args) throws IOException
{
	// Метод isFile() - определить, связан ли файловый объект с файлом
	// 1. Объявить файловый объект и связать его с именем файла
	File f = new File("output.txt"); // имя файла

	// Если файл f существует, то определить его тип
	if (f.exists()) {
	    if (f.isFile()) {
		    System.out.println("File object is file.");
	    }
		else
		    System.out.println("File object is not file.");
	}
	else
	    System.out.println("The file is not present"); // файл отсутствует
}
```
#### Метод isHidden(). Определить, есть ли файловый объект скрытым ####

Метод isHidden() возвращает true, если файловый объект связан с файлом у которого установлен атрибут «скрытый» (hidden). Общая форма использования метода
```java
res = fileObj.isHidden();
```
здесь
    fileObj – файловый объект;
    res – результат работы метода. Если res = true, то файловый объект связан со скрытым файлом.
```java
import java.io.*;

public static void main(String[] args) throws IOException
{
	File f = new File("output.txt");

	if (f.isHidden())
	    System.out.println("The file \"output.txt\" is hidden.");
	else
	    System.out.println("The file \"output.txt\" is not hidden.");
}
```
#### Метод length(). Определить размер в байтах файла, который связан с файловым объектом ####

^9f33f5

Метод length() предназначен для определения размера файла и имеет следующую общую форму
```java
long length()
```
Пример
```java
import java.io.*;

public static void main(String[] args) throws IOException
{
	// Определить размер файла в байтах
	// 1. Объявить файловую переменную
	File f = new File("abc.txt");

	// 2. Создать поток, который записывает символы в файл f
	FileWriter fw = new FileWriter(f);
	// 3. Записать в файл строку "Hello world!"
	fw.write("Hello world!");
	// 4. Закрыть поток
	fw.close();
	// 5. Определить длину файла "abc.txt"
	long len = f.length();
	// 6. Вывести длину файла на консоль
	System.out.println("len = " + len); // len = 12
}
```
Результат работы программы
<p style="background-color: navy; color: yellow">len = 12</p>
#### Метод delete(). Удаление файла ####

Метод delete() используется для удаления файла. Общая форма использования метода
```java
res = fileObj.delete();
```
здесь
    fileObj – файловый объект, который связан с файлом, который нужно удалить;
    res – результат выполнения метода. Если res = true, то удаление файла состоялось успешно.
```java
import java.io.*;

public static void main(String[] args) throws IOException
{
	// Метод delete() - удалить файл по его имени
	// Объявить файловую переменную
	File f = new File("somefile.txt");

	// Удалить файл, если он существует
	if (f.exists()) {
	    f.delete();
	    System.out.println("The file is deleted.");
	}
	else
	    System.out.println("The file is not present.");
}
```
#### Метод mkdir(). Создание папки или каталога ####

Метод mkdir() используется для создания папки (каталога). Общая форма использования метода следующая
```java
res = fileObj.mkdir();
```
здесь
    res – результат типа bool. Если каталог создан успешно, то res = true, в противном случае res = false;
    fileObj – объект типа File, который связан с именем создаваемого каталога.

Пример. Создается каталог с именем 123 в текущем каталоге.
```java
import java.io.*;

public static void main(String[] args) throws IOException
{
	// Метод mkdir() - создать каталог
	// 1. Объявить файловую переменную и связать ее с папкой в текущем каталоге
	//     (задается относительный путь).
	File f = new File("123");

	// Если каталог не существует, то создать его
	if (!f.exists()) {
	    if (f.mkdir()) {
		    System.out.println("The folder is created!"); // создан успешно
	    }
	    else
		    System.out.println("The folder is not created."); // каталог не создан
	}
	else
	    System.out.println("The folder is present.");

	// 2. Создать файловую переменную и связать ее с папкой
	//     C:\Programs\345 - абсолютный путь к папке.
	File f2 = new File("C:\\Programs\\345");
	boolean res = f2.mkdir();

	if (res)
	    System.out.println("The folder C:\\Programs\\345 is created.");
	else
		System.out.println("The folder C:\\Programs\\345 is not created.");
}
```
Результат работы программы
<p style="background-color: navy; color: yellow">The folder is present.<br>
The folder C:\Programs\345 is created.</p>
#### Метод mkdirs(). Создание нескольких вложенных папок ####

Метод mkdirs() позволяет создать несколько уровней вложений папок за один раз. В отличие от метода mkdir(), этот метод создает уровни вложения папок, которые не существуют. В методе mkdir() чтобы создать подпапку нужно, чтобы предварительно обязательно была созданная папка верхнего уровня.

Общая форма использования метода следующая:
```java
res = fileObj.mkdirs();
```
здесь
    fileObj – файловый объект, который содержит строку с именем или именами папок, которые нужно создать;
    res – результат выполнения метода. Если последовательность папок создана успешно, то res = true.
Пример.
```java
import java.io.*;

public static void main(String[] args) throws IOException
{
	// Создать папки по указанному пути
	File f = new File("C:\\ABC\\DEF\\GHI");

	// Создать папки C:\ABC, C:\ABC\DEF, C:\ABC\DEF\GHI
	if (f.mkdirs())
	    System.out.println("The folders is created.");
	else
	    System.out.println("The folders is not created");
}
```
#### Метод renameTo(File). Переименование файла ####

Метод renameTo() предназначен для переименования файла. Общая форма использования метода следующая
```java
res = f1.renameTo(f2);
```
здесь
    res – результат выполнения метода. Если файл переименован успешно, то res = true, иначе res = false;
    f1 – файловая переменная, соответствующая файлу-источнику, который нужно переименовать;
    f2 – файловая переменная, соответствующая новому имени файла-источника f1 после его переименования.
Пример.
```java
import java.io.*;

public static void main(String[] args) throws IOException
{
	// Метод renameTo() - переименовать файл.
	// Переименовать файл strings.txt в файл array.txt.
	// В обеих файлах задается относительный путь
	// 1. Объявить файловую переменную и связать ее с файлом
	File f1 = new File("abc.txt");
	File f2 = new File("array.txt");

	// Если файл f1 существует, то переименовать его
	if (f1.exists()) {
	    if (f1.renameTo(f2)) {
		    System.out.println("Ok!"); // переименован успешно
	    }
	    else
		    System.out.println("The file is not renamed."); // файл не переименован
	}
	else
	    System.out.println("The file is not present");
}
```
#### Метод getTotalSpace(). Определение объема диска ####

С помощью метода getTotalSpace() можно определить общий размер носителя (диска) в байтах. Метод возвращает результат типа long. Общая форма использования метода следующая
```java
totalSpace = fileObj.getTotalSpace();
```
здесь
    fileObj – файловый объект, в котором определено имя диска для которого определяется размер;
    totalSpace – переменная типа long, которая есть результатом выполнения метода.

Пример.
```java
import java.io.*;

public static void main(String[] args) throws IOException
{
	// Определить размер диска
	File f = new File("E:\\");

	// Определить общий объем жесткого диска E:
	long totalSpace = f.getTotalSpace();
	System.out.println("Drive E: - Total space = " + totalSpace);

	// Определить объем диска C:
	f = new File("C:\\");
	totalSpace = f.getTotalSpace();
	System.out.println("Drive C: - Total space = " + totalSpace);
}
```
Результат выполнения программы
<p style="background-color: navy; color: yellow">Drive E: - Total space = 790486839296<br>
Drive C: - Total space = 208684355584</p>
#### Метод getFreeSpace(). Определить свободное место на диске ####

С помощью метода getFreeSpace() можно определить объем в байтах свободного места на носителе. Общая форма использования метода следующая
```java
space = fileObj.getFreeSpace();
```
здесь
    fileObj – файловый объект, который содержит имя носителя, имя файла или имя папки. Если задается имя файла или папки, то определяется объем свободного места для носителя, на котором этот диск и файл размещены;
    space – переменная типа long, которая есть результатом работы метода.

Пример.
```java
import java.io.*;

public static void main(String[] args) throws IOException
{
	// Определить размер диска
	File f = new File("E:\\");

	// Определить размер свободной памяти на диске
	long freeSpace = f.getFreeSpace();
	System.out.println("Drive E: - Free space = " + freeSpace);

	// Определить свободное место на диске C:
	f = new File("C:\\");
	freeSpace = f.getFreeSpace();
	System.out.println("Drive C: - Free space = " + freeSpace);
}
```
Результат выполнения программы
<p style="background-color: navy; color: yellow">Drive E: - Free space = 197617647616<br>
Drive C: - Free space = 18358034432</p>
#### Метод getUsableSpace(). Определение полезного места на диске ####

С помощью метода getUsableSpace() можно определить полезный размер места на носителе (диске). Во многих случаях значение, которое возвращает данный метод равно значению, которое возвращает метод getFreeSpace(). Общая форма использования метода следующая:
```java
space = fileObj.getUsageSpace();
```
где
    fileObj – файловый объект, который содержит имя диска или имя файла. Если для fileObj определено имя файла, то определяется объем носителя, на котором этот файл сохраняется;
    space – переменная типа long, которая есть размером полезного места на диске.
```java
import java.io.*;

public static void main(String[] args) throws IOException
{
	// Определить размер диска
	File f = new File("E:\\");

	// Определить объем полезного места на диске E:
	long usableSpace = f.getUsableSpace();
	System.out.println("Drive E: - Usable space = " + usableSpace);

	// Определить объем диска C: и свободное место на диске C:
	f = new File("C:\\");
	usableSpace = f.getUsableSpace();
	System.out.println("Drive C: - Usable space = " + usableSpace);
}
```
Результат работы программы
<p style="background-color: navy; color: yellow">Drive E: - Free space = 197617647616<br>
Drive C: - Free space = 18358034432</p>
#### Чтение списка файлов в директории ####

Вы можете получить список всех файлов в каталоге, вызвав либо метод Java File list(), либо метод listFiles(). Метод list() возвращает массив строк с именами файлов и/или каталогов каталога, на который указывает объект File. Функция listFiles() возвращает массив файловых объектов, представляющих файлы и/или каталоги в каталоге, на который указывает файл. Вот пример перечисления всех файлов в каталоге с помощью методов Java File list() и listFiles():
```java
File file = new File("c:\\data");

String[] fileNames = file.list();

File[]   files = file.listFiles();
```
