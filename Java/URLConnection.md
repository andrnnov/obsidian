#Java #Networking #URL #URLConnection

## Класс URLConnection в Java

2024-08-08 11:54

Абстрактный класс **_URLConnection_** - это суперкласс всех классов, которые представляют канал связи между приложением и [URL](URL). Экземпляры этого класса могут использоваться как для чтения, так и для записи на ресурс, на который ссылается [URL](URL).

В основном существует два подкласса, которые расширяют класс **_URLConnection_**:
- **HttpURLConnection:** Если мы подключаемся к любому [URL](URL), который использует “http” в качестве протокола, то используется класс [HttpURLConnection](HttpURLConnection).
- **JarURLConnection:** Однако, если мы пытаемся установить соединение с файлом jar в Интернете, то используется JarURLConnection.

### Методы класса URLConnection

| Метод                          | Выполнено действие                                                                                                                             |
| ------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| getContent()                   | Извлекает содержимое **_URLConnection_**                                                                                                       |
| getContentEncoding()           | Возвращает значение поля заголовка content-encoding .                                                                                          |
| getContentLength()             | Возвращает длину поля заголовка содержимого                                                                                                    |
| getDate()                      | Возвращает значение date в поле заголовка                                                                                                      |
| getHeaderFields()              | Возвращает карту, содержащую значения различных полей заголовка в заголовке HTTP                                                               |
| getHeaderField(int i)          | Возвращает значение i-го индекса заголовка                                                                                                     |
| getHeaderField(строковое поле) | Возвращает значение поля с именем “field” в заголовке                                                                                          |
| getInputStream()               | Возвращает входной поток для этого открытого соединения, находящегося внутри класса [OutputStream](OutputStream)                               |
| getOutputStream()              | Возвращает выходной поток к этому соединению класса [OutputStream](OutputStream)                                                               |
| openConnection()               | Открывает соединение с указанным URL-адресом.                                                                                                  |
| setAllowUserInteraction()      | Установка этого значения true означает, что пользователь может взаимодействовать со страницей. Значение по умолчанию равно true.               |
| setDefaultUseCaches()          | Устанавливает значение по умолчанию в поле useCache в качестве заданного значения.                                                             |
| setDoInput()                   | Определяет, разрешено ли пользователю принимать входные данные или нет                                                                         |
| setDoOutput()                  | Задает, разрешено ли пользователю писать на странице. Значение по умолчанию равно false, поскольку большинство URL-адресов не позволяют писать |

Теперь, после понимания методов, шагов, задействованных в описанном выше процессе

1. **Создание URL-адреса:** Создайте объект URL-адреса, используя любой из указанных конструкторов.
2. **Создать объект:** вызовите openConnection(), чтобы создать объект **_URLConnection_**.
3. **Отображение содержимого:** Либо используйте созданный выше объект для отображения информации о ресурсе, либо считывайте / записывайте содержимое файла на консоль с помощью [BufferedReader](BufferedReader) и [InputStream](InputStream) открытого соединения с помощью метода getInputStream().
4. **Закрыть поток:** закройте [InputStream](InputStream) по завершении.

#### Пример 1. Пример программы, которая использует вышеуказанные методы для отображения полей заголовка, а также вывода исходного кода всей страницы в окно консоли.

```java
// Java Program to Illustrate Reading and Writing 
// in URLConnection Class 
  
// Importing required classes 
import java.io.*; 
import java.net.*; 
import java.util.ArrayList; 
import java.util.Date; 
import java.util.HashMap; 
import java.util.List; 
import java.util.Map; 
  
// Class 
// URLConnectionclass 
class Main { 
    // main driver method 
    public static void main(String[] args) { 
        // Try block to check for exceptions 
        try { 
            // Fetching URL by creating 
            URL url = new URL("https://www.geeksforgeeks.org/java"); 
            // Opening the connection to the above URL 
            URLConnection urlcon = url.openConnection(); 
            // Executing the below line would print the 
            // value of 
            // Allow User Interaction field. 
            // System.out.println(urlcon.getAllowUserInteraction()); 
  
            // Executing the below line would print 
            // the value of Content Type field. 
            // System.out.println(urlcon.getContentType()); 
  
            // Executing the below line would print the 
            // value 
            // of URL of the given connection. 
            // System.out.println(urlcon.getURL()); 
  
            // Executing the below line would 
            // print the value of Do Input field. 
            // System.out.println(urlcon.getDoInput()); 
  
            // Executing the below line would 
            // print the value of Do Output field. 
            // System.out.println(urlcon.getDoOutput()); 
  
            // Executing the below line would 
            // print the value of Last Modified field. 
            // System.out.println(new 
            // Date(urlcon.getLastModified())); 
  
            // Executing the below line would 
            // print the value of Content Encoding field. 
            // System.out.println(urlcon.getContentEncoding()); 
  
            // To get a map of all the fields of http header 
            Map<String, List<String> > header = urlcon.getHeaderFields(); 
  
            // Printing all the fields along with their 
            // value 
            for (Map.Entry<String, List<String> > mp : header.entrySet()) { 
                System.out.print(mp.getKey() + " : "); 
                System.out.println(mp.getValue().toString()); 
            } 
  
            System.out.println(); 
            System.out.println("Complete source code of the URL is-"); 
            System.out.println("---------------------------------"); 
  
            // Getting the inputstream of the open 
            // connection 
            BufferedReader br = new BufferedReader(new InputStreamReader( 
                    urlcon.getInputStream())); 
            String i; 
  
            // Printing the source code line by line 
            while ((i = br.readLine()) != null) { 
                System.out.println(i); 
            } 
        } 
  
        // Catch block to handle exceptions 
        catch (Exception e) { 
            // Displaying exceptions 
            System.out.println(e); 
        } 
    } 
}
```
**Вывод:**
<p style="background-color: navy; color: yellow">
null : [HTTP/1.1 200 OK]<br>
Transfer-Encoding : [chunked]<br>
X-Cache : [Hit from cloudfront]<br>
Server : [Apache]<br>
X-Content-Type-Options : [nosniff]<br>
X-Amz-Cf-Pop : [ARN53-P1]<br>
Connection : [keep-alive]<br>
* * * </p>


