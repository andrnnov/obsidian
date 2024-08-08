#Java #Networking #URLConnection #HttpURLConnection

## Класс Java.net.HttpURLConnection в Java

2024-08-08 16:09

**Класс HttpURLConnection** - это абстрактный класс, непосредственно продолжающийся из класса [URLConnection](URLConnection). Он включает в себя всю функциональность своего родительского класса с дополнительными функциями, специфичными для HTTP. HttpsURLConnection - это еще один класс, который используется для более защищенного протокола HTTPS.

### Конструктор

**HttpURLConnection(URL u):** Создает httpurlconnection на указанный [URL](URL)

### Методы (отличные от класса [URLConnection](URLConnection))

| Метод                         | Выполнено действие                                                                                                                                                                                                    |
| ----------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| disconnect()                  | Указано, что запросы к серверу в будущем крайне маловероятны.                                                                                                                                                         |
| getErrorStream()              | Получает поток ошибок, если сервер не может быть подключен или произошла какая-либо ошибка. Он может содержать информацию о том, как исправить ошибку с сервера.                                                      |
| getFollowRedirects()          | Возвращает true или false в зависимости от автоматического перенаправления или нет.                                                                                                                                   |
| getHeaderField()              | Возвращает n-е поле заголовка или null, если оно не существует. Оно переопределяет метод getHeaderField класса URLConnection.                                                                                         |
| getInstanceFollowRedirects()  | Возвращает true или false в зависимости от того, установлено автоматическое перенаправление экземпляра или нет.                                                                                                       |
| getPermission()               | Получает разрешение, необходимое для подключения к целевому хосту и порту.                                                                                                                                            |
| getResponseCode()             | Используется для получения статуса ответа с сервера.                                                                                                                                                                  |
| getResponseMessage()          | Извлекает ответное сообщение.                                                                                                                                                                                         |
| getRequestMethod()            | Возвращает метод запроса.                                                                                                                                                                                             |
| setInstanceFollowRedirects()  | Устанавливает, будут ли запросы кода ответа автоматически перенаправляться этим экземпляром HTTP URL-соединения. Он переопределяет более общий setFollowRedirects()                                                   |
| setRequestMethod()            | Используется для задания метода запроса. По умолчанию используется GET                                                                                                                                                |
| setFixedLengthStreamingMode() | Используется для установки длины содержимого, записываемого в outputstream, если оно известно заранее.                                                                                                                |
| setFollowRedirects()          | Определяет, будет ли запрос кода ответа 3xx перенаправляться автоматически или нет.                                                                                                                                   |
| setChunkedStreamingMode()     | Используется, когда длина содержимого неизвестна. Вместо создания буфера фиксированной длины и записи его на сервер содержимое разбивается на фрагменты и затем записывается. Не все серверы поддерживают этот режим. |
| usingProxy()                  | Возвращает true, если соединение установлено с использованием прокси, в противном случае false                                                                                                                        |

#### Пример 1. [HTTP-доступ](https://www.vogella.com/tutorials/JavaNetworking/article.html#javanetwork_overview)

Java предоставляет HTTP client API для доступа к ресурсам по протоколу HTTP или HTTPS. Основными классами для доступа к Интернету являются  классы [java.net.URL](URL) и `java.net.HttpURLConnection`.

Класс [URL](URL) может использоваться для определения указателя на веб-ресурс, в то время как `HttpURLConnection` класс может использоваться для доступа к веб-ресурсу.

`HttpURLConnection` позволяет создать [InputStream](InputStream).

`HttpURLConnection` поддерживает прозрачное сжатие ответов (через заголовок) `Accept-Encoding: gzip`, указание имени сервера (расширение SSL и TLS) и кэш ответов.

