#Java #FileOutputStream

### Запись файлов и класс FileOutputStream ###

2023-11-28 15:13

Класс FileOutputStream предназначен для записи байтов в файл. Он является производным от класса [OutputStream](OutputStream), поэтому наследует всю его функциональность.

Через конструктор класса FileOutputStream задается файл, в который производится запись. Класс поддерживает несколько конструкторов:
```java
FileOutputStream(String filePath)
FileOutputStream(File fileObj)
FileOutputStream(String filePath, boolean append)
FileOutputStream(File fileObj, boolean append)
```

Файл задается либо через строковый путь, либо через объект File. Второй параметр - append задает способ записи: eсли он равен true, то данные дозаписываются в конец файла, а при false - файл полностью перезаписывается

Например, запишем в файл строку:
```java
import java.io.*;
 
public class Program {
    public static void main(String[] args) {
        String text = "Hello world!"; // строка для записи
        try(FileOutputStream fos=new FileOutputStream("notes.txt"))
        {
            // перевод строки в байты
            byte[] buffer = text.getBytes();
              
            fos.write(buffer, 0, buffer.length);
            System.out.println("The file has been written");
        }
        catch(IOException ex){
            System.out.println(ex.getMessage());
        }
    }
}
```
Для создания объекта FileOutputStream используется конструктор, принимающий в качестве параметра путь к файлу для записи. Если такого файла нет, то он автоматически создается при записи. Так как здесь записываем строку, то ее надо сначала перевести в массив байтов. И с помощью метода write строка записывается в файл.

Для автоматического закрытия файла и освобождения ресурса объект FileOutputStream создается с помощью конструктции try...catch.

При этом необязательно записывать весь массив байтов. Используя перегрузку метода `write()`, можно записать и одиночный байт:
```java
fos.write(buffer[0]); // запись первого байта
```
