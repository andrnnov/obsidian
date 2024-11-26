#Java #Lock
### Блокировки пакета concurrent ###

2023-12-29 10:24

Обычная синхронизация обеспечивает надежное обновление множественных общих переменных в многопоточном приложении предупреждая гонку или повреждение данных и гарантирует, что параллельные потоки, синхронизируемые должным образом, увидят последние значения этих переменных. Но такая синхронизация не совершена и имеет некоторые функциональные ограничения:
- невозможно прервать поток, который ожидает блокировки;
- невозможно опрашивать или пытаться получить блокировку, не будучи готовым к долгому ожиданию;
- блокировка должна быть снята в том же стековом фрейме, в котором была начата.

Пакет _java.util.concurrent.locks_ включает классы, которые можно использовать для блокировки ресурсов с определенными условиями, и которые существенно отличаются от встроенной синхронизации и мониторов. Этот пакет разрешает намного большую гибкость в использовании блокировок без условий и с условием. Классы пакета реализуют следующие интерфейсы:

|   |   |
|---|---|
|• Lock |интерфейс поддерживает порядок блокировки и позволяет использовать многократно связанный условный объект _Condition_;|
|• Condition |интерфейс описывает связанные с блокировками переменные, которые могут выполнять функции монитора объекта;|
|• ReadWriteLock |интерфейс поддерживает пару связанных блокировок : одну для чтения и одну для записи.|

#### Интерфейс Lock ####

Интерфейс _Lock_ — это абстракция, допускающая выполнение блокировок, которые реализуются как классы Java, а не как возможность языка (объекта). Это расширяет возможности применения Lock, которые могут иметь различные алгоритмы планирования. Блокировка _Lock_ является инструментом для того, чтобы управлять доступом к совместно используемому ресурсу параллельным потоками.

Реализации интерфейса _Lock_ существенно расширяют возможности блокировок по сравнению c [_synchronized_](synchronized). Интерфейс _Lock_ позволяет осуществлять более гибкое структурирование и поддерживает многократно связанный условный объект _Condition_.

##### Методы интерфейса Lock #####
|Метод|Описание|
|---|---|
|lock()|Получение блокировки |
|lockInterruptibly()|Получение блокировки, если текущий поток не прерывается  |
|newCondition()|Получение нового Condition, связанного с блокировкой Lock  |
|tryLock()|Получение блокировки, если она свободна во время вызова|
|tryLock(long time, TimeUnit unit)|Получение блокировки в течение заданного времени|
|unlock()|Освобождение блокировки|
Дополнительные возможности, предоставляемые блокировкой _Lock_ накладывают определенные обязанности при ее использовании. Так, отсутствие блочно-структурированной блокировки исключает автоматическое ее освобождение, как это происходит с [_synchronized_](synchronized). Поэтому следует использовать следующую структуру кода, включающую блокировку Lock :
```java
Lock lk = ...;
lk.lock();
try {
   // доступ к защищенному блокировкой ресурсу
} finally {
    // освобождение блокировки
    lk.unlock();
}
```
Подробное описание интерфейса Lock представлено [здесь](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/locks/Lock.html).

#### Класс ReentrantLock ####

Класс _ReentrantLock_, реализующий интерфейс _Lock_, также, как и _synchronized_, обеспечивает многопоточность, но имеет дополнительные возможности, связанные с опросом о блокировании (lock polling), ожиданием блокирования в течение определенного времени и прерыванием ожидания блокировки. Кроме того, _ReentrantLock_ предлагает гораздо более высокую эффективность функционирования в условиях жесткой состязательности. Другими словами, когда несколько потоков пытаются получить доступ к совместно используемому ресурсу, виртуальной машине [JVM](JVM) потребуется меньше времени на установление очередности потоков и больше времени на ее выполнение.

В переводе _reentrant_ может означать _повторно используемый_ (повторный вход). Что может означать блокировка _с повторным входом_? Это учет количества получения определенных блокировок. Т.е. один и тот же поток повторно получает одну и ту же блокировку. Но для того, чтобы реально разблокировать необходимо уже будет два раза снять блокировку. Это аналогично использованию _synchronized_; если поток повторно входит в синхронный блок, защищенный монитором, то блокировка не будет снята при выходе потока из второго (или последующего) блока synchronized, блокировка будет снята только когда поток выйдет из первого блока synchronized, в который он вошел под защитой монитора.

