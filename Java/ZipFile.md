#Java #ZipFile
### Класс ZipFile

2024-01-18 16:14

Класс java.util.zip.ZipFile в Java API предназначен для чтения записей из ZIP-файлов. Он действует как точка доступа к сжатым данным в ZIP-архиве, позволяя разработчикам удобно извлекать файлы и каталоги при эффективном управлении ресурсами.

Класс ZipFile работает путем считывания содержимого ZIP-файла, включая сжатые файлы и каталоги. Он предлагает методы для извлечения метаданных о ZIP-файле, таких, как количество записей, и извлечения фактических данных в форме объекта [ZipEntry](ZipEntry).

У данного класса есть несколько конструкторов. Ниже представлены наиболее часто использующиеся конструкторы:
```java
ZipFile(String name);
ZipFile(File file);
```
А также в нем определены несколько методов. Они представлены в таблице:

|Функция|Описание|
|---|---|
|**Enumeration entries()**|Возвращает перечисление ([Enumeration](Enumeration)) объектов, которые хранятся в архиве. |
|**String getName()**|Возвращает имя архива.|
|**InputStream getInputStream(ZipEntry entry)**|Возвращает поток для чтения данных из одного объекта, который передается через аргумент типа **[ZipEntry](ZipEntry)** (его мы рассмотрим позднее). Может бросить исключение типа **IOException**. |
|**ZipEntry getEntry(String name)**|Возвращает объект архива по его имени.|
|**void close()**|Закрывает архив. Дальнейшая работа с архивом невозможна. В противном случае бросается исключение **IOException**.|

Вот простой пример использования ZipFile для отображения списка записей ZIP-файла:
```java
import java.util.zip.ZipFile;
import java.util.Enumeration;
import java.util.zip.ZipEntry;

public class ZipFileExample {
    public static void main(String[] args) {
        try (ZipFile zipFile = new ZipFile("example.zip")) {
            Enumeration<? extends ZipEntry> entries = zipFile.entries();
            
            while (entries.hasMoreElements()) {
                ZipEntry entry = entries.nextElement();
                System.out.println("Entry Name: " + entry.getName());
            }
        } catch (IOException e) {
            System.err.println("Error opening ZIP file: " + e.getMessage());
        }
    }
}
```
Вывод:
<p style="background-color: navy; color: yellow">
Entry Name: function.cpp<br>
Entry Name: main.cpp<br>
Entry Name: sklad.txt<br>
Entry Name: TConteiner.h<br>
Entry Name: TProduct_TReceiptLine.h</p>
В этом фрагменте вы создаете объект ZipFile, указывая путь к ZIP-файлу. Затем вы получаете список записей ZIP-файла и просматриваете их, выводя имя каждой записи. Оператор try-with-resources гарантирует, что ZIP-файл закроется должным образом, даже если произойдет исключение.

Класс ZipFile является жизненно важным инструментом для работы с ZIP-архивами на Java, обладающим простым API для взаимодействия со сжатыми данными.

Класс java.util.zip.ZipFile используется для чтения записей из ZIP-файла. Здесь показано, как вы можете открыть ZIP-файл и циклически просматривать его записи, используя интерфейс [Enumeration](Enumeration). Сначала вам нужно создать экземпляр ZipFile, указав путь к ZIP-файлу, который вы хотите открыть:
```java
ZipFile zipFile = new ZipFile("example.zip");
```
Как только у вас будет экземпляр ZipFile, вы сможете получить перечисление записей ZIP-файла:
```java
Enumeration<? extends ZipEntry> entries = zipFile.entries();
```
Затем вы можете циклически просматривать записи, используя цикл while:
```java
while (entries.hasMoreElements()) {
    ZipEntry entry = entries.nextElement();
    System.out.println("Entry Name: " + entry.getName());
    }
```
Не забудьте обработать потенциальное исключение IOException, которое может возникнуть при работе с ZipFile. Кроме того, не забудьте закрыть ZipFile, чтобы освободить все системные ресурсы, связанные с ним, когда вы закончите с ним.

#### Чтение содержимого [ZipEntry](ZipEntry)

Получение входных потоков для отдельных объектов [ZipEntry](ZipEntry) в ZIP-файле имеет решающее значение для чтения их содержимого. Класс java.util.zip.ZipFile предоставляет необходимые методы для доступа к этим записям.

Чтобы прочитать содержимое [ZipEntry](ZipEntry), вы должны сначала получить [InputStream](InputStream) для записи, используя метод getInputStream из ZipFile. Это позволяет считывать байты из записи точно так же, как и любой другой входной поток в Java.

Вот краткий пример того, как читать [ZipEntry](ZipEntry):
```java
import java.util.zip.ZipFile;
import java.util.zip.ZipEntry;
import java.io.InputStream;
import java.io.BufferedReader;
import java.io.InputStreamReader;

public class ZipEntryReader {
    public static void main(String[] args) {
        String zipFilePath = "path/to/your/zipfile.zip";
        String entryName = "example.txt"; // Name of the ZipEntry you want to read

        try (ZipFile zipFile = new ZipFile(zipFilePath)) {
            ZipEntry entry = zipFile.getEntry(entryName);
            if (entry != null) {
                try (InputStream stream = zipFile.getInputStream(entry);
                     BufferedReader reader = new BufferedReader(new InputStreamReader(stream))) {
                    String line;
                    while ((line = reader.readLine()) != null) {
                        System.out.println(line);
                    }
                }
            } else {
                System.out.println("Entry not found in the zip file");
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```
Вывод:
<p style="background-color: navy; color: yellow">
Boxes;50;1076;10<br>
Barbie;1500;2345;3<br>
Ken;1500;3257;4<br>
Teddy bear;500;8942;6<br>
stroller;5000;3268;7<br>
toy car;250;9921;9<br>
ABC book;100;3451;10<br>
Shoes;2500;8958;1<br>
Cradle;9500;7249;13<br>
Walkers;3500;2020;2</p>

В этом фрагменте вы открываете ZIP-файл и извлекаете [ZipEntry](ZipEntry) по его имени. Затем вы получаете [InputStream](InputStream) для записи и переносите его в [BufferedReader](BufferedReader) для чтения содержимого построчно.

Не забывайте правильно обрабатывать исключения, так как работа с операциями ввода-вывода может привести к различным ошибкам. Кроме того, убедитесь, что вы закрыли ZipFile и другие ресурсы ввода-вывода, чтобы предотвратить утечку ресурсов, что обычно достигается с помощью инструкции try-with-resources, как показано выше.

Оператор try-with-resources, представленный в Java 7, гарантирует, что каждый ресурс будет закрыт в конце инструкции. В этой конструкции может использоваться любой объект, реализующий java.lang.AutoCloseable или java.io.Closeable.
