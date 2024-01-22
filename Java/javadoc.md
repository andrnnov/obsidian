#Java #javadoc

### Документирование javadoc

2024-01-22 16:39

При документировании приложения необходима также поддержка документации программы. Если документация и код разделены, то непроизвольно создаются сложности, связанные с необходимостью внесения изменений в соответствующие разделы сопроводительной документации при изменении программного кода.

Как правило, все существующие среды разработки IDE приложений Java предлагают решение по связыванию кода с документацией в процессе разработки с использованием **javadoc**. Для этого необходимо соответствующим образом написать комментарий к коду, т.е. документировать. Java комментарии необходимы как для комментирования программы, так и для составления или оформления документации.

Разработан специальный синтаксис для оформления документации в виде комментариев и инструмент для создания из комментариев документации. Этим инструментом является **javadoc**, который обрабатывая файл с исходным текстом программы, выделяет помеченную документацию из комментариев и связывает с именами соответствующих классов, методов и полей. Таким образом, при минимальных усилиях создания комментариев к коду, можно получить хорошую документацию к программе.

**javadoc** — это генератор документации в HTML-формате из комментариев исходного кода Java и определяет стандарт для документирования классов Java. Для создания доклетов и тэглетов, которые позволяют программисту анализировать структуру Java-приложения, **javadoc** также предоставляет API. В каждом случае комментарий должен находиться перед документируемым элементом.

При написании комментариев к кодам Java используют три типа комментариев:
```java
// однострочный комментарий;
/* многострочный комментарий */
/** комментирование документации */
```
Реальный пример комментариев метода в Javadoc:
```java
/**
* Zaps the roadrunner with the number of volts you specify.
* <p>
* Do not exceed more than 30 volts or the zap function will backfire.
* For another way to kill a roadrunner, see the {@link Dynamite#blowDynamite()} method.
*
* @exception IOException if you don't enter a data type amount for the voltage
* @param voltage the number of volts you want to send into the roadrunner's body
* @see #findRoadRunner
* @see Dynamite#blowDynamite
*/
public void zapRoadRunner(int voltage) throws IOException {
   if (voltage < 31) {
       System.out.println("Zapping roadrunner with " + voltage + " volts!!!!");
   }
   else {
    System.out.println("Backfire!!! zapping coyote with 1,000,000 volts!!!!");
   }
}
```
С помощью утилиты **javadoc**, входящей в состав JDK, комментарий документации можно извлекать и помещать в НТМL файл. Утилита **javadoc** позволяет вставлять HTML тэги и использовать специальные ярлыки (дескрипторы) документирования. НТМL тэги заголовков не используют, чтобы не нарушать стиль файла, сформированного утилитой.

Дескрипторы **javadoc**, начинающиеся со знака @, называются автономными и должны помещаться с начала строки комментария (лидирующий символ * игнорируется). Дескрипторы, начинающиеся с фигурной скобки, например **{@code}**, называются встроенными и могут применяться внутри описания.

Комментарии документации применяют для документирования классов, интерфейсов, полей (переменных), конструкторов и методов. В каждом случае комментарий должен находиться перед документируемым элементом.

#### javadoc дескрипторы: @author, @version, @since, @see, @param, @return

|Дескриптор|Применение|Описание|
|---|---|---|
|@author|Класс, интерфейс|Автор|
|@version|Класс, интерфейс|Версия. Не более одного дескриптора на класс|
|@since|Класс, интерфейс, поле, метод|Указывает, с какой версии доступно|
|@see|Класс, интерфейс, поле, метод|Ссылка на другое место в документации|
|@param|Метод|Входной параметр метода|
|@return|Метод|Описание возвращаемого значения|
|@exception имя_класса описание|Метод|Описание исключения, которое может быть послано из метода|
|@throws имя_класса описание|Метод|Описание исключения, которое может быть послано из метода|
|@deprecated|Класс, интерфейс, поле, метод|Описание устаревших блоков кода|
|{@link reference}|Класс, интерфейс, поле, метод|Ссылка|
|{@value}|Статичное поле|Описание значения переменной|

#### Форма документирования кода

Документирование класса, метода или переменной начинается с комбинации символов `/**`, после которого следует тело комментариев; заканчивается комбинацией символов `*/`.

