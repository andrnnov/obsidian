#Java #Networking #URL

## [Класс URL](https://www.geeksforgeeks.org/url-class-java-examples/)

2024-08-07 15:53

**_URL_** (Uniform Resource Locator), представляет собой просто текстовую строку, которая идентифицирует все ресурсы в Интернете, сообщая нам адрес ресурса, способы связи с ним и извлечения чего-либо из него.
![[URL-Class.png]]
URL может иметь множество форм. Однако в наиболее общем виде используется трехкомпонентная система, предложенная ниже:

1. **Протокол:** здесь используется HTTP
2. **Имя хоста:** имя компьютера, на котором находится ресурс.
3. **Имя файла:** путь к файлу на компьютере.
4. **Номер порта:** номер порта, к которому нужно подключиться (обычно необязательно).

### Класс URL

Класс **_URL_** является шлюзом к любому из ресурсов, доступных в Интернете. **_URL_** класса представляет собой единый указатель ресурсов, который является указателем на “ресурс” во Всемирной паутине. Ресурс может указывать на простой файл или каталог, или он может ссылаться на более сложный объект, такой как запрос к базе данных или поисковой системе.

### Конструкторы класса URL

1. **URL(String address) throws MalformedURLException:** он создает объект URL из указанной строки.
2. **URL(String protocol, String host, String file):** Создает объект URL на основе указанного протокола, хоста и имени файла.
3. **URL (String protocol, String host, int port, String file):** Создает объект URL на основе протокола, хоста, порта и имени файла.
4. **URL(URL context, String spec):** Создает объект URL путем синтаксического анализа данной спецификации в заданном контексте.
5. **URL(String protocol, String host, int port, String file, URLStreamHandler handler):**  
    Создает объект URL на основе указанного протокола, хоста, номера порта, файла и обработчика.
6. **URL(URL context, String spec, URLStreamHandler handler):** 
    Создает URL-адрес путем синтаксического анализа данной спецификации с помощью указанного обработчика в указанном контексте.

### Важные методы, используемые в классе URL

| Метод            | Выполнено действие                                                                                                                                                                                |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| getAuthority()   | Возвращает авторитетную часть URL или null, если она пуста                                                                                                                                        |
| getDefaultPort() | Возвращает используемый порт по умолчанию                                                                                                                                                         |
| GetFile()        | Возвращает имя файла.                                                                                                                                                                             |
| getHost()        | Возвращает имя хоста URL в формате IPv6                                                                                                                                                           |
| getPath()        | Возвращает путь к URL-адресу или null, если он пустой                                                                                                                                             |
| getPort()        | Возвращает порт, связанный с протоколом, указанным в URL                                                                                                                                          |
| getProtocol()    | Возвращает протокол, используемый URL                                                                                                                                                             |
| getQuery()       | возвращает часть запроса URL. Запрос - это часть после ‘?’ в URL. Всякий раз, когда для отображения результата используется логика, в URL будет поле запроса. Это похоже на запрос к базе данных. |
| GetRef()         | Возвращает ссылку на объект URL. Обычно ссылкой является часть, отмеченная ‘#’ в URL. Вы можете просмотреть рабочий пример, запросив что-либо в Google и увидев часть после ‘#’                   |
| toString()       | Как и в любом классе, toString() возвращает строковое представление данного объекта URL.                                                                                                          |
#### Пример 1

