
#Java #DesignPatterns #Singleton

## [Паттерны проектирования Singleton](https://vertex-academy.com/tutorials/ru/pattern-singleton-realizacii/)

2024-07-02 11:38

**_Singleton_** (с англ. «одиночка») — это паттерн проектирования, гарантирующий, что у класса будет только один экземпляр. К этому экземпляру будет предоставлена глобальная, то есть доступная из любой части программы, точка доступа. Если попытаться создать новый объект этого класса, то вернётся уже созданный существующий экземпляр.

Например, в любом государстве может быть только одна конституция. Если потребуется её изменить, то нужно будет работать с существующим экземпляром и никак иначе.

Другой пример — менеджер паролей. Он создаёт только один объект для каждой учётной записи и возвращает его при запросе — для одной учётной записи не может быть двух разных паролей.

### Где применяют шаблон проектирования Singleton

**Конфигурационные настройки.** Представим, что у нас есть класс с настройками приложения — параметрами базы данных или внешнего вида интерфейса. Имеет смысл реализовать его как Singleton. Это обеспечит одну точку доступа к настройкам, и весь код сможет ссылаться на одни и те же настройки.

**Подключение к базе данных.** Если наше приложение использует базу данных, Singleton гарантированно создаст только один экземпляр класса, отвечающего за подключение к ней. Так мы предотвратим лишние соединения и упростим подключение в целом.

**Логирование.** Singleton удобно использовать для логов. Вместо создания нового логгера каждый раз, когда нужно что-то залогировать, мы записываем всё в один объект.

**Счётчики и глобальные объекты.** Паттерн «одиночка» подходит для оценки состояния приложения или сбора статистики с его модулей. С классом можно будет взаимодействовать из любой части программы.

**Пул ресурсов.** Если у нас ограниченный пул соединений к внешнему сервису или к другим ресурсам, то Singleton гарантирует, что доступ к ним всегда будет идти через единственный экземпляр.

## Шаги реализации

1. Добавьте в класс приватное статическое поле, которое будет содержать одиночный объект.
2. Объявите статический создающий метод, который будет использоваться для получения одиночки.
3. Добавьте «ленивую инициализацию» (создание объекта при первом вызове метода) в создающий метод одиночки.
4. Сделайте конструктор класса приватным.
5. В клиентском коде замените вызовы конструктора одиночка вызовами его создающего метода.

### Пример 1 - самый простой вариант реализации

```java
public class Singleton {
    private Singleton(){...}
    public static final Singleton INSTANCE = new Singleton();
```

Плюсы и минусы
- Честных Singleton в Java не существует
	Из-за [reflection](ReflectionAPI), нескольких ClassLoader-ов и других причин, нельзя создать настоящий-настоящий Singleton.
- Трудности при тестировании
	Singleton трудно изолировать - это усложняет написание юнит-тестов.
- Нарушает «Принцип единственной обязанности» класса
	«Принцип едиственной обязанности» считается хорошим тоном в ООП. Он состоит в том, что класс должен отвечать только за что-то одно. Например, класс "КореньКвадратный" должен отвечать только за извлечения квадратного корня. Он не должен одновременно печь пирог и гладить кота - только извлекать квадратный корень. Класс Singleton, помимо своих прямых обязанностей, занимается контролем количества своих классов. Это считается плохим тоном.

У нас есть **ПРИВАТНЫЙ** конструктор. А это значит, что мы не сможем создать объект класса как мы это привыкли делать. Например, если мы запустим такой код:
```java
public class Test {
    public static void main(String[] args) {
        Singleton s = new Singleton();
    }
}
```
Получим ошибку: `Singleton() has private access in Singleton`
Наш приватный конструктор не позволяет никому создавать новый экземпляр класса. Но как тогда вообще создать хотя бы первый объект? Это происходит внутри самого класса - в этой строке:
```java
public static final Singleton INSTANCE = new Singleton();
```
Как Вы могли заметить, INSTANCE имеет доступ public. Это значит, что мы можем обращаться к нему из любого другого класса.

Обратите внимание, что мы сделали приватным **конструктор по умолчанию**. Это значит, что мы не сможем наследовать класс **Singleton**.

Например, создадим какой-нибудь класс, который будет наследовать наш **Singleton**:
```java
public class SingletonChild extends Singleton{
}
```
Получим ошибку: `There is no default constructor available Singleton`

#### Реализация

Пишем такой **Singleton**:
```java
public class MySingleton {
 
    private MySingleton() {
        System.out.println("Singleton created!");
    }
 
    public static final MySingleton INSTANCE = new MySingleton();
 
    public void printName() {
        System.out.println("I am a Singleton!");
    }
}
```
Тут все как и в примере выше. Но чтобы было интереснее, мы добавили метод **printName()**. Он печатает строку "I am a Singleton!".

