#Java #Thread 
### Конструкторы класса Thread ###

#### Thread() ####

Выделяет новый объект Thread.
```java
public class ThreadConstructor extends Thread {
    public void run() {
        System.out.println("This is example of Thread Constructor");
    }

    public static void main(String args[]) {
        ThreadConstructor t = new ThreadConstructor();
        t.start();
    }
}
```

#### Thread(String name) ####

Выделяет новый объект Thread. Полная программа приведена ниже.
```java
public class ThreadConstructor1 extends Thread{
    String tname;

    ThreadConstructor1(String tname) {
        this.tname = tname;
    }

    public void run() {
        System.out.println(tname);
    }

    public static void main(String args[]) {
        ThreadConstructor1 t = new ThreadConstructor1("First Thread");
        t.start();
    }
}
```

#### Thread(Runnable r) ####

Выделяет новый объект Thread. Полная программа приведена ниже.
```java
public class ThreadConstructor2 implements Runnable {

    public void run() {
        System.out.println("This is the example of Thread(Runnable target) constructor");
    }

    public static void main(String args[]) {
        ThreadConstructor2 s = new ThreadConstructor2();
        Thread t = new Thread(s);
        t.start();
    }
}
```

#### Thread(Runnable r, String name) ####

Выделяет новый объект Thread. Полная программа приведена ниже.
```java
public class ThreadConstructor3 implements Runnable {

    ThreadConstructor3() {
    }

    public void run() {
        System.out.println("This is the example of Thread(Runnable target, String name) constructor");
    }

    public static void main(String args[]) {
        ThreadConstructor3 s = new ThreadConstructor3();
        Thread t = new Thread(s, "CsharpCorner");

        t.start();
    }
}
```

### Методы класса Thread в Java ###

2023-12-20 12:04
#### public void run() ####

Этот метод используется для выполнения действия для потока. Полная программа приведена ниже.
```java
public class ThreadRunMethod extends Thread {
    public void run() {
        System.out.println("This is the example of run() method");
    }

    public static void main(String args[]) {
        ThreadRunMethod t = new ThreadRunMethod();
        t.start();
    }
}
```

#### public void Thread.start() ####

Этот метод используется для запуска потока. JVM вызывает метод run() для запуска потока.
```java
public class ThreadStartMethod extends Thread {

    public void run() {
        System.out.println("This is the example of start() method");
    }

    public static void main(String args[]) {
        ThreadStartMethod s = new ThreadStartMethod();
        s.start();
    }
}
```

#### public void Thread.sleep(long milliseconds) ####

Метод класса потоков sleep () используется для перехода потока в режим ожидания на определенный промежуток времени. Если один поток переходит в режим ожидания на указанное время, то планировщик потоков переключает другие потоки и так далее.
```java
public class ThreadSleepMethod extends Thread {

    public void run() {
        for (int i = 0; i < 5; i++) {
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                System.out.println(e);
            }
            System.out.println(i);
        }
    }

    public static void main(String args[]) {
        ThreadSleepMethod t1 = new ThreadSleepMethod();
        ThreadSleepMethod t2 = new ThreadSleepMethod();
        t1.start();
        t2.start();
    }
}
```
Вывод следующего кода генерирует следующий результат.
<p style="background-color: navy; color: yellow">0<br>
0<br>
1<br>
1<br>
2<br>
2<br>
3<br>
3<br>
4<br>
4</p>

#### public void Thread.join() ####

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

#### public void Thread.join(long milliseconds) ####

Этот метод используется для ожидания завершения потока в течение указанной миллисекунды.
```java
public class ThreadJoinMethod2 extends Thread {

    public void run() {
        for (int i = 0; i <= 3; i++) {
            try {
                Thread.sleep(700);
            } catch (Exception e) {
                System.out.println(e);
            }
            System.out.println(i);
        }
    }

    public static void main(String args[]) {
        ThreadJoinMethod2 t1 = new ThreadJoinMethod2();
        ThreadJoinMethod2 t2 = new ThreadJoinMethod2();
        ThreadJoinMethod2 t3 = new ThreadJoinMethod2();
        t1.start();
        try {
            t1.join(1000);
        } catch (Exception e) {
            System.out.println(e);
        }
        t2.start();
        t3.start();
        System.out.println("This is Thread join() method example");

    }
}
```
Вывод следующего кода сгенерировал следующий результат.
<p style="background-color: navy; color: yellow">0<br>
This is Thread join() method example<br>
1<br>
0<br>
0<br>
2<br>
1<br>
1<br>
3<br>
2<br>
2<br>
3<br>
3</p>

#### public void Thread.currentThread() ####

