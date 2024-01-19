#Java #ZipInputStream
### Класс Java.util.zip.ZipInputStream в Java

2024-01-19 15:01

Этот класс реализует фильтр входного потока для чтения файлов в формате ZIP. Включает поддержку как сжатых, так и несжатых записей.  

**Конструкторы:**
- **ZipInputStream(InputStream in) :** Создает новый входной поток ZIP.
- **ZipInputStream(InputStream in, Charset charset) :** Создает новый входной поток ZIP

#### Методы

- int available():** возвращает 0 после достижения EOF для текущих входных данных, в противном случае всегда возвращает значение .  Программы не должны рассчитывать, что этот метод вернет фактическое количество байтов, которые могут быть прочитаны без блокировки.
  
	**Syntax:** public int available() throws IOException
    **Overrides:** available in class InflaterInputStream
    **Returns:** 1 перед EOF и 0 после достижения EOF для текущей записи. Программы не должны рассчитывать на то, что этот метод вернет фактическое количество байтов, которые можно было бы прочитать без блокировки.
    **Throws:** IOException

- **void close() :** закрывает этот входной поток и освобождает все системные ресурсы, связанные с потоком.
    
    **Syntax:** public void close() throws IOException
    **Overrides:** close in class InflaterInputStream
    **Throws:** IOException

- **void closeEntry():** закрывает текущую запись ZIP и позиционирует поток для чтения следующей записи.
    
    **Syntax:** public void closeEntry() throws IOException
    **Throws:** ZipException,IOException

- **protected ZipEntry createZipEntry(String name):** Создает новый объект ZipEntry для указанного имени записи.
    
    **Syntax:** protected ZipEntry createZipEntry(String name)
    **Parameters:** name - имя записи в ZIP-файле
    **Returns:** только что созданный ZipEntry

- **ZipEntry getNextEntry() :** Считывает следующую запись ZIP-файла и помещает поток в начало входных данных.
    
    **Syntax:** public ZipEntry getNextEntry() throws IOException
    **Returns:** следующая запись в ZIP-файле или null, если записей больше нет
    **Throws:** ZipException, IOException

- **int read(byte[] b, int off, int len) :** Считывает текущую запись ZIP в массив байтов. Если len не равен нулю, метод блокируется до тех пор, пока не будут доступны какие-либо входные данные; в противном случае байты не считываются и возвращается 0.
    
    **Syntax:** public int read(byte[] b, int off, int len) throws IOException
    **Parameters:** b - буфер, в который считываются данные
			off - начальное смещение в целевом массиве b
			len - максимальное количество прочитанных байт
    **Returns:** фактическое количество прочитанных байт или -1, если достигнут конец записи
    **Throws:** NullPointerException, IndexOutOfBoundsException, ZipException, IOException

- **public long skip(long n):** пропускает указанное количество байтов в текущей записи ZIP.
    
    **Syntax:**public long skip(long n) throws IOException
    **Parameters:** n - количество байтов, которые нужно пропустить
    **Returns:** фактическое количество пропущенных байт
    **Throws:** ZipException, IOException, IllegalArgumentException

##### Пример 1. Java-программа, демонстрирующая методы ZipInputStream 

```java
import java.io.FileInputStream; 
import java.io.IOException; 
import java.io.InputStream; 
import java.util.Arrays; 
import java.util.jar.JarInputStream; 
import java.util.zip.ZipEntry; 
import java.util.zip.ZipInputStream; 
class ZipInputStreamDemo extends ZipInputStream { 
    public ZipInputStreamDemo(InputStream in) { 
        super(in); 
    } 
  
    public static void main(String[] args) throws IOException { 
        FileInputStream fis = new FileInputStream("test.zip"); 
        ZipInputStream zis = new JarInputStream(fis); 
        ZipInputStreamDemo obj = new ZipInputStreamDemo(zis); 
        //illustrating createZipEntry() 
        ZipEntry ze = obj.createZipEntry("ZipEntry"); 
        System.out.println(ze.getName()); 
        //illustrating getNextEntry() 
        ZipEntry je = zis.getNextEntry(); 
        System.out.println(je.getName()); 
        //illustrating skip() method 
        zis.skip(3); 
        //illustrating closeEntry() method 
        zis.closeEntry(); 
        zis.getNextEntry(); 
        byte b[] = new byte[10]; 
        //illustrating available() method 
        //Reads up to byte.length bytes of data from this input stream 
        if(zis.available() == 1) 
            zis.read(b); 
        System.out.println(Arrays.toString(b)); 
        //closing the stream 
        zis.close(); 
    } 
} 
```
Вывод:
<p style="background-color: navy; color: yellow">
ZipEntry<br>
function.cpp<br>
[35, 105, 110, 99, 108, 117, 100, 101, 32, 60]</p>