Теперь, запустим следующий код:
```java
public class Test {
    public static void main(String[] args) {
        MySingleton.INSTANCE.printName();
        System.out.println(MySingleton.INSTANCE.getClass());
    }
}
```
**Вывод:**
<p style="background-color: navy; color: yellow">
Singleton created!<br>
I am a Singleton!<br>
class MySingleton</p>
**Комментарии к коду:**
- Так как первым делом при загрузке класса был создан **INSTANCE**, первым в консоли мы видим сообщение из конструктора - "Singleton created!".
- В **main** мы обратились к нашему единственному экземпляру -  **INSTANCE**, через название класса:
	MySingleton.INSTANCE
- Сначала мы вызвали метод **printName()**:
	MySingleton.INSTANCE.printName();
	В консоли получаем "I am a Singleton!".
- Что еще делать с этим **Singleton**-ом? 
	Применяем на нем универсальный метод **getClass()** и выводим в консоль:
	System.out.println(MySingleton.INSTANCE.getClass());
	В консоли получаем "class MySingleton".

### Пример 2 - Ленивая реализация

Реализация называется ленивой не потому, что Вы можете сэкономить на ней время и пойти попить кофе, а потому, что объект **Singleton**-а создается не сразу при загрузке программы, а только "по вызову".

Код:
```java
public class Singleton {
    private static Singleton instance;
 
    private Singleton(){...}
 
    public static synchronized Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```

Напишем такой класс:
```java
public class MySingleton {
    private static MySingleton instance;

    private MySingleton() {
        System.out.println("Singleton created!");
    }

    public static synchronized MySingleton getInstance() {
        if (instance == null) {
            instance = new MySingleton();
        }
        return instance;
    }
}
```
Запустим его с помощью следующего кода:
```java
public class Test {
    public static void main(String[] args) {
        MySingleton firstInstance = MySingleton.getInstance();
        System.out.println(firstInstance.getClass());
        MySingleton secondInstance = MySingleton.getInstance();
        System.out.println(firstInstance == secondInstance);
    }
}
```
**Вывод:**
<p style="background-color: navy; color: yellow">
Singleton created!<br>
class MySingleton<br>
true</p>

**Комментарии к коду:**

Теперь наш **instance** создается не при загрузке программы, а только по вызову.

Что мы имеем в коде?
- Сначала мы запрашиваем **instance** с помощью метода **getInstance()**. В консоли видите сообщение, которое появляется при вызове конструктора - "Singleton created!"
- Потом используем наш **firstInstance** - например, применяем на нем метод **getClass()** и выводим в консоль. Получаем "class MySingleton".
- Второй раз вызываем метод **getInstance()**. Как и ожидалось, новый объект не создается. Поэтому, в консоли мы не видим нового сообщения "Singleton created!" (оно появится только при вызове конструктора).
- Кроме того, мы сравниваем **firstInstance** и **secondInstance**. Как видите, они равны - т.е. мы получаем один и тот же объект. Значит, наш **Singleton** настоящий!
- Обратите внимание на модификатор **synchronized** возле метода **getInstance()**. Он нужен для корректной работы в многопоточной среде. Но теперь этот метод - "узкое место" в нашей программе. Только один поток в один момент времени может получить к нему доступ - а это замедляет выполнение программы. Если хотите больше узнать про **synchronized** - прочитайте эту статью.

### Пример 3 - Ленивая реализация с быстрой инициализацией

```java
public class Singleton {
    private static volatile Singleton instance;
 
    private Singleton(){...}
 
    public static Singleton getInstance() {
        if (instance == null) {
            synchronized (Singleton.class) {
                if (instance == null) {
                    instance = new Singleton();
                }
            }
        }
        return instance;
    }
}
```

Давайте попробуем реализовать его и запустить.

Представим, что у нас есть такой класс:
```java
public class MySingleton {
    private static volatile MySingleton instance;
 
    private MySingleton(){
        System.out.println("Singleton created!");
    }
 
    public static MySingleton getInstance() {
        if (instance == null) {
            synchronized (MySingleton.class) {
                if (instance == null) {
                    instance = new MySingleton();
                }
            }
        }
        return instance;
    }
}
```
Запускаем:
```java
public class Test {
    public static void main(String[] args) {
        MySingleton firstInstance = MySingleton.getInstance();
        System.out.println(firstInstance.getClass());
        MySingleton secondInstance = MySingleton.getInstance();
        System.out.println(secondInstance == firstInstance);
    }
}
```
**Вывод:**
<p style="background-color: navy; color: yellow">
Singleton created!<br>
class MySingleton<br>
true</p>

