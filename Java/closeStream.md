#Java #JavaIO

## Закрытие потоков

2024-04-04 12:16

При завершении работы с [потоком JavaIO](JavaIO) его надо закрыть с помощью метода close(), который определен в интерфейсе [Closeable](Closeable). Метод close имеет следующее определение:
```java
void close() throws IOException
```
Этот интерфейс уже реализуется в классах [InputStream](InputStream) и [OutputStream](OutputStream), а через них и во всех классах потоков.

При закрытии потока освобождаются все выделенные для него ресурсы, например, файл. В случае, если поток окажется не закрыт, может происходить утечка памяти.

Есть два способа закрытия файла. Первый традиционный заключается в использовании блока [try..catch..finally](Exceptions). Например, считаем данные из файла:
```java
import java.io.*;
 
public class Program {
    public static void main(String[] args) {
        FileInputStream fin=null;
        
        try {
            fin = new FileInputStream("C://SomeDir//notes.txt");
            int i=-1;
            while((i=fin.read())!=-1) {
                System.out.print((char)i);
            }
        }
        catch(IOException ex) {             
            System.out.println(ex.getMessage());
        } 
        finally {
            try {
                if(fin!=null)
                    fin.close();
            }
            catch(IOException ex) {
                System.out.println(ex.getMessage());
            }
        }  
    } 
}
```
Поскольку при открытии или считывании файла может произойти ошибка ввода-вывода, то код считывания помещается в блок try. И чтобы быть уверенным, что поток в любом случае закроется, даже если при работе с ним возникнет ошибка, вызов метода `close()` помещается в блок `finally`. И, так как метод `close()` также в случае ошибки может генерировать исключение IOException, то его вызов также помещается во вложенный блок `try..catch`

Начиная с Java 7 можно использовать еще один способ, который автоматически вызывает метод close. Этот способ заключается в использовании конструкции [try-with-resources (try-с-ресурсами)](try-with-resources). Данная конструкция работает с объектами, которые реализуют интерфейс [AutoCloseable](Closeable). Так как все классы потоков реализуют интерфейс [Closeable](Closeable), который в свою очередь наследуется от `AutoCloseable`, то их также можно использовать в данной конструкции

Итак, перепишем предыдущий пример с использованием конструкции try-with-resources:
```java
import java.io.*;
 
public class Program {
    public static void main(String[] args) {
        try(FileInputStream fin=new FileInputStream("C://SomeDir//notes.txt")) {
            int i=-1;
            while((i=fin.read())!=-1){
                System.out.print((char)i);
            }   
        }
        catch(IOException ex) {
            System.out.println(ex.getMessage());
        } 
    } 
}
```
Синтаксис конструкции следующий: `try(название_класса имя_переменной = конструктор_класса)`. Данная конструкция также не исключает использования блоков catch.

После окончания работы в блоке try у ресурса (в данном случае у объекта [FileInputStream](FileInputStream)) автоматически вызывается метод close().

Если нам надо использовать несколько потоков, которые после выполнения надо закрыть, то мы можем указать объекты потоков через точку с запятой:
```java
try(FileInputStream fin=new FileInputStream("C://SomeDir//Hello.txt"); 
        FileOutputStream fos = new FileOutputStream("C://SomeDir//Hello2.txt"))
{
    //..................
}
```