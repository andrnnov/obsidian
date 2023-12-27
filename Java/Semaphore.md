#Java #Semaphore
### Семафор ###

2023-12-25 16:11

Семафор — это средство для синхронизации доступа к какому-то ресурсу. **Его особенность заключается в том, что при создании механизма синхронизации он использует счетчик.** Счетчик указывает нам, сколько потоков одновременно могут получать доступ к общему ресурсу.

Семафоры в Java представлены классом Semaphore. При создании объектов-семафоров мы можем использовать такие конструкторы:
```java
Semaphore(int permits)
Semaphore(int permits, boolean fair)
```
В конструктор мы передаем:
- **`int permits`** — начальное и максимальное значение счетчика. То есть то, сколько потоков одновременно могут иметь доступ к общему ресурсу;  
- **`boolean fair`** — для установления порядка, в котором потоки будут получать доступ. Если `fair` = _true_, доступ предоставляется ожидающим потокам в том порядке, в котором они его запрашивали. Если же он равен _false_, порядок будет определять планировщик потоков.

Для получения разрешения у семафора надо вызвать метод acquire(), который имеет две формы:
```java
void acquire() throws InterruptedException
void acquire(int permits) throws InterruptedException
```
Для получения одного разрешения применяется первый вариант, а для получения нескольких разрешений - второй вариант.

После вызова этого метода пока поток не получит разрешение, он блокируется.

После окончания работы с ресурсом полученное ранее разрешение надо освободить с помощью метода release():
```java
void release()
void release(int permits)
```
Первый вариант метода освобождает одно разрешение, а второй вариант - количество разрешений, указанных в permits.

##### Пример 1. Используем семафор в простом примере: #####
```java
import java.util.concurrent.Semaphore;
 
public class Program {
    public static void main(String[] args) {
        Semaphore sem = new Semaphore(1); // 1 разрешение
        CommonResource res = new CommonResource();
        new Thread(new CountThread(res, sem, "CountThread 1")).start();
        new Thread(new CountThread(res, sem, "CountThread 2")).start();
        new Thread(new CountThread(res, sem, "CountThread 3")).start();
    }
}
class CommonResource{
    int x=0;  
}
 
class CountThread implements Runnable{
    CommonResource res;
    Semaphore sem;
    String name;
    CountThread(CommonResource res, Semaphore sem, String name){
        this.res=res;
        this.sem=sem;
        this.name=name;
    }
      
    public void run(){
        try{
            System.out.println(name + " ожидает разрешение");
            sem.acquire();
            res.x=1;
            for (int i = 1; i < 5; i++){
                System.out.println(this.name + ": " + res.x);
                res.x++;
                Thread.sleep(100);
            }
        }
        catch(InterruptedException e){System.out.println(e.getMessage());}
        System.out.println(name + " освобождает разрешение");
        sem.release();
    }
}
```
Итак, здесь есть общий ресурс CommonResource с полем x, которое изменяется каждым потоком. Потоки представлены классом CountThread, который получает семафор и выполняет некоторые действия над ресурсом. В основном классе программы эти потоки запускаются. В итоге мы получим следующий вывод:
<p style="background-color: navy; color: yellow">
CountThread 1 ожидает разрешение<br>
CountThread 2 ожидает разрешение<br>
CountThread 3 ожидает разрешение<br>
CountThread 1: 1<br>
CountThread 1: 2<br>
CountThread 1: 3<br>
CountThread 1: 4<br>
CountThread 1 освобождает разрешение<br>
CountThread 3: 1<br>
CountThread 3: 2<br>
CountThread 3: 3<br>
CountThread 3: 4<br>
CountThread 3 освобождает разрешение<br>
CountThread 2: 1<br>
CountThread 2: 2<br>
CountThread 2: 3<br>
CountThread 2: 4<br>
CountThread 2 освобождает разрешение</p>