Статический метод класса Thread currentThread() возвращает ссылку на объект Thread, который вызывает этот метод.
```java
public class ThreadCurrentMethod extends Thread {

        @Override
        public void run() {
            Thread t = Thread.currentThread();
            String threadName = t.getName();
            System.out.println("Inside run() method:  " + threadName);
        }

        public static void main(String[] args) {
            ThreadCurrentMethod ct = new ThreadCurrentMethod ();
            ct.start();

            Thread t = Thread.currentThread();
            String threadName = t.getName();
            System.out.println("Inside  main() method:  " + threadName);
        }
    }
```
Вывод следующего кода генерирует следующий результат.
<p style="background-color: navy; color: yellow">Inside  main() method:  main<br>
Inside run() method:  Thread-0</p>

#### public String Thread.getName() ####

Этот метод используется для возврата имени потока.
```java
public class ThreadGetnameMethod extends Thread {

    public void run() {
        System.out.println("threads running fast...");
    }

    public static void main(String args[]) {
        ThreadGetnameMethod t1 = new ThreadGetnameMethod();

        System.out.println("Name of thread 1:" + t1.getName());
        t1.start();
    }
}
```
Вывод следующего кода генерирует следующий результат.
<p style="background-color: navy; color: yellow">Name of thread 1:Thread-0<br>
threads running fast...</p>
#### public String Thread.setName(String name) ####

Этот метод используется для изменения имени потока.
```java
public class ThreadSetnameMethod extends Thread {

    public void run() {
        System.out.println("threads running fast...");
    }

    public static void main(String args[]) {
        ThreadSetnameMethod t1 = new ThreadSetnameMethod();
        System.out.println("Name of thread 1: " + t1.getName());
        t1.start();

        t1.setName("Strong Thread");
        System.out.println("After changing name of thread 1:" + t1.getName());
    }
}
```
На выходе кода генерируется следующий результат.
<p style="background-color: navy; color: yellow">Name of thread 1:Thread-0<br>
After changing name of thread 1: Strong Thread<br>
threads running fast...</p>

#### public int Thread.currentThread().getPriority() ####

Этот метод используется для возврата приоритета потока. Полная программа приведена ниже.
```java
public class ThreadGetPriorityMethod extends Thread {

    public void run() {

        System.out.println("Current thread priority is:" + Thread.currentThread().getPriority());
    }

    public static void main(String args[]) {
        ThreadGetPriorityMethod g = new ThreadGetPriorityMethod();
        g.start();
    }
}
```
Вывод следующего кода генерирует следующий результат.
<p style="background-color: navy; color: yellow">Current thread priority is:5</p>

#### public void Thread.currentThread().setPriority(int priority) ####

Этот метод используется для изменения приоритета потока. Приоритеты потоков представлены цифрами от 1 до 10. В классе Thread определены три константы:
1. public static int MIN_PRIORITY
2. public static int NORM_PRIORITY
3. public static int MAX_PRIORITY
По умолчанию приоритет потока NORM_PRIORITY равен 5.
Значение MIN_PRORITY равно 0, а MAX_PRIORITY равно 10.
```java
public class ThreadSetPriorityMethiod extends Thread {

    public void run() {
        System.out.println("Current thread priority is:" + Thread.currentThread().getPriority());
    }

    public static void main(String args[]) {
        ThreadSetPriorityMethiod s = new ThreadSetPriorityMethiod();
        s.setPriority(8);
        // s.setPriority(Thread.MAX_PRIORITY); !!!
        s.start();
    }
}
```
Вывод следующего кода генерирует следующий результат.
<p style="background-color: navy; color: yellow">Current thread priority is:8</p>
Планировщик потоков является частью JVM, которая решает, какой поток должен выполняться. Нет никакой гарантии, что планировщик выберет тот поток, который будет выполняться. Любой поток в состоянии выполнения может быть выбран планировщиком в качестве единственного запущенного потока, и если поток не находится в состоянии выполнения, то он не может быть выбран в качестве текущего запущенного потока. Некоторые методы могут в некоторой степени влиять на планировщик, и мы не можем контролировать поведение планировщика потоков. В одном процессе на Java может выполняться только один поток одновременно.

Планировщик потоков обычно использует упреждающее планирование или планирование с разделением по времени для планирования потоков в Java.

При упреждающем планировании задачи с наивысшим приоритетом выполняются до тех пор, пока не перейдут в ожидающее или мертвое состояние или не появится задача с более высоким приоритетом.

При планировании с разделением по времени задача выполняется в течение заранее определенного отрезка времени, а затем повторно входит в пул готовых задач. Затем планировщик потоков решает, какая задача должна выполняться следующей, на основе приоритета и других факторов.