**Комментарии к коду:**

В принципе, вывод мало чем отличается от вывода в примере номер два. Давайте лучше разберемся с кодом самого **Singleton**:
- Во-первых, у нас есть переменная с модификатором **[volatile](volatile)**. Этот модификатор делает так, что каждый поток не создает свою копию переменной, а все потоки работают с одной и той же. Действительно, зачем нам копии **Singleton**-а. Он же **Singleton**!
- Дальше у нас есть метод **getInstance()**. Метод getInstance() синхронизирован, и входить в него можно только по одному.

### Пример 4 - Хитрая реализация с внутренним классом

```java
public class Singleton {
 
    private Singleton(){...}
    
    private static class SingletonHolder {
        public static final Singleton HOLDER_INSTANCE = new Singleton();
    }
    
    public static Singleton getInstance() {
        return SingletonHolder.HOLDER_INSTANCE;
    }
}
```
Давайте попробуем реализовать его и запустить.

Напишем такой класс:
```java
public class MySingleton {
 
    private MySingleton() {
        System.out.println("Singleton created!");
    }
 
    private static class SingletonHolder {
        public static final MySingleton HOLDER_INSTANCE = new MySingleton();
    }
 
    public static MySingleton getInstance() {
        return SingletonHolder.HOLDER_INSTANCE;
    }
}
```
Запустим его с помощью следующего кода:
```java
public class Test {
    public static void main(String[] args) {
        MySingleton firstInstance = MySingleton.getInstance();
        System.out.println(firstInstance.getClass());
        MySingleton secondInstance = MySingleton.getInstance();
    }
}
```
**Вывод:**
<p style="background-color: navy; color: yellow">
Singleton created!<br>
class MySingleton</p>

**Комментарии к коду:**

Как видите, код в этом примере и в прошлом почти идентичный. Единственная разница - в реализации через внутренний класс.

В чем особенность внутреннего класса? Он позволяет нам, опять же, осуществить ленивую реализацию благодаря особенностям самой Джавы. Дело в том, что внутренние классы загружаются только тогда, когда мы обращаемся к ним впервые - в отличии от "внешних" классов, которые загружаются сразу при запуске программы.

Более того, она потокобезопасна - за счет той же особенности. Почему? Есть такая проблема - если несколько потоков одновременно "стучатся" к одному и тому же объекту, один из них может получить недогруженный объект. Но тут такого нет - благодаря особенностям загрузки внутренних классов

### Пример 5 - Самая хитрая реализация

```java
public enum Singleton {
    INSTANCE;
}
```
Давайте попробуем реализовать его и запустить.

Напишем такой класс:
```java
public enum MySingleton {
 
    INSTANCE;
 
    private MySingleton() {
        System.out.println("Singleton created! By the way, in Enums the constructor is private by default - so there is no need to write private constructor by yourself");
    }
}
```
Обратите внимание - по умолчанию конструктор у **[Enum](Enum)** приватный. Это значит, что в отличии от других реализаций, в которых мы **обязательно** должны указывать, что конструктор приватный (иначе **Singleton**-а не выйдет), то тут мы можем явно не объявлять приватный конструктор.

Запустим его с помощью следующего кода:
```java
ublic class Test {
    public static void main(String[] args) {
        System.out.println(MySingleton.INSTANCE);
        System.out.println(MySingleton.INSTANCE);
    }
}
```
**Вывод:**
<p style="background-color: navy; color: yellow">
Singleton created! By the way, in Enums the constructor is private by default - so there is no need to write private constructor by yourself<br>
INSTANCE<br>
INSTANCE</p>

**Комментарии к коду:**

Теперь мы реализовали **Singleton** через **[Enum](Enum)**. Это очень удобно - мы можем не прописывать явно приватный конструктор (но тут мы прописали чтобы показать, как создается **Singleton**).

В методе **main** мы обратились к нему два раза. Как видите по сообщению в консоли, **INSTANCE** был создан всего один раз - сообщение **"Singleton created! By the way, in Enums the constructor is private by default - so there is no need to write private constructor by yourself"** было выведено всего один раз.

### Пример 6

