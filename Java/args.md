#Java #args
### Аргументы командной строки в Java

2024-01-18 10:11

Аргументы командной строки Java (Command-Line Arguments) — это способ ввода данных в программу через командную строку. Программисты могут передавать эти аргументы непосредственно из консоли, к которой будет обращаться метод main(). При необходимости аргументами командной строки можно пренебречь, передав значения непосредственно методу main().

Аргументы командной строки упаковываются и передаются в args[]. Это массив строк, который содержит все переданные ему аргументы командной строки. Каждый аргумент будет храниться по индексу, начиная с `args[0]` до `args[n]`.

Аргументы командной строки передаются через командную строку или терминал. Все переданные через них аргументы будут преобразованы и заключены в массив args[] внутри JVM.

Предположим, у нас есть файл с каким-то кодом Java. Следующие этапы продемонстрируют, как передавать аргументы командной строки в Java:
1. Сохраните программу Java с расширением .java.
2. Откройте терминал/командную строку в каталоге, где программа хранится локально.
3. Скомпилируйте программу Java для преобразования файла .java в файл .class.
	- Команда: javac filename.java
1. Запустите программу и передайте аргументы после того, как имя файла будет разделено пробелами.
    - Команда: java filename argument1 argument2 .... argumentN

Поскольку аргументы хранятся в массиве `args[]`, это означает, что мы можем легко получить к ним доступ с помощью `args[i]`, где указывается индекс, который может варьироваться от 0 до n (общее количество переданных аргументов).
```java
class Arguments {
    public static void main( String[] args ) {
        System.out.println(" Hello World! ");
        // args.length is used to get length of args array

        System.out.println(" Total number of args: " + args.length);
        // iterating over the args array to print the args if available

        for (int i = 0; i < args.length; i++) {
            System.out.println(" Arg " + i + ": " + args[i]);
        }
    }
}
```
Вывод:
<p style="background-color: navy; color: yellow">
Hello World!<br>
Total number of args: 7<br>
Arg 0: Welcome<br> 
Arg 1: to<br>
Arg 2: this<br> 
Arg 3: blog<br> 
Arg 4: and<br> 
Arg 5: Happy<br> 
Arg 6: Learning</p>

В Java 5 были введены переменные, которые представляют собой массивы [Varargs](Varargs). Следовательно, мы можем определить наш _main_ с помощью переменной _String_:
```java
public static void main(String... args) {
    // handle arguments
}
```

#### Парсинг аргументов командной строки в Java

При работе с командной строкой, часто сталкиваются с ситуацией, когда необходимо обработать аргументы командной строки. Возьмем, к примеру, консольное приложение, которое принимает на входе имя файла и опцию для обработки этого файла. Имя файла и опцию мы передаем в программу как аргументы командной строки.

#### Стандартный подход

В Java аргументы командной строки передаются в метод `main()` в виде массива строк `(String[] args)`. Этот массив содержит значения, переданные программе при запуске. Рассмотрим пример:
```java
public class Main {
  public static void main(String[] args) {
    for (String arg : args) {
      System.out.println(arg);
    }
  }
}
```
В этом примере, все аргументы, переданные программе, будут выведены на экран. Однако, этот подход не всегда удобен, особенно когда количество и порядок аргументов может меняться.

#### Использование библиотек для парсинга аргументов

Для более удобного и гибкого парсинга аргументов командной строки можно использовать специализированные библиотеки, такие как Apache Commons CLI, JCommander и др.

##### Apache Commons CLI

Apache Commons CLI предоставляет набор классов для парсинга аргументов командной строки. Он поддерживает простые однобуквенные опции, длинные опции, сбор аргументов и автоматическое создание сообщений с использованием.
import org.apache.commons.cli.*;
```java
public class Main {
  public static void main(String[] args) {
    Options options = new Options();
    options.addOption("f", "file", true, "имя файла");
    options.addOption("o", "option", true, "опция обработки");
 
    CommandLineParser parser = new DefaultParser();
    try {
      CommandLine cmd = parser.parse(options, args);
      if (cmd.hasOption("f")) {
        System.out.println(cmd.getOptionValue("f"));
      }
      if (cmd.hasOption("o")) {
        System.out.println(cmd.getOptionValue("o"));
      }
    } catch (ParseException e) {
      e.printStackTrace();
    }
  }
}
```
В примере выше, приложение ожидает два аргумента: `-f` (или `--file`) с именем файла и `-o` (или `--option`) с опцией обработки.

##### JCommander

JCommander — это другая мощная библиотека для парсинга аргументов командной строки в Java. Она позволяет использовать аннотации для указания ожидаемых аргументов.
```java
import com.beust.jcommander.*;
 
public class Main {
  @Parameter(names = {"-f", "--file"}, description = "Имя файла")
  private String file;
 
  @Parameter(names = {"-o", "--option"}, description = "Опция обработки")
  private String option;
 
  public static void main(String[] args) {
    Main main = new Main();
    JCommander.newBuilder().addObject(main).build().parse(args);
    System.out.println(main.file);
    System.out.println(main.option);
  }
}
```
В этом примере, JCommander использует аннотации для связывания аргументов командной строки с полями класса.

Есть различные способы парсинга аргументов командной строки в Java. Можно использовать стандартный подход и работать с массивом строк, переданным в метод   `main()`, или использовать библиотеки для более удобного и гибкого парсинга аргументов. Выбор подхода зависит от конкретной задачи и личных предпочтений.