Одним из интересных методов интерфейса _Lock_ и его реализации _ReentrantLock_ является запрос блокировки с возможностью прерывания процесса ожидания. Т.е. если поток запрашивает блокировку методом lockInterruptibly() и не получает ее сразу же, то переходит в процесс ожидания. Методом _interrupt_ работу потока можно прервать. Тогда ожидающий блокировки поток просыпается, и генерируется исключительная ситуация InterruptedException. После этого попыток доступа к защищенному ресурсу (получения блокировок) не делается и освобождать блокировку не требуется. Структура кода использования блокировки _lockInterruptibly_ имеет следующий вид:
```java
Lock l = new ReentrantLock();
try {
    l.lockInterruptibly();
    try {
        // работа с защищенным ресурсом
    } finally {
        l.unlock();
    }
} catch (InterruptedException e) {
    System.err.println("Interrupted wait");
}
```
Внутренний блок try-finally получает блокировку и доступ к защищенным ресурсам; после завершения работы блокировка освобождается. Внешний блок try-catch обрабатывает исключительные ситуации запроса блокировки. Если поток прерван в результате исключительной ситуации, то выполняется перехват _catch (InterruptedException)_ и метод снятия блокировки _unlock_ не вызывается.

Практика показывает, что реализация _ReentrantLock_ гораздо более масштабируемая в условиях состязательности, чем _synchronized_. Это значит, что если несколько потоков соперничают за право получения блокировки, общая пропускная способность обычно лучше у _ReentrantLock_, чем у _synchronized_. И наоборот, если особого столкновения за право получения блокировки не наблюдается, то можно использовать и _synchronized_.

Подробное описание ReentrantLock представлено [здесь](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/locks/ReentrantLock.html).

#### Пример использования ReentrantLock ####

В примере ReentrantLockExample, листинг которого представлен ниже, используется внутренний класс _LockClass_ для организации двух потоков. Константы TIME_WAIT и TIME_SLEEP используются потоками для организации определенных задержек при выполнении. Текстовая переменная _resource_ используется в качестве общего ресурса, значение которого будет изменяться внутри потоков. Метод printMessage выводит в консоль сообщения потоков с указанием времени.

В конструкторе примера создается блокировка lock типа _ReentrantLock_ и два потока, которые будут использовать _lock_ для блокирования доступа к текстовому ресурсу. Сначала каждый поток пытается в течение определенного времени (TIME_WAIT, мс) блокировать доступ к ресурсу resource с использованием метода _tryLock_. Если блокировка получена, то текст строки resource изменяется. После этого в потоке выполняется некоторая задержка по времени (TIME_SLEEP, мс) и поток завершает свою работу с освобождением блокировки методом _unlock_. Если поток в течение времени TIME_WAIT не смог блокировать ресурс, то он переходит к стадии задержки и завершению работы.

Оперируя временем ожидания блокировки TIME_WAIT и временем задержки TIME_SLEEP можно дать возможность либо каждому из потока изменить значение resource, либо только одному.
```java
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.concurrent.TimeUnit;
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;
 
public class ReentrantLockExample {
    String      resource = "Hello, World!";
    SimpleDateFormat sdf;
    sdf = new SimpleDateFormat("HH:mm:ss  ");

    Lock  lock;

    final  int  TIME_WAIT  = 7000;
    final  int  TIME_SLEEP = 5000;
    
    ReentrantLockExample() {
        lock = new ReentrantLock();
        Thread thread1;
        Thread thread2;
        thread1 = new Thread(new LockClass("first","Первый поток"));
        thread2 = new Thread(new LockClass("second","Второй поток"));
        thread1.start();
        thread2.start();

        printMessage(null);

        while (thread1.isAlive() || thread2.isAlive()) {
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        System.out.println("\nЗавершение работы примера");
        System.exit(0);
    }
    //-----------------------------------------------------
    void printMessage(final String msg) {
        String text = sdf.format(new Date());
        if (msg == null)
            text += resource;
        else
            text += msg;
        System.out.println(text);
    }
    //-----------------------------------------------------
    class LockClass implements Runnable {
        String name;
        String text;
        public LockClass(String name, String text) {
            this.name = name;
            this.text = text;
        }

        @Override
        public void run() {
            boolean locked = false;
            try {
                // Получение блокировки в течение TIME_WAIT
                locked = lock.tryLock(TIME_WAIT,
                                    TimeUnit.MILLISECONDS);
                if (locked) {
                    resource = text;
                    printMessage(null);
                }
                Thread.sleep(TIME_SLEEP);
            } catch (InterruptedException e) {
                e.printStackTrace();
            } finally{
                // Убираем блокировку
                String text = name + " : завершил работу";
                printMessage(text);
                if (locked)
                    lock.unlock();
            }
        }
    }
    //-----------------------------------------------------
    public static void main(String[] args) {
        new ReentrantLockExample();
    }
}
```
**Сообщения потоков**

