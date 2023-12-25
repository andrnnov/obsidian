#Java #interrapt
### [Завершение и прерывание потока](https://metanit.com/java/tutorial/8.4.php) ###

2023-12-25 11:27

При организации потока в виде бесконечного цикла (например, при прослушивании определенного порта на предмет получения данных), мы должны предусмотреть механизм завершения потока.

#### Завершение потока ####

Распространенный способ завершения потока представляет опрос логической переменной. И если она равна, например, false, то поток завершает бесконечный цикл и заканчивает свое выполнение.

Определим следующий класс потока:
```java
class MyThread implements Runnable {
    private boolean isActive;
      
    void disable(){
        isActive=false;
    }
      
    MyThread(){
       isActive = true;
    }
      
    public void run(){   
        System.out.printf("%s started... \n", Thread.currentThread().getName());
        int counter=1; // счетчик циклов
        while(isActive){
            System.out.println("Loop " + counter++);
            try{
                Thread.sleep(400);
            }
            catch(InterruptedException e){
                System.out.println("Thread has been interrupted");
            }
        }
        System.out.printf("%s finished... \n", Thread.currentThread().getName());
    }
}
```
Переменная `isActive` указывает на активность потока. С помощью метода `disable()` мы можем сбросить состояние этой переменной.

Теперь используем этот класс:
```java
public static void main(String[] args) {  
    System.out.println("Main thread started...");
    MyThread myThread = new MyThread();
    new Thread(myThread,"MyThread").start();
         
    try{
        Thread.sleep(1100);
        myThread.disable();
        Thread.sleep(1000);
    }
    catch(InterruptedException e){
        System.out.println("Thread has been interrupted");
    }
    System.out.println("Main thread finished...");
}
```
Итак, вначале запускается дочерний поток: `new Thread(myThread,"MyThread").start()`. Затем на 1100 миллисекунд останавливаем Main thread и потом вызываем метод `myThread.disable()`, который переключает в потоке флаг isActive. И дочерний поток завершается.

#### Метод interrupt() ####

Еще один способ вызова завершения или прерывания потока представляет метод interrupt(). Вызов этого метода устанавливает у потока статус, что он прерван. Сам метод возвращает true, если поток может быть прерван, в ином случае возвращается false.

Метод **interrupt()** также **способен вывести поток из состояния ожидания или спячки**. Т.е. если у потока были вызваны методы sleep() или wait() – текущее состояние прервется и будет выброшено исключение InterruptedException. **Флаг в этом случае не выставляется**.

При этом сам вызов этого метода НЕ завершает поток, он только устанавливает статус: в частности, метод isInterrupted() класса [Thread](Thread) будет возвращать значение true. Мы можем проверить значение возвращаемое данным методом и произвести некоторые действия. Например:
```java
class JThread extends Thread {
      
    JThread(String name){
        super(name);
    }
    public void run(){  
        System.out.printf("%s started... \n", Thread.currentThread().getName());
        int counter=1; // счетчик циклов
        while(!isInterrupted()){
            System.out.println("Loop " + counter++);
        }
        System.out.printf("%s finished... \n", Thread.currentThread().getName());
    }
}

public class Program {
    public static void main(String[] args) {        
        System.out.println("Main thread started...");
        JThread t = new JThread("JThread");
        t.start();
        try{
            Thread.sleep(150);
            t.interrupt();
            Thread.sleep(150);
        }
        catch(InterruptedException e){
            System.out.println("Thread has been interrupted");
        }
        System.out.println("Main thread finished...");
    }
}
```
В классе, который унаследован от [Thread](Thread), мы можем получить статус текущего потока с помощью метода isInterrupted(). И пока этот метод возвращает false, мы можем выполнять цикл. А после того, как будет вызван метод interrupt, isInterrupted() возвратит true, и соответственно произойдет выход из цикла.

Возможный консольный вывод:
<p style="background-color: navy; color: yellow">Main thread started...<br>
JThread started...<br>
Loop 1<br>
Loop 2<br>
Loop 3<br>
Loop 4<br>
JThread finished...<br>
Main thread finished...</p>

Если основная функциональность заключена в классе, который реализует интерфейс [Runnable](Runnable), то там можно проверять статус потока с помощью метода Thread.currentThread().isInterrupted():

```java
class MyThread implements Runnable {
    public void run(){
        System.out.printf("%s started... \n", Thread.currentThread().getName());
        int counter=1; // счетчик циклов
        while(!Thread.currentThread().isInterrupted()){
            System.out.println("Loop " + counter++);
        }
        System.out.printf("%s finished... \n", Thread.currentThread().getName());
    }
}
public class Program {
    public static void main(String[] args) {
        System.out.println("Main thread started...");
        MyThread myThread = new MyThread();
        Thread t = new Thread(myThread,"MyThread"); 
        t.start();
        try{
            Thread.sleep(150);
            t.interrupt();
            Thread.sleep(150);
        }
        catch(InterruptedException e){
            System.out.println("Thread has been interrupted");
        }
        System.out.println("Main thread finished...");
    }
}
```
однако при получении статуса потока с помощью метода `isInterrupted()` следует учитывать, что если мы обрабатываем в цикле исключение InterruptedException в блоке catch, то при перехвате исключения статус потока автоматически сбрасывается, и после этого isInterrupted будет возвращать false.

Например, добавим в цикл потока задержку с помощью метода [[Method-Thread#public void Thread.sleep(long milliseconds)|sleep]]:
```java
public void run(){   
    System.out.printf("%s started... \n", Thread.currentThread().getName());
    int counter=1; // счетчик циклов
    while(!isInterrupted()){
        System.out.println("Loop " + counter++);
        try{
            Thread.sleep(100);
        }
        catch(InterruptedException e){
            System.out.println(getName() + " has been interrupted");
            System.out.println(isInterrupted());    // false
            interrupt();    // повторно сбрасываем состояние
        }
    }
    System.out.printf("%s finished... \n", Thread.currentThread().getName());
}
```
Когда поток вызовет метод interrupt, метод sleep сгенерирует исключение InterruptedException, и управление перейдет к блоку catch. Но если мы проверим статус потока, то увидим, что метод isInterrupted возвращает false. Как вариант, в этом случае мы можем повторно прервать текущий поток, опять же вызвав метод interrupt(). Тогда при новой итерации цикла while метода isInterrupted возвратит true, и произойдет выход из цикла.

Либо мы можем сразу же в блоке catch выйти из цикла с помощью break:
```java
while(!isInterrupted()){ 
    System.out.println("Loop " + counter++);
    try{
        Thread.sleep(100);
    }
    catch(InterruptedException e){
        System.out.println(getName() + " has been interrupted");
        break;  // выход из цикла
    }
}
```
Если бесконечный цикл помещен в конструкцию try...catch, то достаточно обработать InterruptedException:
```java
public void run(){   
    System.out.printf("%s started... \n", Thread.currentThread().getName());
    int counter=1; // счетчик циклов
    try{
        while(!isInterrupted()){
            System.out.println("Loop " + counter++);
            Thread.sleep(100);
        }
    }
    catch(InterruptedException e){
        System.out.println(getName() + " has been interrupted");
    }
    System.out.printf("%s finished... \n", Thread.currentThread().getName());
}
```

