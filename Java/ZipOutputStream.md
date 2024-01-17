#Java #ZipOutputStream
### Класс Java.util.zip.ZipOutputStream в Java 

2024-01-17 15:24

Этот класс реализует фильтр выходного потока для записи файлов в формате ZIP. Включает поддержку как сжатых, так и несжатых записей.  

**Конструктор:**
- **ZipOutputStream (выходной поток out) :** Создает новый поток вывода ZIP.
- **ZipOutputStream (вывод выходного потока, Charset charset) :** Создает новый поток вывода ZIP.

Каждый из них первым аргументом принимает поток, в который мы будем архивировать файлы. Чаще всего в качестве потока используют объект класса **FileOutputStream**. Второй конструктор дополнительно вторым аргументом принимает кодировку, в которой будут сохранятся имена файлов в архив.

Перед началом архивирования можно указать уровень компрессии. Уровень компрессии — это число от 0 до 9. Задать уровень компресии можно с помощью функции **setLevel** объекта **ZipOutputSream**. По умолчанию используется уровень, равный следующему значению: **Deflater.DEFAULT_COMPRESSION**.

После того как установлен уровень компрессии можно приступать к самому архивированию. Для того чтобы добавить файл или папку в архив, нужно создать объект класса **ZipEntry**. Потом вызвать функцию **putNextEntry**, которой передается объект класса **ZipEntry**. Например, это можно сделать так:
```java
ZipEntry ze = new ZipEntry(nameEntry);
out.putNextEntry(ze);
```
После вызова функции **putNextEntry()** будет создана запись в архиве. Но сам файл еще не будет заархивирован. Для этого нужно скопировать все содержимое этого файла в поток **ZipOutputStream**. Это можно сделать, написав следующую вспомогательную функцию:
```java
void write(InputStream in, OutputStream out) throws IOException {
    byte[] buffer = new byte[1024];
    while (in.read(buffer) != -1) {
        out.write(buffer);
    }
}
```
Это классический прием копирования данных из входного потока в выходной поток.

Пусть у нас есть переменная **file**, которая ссылается на файл в папке. Тогда скопировать содержимое этого файла в архив можно следующим образом:
```java
out.putNextEntry(new ZipEntry(file.getPath()));
try (InputStream in = new FileInputStream(file)) {
    write(in, out);
}
out.closeEntry();
```
Обратим внимание на вызов функции **closeEntry()**. Этот вызов необходим для корректного добавления записи в архив.

Заметим, что с помощью такого куска кода можно заархивировать либо файл, либо папку, но без ее содержимого. Для того чтобы заархивировать содержимое папки можно поступить следующим образом: создать объект класса **File**, который будет ссылаться на папку. Вызвать у этого объекта функцию **listFiles()** (напомним, эта функция возвращает список объектов **File**, ссылающиехся на содержимое папки). Потом циклом пройтись по всем этим объектам и каждый заархивировать. Если в исходной папке есть подпапки, то нужно вызвать функцию архивирования рекурсивно для подпапки.

При архивировании пустой папки есть одна особенность вызова функции **putNextEntry()**. Для того чтобы добавить в архив пункт, являющийся папкой, нужно к имени папки добавить в конце символ “/”.

#### Методы: 

- **void close() :** закрывает выходной поток ZIP, а также фильтруемый поток.
```
Syntax: public void close() throws IOException
Overrides: close in class DeflaterOutputStream
Throws: ZipException, IOException
```
- **void closeEntry() :** закрывает текущую запись ZIP и позиционирует поток для записи следующей записи.
```
Syntax :public void closeEntry() throws IOException
Throws: ZipException, IOException
```
- **void finish() :** завершает запись содержимого выходного потока ZIP без закрытия базового потока. Используйте этот метод при последовательном применении нескольких фильтров к одному и тому же выходному потоку.
```
Syntax:public void finish() throws IOException
Overrides: finish in class DeflaterOutputStream
Throws: ZipException, IOException
```
- **void putNextEntry(ZipEntry e):** начинает запись новой записи ZIP-файла и помещает поток в начало входных данных. Закрывает текущую запись, если она все еще активна. Метод сжатия по умолчанию будет использоваться, если для записи не был указан метод сжатия, и текущее время будет использоваться, если для записи не установлено время модификации.
```
Syntax: public void putNextEntry(ZipEntry e) throws IOException
Parameters: e - the ZIP entry to be written
Throws: ZipException, IOException
```
- **void setComment(String comment):** задает комментарий к ZIP-файлу.
```
Syntax: public void setComment(String comment)
Parameters: comment - the comment string
Throws: IllegalArgumentException
```
- **void setLevel(int level) :** устанавливает уровень сжатия для последующих записей, которые будут DEFLATED. Значение по умолчанию - DEFAULT_COMPRESSION .
```
Syntax: public void setLevel(int level)
Parameters: level - the compression level (0-9)
Throws: IllegalArgumentException
```
- **void setMethod(int method) :** Устанавливает метод сжатия по умолчанию для последующих записей. Это значение по умолчанию будет использоваться всякий раз, когда метод сжатия не указан для отдельной записи ZIP-файла и изначально имеет значение DEFLATED.
```
Syntax: public void setMethod(int method)
Parameters: method - the default compression method
Throws: IllegalArgumentException
```
- **void write(byte[] b, int off, int len)**: записывает массив байтов в текущие данные записи ZIP. Этот метод будет блокироваться до тех пор, пока не будут записаны все байты.
```
Syntax: public void write(byte[] b, int off, int len)
Parameters: b - the data to be written
		    off - the start offset in the data
		    len - the number of bytes that are written
Throws: ZipException, IOException
```

