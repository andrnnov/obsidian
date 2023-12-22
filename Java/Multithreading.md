#Java #Multithreading #Thread #Runnable 
### Многопоточность в Java ###

2023-12-21 12:33

Существует множество определений многопоточности:
- **Многопоточность** — это способность процессора независимо выполнять процессы или потоки. Все программы выполняются потоками. Поток — это легковесный подпроцесс, наименьшая единица обработки.
- **Многопоточность** — это процесс одновременного выполнения нескольких потоков.

#### Преимущества многопоточности: ####

- с использованием многопоточности можно разрабатывать более адаптивные приложения: мы можем выполнять несколько операций одновременно, например, скачивание некоторых ресурсов и общение в чате одновременно;
- мы можем добиться лучшего использования ресурсов: по умолчанию программа Java является однопоточной. Может быть несколько ядер процессора, которые можно использовать, применяя многопоточность;  
- общая производительность может быть увеличена в несколько раз.

#### Недостатки многопоточности: ####

- потоки манипулируют данными, расположенными в одной и той же памяти, принадлежат одному и тому же процессу, и необходимо обеспечивать синхронизацию и согласованность данных между потоками;
- довольно сложно проектировать многопоточные приложения и трудно отлаживать в случае ошибок;    
- когда потоков много, процессору приходится переключаться между потоками. Этот процесс называется [**_переключением контекста_**.](https://ru.wikipedia.org/wiki/%D0%9F%D0%B5%D1%80%D0%B5%D0%BA%D0%BB%D1%8E%D1%87%D0%B5%D0%BD%D0%B8%D0%B5_%D0%BA%D0%BE%D0%BD%D1%82%D0%B5%D0%BA%D1%81%D1%82%D0%B0) Переключение между потоками — дорогостоящая операция, поскольку процессор должен сохранять локальные данные одного потока и загружать локальные данные другого потока. В конечном счете общая производительность пострадает, а не улучшится, если будет слишком много потоков.

Java предоставляет базовый класс для создания потоков — класс  [Thread](Thread). Существует два способа создания потоков: либо наследование класса [Thread](Thread) и переопределение метода [[Method-Thread#public void run()|run()]], либо реализация интерфейса [Runnable](Runnable) и передача его реализации классу [Thread](Thread) в качестве аргумента конструктора. 

#### Создание потоков путем наследования класса [Thread](Thread) ####

```java
    public class App {      
        public static void main(String[] args) {         
	        var ferrari = new Car("Ferrari");         
	        var bmw = new Car("BMW");         
	        ferrari.start();         
	        bmw.start();         
	        
			System.out.println("Method continues execution... " + 
						"Main method is executed by thread " + 
						Thread.currentThread().getName());
	    }  
	}  
	
	class Car extends Thread {      
		private final String model;      
		
		public Car(String model) {
			this.model = model;     
		}      
		
		@Override     
		public void run() {         
			try { 
				Thread.sleep(1000);
			} catch (InterruptedException exception) {
				exception.printStackTrace();         
			}         
			System.out.println("Car " + model + " is being driven by thread " + 
							Thread.currentThread().getName());     
		}  
	}
```
В приведенном выше фрагменте кода мы создаем класс Car, который наследует класс Thread и переопределяет его метод  run(). Внутри метода run() мы просто выводим модель автомобиля и имя выполняемого потока.

[[Method-Thread#public void Thread.sleep(long milliseconds)|Thread.sleep(1000)]] — останавливает этот поток на заданный период времени (в миллисекундах). В **main**-методе мы создаем два экземпляра (ferrari, bmw) класса Car и вызываем метод [[Method-Thread#public void Thread.start()|start()]] для каждого из них. Затем выводим какое-нибудь сообщение. По умолчанию всякий раз, когда запускается любая Java-программа, она выполняется основным потоком. Запуск этой программы дает следующий вывод.
<p style="background-color:navy; color: yellow">Method continues execution... Main method is executed by thread main<br>
Car Ferrari is being driven by thread Thread-0<br>
Car BMW is being driven by thread Thread-1</p>
Вывод программы

Как видим из вывода, вывод сообщения, которое написали в методе **main** — последняя команда в программе, но она выводится в консоль первой и не ждёт выполнения вызовов методов — ferrari.start() и bmw.start(). Это и есть магия многопоточности. Сколько бы времени ни потребовалось для выполнения методов — ferrari.start() и bmw.start(_), поток main дальше выполняется и не ждёт их завершения.

#### Создание потоков путем реализации интерфейса [Runnable](Runnable) ####

```java
	public class App {      
		public static void main(String[] args) {         
			var ferrari = new Car("Ferrari");         
			var bmw = new Car("BMW");         
			var ferrariThread = new Thread(ferrari, "Ferrari-Thread");         
			var bmwThread = new Thread(bmw, "BMW-Thread");       
			ferrariThread.start();         
			bmwThread.start();         
			System.out.println("Method continues execution... " + 
								"Main method is executed by thread " + 
								Thread.currentThread().getName());     
		}  
	}
	
	class Car implements Runnable {
		private final String model;      
		
		public Car(String model) {
			this.model = model;
		}      
		
		@Override     
		public void run() { 
			try {             
				Thread.sleep(1000);         
			} catch (InterruptedException exception) { 
				exception.printStackTrace();
	        }         
			System.out.println("Car " + model + " is being driven by thread " + 
						    Thread.currentThread().getName());     
		} 
	}
```


Приведенный выше фрагмент кода выполняет ту же логику, которую мы обсуждали выше, однако он немного отличается от предыдущего фрагмента кода. В этом случае мы реализовываем интерфейс [Runnable](Runnable) и переопределяем его метод [[Method-Thread#public void run()|run()]] и передаём их конструктору класса **_`Thread`_**. Один из конструкторов класса [Thread](Thread) принимает интерфейс [Runnable](Runnable) в качестве одного из своих аргументов. Вывод программы аналогичен

<p style="background-color:navy; color: yellow">Method continues execution... Main method is executed by thread main<br>
Car Ferrari is being driven by thread Ferrari-Thread<br>
Car BMW is being driven by thread BMW-Thread</p>

Вывод программы

Принимая во внимание два способа создания потоков, второй считается более предпочтительным, поскольку множественное наследование запрещено в Java, и, унаследовав класс [Thread](Thread), мы не сможем унаследовать какой-либо другой класс. Однако, реализовав интерфейс [Runnable](Runnable), мы сможем унаследовать другой класс. Это небольшое преимущество второго способа.
#### Что произойдет, если мы вызовем метод run() класса Thread? ####
```java
	public class App {
	    public static void main(String[] args) {
		    var ferrari = new Car("Ferrari");         
	        var bmw = new Car("BMW");         
	        ferrari.run();       
	        bmw.run();         
	        System.out.println("Method continues execution... " + 
					            "Main method is executed by thread - " + 
						        Thread.currentThread().getName()); 
		}
	}  
	
	class Car extends Thread {
	    private final String model;      
	    public Car(String model) {         
		    this.model = model;     
		}
		
	@Override     
	public void run() {
		try {             
			Thread.sleep(1000);         
		} catch (InterruptedException exception) {             
			exception.printStackTrace();
		}         
		System.out.println("Car " + model + " is being driven by thread " + 
							Thread.currentThread().getName());     
	}  
}
```

Давайте рассмотрим приведенный выше фрагмент кода. В этом примере аналогичным 
образом мы создали класс Car, который наследует класс Thread, переопределили метод run(), создали два экземпляра класса Car(ferrari, bmw). Вместо вызова метода start() мы вызвали метод run() у экземпляров (ferrari, bmw). Запуск этой программы дает следующий результат
аналогичен.

<p style="background-color:navy; color: yellow">Method continues execution... Main method is executed by thread main<br>
Car Ferrari is being driven by thread main<br>
Car BMW is being driven by thread main</p>
Вывод программы

При вызове метода run(), программа выполняется последовательно, в том порядке, в котором мы написали. Вызов метода run() не создает новый поток, он ведет себя как обычный метод в Java.

#### Процессы и потоки ####

Термины «процесс» и «поток» повсеместно используются, когда речь идет о многопоточности. Давайте подробно рассмотрим эти две концепции.

_**Процесс — это исполняемая программа, или, другими словами, просто запущенная программа**_
- когда вы запускаете какое-нибудь приложение или веб-браузер, запускаются разные процессы;
- операционная система назначает каждому процессу отдельные регистры, программные счетчики, память кучи и стека;  
- процессы полностью независимы и не имеют общей памяти или данных;
- переключение контекста и связь между процессами занимают больше времени, поскольку они тяжелые, создание новых процессов требует больше ресурсов по сравнению с потоками.  

**_Поток — это легкий процесс_**
- это единица выполнения внутри данного процесса, один процесс может иметь один и более потоков;
- каждый поток с данным процессом разделяет память и ресурсы, поэтому программисты имеют дело с параллелизмом и синхронизацией;
- создание нового потока требует меньше ресурсов, чем новый процесс, коммуникация между потоками и переключением контекста быстрее по сравнению с переключением контекста и коммуникации процессов.  

#### Многопоточность и алгоритм разделения времени ####

Представьте, что у вас есть устройство с одним ядром и запущенное приложение, которое требует **_`k`_** потоков (**_`k > 1`_**). В этом случае одному процессору приходится обрабатывать **_`k`_** потоков. Как процессор обрабатывает `k` – потоков? Вот где алгоритм **time-slicing** делает всю магию.

При наличии нескольких потоков время обработки одноядерного процессора распределяется между процессами и потоками. Все потоки планируются процессором случайным образом c помощью **_`thread scheduler`_**, и каждый поток получает минимальное количество времени для выполнения. Как только выделенное время истекает, другой поток получает свою часть процессорного времени и начинает свою часть выполнения. Этот процесс выделения процессором времени потокам продолжается до тех пор, пока все потоки не завершат свое выполнение. Это называется алгоритмом квантования времени (time slicing algorithm). Под капотом потоки выполняются последовательно, однако они выполняются настолько быстро, что у нас возникает ощущение параллельного выполнения. Это называется **_`simulated or fake concurrency`_**.

#### Жизненный цикл потока ####

Потоки проходят через различные состояния в течение своего жизненного цикла:
![[Thread States new.png]]

**NEW** - это состояние, когда поток был создан, но еще не запущен. В этом состоянии поток ожидает своего запуска с помощью метода **start**().  

```java
Runnable runnable = new NewState();
Thread t = new Thread(runnable);
System.out.println(t.getState());
```

В данном случае метод t.getState() в консоль выведет "**NEW**"

В многопоточной среде планировщик потоков(**_Thread-Scheduler_**) (который является частью JVM) выделяет фиксированное количество времени для каждого потока. Таким образом, он выполняется в течение определенного периода времени, затем передает управление другим выполняемым потокам.

Когда мы создаем новый поток и вызываем для него метод **start**(), он переходит из состояния **NEW** в состояние **RUNNABLE**. Потоки в этом состоянии либо запущены, либо готовы к запуску, но они ожидают выделения ресурсов системой.

Например, давайте добавим метод t.start() в наш предыдущий код и попытаемся получить доступ к его текущему состоянию:

```java
Runnable runnable = new NewState();
Thread t = new Thread(runnable);
t.start();
System.out.println(t.getState());
```

Теперь метод t.getState() **вероятнее всего** в консоль выведет "**RUNNABLE**".  
Почему вероятнее всего? Дело в том, что когда наш элемент управления достигнет t.getState(), мы не всегда можем быть уверены, что он будет находиться в состоянии RUNNABLE. Это связано с тем, что в некоторых случаях элемент может быть немедленно запланирован планировщиком потоков (**_Thread-Scheduler)_** и завершить своё выполнение. Именно в таких ситуациях возможны другие результаты.

Поток переходит в состояние **Blocked**, когда ожидает блокировки монитора(**monitor lock**) и пытается получить доступ к разделу кода, который заблокирован каким-либо другим потоком.

Давайте попробуем воспроизвести это состояние:  
```java
public class BlockedState {
    public static void main(String[] args) throws InterruptedException {
        Thread t1 = new Thread(new DemoBlockedRunnable());
        Thread t2 = new Thread(new DemoBlockedRunnable());
        
        t1.start();
        t2.start();
        
        Thread.sleep(1000);
        
        System.out.println(t2.getState());
        System.exit(0);
    }
}

class DemoBlockedRunnable implements Runnable {
    @Override
    public void run() {
        commonResource();
    }
    
    public static synchronized void commonResource() {
        while(true) {
          
        }
    }
}
```
Разбор кода:
1. Мы создали два разных потока – t1 и t2
2. t1 запускается и вводит синхронизированный метод commonResource(); это означает, что только один поток может получить к нему доступ; все остальные последующие потоки, которые попытаются получить доступ к этому методу, будут заблокированы от дальнейшего выполнения до тех пор, пока текущий не завершит обработку.
3. Когда t1 входит в этот метод, он сохраняется в бесконечном цикле while; Это сделано для имитации интенсивной обработки, чтобы все остальные потоки не могли войти в этот метод.
4. Теперь, когда мы запускаем t2, он пытается ввести метод commonResource(), к которому уже обращается t1, таким образом, t2 будет сохранен в состоянии **BLOCKED**.  

Вызовем t2.getState() и получим результат "**BLOCKED**".

Поток находится в состоянии **_WAITING_**, когда он ожидает, пока какой-либо другой поток выполнит определенное действие. Согласно JavaDocs, любой поток может войти в это состояние, вызвав любой из этих трех методов:
1. object.wait()  
2. thread.join()  
3. LockSupport.park()  

Обратите внимание, что в wait() и join() – мы не определяем какой-либо период ожидания, поскольку этот сценарий рассматривается в следующем разделе.

А пока давайте попробуем воспроизвести это состояние:
```java
public class WaitingState implements Runnable {
    public static Thread t1;

    public static void main(String[] args) {
        t1 = new Thread(new WaitingState());
        t1.start();
    }

    public void run() {
        Thread t2 = new Thread(new DemoWaitingStateRunnable());
        t2.start();

        try {
            t2.join();
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
            e.printStackTrace();
        }
    }
}

class DemoWaitingStateRunnable implements Runnable {
    public void run() {
        try {
            Thread.sleep(1000);
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
            e.printStackTrace();
        }
        
        System.out.println(WaitingState.t1.getState());
    }
}
```
Разбор кода:
1. Мы создали и запустили t1
2. t1 создает t2 и запускает его
3. Пока продолжается работа t2, мы вызываем t2.join(), это переводит t1 в состояние ожидания(**_WAITING_**_)_, пока t2 не завершит выполнение.
4. Поскольку t1 ожидает завершения t2, мы вызываем t1.getState() из t2 и получаем результат "**_WAITING_**"

Поток находится в состоянии **TIMED_WAITING**, когда он ожидает, пока другой поток выполнит определенное действие в течение заданного промежутка времени.

Согласно JavaDocs, существует пять способов перевести поток в состояние **TIMED_WAITING**:
1. thread.sleep(long millis)
2. wait(int timeout) or wait(int timeout, int nanos)
3. thread.join(long millis)
4. LockSupport.parkNanos
5. LockSupport.parkUntil

Давайте попробуем воспроизвести это состояние:  
```java
public class TimedWaitingState {
    public static void main(String[] args) throws InterruptedException {
        DemoTimeWaitingRunnable runnable= new DemoTimeWaitingRunnable();
        Thread t1 = new Thread(runnable);
        t1.start();
        Thread.sleep(1000);
        System.out.println(t1.getState());
    }
}

class DemoTimeWaitingRunnable implements Runnable {
    @Override
    public void run() {
        try {
            Thread.sleep(5000);
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
            e.printStackTrace();
        }
    }
}
```
Здесь мы создали и запустили поток t1, который переводится в спящее состояние с периодом ожидания 5 секунд; результатом будет "TIMED_WAITING"

**_TERMINATED -_** это состояние мертвого потока. Поток находится в состоянии **_TERMINATED_**, когда он либо завершил выполнение, либо был как-то прерван.

Попробуем вызвать это состояние:  
```java
public class TerminatedState implements Runnable {
    public static void main(String[] args) throws InterruptedException {
        Thread t1 = new Thread(new TerminatedState());
        t1.start();
        Thread.sleep(1000);
        System.out.println(t1.getState());
    }
    
    @Override
    public void run() {
    }
}
```
Здесь, мы запустили поток t1, но метод Thread.sleep(1000) дает время, для завершения t1, вследствие чего, эта программа выдает нам в результате "**TERMINATED"**.