Пример исполнен для двух вариантов значений констант TIME_WAIT и TIME_SLEEP. В первом варианте значение TIME_WAIT, равное 7c, больше значения TIME_SLEEP (5c). Поэтому оба потока получают доступ к ресурсу и изменяют значение ресурса.
<p style="background-color: navy; color: yellow">
14:26:09  Hello, World!<br>
14:26:09  Первый поток<br>
14:26:14  first : завершил работу<br>
14:26:14  Второй поток<br>
14:26:19  second : завершил работу<br>
<br>
Завершение работы примера</p>
 Во втором варианте время ожидания TIME_WAIT (5c), меньше времени задержки TIME_SLEEP (7c). Поэтому только один поток получает доступ к ресурсу для изменения значения ресурса; второй поток разрешение на блокировку не получил по времени.
<p style="background-color: navy; color: yellow">
14:28:10  Hello, World!<br>
14:28:10  Второй поток<br>
14:28:17  second : завершил работу<br>
14:28:22  first : завершил работу<br>
<br>
Завершение работы примера</p>
#### Пример блокировки lockInterruptibly ####

Основная идея примера LockInterruptiblyExample связана с тем, чтобы в очередь (в ожидание) на получение блокировки поставить два потока, а в первом потоке, получившем блокировку, прервать работу одного из потоков. Все потоки используют измененный, по сравнению с исходным примером, класс _LockClass_, реализующий интерфейс [Runnable](Runnable).

Следующий код демонстрирует старт трёх потоков; второй и третий потоки стартуют с небольшой задержкой, чтобы надежно первый поток захватил блокировку lock, в противном случае первым захватить блокировку может и второй поток, работу которого необходимо прерывать.
```java
import java.util.Date;
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

import java.text.SimpleDateFormat;

public class LockInterruptiblyExample {
	private String resource = "Hello, World!";
    private Lock   lock;
	
    SimpleDateFormat sdf = new SimpleDateFormat("HH:mm:ss  ");
    final  int  TIME_SLEEP = 7000;
    
    Thread thread1;
    Thread thread2;
    Thread thread3;
    
    LockInterruptiblyExample() {
		lock = new ReentrantLock();
		thread1 = new Thread(new LockClass("first" , "Первый поток")); 
		thread2 = new Thread(new LockClass("second", "Второй поток"));
		thread3 = new Thread(new LockClass("third" , "Третий поток"));

		thread1.start();
    	try {
            Thread.sleep(400);
    		thread2.start();
    		thread3.start();
        } catch (InterruptedException e) {}
		
	    while (thread1.isAlive() || thread2.isAlive() || thread3.isAlive()) {
	    	try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        System.out.println("\nЗавершение работы примера");
        System.exit(0);
	}
	
	void printMessage(final String msg)	{
	    String text = sdf.format(new Date());
	    if (msg == null)
	    	text += resource;
	    else
	    	text += msg;
	    System.out.println(text);
	}
	
	class LockClass implements Runnable {
		String name;
		String text;
	    public LockClass(final String name, final String text) {
	    	this.name = name;
			this.text = text;
		}
	     
	    @Override
	    public void run() {
	    	try {
	    		printMessage("Wait (" + name + ") ...");
	    		lock.lockInterruptibly();
	    	    try {
	            	Thread.sleep(2000);
	    	    	if (name.equalsIgnoreCase("first")) {
	    	    		printMessage("Прерывание второго потока");
	    	    		thread2.interrupt();
	    	    		thread2.join();
	    	    	}
	    	        // доступ к ресурсу
	            	resource = text;
	            	printMessage(null);
	            	Thread.sleep(TIME_SLEEP);
	    	    } finally {
		        	// Убираем блокировку
	    	    	lock.unlock();
	            	String text = name + " : завершил работу";
	            	printMessage(text);
	    	    }
	    	} catch (InterruptedException e) {
	    		printMessage(name + " : interrupted wait");
	    	}
	    }	
    }
	public static void main(String[] args) {
		new LockInterruptiblyExample();
	}
}

```
Метод _run_ класса LockClass (листинг ниже) претерпевает значительные изменения. В первую очередь это касается вызов метода lockInterruptibly для получения блокировки. После этого следует небольшая задержка в 2 сек, и далее выполняется проверка, если это первый поток, то он прерывает работу второго потока. После чего первый поток дает возможность второму потоку завершить работу, а сам изменяет и печатает строку общего ресурса, снимает блокировку и завершает работу. Второй же поток не попадает в секцию try...finally, а завершается с исключением, которое перехватывает catch (InterruptedException).

