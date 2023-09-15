###  Считывание с клавиатуры — «ридеры» ###

#Java #BufferedReader

2023-09-05 16:49

```java
BufferedReader reader = new BufferedReader(new InputStreamReader(System.in));
```

`System.in` — это объект класса `InputStream`. Это входящий поток, и он привязан к системному устройству ввода данных — клавиатуре.

`System.out` — поток для отправки данных на консоль, а `System.in` — для получения данных с клавиатуры.

В классе `InputStream` (а `System.in`, напомню, является объектом класса `InputStream`) есть метод `read()`, который позволяет считывать данные. Одна проблема: он считывает байты, а не символы. 

```java
public class Main {

   public static void main(String[] args) throws IOException {

       while (true) {
           int x = System.in.read();
           System.out.println(x);
       }
   }
}
```

Мы передаем поток `System.in` объекту `InputStreamReader`.

```java
new InputStreamReader(System.in)
```

`InputStreamReader` не только получает данные из потока. Он еще и преобразует байтовые потоки в символьные. Иными словами, тебе уже не нужно самому заботиться о переводе считанных данных с “компьютерного” языка на “человеческий” — `InputStreamReader` сделает все за тебя.

```java
import java.io.FileInputStream;
import java.io.IOException;
import java.io.InputStreamReader;

public class Main {

   public static void main(String[] args) throws IOException {
       InputStreamReader inputStreamReader = new InputStreamReader(new FileInputStream("C:\\Users\\username\\Desktop\\testFile.txt"));
   }
}
```

[**`BufferedReader`**](BufferedReader) при считывании данных использует специальную область — буфер, куда “складывает” прочитанные символы. В итоге, когда эти символы понадобятся нам в программе — они будут взяты из буфера, а не напрямую из источника данных (клавиатуры, файла и т.п.), а это экономит очень много ресурсов.
Главный плюс в том, что `BufferedReader` умеет читать данные не только по одному символу (хотя метод `read()` для этих целей у него тоже есть), а еще и целыми строками! Делается это с помощью метода `readLine()`.

```java
public class Main {

   public static void main(String[] args) throws IOException {

       BufferedReader reader = new BufferedReader(new InputStreamReader(System.in));
       String s = reader.readLine();
       System.out.println("Мы считали с клавиатуры эту строку:");
       System.out.println(s);
   }
}
```

