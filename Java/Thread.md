#Java #Thread
### Класс Thread ###

2023-12-19 15:37

В классе _Thread_ определены семь перегруженных конструкторов, большое количество методов, предназначенных для работы с потоками, и три константы (приоритеты выполнения потока).
#### Конструкторы класса Thread ####

[[Method-Thread#Thread()|Thread()]];
[[Method-Thread#Thread(Runnable r)|Thread(Runnable target)]];
[[Method-Thread#Thread(Runnable r, String name)|Thread(Runnable target, String name)]];
[[Method-Thread#Thread(String name)|Thread(String name)]];
Thread(ThreadGroup group, Runnable target);
Thread(ThreadGroup group, Runnable target, String name);
Thread(ThreadGroup group, String name);
где :
- target – экземпляр класса реализующего интерфейс [Runnable](Runnable);
- name – имя создаваемого потока;
- group – группа к которой относится поток.

Несмотря на то, что главный поток создаётся автоматически, им можно управлять. Для этого необходимо создать объект класса _Thread_ вызовом метода [[Method-Thread#public void Thread.currentThread()|currentThread()]].
#### Методы класса Thread ####

Наиболее часто используемые методы класса _Thread_ для управления потоками:
- long getId() - получение идентификатора потока;
- [[Method-Thread#public String Thread.getName()|String getName()]] - получение имени потока;
- [[Method-Thread#public int Thread.currentThread().getPriority()|int getPriority()]] - получение приоритета потока;
- [[Multithreading#Жизненный цикл потока|State getState()]] - определение состояния потока;
- [[Method-Thread#public void Thread.currentThread()|static Thread currentThread()]] - возвращает ссылку на объект Thread, в который он был вызван;
- [[Kill-Thread#Метод interrupt()|void interrupt()]] - прерывание выполнения потока;
- [[Method-Thread#Метод Thread.isAlive()|boolean isAlive()]] - проверка, выполняется ли поток;
- [[Daemon-Threads#Еще один пример программы потока демона|boolean isDaemon()]] - проверка, является ли поток «daemon»;
- [void join()](Thread.join()) - ожидание завершения потока;
- [[Method-Thread#public void Thread.join(long milliseconds)|void join(millis)]] - ожидание millis миллисекунд завершения потока;
- [void notify()](wait-notify) - «пробуждение» отдельного потока, ожидающего «сигнала»;
- [void notifyAll()](wait-notify) - «пробуждение» всех потоков, ожидающих «сигнала»;
- [[Method-Thread#public void run()|void run()]] - запуск потока, если поток был создан с использованием интерфейса Runnable;
- [[Method-Thread#public String Thread.setName(String name)|setName(String threadName)]] – задает имя потока;
- [void setDaemon(bool)](Daemon-Threads) - определение «daemon» потока;
- [[Method-Thread#public void Thread.currentThread().setPriority(int priority)|void setPriority(int)]] - определение приоритета потока;
- [[Method-Thread#public void Thread.sleep(long milliseconds)|void sleep(int)]] - приостановка потока на заданное время;
- [[Method-Thread#public void Thread.start()|void start()]] - запуск потока;
- [void wait()](wait-notify) - приостановка потока, пока другой поток не вызовет метод notify();
- void wait(millis) - приостановка потока на millis миллисекунд или пока другой поток не вызовет метод notify();
- [[Method-Thread#Метод Thread.yield()|yield()]] - позволяет досрочно завершить квант времени текущей нити или, другими словами, переключает процессор на следующую нить.

#### [[Multithreading#Жизненный цикл потока|Жизненный цикл потока]] ####

При выполнении программы объект Thread может находиться в одном из четырех основных состояний: «новый», «работоспособный», «неработоспособный» и «пассивный». При создании потока он получает состояние «новый» (NEW) и не выполняется. Для перевода потока из состояния «новый» в «работоспособный» (RUNNABLE) следует выполнить метод start(), вызывающий метод run().

![[Thread States new.png]]

Поток может находиться в одном из состояний, соответствующих элементам статически вложенного перечисления Thread.State:
NEW — поток создан, но еще не запущен;  
RUNNABLE — поток выполняется;  
BLOCKED — поток блокирован;  
WAITING — поток ждет окончания работы другого потока;  
TIMED_WAITING — поток некоторое время ждет окончания другого потока;  
TERMINATED — поток завершен.
#### Пример использования [Thread](Thread) ####

В примере ChickenEgg рассматривается параллельная работа двух потоков (главный поток и поток Egg), в которых идет спор, «что было раньше, яйцо или курица?». Каждый поток высказывает свое мнение после небольшой задержки, формируемой методом ChickenEgg.getTimeSleep(). Побеждает тот поток, который последним говорит свое слово.
```java
import java.util.Random;

class Egg extends Thread
{
    @Override
    public void run()
    {
        for(int i = 0; i < 5; i++) {
            try {
                // Приостанавливаем поток
                sleep(ChickenEgg.getTimeSleep());
                System.out.println("Яйцо");
            }catch(InterruptedException e){}
        }
    }
}
public class ChickenEgg
{
    public static int getTimeSleep()
    {
        final Random random = new Random();
        int tm = random.nextInt(1000);
        if (tm < 10)
            tm *= 100;
        else if (tm < 100)
            tm *= 10;
        return tm;
    }
    public static void main(String[] args)
    {
        Egg egg = new Egg (); // Создание потока
        System.out.println(
                  "Начинаем спор : кто появился первым ?");

        egg.start(); // Запуск потока
        for(int i = 0; i < 5; i++) {
            try {
                // Приостанавливаем поток
                Thread.sleep(ChickenEgg.getTimeSleep());
                System.out.println("Курица");	
            }catch(InterruptedException e){}
        }
        if(egg.isAlive()) {
            // Cказало ли яйцо последнее слово?
            try {
                // Ждем, пока яйцо закончит высказываться
                egg.join();
            } catch (InterruptedException e){}

            System.out.println("Первым появилось яйцо !!!");
        } else {
            //если оппонент уже закончил высказываться
            System.out.println("Первой появилась курица !!!");
        }
        System.out.println("Спор закончен");
    }
}
```
При выполнении программы в консоль было выведено следующее сообщение.
<p style="background-color: navy; color: yellow">Начинаем спор : кто появился первым ?
Курица<br>
Курица<br>
Яйцо<br>
Курица<br>
Яйцо<br>
Яйцо<br>
Курица<br>
Курица<br>
Яйцо<br>
Яйцо<br>
Первым появилось яйцо !!!<br>
Спор закончен</p>

Невозможно точно предсказать, какой поток закончит высказываться последним. При следующем запуске «победитель» может измениться. Это происходит вследствии так называемого «асинхронного выполнения кода». Асинхронность обеспечивает независимость выполнения потоков. Или, другими словами, параллельные потоки независимы друг от друга, за исключением случаев, когда бизнес-логика зависимости выполнения потоков определяется предусмотренными для этого средств языка.