##### Пример 1 #####

Пример программы, которая архивирует файл или папку в указанный архив. Источник архивации и название архива передаются программы через аргументы командной строки.
```java
import java.io.*;
import java.util.zip.ZipEntry;
import java.util.zip.ZipOutputStream;

/**
 * Пример использования класса ZipOutputStream
 * */
public class Main {
    /*Объект класса File хранит ссылку на файл или папку, которую мы хотим 
                                                                   заархивировать*/
    private static File srcObject;

    /*Объект класса File хранит ссылку на zip файл, вкоторый мы хотим архивировать*/
    private static File destFile;

    /*Вспомогательная переменная для удаления из полного пути всех файлов при 
                                                                   архивировании*/
    private static String prefixObject;

    /**
     * Вспомогательная функция для копирования байтов из одного потока в другой
     * @param in поток ввода
     * @param out поток вывода
     * */
    private static void write(InputStream in, OutputStream out) throws IOException {
        byte[] buffer = new byte[1024];
        while (in.read(buffer) != -1) {
            out.write(buffer);
        }
    }

    /**
     * Функция для проверки аргументов командной строки
     * @param args аргументы командной строки
     * @return true, если мы корректно передали неообходимые аргументы, 
     *                                                     и false в противном случае
     * */
    private static boolean checkArgs(String[] args) {
        if (args.length < 2) {
            System.out.println("Введите путь к папке/файлу и путь к архиву");
            return false;
        }

        String srcName = args[0];

        srcObject = new File(srcName);
        if (!srcObject.exists()) {
            System.out.println("Источник для архивирования не существует на диске");
            return false;
        }

        String destName = args[1];
        destFile = new File(destName);
        File destParentDirectory = new File(destFile.getParent());
        if (!destParentDirectory.exists()) {
            System.out.println("Папка для сохранения архива не существует");
            return false;
        }

        return true;
    }

    /**
     * Вспомогательная функция проверки на пустоту директории
     * @param directory директория
     * @return true если папка пуста, и false в противном случае
     * */
    private static boolean isEmptyDirectory(File directory) {
        return directory.list().length == 0;
    }

    /**
     * Функция для добавления в архив файла
     * @param src файл, который хотим заархивировать
     * @param out поток для добавления в архив записи
     * @param entryName имя записи в архиве
     * */
    private static void toArchiveTheFile(File src, ZipOutputStream out, 
                                               String entryName) throws IOException {
        /*Добавляем новую запись в архиве*/
        out.putNextEntry(new ZipEntry(entryName));
        /*Копируем содержимое файла в поток архива*/
        try (InputStream in = new FileInputStream(src)) {
            write(in, out);
        }
        /*Закрываем запись в архиве*/
        out.closeEntry();
    }

    /**
     * Функция для архивирования папки со всей ее иерархией
     * @param src ссылка на директорию, которую хотим заархивировать
     * @param out поток для архивации
     * */
    private static void arhive(File src, ZipOutputStream out) throws IOException {
        /*Просматриваем каждый файл и папку в заданной папке*/
        for (File object : src.listFiles()) {
            /*Отбрасываем ненужные папки в пути для задания имени записи в архиве*/
            String entryName = object.getPath().substring(prefixObject.length() + 1);

            /*Если объект это папка*/
            if (object.isDirectory()) {
                /*либо она пустая либо нет*/
                if (isEmptyDirectory(object)) {
                    /*Если пустая, то нужно просто создать запись в архиве*/
                    System.out.print("name: " + entryName);
                    out.putNextEntry(new ZipEntry(entryName + "/"));
                    out.closeEntry();
                    System.out.println(" ------ OK");
                } else {
                  /*если папка не пустая, то мы вызываемся рекурсивно на этой папке*/
                    arhive(object, out);
                }
            } else {
                /*
                  Если рассматриваемый объект это файл, то нужно его заархивировать.
                  Для этого мы используем функцию toArchiveTheFile
                */
                System.out.print("name: " + entryName);
                toArchiveTheFile(object, out, entryName);
                System.out.println(" ------ OK");
            }
        }
    }

    public static void main(String[] args) throws IOException {
        /*Проверяем аргументы командной строки*/
        if (checkArgs(args)) {
            System.out.println("start arhiving...");
          
          /*отбрасываем все папки в пути до корня от нашего рассматриваемого объекта*/
            prefixObject = srcObject.getParent();

            /*Создаем поток для архивирования*/
            ZipOutputStream out = new ZipOutputStream(new FileOutputStream(destFile));
            /*Если мы захотели заархивироваться один файл*/
            if (srcObject.isFile()) {
                /*то просто его заархивируем*/
                String fileName = srcObject
                                      .getPath() 
                                      .substring(prefixObject.length() + 1);

                toArchiveTheFile(srcObject, out, fileName);
                System.out.println(" ------ OK");
            } else if (isEmptyDirectory(srcObject)) { 
                /*Если мы хотим заархивировать пустую папку*/
                /*То просто создадим запись в архиве*/
                out.putNextEntry(new ZipEntry(srcObject.getName() + "/"));
                out.closeEntry();
            } else {
                /*Если мы хотим заархивировать не пустую папку, 
                              то воспользуемся функцией arhive для архивации папки*/
                arhive(srcObject, out);
            }
            out.close();
            System.out.println("end arhiving.");
        }
    }
}
```