В тело комментариев можно вставлять различные дескрипторы. Каждый дескриптор, начинающийся с символа '@' должен стоять первым в строке. Несколько дескрипторов одного и того же типа необходимо группировать вместе. Встроенные дескрипторы (начинаются с фигурной скобки) можно помещать внутри любого описания.
```java
/** 
 * Класс продукции со свойствами <b>maker</b> и <b>price</b>.
 * @autor Киса Воробьянинов
 * @version 2.1
*/
class Product {
    /** Поле производитель */
    private String maker;

    /** Поле цена */
    public double price;

    /** 
     * Конструктор - создание нового объекта
     * @see Product#Product(String, double)
     */
    Product() {
        setMaker("");
        price=0;
    }

    /** 
     * Конструктор - создание нового объекта с определенными значениями
     * @param maker - производитель
     * @param price - цена
     * @see Product#Product()
     */
    Product(String maker,double price){
        this.setMaker(maker);
        this.price=price;
    }

    /**
     * Функция получения значения поля {@link Product#maker}
     * @return возвращает название производителя
     */
    public String getMaker() {
        return maker;
    }

   /**
     * Процедура определения производителя {@link Product#maker}
     * @param maker - производитель
     */
    public void setMaker(String maker) {
        this.maker = maker;
    }
}
```
Для документирования кода можно использовать HTML теги. При использовании ссылочных дескрипторов **@see** и **@link** нужно сначала указать имя класса и после символа "#" его метод или поле.

Связывание с другими Javadocs выполняется с помощью тега `@link` :
```java
/**
 * You can link to the javadoc of an already imported class using {@link ClassName}.
 *
 * You can also use the fully-qualified name, if the class is not already imported: 
 *  {@link some.other.ClassName}
 *
 * You can link to members (fields or methods) of a class like so:
 *  {@link ClassName#someMethod()}
 *  {@link ClassName#someMethodWithParameters(int, String)}
 *  {@link ClassName#someField}
 *  {@link #someMethodInThisClass()} - used to link to members in the current class
 *  
 * You can add a label to a linked javadoc like so:
 *  {@link ClassName#someMethod() link text} 
 */
```

Если вы хотите добавить **ссылки на внешние ресурсы,** вы можете просто использовать тег HTML `<a>`. Вы можете использовать его в любом месте или внутри обоих тегов `@link` и `@see`.
```java
/**
 * Wondering how this works? You might want
 * to check this <a href="http://stackoverflow.com/">great service</a>.
 *
 * @see <a href="http://stackoverflow.com/">Stack Overflow</a>
 */
```

#### Фрагменты кода внутри документации

Канонический способ написания кода внутри документации - с конструкцией `{@code }` . Если у вас есть многострочный код, завершающий внутри `<pre></pre>` .
```java
/**
 * The Class TestUtils.
 * <p>
 * This is an {@code inline("code example")}.
 * <p>
 * You should wrap it in pre tags when writing multiline code.
 * <pre>{@code
 *  Example example1 = new FirstLineExample();
 *  example1.butYouCanHaveMoreThanOneLine();
 * }</pre>
 * <p>
 * Thanks for reading.
 */
class TestUtils {
```

Иногда вам может потребоваться ввести сложный код внутри комментария javadoc. Знак `@` является особенно проблематичным. Использование старого `<code>` рядом с конструкцией `{@literal }` решает проблему.
```java
/**
 * Usage:
 * <pre><code>
 * class SomethingTest {
 * {@literal @}Rule
 *  public SingleTestRule singleTestRule = new SingleTestRule("test1");
 *
 * {@literal @}Test
 *  public void test1() {
 *      // only this test will be executed
 *  }
 *
 *  ...
 * }
 * </code></pre>
 */
class SingleTestRule implements TestRule { }
```

#### Создание Javadocs из командной строки

Многие IDE обеспечивают поддержку для генерации HTML из Javadocs автоматически; некоторые средства сборки (например, [Maven](https://maven.apache.org/) и [Gradle](https://gradle.org/)) также имеют плагины, которые могут обрабатывать создание HTML.

Однако для создания Javadoc HTML эти инструменты не требуются; это можно сделать с помощью инструмента командной строки `javadoc`.

Самое основное использование инструмента:

```
javadoc JavaFile.java
```

Что будет генерировать HTML из комментариев Javadoc в `JavaFile.java`.

Более практичное использование инструмента командной строки, который будет рекурсивно читать все java-файлы в `[source-directory]`, создавать документацию для `[package.name]` и всех подпакетов и размещать сгенерированный HTML в `[docs-directory]` является:

```
javadoc -d [docs-directory] -subpackages -sourcepath [source-directory] [package.name]
```