##### Сообщения потоков #####

Ниже представлены сообщения потоков. Сначала потоки запрашивают блокировку, первый поток, пришедший первым, получает ее, а два потока остаются в ожидании освобождения/получения блокировки. После небольшой задержки первый поток прерывает работу второго потока и ждет его завершения. Далее первый поток освобождает блокировку и завершает работу. Сразу же после этого третий поток получает блокировку и далее по сценарию.
<p style="background-color: navy; color: yellow">
11:17:20  Wait (first) ...<br>
11:17:21  Wait (second) ...<br>
11:17:21  Wait (third) ...<br>
11:17:22  Прерывание второго потока<br>
11:17:22  second : interrupted wait<br>
11:17:22  Первый поток<br>
11:17:29  first : завершил работу<br>
11:17:31  Третий поток<br>
11:17:38  third : завершил работу<br>
<br>
Завершение работы примера</p>

#### Интерфейс Condition ####

Интерфейсное условие _Condition_ в сочетании с блокировкой _Lock_ позволяет заменить методы [монитора](synchronized)/[мьютекса](Mutex) (wait, notify и notifyAll) объектом, управляющим ожиданием событий. Блокировка Lock заменяет использование synchronized, а Condition — объектные методы монитора.

#### Методы интерфейса Condition ####

|Метод|Описание|
|---|---|
|await()|Переводит поток в состояние ожидания до тех пор, пока не будет выполнено некоторое условие или пока другой поток не вызовет методы signal/signalAll|
|await(long time, TimeUnit unit)|Переводит поток в состояние ожидания на определенное время пока не будет выполнено некоторое условие или пока другой поток не вызовет методы signal/signalAll|
|signal()|Сигнализирует потоку, у которого ранее был вызван метод await(), о возможности продолжения работы. Применение аналогично использованию методу notify класса Object|
|signalAll()|Сигнализирует всем потокам, у которых ранее был вызван метод await(), о возможности продолжения работы. Применение аналогично использованию методу notifyAll класса Object|
Условие _Condition_, иначе именуемое как очередь условия, предоставляет средство управления для одного потока, чтобы приостановить его выполнение до тех пор, пока он не будет уведомлен другим потоком. Объект Condition связывают с блокировкой. Чтобы получить Condition для блокировки Lock, используют метод newCondition().
```java
ReentrantLock locker = new ReentrantLock();
Condition condition = locker.newCondition();
```
Чтобы перевести поток в ожидание, если определенное условие не выполняется, то используется метод _await_ :
```java
while (условие)
    condition.await();
```
После завершения всех действий в потоке (при выходе) подается сигнал об изменении условия другим потокам:
```java
condition.signalAll();
```
Подробное описание Condition представлено [здесь](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/locks/Condition.html).

### Пример использования Condition

Пример ReentrantCondExample демонстрирует использование объекта условия _Condition_ с блокировкой _ReentrantLock_. В примере описывается торговый склад, в который производитель завозит товар из списка GOODS. Товар регистрируется в [коллекции](Collections) _goods_. Потребитель забирает товар со склада.

