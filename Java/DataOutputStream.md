#Java #DataOutputStream 
### Классы DataOutputStream ###

2023-11-29 15:40

Классы DataOutputStream позволяют записывать данные примитивных типов.
#### Запись данных и DataOutputStream ####

Класс DataOutputStream представляет поток вывода и предназначен для записи данных примитивных типов, таких, как int, double и т.д. Для записи каждого из примитивных типов предназначен свой метод:
- writeBoolean(boolean v) : записывает в поток булевое однобайтовое значение
- writeByte(int v): записывает в поток 1 байт, которые представлен в виде целочисленного значения
- writeChar(int v): записывает 2-байтовое значение char
- writeDouble(double v): записывает в поток 8-байтовое значение double
- writeFloat(float v): записывает в поток 4-байтовое значение float
- writeInt(int v): записывает в поток целочисленное значение int
- writeLong(long v): записывает в поток значение long
- writeShort(int v): записывает в поток значение short
- writeUTF(String str): записывает в поток строку в кодировке UTF-8

Класс [DataInputStream](DataInputStream) часто используется вместе с DataOutputStream.
Теперь давайте реализуем несколько из вышеперечисленных методов этого класса, которые обсуждались выше.
```java
// Java program to Demonstrate DataInputStream Class 
  
// Importing I/O classes 
import java.io.*; 
  
// Main class 
class DataInputStreamDemo { 
    // Main driver method 
    public static void main(String args[]) throws IOException { 
        // Writing the data 
        // Try block to check for exceptions 
        try ( DataOutputStream dout = 
                        new DataOutputStream(new FileOutputStream("file.dat")) ) { 
            dout.writeDouble(1.1); 
            dout.writeInt(55); 
            dout.writeBoolean(true); 
            dout.writeChar('4'); 
        } 
  
        // Catch block to handle the exceptions 
        catch (FileNotFoundException ex) { 
            // Display message when FileNotFoundException occurs 
            System.out.println("Cannot Open the Output File"); 
            return; 
        } 
  
        // Reading the data back. 
  
        // Try block to check for exceptions 
        try ( DataInputStream din = 
                        new DataInputStream(new FileInputStream("file.dat")) ) { 
            // Illustrating readDouble() method 
            double a = din.readDouble(); 
            // Illustrating readInt() method 
            int b = din.readInt(); 
            // Illustrating readBoolean() method 
            boolean c = din.readBoolean(); 
            // Illustrating readChar() method 
            char d = din.readChar(); 
            // Print the values 
            System.out.println("Values: " + a + " " + b + " " + c + " " + d); 
        } 
        // Catch block to handle the exceptions 
        catch (FileNotFoundException e) { 
            // Display message when FileNotFoundException occurs 
            System.out.println("Cannot Open the Input File"); 
            return; 
        } 
    } 
}