API относительно прост. Например, для получения веб-страницы www.vogella.com вы можете использовать следующий пример.
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class DownloadWebpageExample {
    private static final String newLine  = System.getProperty("line.separator");
    public static void main(String[] args) {
        try  {
            URL url = new URL("https://www.vogella.com/");
            HttpURLConnection con = (HttpURLConnection) url.openConnection();
            String readStream = readStream(con.getInputStream());
            // Give output for the command line
            System.out.println(readStream);
        } catch (Exception e) {
            e.printStackTrace();
        }

    }

    private static String readStream(InputStream in) {
        StringBuilder sb = new StringBuilder();
        try (BufferedReader reader = new BufferedReader(new InputStreamReader(in));) {
            String nextLine = "";
            while ((nextLine = reader.readLine()) != null) {
                sb.append(nextLine + newLine);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
        return sb.toString();
    }
}
```
Javadoc из `HttpURLConnection` предлагает не использовать повторно экземпляр `HttpURLConnection`. Если вы используете его таким образом, `HttpURLConnection` проблем с потоковой обработкой не возникнет, поскольку он не будет использоваться совместно между различными `Threads`.

В качестве альтернативы вы также можете использовать класс scranner .
```java
import java.io.IOException;
import java.io.InputStream;
import java.net.URL;
import java.util.Scanner;

public class DowloadWebpageExampleScanner {
    public static void main(String[] args) {
        try (
                InputStream openStream = new URL("https://www.vogella.com/").openStream();
                Scanner scanner = new Scanner(openStream, "UTF-8");) {
            String out = scanner.useDelimiter("\\A").next();
            System.out.println(out);
        } catch (IOException e) {
            e.printStackTrace();
        }

    }
}
```

#### Пример 1. [Чтение веб-страницы с помощью Java](https://www.vogella.com/tutorials/JavaNetworking/article.html#javanetwork_example_readpage)

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

#### Пример 2. [Получение кода возврата с веб-страницы](https://www.vogella.com/tutorials/JavaNetworking/article.html#javanetwork_returncode)

Коды возврата HTML - это стандартные коды, которые веб-сервер возвращает, если произошла определенная ситуация. Например, код возврата "200" означает, что HTML-запрос выполнен нормально и сервер выполнит требуемое действие, например, отправит веб-страницу.

Следующий код откроет веб-страницу и напечатает код возврата для доступа в HTML.

Наиболее важными кодами возврата HTML являются:

Таблица 1. Коды возврата HTML

|Код возврата|Объяснение|
|---|---|
|200|ОК|
|301|Постоянное перенаправление на другую веб-страницу|
|400|Неверный запрос|
|404|Не найдено|
```java
import java.io.IOException;
import java.net.HttpURLConnection;
import java.net.URL;

public class ReadReturnCode {
  public static void main(String[] args) throws IOException {
    String urltext = "https://www.vogella.com/";
    URL url = new URL(urltext);
    int responseCode = ((HttpURLConnection) url.openConnection())
        .getResponseCode();
    System.out.println(responseCode);
  }
}
```

#### Пример 3. [Тип контента / MIME-тип](https://www.vogella.com/tutorials/JavaNetworking/article.html#javanetwork_mime)

Тип интернет-медиа (сокращенно MIME), который также называется Content-type, определяет тип веб-ресурса. Тип MIME - это состоящий из двух частей идентификатор форматов файлов в Интернете. Для HTML-страницы тип содержимого - "text / html".

Следующий код проверит код возврата URL-адреса и получит content-type (MIME-тип) для веб-ресурса.
```java
import java.io.IOException;
import java.net.HttpURLConnection;
import java.net.URL;

public class ReadMimeType {
  public static void main(String[] args) throws IOException {
    String urltext = "https://www.vogella.com/";
    URL url = new URL(urltext);
    String contentType = ((HttpURLConnection) url.openConnection())
        .getContentType();
    System.out.println(contentType);
  }
}
```
**Вывод:**
<p style="background-color: navy; color: yellow">
text/html</p>

#### Пример 4. [Использование Http get services](https://www.vogella.com/tutorials/JavaNetworking/article.html#usinghttpget)

Несколько веб-сайтов предлагают услуги через Http get-вызовы. Например, вы можете отправить get-запрос на "http://tinyurl" или [http://tr.im"](http://tr.im/) и получить сокращенную версию URL-адреса, который вы передаете в качестве параметра. Ниже будет продемонстрировано, как вызвать службу get из "http://TinyUrl " или "http://tr.im " через Java. Создайте Java-проект "de.vogella.web.get" и создайте следующие классы, которые будут вызывать GetService и возвращать результат.
```java
package de.vogella.web.get;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.net.URL;

public class TinyURL  {
  private static final String tinyUrl = "http://tinyurl.com/api-create.php?url=";
  
  public String shorter(String url) throws IOException {
    String tinyUrlLookup = tinyUrl + url;
    BufferedReader reader = new BufferedReader(new InputStreamReader(new URL(tinyUrlLookup).openStream()));
    String tinyUrl = reader.readLine();
    return tinyUrl;
  }
}
```

```java
package de.vogella.web.get;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.net.URL;

public class Trim {
  private static final String trimUrl = "http://api.tr.im/v1/trim_simple?url=";
  
  public String shorter(String url) throws IOException {
    String tinyUrlLookup = trimUrl + url;
    BufferedReader reader = new BufferedReader(new InputStreamReader(new URL(tinyUrlLookup).openStream()));
    String tinyUrl = reader.readLine();
    return tinyUrl;
  }
}
```
И небольшой тест.
```java
package de.vogella.web.get;

import java.io.IOException;

public class Test {
  /**
   * @param args
   * @throws IOException 
   */
  public static void main(String[] args) throws IOException {
    String s = "https://www.vogella.com/";
    TinyURL tiny = new TinyURL();
    System.out.println(tiny.shorter(s));
    Trim trim= new Trim ();
    System.out.println(trim.shorter(s));
  }
}
```