##### Пример 2.  Java-программа для разархивирования. 

Имя архива и путь до целевой папки передаются через [аргументы командной строки](args).
Для того чтобы полностью извлечь файл, нужно скопировать его содержимое из архива в созданный файл в целевой папке. Для этого используют функцию **getInputStream()** у объекта типа **[ZipFile](ZipFile)**.
cd onedrive```java
import java.io.*;
import java.util.Enumeration;
import java.util.zip.ZipEntry;
import java.util.zip.ZipFile;

public class Main {
    private static File src;
    private static File dest;

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
     * Функция для разархивирования архива
     * */
    private static void extract() throws IOException {
        /*Создаем ссылку на наш архив*/
        ZipFile zipFile = new ZipFile(src.getPath());
        /*Получаем список его записей*/
        Enumeration entries = zipFile.entries();

        /*Пока мы не просмотрим все записи*/
        while (entries.hasMoreElements()) {
            /*Получим очередную запись*/
            ZipEntry entry = (ZipEntry) entries.nextElement();
            /*Выведем ее имя*/
            System.out.print("name: " + entry.getName());

            /*Если наща запись это файл*/
            if (!entry.isDirectory()) {
                /*
                  то нужно перед распаковкой создать весь путь с учетом путей в архиве
                  (мы должны распаковывать в файл, с тем же путем что в записи).
                  Поэтому нужно создать все папки на пути до корневой папки
                */

                /*создади ссылку на наш будущий файл*/
                File file = new File(entry.getName());

                /*Создадим все несуществующие папки*/
                File dir = new File(dest.getAbsolutePath() + "/" + file.getParent());
                dir.mkdirs();

                /*
                  Скопируем все содержимое из файла в архиве в результирующий файл.
                  Для это воспользуемся функцией getInputStream(entry) 
                                                            и функцией write(in, out).
                */
                File dest = new File(dir, file.getName());
                try (
                        InputStream in = zipFile.getInputStream(entry);
                        OutputStream out = new FileOutputStream(dest)
                ) {
                    write(in, out);
                }

            } else {
                /*Если рассматриваемая запись это папка, то нужно просто создать 
                                                  все папки на пути от этой до корня*/
                File dir = new File(dest.getAbsolutePath() + "/" + entry.getName());
                dir.mkdirs();
            }
            System.out.println(" ------- OK");
        }

        /*После работы с архивом обязательно его закроем*/
        zipFile.close();
    }

    /**
     * Функция для проверки аргументов командной строки
     * @param args аргументы командной строки
     * @return true, если мы корректно передали неообходимые аргументы, 
     *                                                     и false в противном случае
     * */
    private static boolean checkArgs(String[] args) {
        /*Проверяем что программе переданны не пути*/
        if (args.length < 2) {
            System.out.println("Введите путь к архиву и путь для распаковки");
            return false;
        }

        String zipName = args[0];
        src = new File(zipName);
        if (!src.exists()) {
            System.out.println("Заданный архив не существует");
            return false;
        }

        String destName = args[1];
        dest = new File(destName);
        if (!dest.exists()) {
            System.out.println("Задан несуществующий путь для разархивирования");
            return false;
        }

        return true;
    }

    public static void main(String[] args) throws IOException {
        if (checkArgs(args)) {
            System.out.println("start extraction");
            extract();
            System.out.println("end extraction");
        }
    }
}
```
Вывод:
<p style="background-color: navy; color: yellow">
start extraction<br>
name: function.cpp ------- OK<br>
name: main.cpp ------- OK<br>
name: sklad.txt ------- OK<br>
name: TConteiner.h ------- OK<br>
name: TProduct_TReceiptLine.h ------- OK<br>
end extraction</p>
