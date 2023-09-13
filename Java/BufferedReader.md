#BufferedReader 

2023-09-07 10:25

Считывает текст из потока ввода символов, буферизуя символы таким образом, чтобы обеспечить эффективное чтение символов, массивов и строк. Размер буфера может быть указан или может использоваться размер по умолчанию. Значение по умолчанию достаточно велико для большинства целей. В общем случае каждый запрос на чтение, выполняемый средством чтения, вызывает выполнение соответствующего запроса на чтение базового символьного или байтового потока. Поэтому рекомендуется обернуть  BufferedReader вокруг любого устройства чтения, операции read() которого могут быть дорогостоящими, например FileReaders и InputStreamReaders. Программы, использующие DataInputStreams для текстового ввода, могут быть локализованы путем замены каждого DataInputStreams соответствующим **BufferedReader**.

### **Конструкторы класса BufferedReader**

|Конструктор|Действие|
|---|---|
|BufferedReader (Reader in)|Создает буферизующий поток ввода символов, который использует входной буфер размера по умолчанию|
|BufferedReader (Reader in, int sz)|Создает буферизующий поток ввода символов, который использует входной буфер указанного размера.|

### **Методы класса BufferedReader**

|Имя метода|Действие|
|---|---|
|[close()](https://translated.turbopages.org/proxy_u/en-ru.ru.f627e4fc-64f83b21-4c7afbb3-74722d776562/https/www.geeksforgeeks.org/bufferedreader-close-method-in-java-with-examples/#:~:text=The%20close()%20method%20of,associated%20with%20the%20stream%20operations.&text=Parameters%3A%20This%20method%20does%20not,does%20not%20return%20any%20value.)|Закрывает поток и освобождает все связанные с ним системные ресурсы.Как только поток будет закрыт, дальнейшие вызовы read(), ready(), mark(), reset() или skip() вызовут исключение IOException. Закрытие ранее закрытого потока не имеет никакого эффекта.|
|[mark()](https://translated.turbopages.org/proxy_u/en-ru.ru.f627e4fc-64f83b21-4c7afbb3-74722d776562/https/www.geeksforgeeks.org/bufferedreader-mark-method-in-java-with-examples/)|Отмечает текущую позицию в потоке. Последующие вызовы reset() будут пытаться переместить поток в эту точку.|
|[markSupported()](https://translated.turbopages.org/proxy_u/en-ru.ru.f627e4fc-64f83b21-4c7afbb3-74722d776562/https/www.geeksforgeeks.org/bufferedreader-marksupported-method-in-java-with-examples/)|Сообщает, поддерживает ли этот поток операцию mark(), которую он выполняет.|
|read()|Считывает один символ.|
|read(char[] cbuf, int off, int len)|Считывает символы в часть массива. Этот метод реализует общий контракт соответствующего метода чтения класса Reader. В качестве дополнительного удобства он пытается прочитать как можно больше символов, многократно вызывая метод read базового потока.|
|[readLine()](https://translated.turbopages.org/proxy_u/en-ru.ru.f627e4fc-64f83b21-4c7afbb3-74722d776562/https/www.geeksforgeeks.org/bufferedreader-readline-method-in-java-with-examples/)|Считывает строку текста. Считается, что строка завершается любым из перевода строки (‘\n’), возврата каретки (‘\r’) или возврата каретки, за которым сразу следует перевод строки.|
|[ready ()](https://translated.turbopages.org/proxy_u/en-ru.ru.f627e4fc-64f83b21-4c7afbb3-74722d776562/https/www.geeksforgeeks.org/bufferedreader-ready-method-in-java-with-examples/)|Сообщает, готов ли этот поток к чтению.|
|[reset()](https://translated.turbopages.org/proxy_u/en-ru.ru.f627e4fc-64f83b21-4c7afbb3-74722d776562/https/www.geeksforgeeks.org/bufferedreader-reset-method-in-java-with-examples/)|Сбрасывает поток до самой последней отметки.|
|[skip(long)](https://translated.turbopages.org/proxy_u/en-ru.ru.f627e4fc-64f83b21-4c7afbb3-74722d776562/https/www.geeksforgeeks.org/bufferedreader-skiplong-method-in-java-with-examples/)|Пропускает символы.|

**Реализация:** Содержимое внутри файла выглядит следующим образом:

==This is first line
this is second line==

**Пример**

```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;
  

class GFG {
    public static void main(String[] args)
        throws IOException
    {
        FileReader fr = new FileReader("file.txt");
        BufferedReader br = new BufferedReader(fr); 
        char c[] = new char[20];
        // Illustrating markSupported() method
        if (br.markSupported()) {
            System.out.println("mark() method is supported");
            // Illustrating mark method
            br.mark(100);
        }
        // Skipping 8 characters
        br.skip(8);  
        // Illustrating ready() method
        if (br.ready()) {
            // Illustrating readLine() method
            System.out.println(br.readLine());
            // Illustrating read(char c[],int off,int len)
            br.read(c);
            for (int i = 0; i < 20; i++) {
                System.out.print(c[i]);
            }
            System.out.println();
            // Illustrating reset() method
            br.reset();
            for (int i = 0; i < 8; i++) {
                // Illustrating read() method
                System.out.print((char)br.read());
            }
        }
    }
}
```
**Вывод:**

==mark() method is supported
first line
this is second line
This is==