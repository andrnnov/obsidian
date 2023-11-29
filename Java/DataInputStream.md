#Java #DataInputStream 
### Класс DataInputStream ###

2023-11-29 11:02

Класс DataInputStream позволяют считывать данные примитивных типов.
#### Считывание данных и DataInputStream ####

Класс DataInputStream действует противоположным образом - он считывает из потока данные примитивных типов. Соответственно для каждого примитивного типа определен свой метод для считывания:
- boolean readBoolean(): считывает из потока булевое однобайтовое значение
- byte readByte(): считывает из потока 1 байт
- char readChar(): считывает из потока значение char
- double readDouble(): считывает из потока 8-байтовое значение double
- float readFloat(): считывает из потока 4-байтовое значение float
- int readInt(): считывает из потока целочисленное значение int
- long readLong(): считывает из потока значение long
- short readShort(): считывает значение short
- String readUTF(): считывает из потока строку в кодировке UTF-8
- int skipBytes(int n): пропускает при чтении из потока n байтов

Рассмотрим применение класса на примере:
```java
import java.io.*;
 
public class Program {
    public static void main(String[] args) {
        Person tom = new Person("Tom", 34, 1.68, false);
        // запись в файл
        try(DataOutputStream dos = new DataOutputStream(new FileOutputStream("data.bin")))
        {
           // записываем значения
            dos.writeUTF(tom.name);
            dos.writeInt(tom.age);
            dos.writeDouble(tom.height);
            dos.writeBoolean(tom.married);
            System.out.println("File has been written");
        }
        catch(IOException ex){
            System.out.println(ex.getMessage());
        }  
          
        // обратное считывание из файла
        try(DataInputStream dos = new DataInputStream(new FileInputStream("data.bin")))
        {
           // записываем значения
            String name = dos.readUTF();
            int age = dos.readInt();
            double height = dos.readDouble();
            boolean married = dos.readBoolean();
            System.out.printf("Name: %s  Age: %d  Height: %f  Married: %b", 
                    name, age, height, married);
        }
        catch(IOException ex){
            System.out.println(ex.getMessage());
        }  
    } 
}
  
class Person
{
    public String name;
    public int age;
    public double height;
    public boolean married;
      
    public Person(String n, int a, double h, boolean m)
    {
        this.name=n;
        this.height=h;
        this.age=a;
        this.married=m;
    }
}
```
Здесь мы последовательно записываем в файл данные объекта Person.

Объект [DataOutputStream](DataOutputStream) в конструкторе принимает поток вывода: `DataOutputStream (OutputStream out)`. В данном случае в качестве потока вывода используется объект [FileOutputStream](FileOutputStream), поэтому вывод будет происходить в файл. И с помощью выше рассмотренных методов типа `writeUTF()` производится запись значений в бинарный файл.

Затем происходит чтение ранее записанных данных. Объект DataInputStream в конструкторе принимает поток для чтения: `DataInputStream(InputStream in)`. Здесь таким потоком выступает объект [`FileInputStream`](FileInputStream).