##### Пример 2 #####

```java
//Java program demonstrating ZipOutputStream methods 
import java.io.FileInputStream; 
import java.io.FileOutputStream; 
import java.io.IOException; 
import java.util.Arrays; 
import java.util.zip.ZipEntry; 
import java.util.zip.ZipInputStream; 
import java.util.zip.ZipOutputStream; 
  
class ZipOutputStreamDemo { 
    public static void main(String[] args) throws IOException { 
    FileOutputStream fos = new FileOutputStream("zipfile"); 
        ZipOutputStream zos = new ZipOutputStream(fos); 
        //illustrating setMethod() 
        zos.setMethod(8); 
        //illustrating setLevel method 
        zos.setLevel(5);
        ZipEntry ze1 = new ZipEntry("ZipEntry1"); 
        //illustrating putNextEntry method 
        zos.putNextEntry(ze1); 
        //illustrating setComment 
        zos.setComment("This is my first comment");
        //illustrating write() 
        for(int i = 0; i < 10; i++) 
            zos.write(i); 
        //illustrating write(byte b[], int off, int len) 
        byte b[] = { 11, 12, 13}; 
        zos.write(b); 
        //illustrating closeEntry() 
        zos.closeEntry();
        //Finishes writing the contents of the ZIP output stream 
        // without closing the underlying stream 
        zos.finish(); 
        //closing the stream 
        zos.close(); 
        FileInputStream fin = new FileInputStream("zipfile"); 
        ZipInputStream zin = new ZipInputStream(fin); 
        //Reads the next ZIP file entry 
        ZipEntry ze = zin.getNextEntry(); 
        //the name of the entry. 
        System.out.println(ze.getName()); 
        //illustrating getMethod 
        System.out.println(ze.getMethod()); 
        //Reads up to byte.length bytes of data from this input stream 
        // into an array of bytes. 
        byte c[] = new byte[13]; 
        if(zin.available() == 1) 
            zin.read(c); 
        System.out.print(Arrays.toString(c)); 
        //closes the current ZIP entry 
        zin.closeEntry(); 
        //closing the stream 
        zin.close();
    } 
} 
```

##### Пример 3 #####

```java
import java.io.*;
import java.util.zip.*;
  
public class Program {
    public static void main(String[] args) {
        String filename = "notes.txt";
        try(ZipOutputStream zout = new ZipOutputStream(new FileOutputStream("output.zip"));
                FileInputStream fis= new FileInputStream(filename);)
        {
            ZipEntry entry1=new ZipEntry("notes.txt");
            zout.putNextEntry(entry1);
            // считываем содержимое файла в массив byte
            byte[] buffer = new byte[fis.available()];
            fis.read(buffer);
            // добавляем содержимое к архиву
            zout.write(buffer);
            // закрываем текущую запись для новой записи
            zout.closeEntry();
        }
        catch(Exception ex){
	        System.out.println(ex.getMessage());
        } 
    } 
}