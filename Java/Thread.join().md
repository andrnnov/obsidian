#Java  #Thread 
### [Жизненный цикл потоков, Thread.join()](https://proglib.io/p/vvedenie-v-mnogopotochnost-v-java-chast-2-zhiznennyy-cikl-potokov-thread-join-i-potoki-demony-2022-11-30) ###

2023-12-21 14:50

В Java потоки проходят четыре состояния в своём жизненном цикле:
- New
- Running
- Waiting — `[ Blocked, Waiting, TimedWaiting]`
- Dead / Terminated
![[Thread States.png]]
`New` — состояние, когда поток создан и готов к использованию. Это состояние, когда мы еще не запустили поток.

`Running` — состояние, в которое поток переходит после того, как мы его запустили. В этом состоянии поток выполняет свою работу, т. е. логику, которую мы определили.

`Waiting` — состояние ожидания, в которое поток может перейти во время своего выполнения. Есть три состояний ожидания — `Blocked`, `Waiting`, `TimedWaiting`. Например, когда поток пытается получить [_монитор объекта_](https://ru.wikipedia.org/wiki/%D0%9C%D0%BE%D0%BD%D0%B8%D1%82%D0%BE%D1%80_(%D1%81%D0%B8%D0%BD%D1%85%D1%80%D0%BE%D0%BD%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D1%8F)), он входит в состояние блокировки — `Blocked`; когда поток ожидает выполнения другого потока, тогда поток переходит в состояние ожидания — `Waiting`, а когда поток ожидает только определённое количество времени для выполнения другого потока, поток входит в состояние — `TimedWaiting`. Поток возвращается в состояние — `Running`, как только другие потоки выполнили или освободили монитор объекта. Поток может бесконечно менять свое состояние из состояния — `Running` в состояние — `Waiting` и наоборот.

`Dead / Terminated` — состояние, в которое поток переходит после завершения выполнения или в случае возникновения исключений. Поток после выполнения не может быть запущен снова. Если мы попытаемся запустить поток в состоянии — `Dead / Terminated`, мы получим исключение `IllegalStateException`.

#### public void Thread.join() ####

Ещё один полезный метод, предоставляемый классом `Thread` — `join()`. При написании многопоточных программ могут быть случаи, когда необходимо ждать завершения выполнения какого-либо потока и после этого продолжить выполнение текущего потока. В таких случаях полезно применять метод — `join()`. Данный метод позволяет одному потоку ожидать завершения другого.

Рассмотрим следующий пример:
```java
public class App {
    public static void main(String[] args) {
        var threadTwo = new Thread(() -> {
            try {
                Thread.sleep(2000);
                int counter = 0;
                for (int i = 0; i < 1000; i++) {
                    counter ++;
                }
                var thread = Thread.currentThread().getName();
                System.out.println(thread + " has finished its execution, counter = " +
					                 counter);
            } catch (InterruptedException exception) {
                exception.printStackTrace();
        }, "Counter thread");
        threadTwo.start();
        System.out.println("Main method executing");
    }
}
```
В этом примере мы создаем поток — `threadTwo`, который ждёт две секунды и считает до 1000. А затем выводит сообщение о завершении его выполнения. Если мы запустим эту программу, мы получим следующий вывод.
<p style="background-color: navy; color: yellow">Main method executing<br>
Counter thread has finished its execution, counter = 1000</p>
Как только `threadTwo` начинает выполняться, метод `main()` продолжает свое выполнение, он печатает — _«Main method executing»_ и завершает свое выполнение. Параллельно выполняется `threadTwo`, считает до 1000, потом выводит — _«Counter has finished its execution, counter = 1000»_ и заканчивает выполнение.

Но что, если мы хотим, чтобы основной поток ждал завершения выполнения потока — `threadTwo`? Как этого добиться? Довольно просто — использование `join()` делает то, что нужно.  
  
Рассмотрим следующий пример:
```java
public class App {

    public static void main(String[] args) throws InterruptedException {
        var threadTwo = new Thread(() -> {
            try {
                Thread.sleep(2000);
                int counter = 0;
                for (int i = 0; i < 1000; i++) {
                    counter ++;
                }
                var thread = Thread.currentThread().getName();
                System.out.println(thread + " has finished its execution, counter = " +
					                counter);
            } catch (InterruptedException exception) {
                exception.printStackTrace();
            }
        }, "Counter thread");
        threadTwo.start();
        threadTwo.join();
        System.out.println("Main method executing");
    }
}
```
Данный пример почти то же самое с предыдущим примером, но с небольшой разницей. Сразу после `threadTwo.start()` мы добавили вызов метода — `join()` у потока `threadTwo`. Если мы запустим эту программу, мы получим следующий вывод.
<p style="background-color: navy; color: yellow">Counter thread has finished its execution, counter = 1000<br>
Main method executing</p>
Порядок вывода в этом примере изменился. Сразу после запуска `threadTwo`, основной поток вызывает метод `join()` у потока — `threadTwo`. Это приводит к тому, что основной поток переходит в состояние ожидания и ждет, пока `threadTwo` не завершит свое выполнение. Как видно из вывода, поток — `threadTwo` завершает выполнение, считает до 1000 и выводит сообщение — _«Counter has finished its execution, counter = 1000»_ и заканчивает выполнение. После этого mainThread продолжает свое выполнение и выводит следующее сообщение — _«Main method executing»_.

Вдобавок, если во время выполнения потока — `threadTwo` возникнет исключение, основной поток продолжит свое выполнение аналогично как в случае с успешным выполнением потока — `threadTwo`, ситуаций [`deadlock`](https://ru.wikipedia.org/wiki/Deadlock) не будет.

####  Пример 2 ####

Метод join используется для ожидания завершения потока.
```java
public class ThreadJoinMethod1 extends Thread {

    public void run() {
        for (int i = 0; i <= 3; i++) {
            try {
                Thread.sleep(1000);
            } catch (Exception e) {
                System.out.println(e);
            }
            System.out.println(i);
        }
    }

    public static void main(String args[]) {
        ThreadJoinMethod1 t1 = new ThreadJoinMethod1();
        ThreadJoinMethod1 t2 = new ThreadJoinMethod1();
        ThreadJoinMethod1 t3 = new ThreadJoinMethod1();
        t1.start();
        try {
            t1.join();
        } catch (Exception e) {
            System.out.println(e);
        }

        t2.start();
        t3.start();

        System.out.println("This is Thread join() method example");
    }
}
```
Выходные данные следующего кода перечислены ниже.
<p style="background-color: navy; color: yellow">0<br>
1<br>
2<br>
3<br>
This is Thread join() method example<br>
0<br>
0<br>
1<br>
1<br>
2<br>
2<br>
3<br>
3</p>