##### Пример 2. Классический пример использования семафоров — [задача об обедающих философах](https://ru.wikipedia.org/wiki/%D0%97%D0%B0%D0%B4%D0%B0%D1%87%D0%B0_%D0%BE%D0%B1_%D0%BE%D0%B1%D0%B5%D0%B4%D0%B0%D1%8E%D1%89%D0%B8%D1%85_%D1%84%D0%B8%D0%BB%D0%BE%D1%81%D0%BE%D1%84%D0%B0%D1%85) #####

Представь, что у нас есть 5 философов, которым нужно пообедать. При этом у нас есть один стол, и одновременно находиться за ним могут не более двух человек. Наша задача — накормить всех философов. Никто из них не должен остаться голодным, и при этом они не должны «заблокировать» друг друга при попытке сесть за стол (мы должны избежать deadlock). 

Вот как будет выглядеть наш класс философа:
```java
class Philosopher extends Thread {
   private Semaphore sem;
   // поел ли философ
   private boolean full = false;
   private String name;

   Philosopher(Semaphore sem, String name) {
       this.sem=sem;
       this.name=name;
   }

   public void run()
   {
       try
       {
           // если философ еще не ел
           if (!full) {
               //Запрашиваем у семафора разрешение на выполнение
               sem.acquire();
               System.out.println (name + " садится за стол");
               // философ ест
               sleep(300);
               full = true;
               System.out.println (name + " поел! Он выходит из-за стола");
               sem.release();
               // философ ушел, освободив место другим
               sleep(300);
           }
       }
       catch(InterruptedException e) {
           System.out.println ("Что-то пошло не так!");
       }
   }
}
```
А вот код для запуска нашей программы:
```java
public class Main {

   public static void main(String[] args) {
       Semaphore sem = new Semaphore(2);
       
       new Philosopher(sem,"Сократ").start();
       new Philosopher(sem,"Платон").start();
       new Philosopher(sem,"Аристотель").start();
       new Philosopher(sem,"Фалес").start();
       new Philosopher(sem,"Пифагор").start();
   }
}
```
Мы создали семафор со счетчиком 2, чтобы соответствовать условию, одновременно есть могут только два философа. То есть, одновременно работать могут только два потока, ведь наш класс Philosopher унаследован от [Thread](Thread).

Методы acquire() и release() класса Semaphore управляют его счетчиком разрешений. Метод acquire() запрашивает разрешение на доступ к ресурсу у семафора. Если счетчик > 0, разрешение предоставляется, а счетчик уменьшается на 1. Метод release() «освобождает» выданное ранее разрешение и возвращает его в счетчик (увеличивает счетчик разрешений семафора на 1).

Вот какой вывод в консоль мы получили:
<p style="background-color: navy; color: yellow">Сократ садится за стол<br>
Платон садится за стол<br>
Сократ поел! Он выходит из-за стола<br>
Платон поел! Он выходит из-за стола<br>
Аристотель садится за стол<br>
Пифагор садится за стол<br>
Аристотель поел! Он выходит из-за стола<br>
Пифагор поел! Он выходит из-за стола<br>
Фалес садится за стол<br>
Фалес поел! Он выходит из-за стола</p>
Можно заметить некоторое сходство между [мьютексом](Mutex) и семафором. У них, в общем-то, одинаковое предназначение: синхронизировать доступ к какому-то ресурсу.

Разница только в том, что [мьютекс](Mutex) объекта может захватить одновременно только один поток, а в случае с семафором используется счетчик потоков, и доступ к ресурсу могут получить сразу несколько из них. 
И это не просто случайное сходство. На самом деле **[мьютекс](Mutex) — это одноместный семафор**. То есть, это семафор, счетчик которого изначально установлен в значении 1. Его еще называют «двоичным семафором», поскольку его счетчик может иметь только 2 значения — 1 («свободно») и 0 («занято»).

##### Пример 3. Парковка #####

