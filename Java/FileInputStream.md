#Java #FileInputStream
### Чтение файлов и класс FileInputStream ###

2023-11-28 15:18

Для считывания данных из файла предназначен класс FileInputStream, который является наследником класса [InputStream](InputStream) и поэтому реализует все его методы.

Для создания объекта FileInputStream мы можем использовать ряд конструкторов. Наиболее используемая версия конструктора в качестве параметра принимает путь к считываемому файлу:
```java
FileInputStream(String fileName) throws FileNotFoundException
```
Если файл не может быть открыт, например, по указанному пути такого файла не существует, то генерируется исключение FileNotFoundException.

Считаем данные из ранее записанного файла и выведем на консоль:
```java
import java.io.*;
 
public class Program {
    public static void main(String[] args) {
        try(FileInputStream fin=new FileInputStream("notes.txt"))
        {    
            int i;
            while((i=fin.read())!=-1){
                System.out.print((char)i);
            }   
        }
        catch(IOException ex){
            System.out.println(ex.getMessage());
        } 
    }
}
```
В данном случае мы считываем каждый отдельный байт в переменную i:
```java
while((i=fin.read())!=-1){
```
Когда в потоке больше нет данных для чтения, метод возвращает число -1.

Затем каждый считанный байт конвертируется в объект типа char и выводится на консоль.

Подобным образом можно считать данные в массив байтов и затем производить с ним манипуляции:
```java
import java.io.*;
  
public class Program {
     public static void main(String[] args) {
        try(FileInputStream fin=new FileInputStream("notes.txt"))
        {
            byte[] buffer = new byte[256];
            System.out.println("File data:");
             
            int count;
            while((count=fin.read(buffer))!=-1){
                 for(int i=0; i<count;i++){
                    System.out.print((char)buffer[i]);
                }
            }   
        }
        catch(IOException ex){
            System.out.println(ex.getMessage());
        } 
    }
}
```
В данном случае с помощью метода `read()` считываем данные в массив buffer длиной 256 байтов. Метод возвращает количество считанных байтов.

Поскольк файл может быть больше 256 байтов, то считываем в цикле while до конца файла. Когда больше не останется файлов для считывания, то метод возвратит -1.
```java
while((count=fin.read(buffer))!=-1){
```
Поскольку количество считанных байтов/размер файла могут быть меньше 256 байт, то реальное количество считанных байт сохраняем в переменную count. Затем выводим считанное количество данных на консоль в цикле for.
```java
for(int i=0; i<count;i++){
    System.out.print((char)buffer[i]);
}
```
Совместим классов оба класса ([FileOutputStream](FileOutputStream), FileInputStream) и выполним чтение из одного и запись в другой файл:
```java
import java.io.*;
  
public class Program {
  
    public static void main(String[] args) {
          
        try(FileInputStream fin=new FileInputStream("notes.txt");
                FileOutputStream fos=new FileOutputStream("notes_new.txt"))
        {
            byte[] buffer = new byte[256];
             
            int count;
            // считываем буфер
            while((count=fin.read(buffer))!=-1){
               
                // записываем из буфера в файл
                fos.write(buffer, 0, count);
            }
            System.out.println("File has been written");
        }
        catch(IOException ex){
              
            System.out.println(ex.getMessage());
        } 
    } 
}
```
Классы FileInputStream и [FileOutputStream](FileOutputStream), предназначены прежде всего для записи двоичных файлов, то есть для записи и чтения байтов. И хотя они также могут использоваться для работы с текстовыми файлами, но все же для этой задачи больше подходят другие классы.