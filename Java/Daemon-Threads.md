#Java #Thread 
### [Потоки-демоны (Daemon Threads)](https://proglib.io/p/vvedenie-v-mnogopotochnost-v-java-chast-2-zhiznennyy-cikl-potokov-thread-join-i-potoki-demony-2022-11-30) ###

2023-12-21 15:37

В Java существует два типа потоков — пользовательские (те, которые мы создаем) потоки и `потоки-демоны`. Когда запускается Java-программа, сразу же начинается выполняться один поток — основной поток. Основной поток запускает метод `main()`. Мы можем создавать новые потоки из основного потока. Основной поток завершает выполнение последним, поскольку он выполняет различные операции завершения работы c потоками ввода и вывода, отключает соединения с базами данных и т. д.
![[Daemon Threads.png]]
`Потоки-демоны` в основном функционируют как вспомогательные потоки, они выполняют разные операции в фоновом режиме. Например, `Garbage Collection` в Java выполняется в фоновом режиме как `поток-демон`.

В основном потоке мы можем создавать столько потоков, сколько необходимо. Более того, класс `Thread` предоставляет метод `setDaemon(boolean)`, который позволяет рабочему (=пользовательскому) потоку превратиться в поток-демон.

**Потоки-демоны:**
- поток с низким приоритетом, работающий в фоновом режиме;  
- поток-демон автоматически завершается виртуальной машиной Java, когда все остальные рабочие (worker threads) потоки завершают выполнение;  
- обычно потоки-демоны используются для операций ввода-вывода и сервисов (в смартфонах для связи Bluetooth или NFC).  

Основное различие между пользовательским потоком и потоком-демон заключается в том, что когда все рабочие (=основные или пользовательские) потоки завершают выполнение или умирают, потоки-демоны автоматически завершаются JVM, даже если они все еще выполняются.

Давайте определим наш собственный поток-демон. Мы создадим поток-демон, который будет печатать сообщение каждую секунду.`
```java
public class App {

    public static void main(String[] args) {
        var worker = new Thread(() -> {
            try {
                Thread.sleep(3000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            var threadName = Thread.currentThread().getName();
            System.out.println("Thread is finishing its execution with name: " +
					             threadName);
        }, "Worker");

        var daemon = new Thread(() -> {
            while (true) {
                try {
                    Thread.sleep(1000);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
                var threadName = Thread.currentThread().getName();
                System.out.println("Thread is executing with name: " + threadName);
            }
        }, "Daemon");
        daemon.setDaemon(true);
        worker.start();
        daemon.start();

        var threadName = Thread.currentThread().getName();
        System.out.println("Thread is executing with name: " + threadName);
    }
}
```
В приведенном выше примере мы создаем два потока и называем их `Worker` и `Daemon`. Поток — `worker` ожидает три секунды, затем печатает сообщение — _«Thread is finishing its execution with name: Worker»_, а затем завершает выполнение.

Поток `daemon` выполняется в цикле, каждую секунду печатает сообщение _«Thread is executing with name: Daemon»_ и никогда не выходит из цикла. Для потока `daemon` инициализируем флаг `daemonFlag`, как true — `daemon.setDaemon(true)`. Поток `daemon` будет работать бесконечно, пока другие потоки не завершат выполнения.

После запуска потоков `worker` и `daemon`, основной поток продолжает выполнение — выводит сообщение _«Thread is executing with name: main»_ и завершает выполнение.

Как только поток `worker` завершит свое выполнение, рабочих потоков не останется, и поток-демон будет завершен `JVM`.

Если мы запустим программу, мы получим следующий вывод.
<p style="background-color: navy; color: yellow">Thread is executing with name: main<br>
Thread is executing with name: Daemon<br>
Thread is executing with name: Daemon<br>
Thread is finishing its execution with name: Worker</p>
Кроме того, `setDaemon(boolean)` можно вызывать только в том случае, если поток находится в состоянии `New` и пока ещё не запущен, иначе мы получим исключение `IllegalThreadStateException`.

#### Еще один пример программы потока демона ####

Давайте возьмем простой пример программы для демонстрации потока демона.
**boolean isDaemon()** проверяет, является ли поток «daemon».
```java
public class MyDaemon implements Runnable {
	public void run() {  
		// Checking whether a thread is Daemon or not
		if(Thread.currentThread().isDaemon()) { 
			System.out.println(Thread.currentThread() + " is a daemon thread");  
		}  
		else {   
		    System.out.println(Thread.currentThread() + " is a user (normal) thread");  
		}
	}  
	
	public static void main(String[] args) {
		MyDaemon obj = new MyDaemon();
		Thread t1 = new Thread(obj, "Thread 1");
	    t1.setDaemon(true); // Set to daemon.

		Thread t2 = new Thread(obj, "Thread 2");
		t1.start(); // Execution starts.
		t2.start();
  
		System.out.println("Main thread ending"); 
	}
}
```
Если мы запустим программу, мы получим следующий вывод.
<p style="background-color: navy; color: yellow">Main thread ending<br>
Thread[Thread 1,5,main] is a daemon thread<br>
Thread[Thread 2,5,main] is a user (normal) thread</p>
Давайте возьмем другой пример программы, в которой мы вызовем метод setDaemon() после запуска потока (т.е. до вызова метода start()), и он выдаст исключение IllegalThreadStateException. Посмотрите на исходный код, чтобы лучше понять.

```java
public class MyDaemon implements Runnable {
	public void run() {  
		System.out.println(Thread.currentThread() + " is a daemon thread");  
	}  
	
	public static void main(String[] args) {
		MyDaemon obj = new MyDaemon();
		Thread t1 = new Thread(obj, "Thread 1");

		t1.start(); // Execution starts.
		t1.setDaemon(true); // It will throw IllegalThreadStateException.
  
		System.out.println("Main thread ending"); 
	}
}
```

Вывод:
<p style="background-color: navy; color: red">Exception in thread "main" Thread[Thread 1,5,main] is a daemon thread
      java.lang.IllegalThreadStateException<br>
	at java.lang.Thread.setDaemon(Unknown Source)<br>
	at thread11.MyDaemon.main(MyDaemon.java:15)</p>
В этой программе мы вызвали метод setDaemon() после вызова метода start(). Следовательно, он вызвал исключение IllegalThreadStateException.