```java
// Java program implementing Singleton class
// with using  getInstance() method
 
// Class 1
// Helper class
class Singleton {
    // Static variable reference of single_instance
    // of type Singleton
    private static Singleton single_instance = null;
 
    // Declaring a variable of type String
    public String s;
 
    // Constructor
    // Here we will be creating private constructor
    // restricted to this class itself
    private Singleton() {
        s = "Hello I am a string part of Singleton class";
    }
 
    // Static method
    // Static method to create instance of Singleton class
    public static synchronized Singleton getInstance() {
        if (single_instance == null)
            single_instance = new Singleton();
 
        return single_instance;
    }
}
 
// Class 2
// Main class
class Main {
    // Main driver method
    public static void main(String args[])
    {
        // Instantiating Singleton class with variable x
        Singleton x = Singleton.getInstance();
 
        // Instantiating Singleton class with variable y
        Singleton y = Singleton.getInstance();
 
        // Instantiating Singleton class with variable z
        Singleton z = Singleton.getInstance();
 
        // Printing the hash code for above variable as
        // declared
        System.out.println("Hashcode of x is " + x.hashCode());
        System.out.println("Hashcode of y is " + y.hashCode());
        System.out.println("Hashcode of z is " + z.hashCode());
 
        // Condition check
        if (x == y && y == z) {
            // Print statement
            System.out.println(
                "Three objects point to the same memory location on the heap i.e, to the same object");
        }
        else {
            // Print statement
            System.out.println(
                "Three objects DO NOT point to the same memory location on the heap");
        }
    }
}
```
**Вывод:**
<p style="background-color: navy; color: yellow">
Hashcode of x is 2129789493<br>
Hashcode of y is 2129789493<br>
Hashcode of z is 2129789493<br>
Three objects point to the same memory location on the heap i.e, to the same object</p>
**Объяснение вывода:**
В одноэлементном классе, когда мы впервые вызываем метод getInstance() , он создает объект класса с именем single_instance и возвращает его в переменную. Поскольку single_instance является статическим, он изменяется с нуля на какой-либо объект. В следующий раз, если мы попытаемся вызвать метод getInstance(), поскольку значение single_instance не равно нулю, оно будет возвращено в переменную вместо повторного создания экземпляра класса Singleton. Эта часть выполняется условием if.

В основном классе мы создаем экземпляр одноэлементного класса с тремя объектами x, y и z, вызывая статический метод getInstance(). Но на самом деле после создания объекта x переменные y и z указывают на объект x. Следовательно, если мы изменяем переменные объекта x, это отражается при доступе к переменным объектов y и z. Также, если мы изменяем переменные объекта z, это отражается при доступе к переменным объектов x и y.

### Пример 7

```java
// Java program implementing Singleton class
// with method name as that of class
 
// Class 1
// Helper class
class Singleton {
    // Static variable single_instance of type Singleton
    private static Singleton single_instance = null;
 
    // Declaring a variable of type String
    public String s;
 
    // Constructor of this class
    // Here private constructor is used to
    // restricted to this class itself
    private Singleton() {
        s = "Hello I am a string part of Singleton class";
    }
 
    // Method
    // Static method to create instance of Singleton class
    public static Singleton Singleton() {
        // To ensure only one instance is created
        if (single_instance == null) {
            single_instance = new Singleton();
        }
        return single_instance;
    }
}
 
// Class 2
// Main class
class Main {
    // Main driver method
    public static void main(String args[]) {
        // Instantiating Singleton class with variable x
        Singleton x = Singleton.Singleton();
 
        // Instantiating Singleton class with variable y
        Singleton y = Singleton.Singleton();
 
        // instantiating Singleton class with variable z
        Singleton z = Singleton.Singleton();
 
        // Now  changing variable of instance x
        // via toUpperCase() method
        x.s = (x.s).toUpperCase();
 
        // Print and display commands
        System.out.println("String from x is " + x.s);
        System.out.println("String from y is " + y.s);
        System.out.println("String from z is " + z.s);
        System.out.println("\n");
 
        // Now again changing variable of instance z
        z.s = (z.s).toLowerCase();
 
        System.out.println("String from x is " + x.s);
        System.out.println("String from y is " + y.s);
        System.out.println("String from z is " + z.s);
    }
}
```
**Вывод:**
<p style="background-color: navy; color: yellow">
String from x is HELLO I AM A STRING PART OF SINGLETON CLASS<br>
String from y is HELLO I AM A STRING PART OF SINGLETON CLASS<br>
String from z is HELLO I AM A STRING PART OF SINGLETON CLASS<br>
<br>
String from x is hello i am a string part of singleton class<br>
String from y is hello i am a string part of singleton class<br>
String from z is hello i am a string part of singleton class</p>
**Объяснение:** В классе Singleton, когда мы впервые вызываем метод Singleton(), он создает объект класса Singleton с именем Single_instance и возвращает его в переменную. Поскольку single_instance является статическим, он изменяется с нуля на какой-либо объект. В следующий раз, если мы попытаемся вызвать метод Singleton(), поскольку значение Single_instance не равно нулю, оно будет возвращено в переменную вместо повторного создания экземпляра класса Singleton.