В конструкторе примера создаются торговый склад store и два потока: producer, consumer, исходный код которых представлен ниже. Метод printMessage выводит сообщения потоков в консоль.
```java
import java.text.SimpleDateFormat;

import java.util.Date;
import java.util.List;
import java.util.ArrayList;
import java.util.concurrent.locks.Condition;
import java.util.concurrent.locks.ReentrantLock;

public class ReentrantCondExample {
    Store             store = null;
    SimpleDateFormat  sdf   = null;
    final String[]    GOODS = {"Молоко", "Кефир", "Ряженка", "Кофе", "Чай"};
    List<String>     goods = new ArrayList<String>();

    ReentrantCondExample()
    {
        store = new Store();
        sdf   = new SimpleDateFormat("HH:mm:ss  ");

        Thread producer = new Thread(new Producer()); 
        Thread consumer = new Thread(new Consumer());
        producer.start();
        consumer.start();

        while (producer.isAlive() || consumer.isAlive()) {
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        System.out.println("\nЗавершение работы примера");
        System.exit(0);
        
    }
    //-----------------------------------------------------
    void printMessage(final String msg) {
        if (msg != null) {
            String text = sdf.format(new Date()) + msg;
            System.out.println(text);
        } else
            System.out.println("\tТоваров на складе:" + goods.size());
    }
    //-----------------------------------------------------
    public static void main(String[] args) {
        new ReentrantCondExample();
    }
}
```
Производитель представлен внутренним классом Producer. Время задержки в методе _run_ класса определяет возможный интервал доставки товара. Потребитель представлен классом Consumer. Время задержки в методе _run_ класса определяет возможный интервал реализации товара. Производитель завозит товар чаще (время задержки меньше), чем потребитель забирает товар (время задержки больше). На складе всего 3 места для товара. Таким образом, работу производителя необходимо притормаживать. Эту функцию выполняет блокировка lock с условием _cond_ в классе _Store_.
```java
// Производитель
class Producer implements Runnable {
    public void run() {
        for (int i = 0; i < GOODS.length; i++) {
            store.put(GOODS[i]);
            try {
                Thread.sleep(2000);
            } catch (InterruptedException e) { }
        }
    }
}
//-----------------------------------------------------
// Потребитель
class Consumer implements Runnable {
    public void run(){
        for (int i = 0; i > GOODS.length; i++) {
            try {
                Thread.sleep(8000);
            } catch (InterruptedException e) { }
            store.get();
        }
    }
}
```
Класс Store включает метод получения товара _put_ и метод выдачи товара _get_. Шаблон выполнения операций обоих методов идентичен: сначала метод получает блокировку, чтобы другой поток не вошел в данный метод; после этого выполняется проверка условий. Если условия не соблюдаются, то поток переводится в стадию ожидания методом _cond.await()_. Для второго потока условия должны быть соблюдены (такая бизнес-логика работы склада), и он должен выполнить свою операцию. После этого второй поток «будит» первый, а сам завершает операцию и разблокирует метод. «Разбуженный» первый поток вновь выполняет проверку условия, и далее действует согласно предписанному сценарию (либо продолжение выполнения, либо переход в ожидание).
```java
// Склад с товаром
class Store {
    ReentrantLock  lock;  // блокировка
    Condition      cond;  // условие блокировки

    Store() {
        lock = new ReentrantLock();
        cond = lock.newCondition(); 
    }

    public void get() {
        lock.lock();
        try {
            // ожидание на пустом складе
            while (goods.size() < 1)
                cond.await();

            printMessage("Реализация : " + goods.get(0));
            goods.remove(0);
            printMessage(null);
            // Сигнализация
            cond.signalAll();
        } catch (InterruptedException e){} 
        finally{
            lock.unlock();
        }
    }
    public void put(final String good) {
        lock.lock();
        try {
            // ожидание освобождения места
            while (goods.size() >= 3)
                cond.await();
            goods.add(good);

            printMessage("Доставка : " + good);
            printMessage(null);
            // Сигнализация
            cond.signalAll();
        } catch (InterruptedException e){ }
        finally{
            lock.unlock();
        }
    }
}
```
##### Выполнение примера #####

Сообщения в консоли показывают, что сначала идет наполнение склада до 3-х единиц товара поскольку время задержки Producer (2000 мс) значительно меньше времени задержки Consumer (8000 мс). При полном наполнении склада Producer останавливается в ожидании освобождения склада. Как только со склада забирается товар, т.е. освобождается место, сразу же производитель завозит новый товар и снова переходит в режим ожидания. Таким образом, видим, что блокировка с условием работает точно так, как ей предписано документацией.
