#Java #ZipEntry

### Класс ZipEntry

2024-01-19 12:06

С помощью класса **[ZipFile](ZipEntry)** можно получить список папок и файлов в архиве. Чтобы можно было производить с ними какие-то операции имеется класс **ZipEntry**.

В классе **ZipEntry** объявлены две константы:
```java
public static final int STORED;
public static final int DEFLATED;
```
Константа **STORED** означает, что файл был сохранен в архиве без компрессии, а константа **DEFLATED** означает, что файл был сохранен в архиве с компрессией.

С помощью следующего конструктора можно создавать новый элемент архива с заданным именем:
```java
public ZipEntry(String name);
```
В классе **ZipEntry** есть целое множество функций. Их можно разделить на две группы: функции для работы с атрибутами элемента и функции для извлечения элемента из архива.
Функции для работы с элементами архива:

|Функция|Описание|
|---|---|
|**public long getScr()**|Возвращает значение контрольной суммы элемента.|
|**public void setScr(long src)**|Изменяет значение контрольной суммы элемента на **src**.|
|**public int getMethod()**|Возвращает способ компрессии элемента: **STORED** или **DEFLATED**|
|**public void setMethod(int method)**|Устанавливает способ компрессии.|
|**public long getCompressedSize()**|Возвращает размер сжатого файла или значение -1, если этот размер не известен.|
|**public boolean isDirectory()**|Возвращает **true** если обозреваемый элемент является директорией, и **false** – в противном случае. Заметим, что для того чтобы создать в архиве папку нужно к имени элемента добавить в конце символ «/».|
|**public String getName()**|Позволяет узнать имя элемента. Заметим, что изменить имя элемента нельзя.|
|**public long getSize()**|Возвращает размер несжатого файла.|
|**public long getTime()**|Возвращает время модификации файла.|
Пример для получения информации о файлах архива. Путь к архиву передается через [командную строку](args).
```java
import java.io.File;
import java.io.IOException;
import java.util.ArrayList;
import java.util.Enumeration;
import java.util.List;
import java.util.zip.ZipEntry;
import java.util.zip.ZipFile;

/**
 * Программа для вывода информации о файлах, хранящихся в архиве
 * */
public class Main {
    /**
     * Вспомогательная функция для вывода заданного количества символа
     * @param c символ для вывода
     * @param count количество вывода символа
     * */
    private static void printCharacter(char c, int count) {
        for (int i = 0; i < count; i++) {
            System.out.print(c);
        }
    }

    /**
     * Вспомогательная функция для вывода разделителя строк
     * @param maxLengths Ширина каждой ячейки таблицы
     * */
    private static void printSeparator(int[] maxLengths) {
        System.out.print("+");
        for (int i = 0; i < 4; i++) {
            printCharacter('-', maxLengths[i]);
            System.out.print("+");
        }
        System.out.println();
    }

    /**
     * Функция для получения каждой записи в архиве
     * @param zipFile объект класса ZipFile - ссылка на архив
     * @return список записей архива
     * */
    private static List<ZipEntry> getZipEntries(ZipFile zipFile) {
        List<ZipEntry> zipEntries = new ArrayList<>();

        Enumeration enumeration = zipFile.entries();

        while (enumeration.hasMoreElements()) {
            ZipEntry entry = (ZipEntry) enumeration.nextElement();
            zipEntries.add(entry);
        }

        return zipEntries;
    }

    /**
     * Вспомогательная функция для расчета максимальной ширины каждого столбца
     * @param zipEntries список записей архива
     * @return массив значений ширины
     * */
    private static int[] getMaxLengths(List<ZipEntry> zipEntries) {
        int[] maxLengths = new int[4];

        maxLengths[0] = "name".length() + 2;
        maxLengths[1] = "type".length() + 2;
        maxLengths[2] = "size".length() + 2;
        maxLengths[3] = "compressed size".length() + 2;

        for (ZipEntry entry : zipEntries) {
            String name = entry.getName();
            String type = entry.isDirectory() ? "directory" : "file";
            String size = String.valueOf(entry.getSize());
            String compressedSize = String.valueOf(entry.getCompressedSize());

            maxLengths[0] = Math.max(maxLengths[0], name.length() + 2);
            maxLengths[1] = Math.max(maxLengths[1], type.length() + 2);
            maxLengths[2] = Math.max(maxLengths[2], size.length() + 2);
            maxLengths[3] = Math.max(maxLengths[3], compressedSize.length() + 2);
        }
        return maxLengths;
    }

    /**
     * Вспомогательная функция для вывода одной строки таблицы
     * @param tdValues значения, которые пишутся в ячейке строки
     * @param maxLengths максимальная ширина каждого столбца
     * */
    private static void printLine(String[] tdValues, int[] maxLengths) {
        System.out.print("|");
        for (int i = 0; i < tdValues.length; i++) {
            int sizeSpace = (maxLengths[i] - tdValues[i].length()) >> 1;
            printCharacter(' ', sizeSpace);
            System.out.print(tdValues[i]);
            printCharacter(' ', sizeSpace);
            if ((maxLengths[i] - tdValues[i].length()) % 2 != 0) {
                System.out.print(" ");
            }
            System.out.print("|");
        }
        System.out.println();
        printSeparator(maxLengths);
    }

    /**
     * Функция для вывода заголовка таблицы
     * @param maxLengths максимальная ширина каждого столбца
     * */
    private static void printCaptionTable(int[] maxLengths) {
        printSeparator(maxLengths);

        String[] tdValues = new String[4];
        tdValues[0] = "name";
        tdValues[1] = "type";
        tdValues[2] = "size";
        tdValues[3] = "compressed size";

        printLine(tdValues, maxLengths);
    }

    /**
     * Функция для вывода информаци о записи архива
     * @param entry запись архива
     * @param maxLengths максимальная ширина каждого столбца
     * */
    private static void printInfoZipEntry(ZipEntry entry, int[] maxLengths) {
        String[] tdValues = new String[4];
        tdValues[0] = entry.getName();
        tdValues[1] = (entry.isDirectory()) ? "directory" : "file";
        tdValues[2] = String.valueOf(entry.getSize());
        tdValues[3] = String.valueOf(entry.getCompressedSize());

        printLine(tdValues, maxLengths);
    }


    private static File file;

    /**
     * Функция для вывода информации о всех записях архива
     * */
    private static void printInfoZip() throws IOException {
        ZipFile zipFile = new ZipFile(file);

        List<ZipEntry> zipEntries = getZipEntries(zipFile);
        int[] maxLengths = getMaxLengths(zipEntries);

        zipFile.close();

        printCaptionTable(maxLengths);
        for (ZipEntry entry : zipEntries) {
            printInfoZipEntry(entry, maxLengths);
        }
    }

    /**
     * Функция для проверки аргументов командной строки
     * @param args аргументы командной строки
     * @return true, если мы корректно передали неообходимые аргументы, 
     *                                                     и false в противном случае
     * */
    private static boolean checkArgs(String[] args) {
        if (args.length == 0) {
            System.out.println("Введите путь к архиву");
            return false;
        }

        String pathname = args[0];
        file = new File(pathname);
        if (!file.exists()) {
            System.out.println("Файла не существует на диске");
            return false;
        }

        return true;
    }

    public static void main(String[] args) throws IOException {
        if (checkArgs(args)) {
            printInfoZip();
        }
    }
}
```
Вывод:
```
+-------------------------+------+------+-----------------+
|          name           | type | size | compressed size |
+-------------------------+------+------+-----------------+
|      function.cpp       | file | 4148 |      1109       |
+-------------------------+------+------+-----------------+
|        main.cpp         | file | 696  |       335       |
+-------------------------+------+------+-----------------+
|        sklad.txt        | file | 201  |       158       |
+-------------------------+------+------+-----------------+
|      TConteiner.h       | file | 1987 |       754       |
+-------------------------+------+------+-----------------+
| TProduct_TReceiptLine.h | file | 1260 |       447       |
+-------------------------+------+------+-----------------+
```