Рассмотрим следующий пример. Существует парковка, которая одновременно может вмещать не более 5 автомобилей. Если парковка заполнена полностью, то вновь прибывший автомобиль должен подождать пока не освободится хотя бы одно место. После этого он сможет припарковаться.
```java
import java.util.concurrent.Semaphore;

public class Parking {
    //Парковочное место занято - true, свободно - false
    private static final boolean[] PARKING_PLACES = new boolean[5];
    //Устанавливаем флаг "справедливый", в таком случае метод
    //aсquire() будет раздавать разрешения в порядке очереди
    private static final Semaphore SEMAPHORE = new Semaphore(5, true);

    public static void main(String[] args) throws InterruptedException {
        for (int i = 1; i <= 7; i++) {
            new Thread(new Car(i)).start();
            Thread.sleep(400);
        }
    }

    public static class Car implements Runnable {
        private int carNumber;

        public Car(int carNumber) {
            this.carNumber = carNumber;
        }

        @Override
        public void run() {
            System.out.printf("Автомобиль №%d подъехал к парковке.\n", carNumber);
            try {
                //acquire() запрашивает доступ к следующему за вызовом этого метода блоку кода,
                //если доступ не разрешен, поток вызвавший этот метод блокируется до тех пор,
                //пока семафор не разрешит доступ
                SEMAPHORE.acquire();

                int parkingNumber = -1;

                //Ищем свободное место и паркуемся
                synchronized (PARKING_PLACES){
                    for (int i = 0; i < 5; i++)
                        if (!PARKING_PLACES[i]) {      //Если место свободно
                            PARKING_PLACES[i] = true;  //занимаем его
                            parkingNumber = i;         //Наличие свободного места, гарантирует семафор
                            System.out.printf("Автомобиль №%d припарковался на месте %d.\n", carNumber, i);
                            break;
                        }
                }

                Thread.sleep(5000);       //Уходим за покупками, к примеру

                synchronized (PARKING_PLACES) {
                    PARKING_PLACES[parkingNumber] = false;//Освобождаем место
                }
                
                //release(), напротив, освобождает ресурс
                SEMAPHORE.release();
                System.out.printf("Автомобиль №%d покинул парковку.\n", carNumber);
            } catch (InterruptedException e) {
            }
        }
    }
}
```
Результат работы программы:
<p style="background-color: navy; color: yellow">
Автомобиль №1 подъехал к парковке. <br>
Автомобиль №1 припарковался на месте 0.  <br>
Автомобиль №2 подъехал к парковке.  <br>
Автомобиль №2 припарковался на месте 1. <br> 
Автомобиль №3 подъехал к парковке.  <br>
Автомобиль №3 припарковался на месте 2. <br> 
Автомобиль №4 подъехал к парковке.  <br>
Автомобиль №4 припарковался на месте 3. <br> 
Автомобиль №5 подъехал к парковке.  <br>
Автомобиль №5 припарковался на месте 4. <br> 
Автомобиль №6 подъехал к парковке.  <br>
Автомобиль №7 подъехал к парковке.  <br>
Автомобиль №1 покинул парковку.  <br>
Автомобиль №6 припарковался на месте 0.  <br>
Автомобиль №2 покинул парковку.  <br>
Автомобиль №7 припарковался на месте 1.  <br>
Автомобиль №3 покинул парковку.  <br>
Автомобиль №4 покинул парковку.  <br>
Автомобиль №5 покинул парковку.  <br>
Автомобиль №6 покинул парковку.  <br>
Автомобиль №7 покинул парковку.</p>
Семафор отлично подходит для решения такой задачи: он не дает автомобилю (потоку) припарковаться (зайти в заданный блок кода и воспользоваться общим ресурсом) если мест на парковке нет (счётчик равен 0) Стоит отметить, что класс Semaphore поддерживает захват и освобождение более чем одного разрешения за раз, но в данном задаче это не нужно.