```java
// Java program to demonstrate working of URL 
  
// Importing required classes 
import java.net.MalformedURLException; 
import java.net.URL; 
  
// Main class 
// URL class 
public class Main { 
  
    // Main driver method 
    public static void main(String[] args) throws MalformedURLException { 
        // Creating a URL with string representation 
        URL url1 = new URL( 
            "https://www.google.co.in/?gfe_rd=cr&ei=ptYq"
            + "WK26I4fT8gfth6CACg#q=geeks+for+geeks+java"); 
        // Creating a URL with a protocol,hostname,and path 
        URL url2 = new URL("http", "www.geeksforgeeks.org", 
                           "/jvm-works-jvm-architecture/"); 
        URL url3 = new URL( 
            "https://www.google.co.in/search?"
            + "q=gnu&rlz=1C1CHZL_enIN71"
            + "4IN715&oq=gnu&aqs=chrome..69i57j6"
            + "9i60l5.653j0j7&sourceid=chrome&ie=UTF"
            + "-8#q=geeks+for+geeks+java"); 
  
        // Printing the string representation of the URL 
        System.out.println(url1.toString()); 
        System.out.println(url2.toString()); 
        System.out.println(); 
        System.out.println("Different components of the URL3-"); 
  
        // Retrieving the protocol for the URL 
        System.out.println("Protocol:- " + url3.getProtocol()); 
        // Retrieving the hostname of the url 
        System.out.println("Hostname:- " + url3.getHost()); 
        // Retrieving the default port 
        System.out.println("Default port:- " + url3.getDefaultPort()); 
        // Retrieving the query part of URL 
        System.out.println("Query:- " + url3.getQuery()); 
        // Retrieving the path of URL 
        System.out.println("Path:- " + url3.getPath()); 
        // Retrieving the file name 
        System.out.println("File:- " + url3.getFile()); 
        // Retrieving the reference 
        System.out.println("Reference:- " + url3.getRef()); 
    } 
}
```
**Вывод:**
<p style="background-color: navy; color: yellow">
https://www.google.co.in/?gfe_rd=cr&ei=ptYqWK26I4fT8gfth6CACg#q=geeks+for+geeks+java<br>
http://www.geeksforgeeks.org/jvm-works-jvm-architecture/<br>
Different components of the URL3-<br>
Protocol:- https<br>
Hostname:- www.google.co.in<br>
Default port:- 443<br>
Query:- q=gnu&rlz=1C1CHZL_enIN714IN715&oq=gnu&aqs=chrome..69i57j69i60l5.653j0j7&sourceid=chrome&ie=UTF-8<br>
Path:- /search<br>
File:- /search?q=gnu&rlz=1C1CHZL_enIN714IN715&oq=gnu&aqs=chrome..69i57j69i60l5.653j0j7&sourceid=chrome&ie=UTF-8<br>
Reference:- q=geeks+for+geeks+java</p>
#### Пример 2. [Получение странички из интернета](https://javarush.com/quests/lectures/questsyntaxpro.level15.lecture06)

Создает объект URL с путем к странице.  Получает [InputStream](InputStream) у интернет-объекта.
Читает все байты и возвращает массив байт. Преобразуем массив в строку и выводим строку на экран:
```java
// Java program to demonstrate working of URL
import java.io.IOException;
import java.io.InputStream;
import java.net.URL;

// Main class
// URL class
public class Main {
    public static void main(String[] args) throws IOException {
        URL url = new URL("https://javarush.com");
        InputStream input = url.openStream();
        byte[] buffer = input.readAllBytes();
        String str = new String(buffer);
        System.out.println(str);
    }
}
```
**На экране отобразится содержимое HTML-файла:**
```
<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="utf-8"/>
  <link rel="icon" href="/kit/favicon.png"/>
  <meta name="viewport" content="width=device-width, initial-scale=1"/>
  . . .
  ```
  
#### Сравнение работы File и URL

`URL` — это такой аналог [File](File) или [[Files, Path#Path|Path]], только [[Files, Path#Path|Path]] хранит путь к ресурсу в файловой системе, а `URL` — путь к ресурсу в интернете.

Вся магия происходит, когда мы за один вызов метода `openStream()` получаем сразу объект типа [InputStream](InputStream). Это же стандартный объект, и мы его уже изучили вдоль и поперек. Все становится очевидно уже после получения объекта типа [InputStream](InputStream). Ведь как вычитать из него данные, мы уже знаем.

Сравните: отличаются только две первые строчки, и то немного. Вот оно, преимущество стандартизации и работы с цепочками потоков данных:

**Работа с интернетом**

```java
URL url = new URL("https://javarush.com");
InputStream input = url.openStream();

byte[] buffer = input.readAllBytes();
String str = new String(buffer);
System.out.println(str);
```

**Работа с файлом**

```java
File file = new File("c:\\readme.txt");
InputStream input = new FileInputStream(file);

byte[] buffer = input.readAllBytes();
String str = new String(buffer);
System.out.println(str);
```

#### Пример 3. [Чтение веб-страницы с помощью Java](https://www.vogella.com/tutorials/JavaNetworking/article.html#javanetwork_example_readpage)

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.net.URL;

public class ReadWebPage {
  public static void main(String[] args) {
    String urlText = "https://www.vogella.com/";
    BufferedReader in = null;
    try {
      URL url = new URL(urlText);
      in = new BufferedReader(new InputStreamReader(url.openStream()));

      String inputLine;
      while ((inputLine = in.readLine()) != null) {
        System.out.println(inputLine);
      }
    } catch (Exception e) {
      e.printStackTrace();
    } finally {
      if (in != null) {
        try {
          in.close();
        } catch (IOException e) {
          e.printStackTrace();
        }
      }
    }
  }
}
```