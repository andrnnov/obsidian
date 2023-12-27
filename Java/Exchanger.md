#Java #Exchanger
### [Обмен между потоками. Класс Exchanger](https://metanit.com/java/tutorial/8.7.php) ###

2023-12-27 12:32

Класс Exchanger предназначен для обмена данными между потоками. Он является типизированным и типизируется типом данных, которыми потоки должны обмениваться.

Обмен данными производится с помощью единственного метода этого класса exchange():
```java
V exchange(V x) throws InterruptedException
V exchange(V x, long timeout, TimeUnit unit) throws InterruptedException, TimeoutException
```
Параметр x представляет буфер данных для обмена. Вторая форма метода также определяет параметр timeout - время ожидания и unit - тип временных единиц, применяемых для параметра timeout.

Данный класс очень просто использовать:
```java
import java.util.concurrent.Exchanger;
  
public class Program {
    public static void main(String[] args) {
        Exchanger<String> ex = new Exchanger<String>();
        new Thread(new PutThread(ex)).start();
        new Thread(new GetThread(ex)).start();
    }
}
  
class PutThread implements Runnable{
    Exchanger<String> exchanger;
    String message;
  
    PutThread(Exchanger<String> ex){
        this.exchanger=ex;
        message = "Hello Java!";
    }
    public void run(){
        try{
            message=exchanger.exchange(message);
            System.out.println("PutThread has received: " + message);
        }
        catch(InterruptedException ex){
            System.out.println(ex.getMessage());
        }
    }
} 
class GetThread implements Runnable{
    Exchanger<String> exchanger;
    String message;
  
    GetThread(Exchanger<String> ex){
        this.exchanger=ex;
        message = "Hello World!";
    }
    public void run(){
        try{
            message=exchanger.exchange(message);
            System.out.println("GetThread has received: " + message);
        }
        catch(InterruptedException ex){
            System.out.println(ex.getMessage());
        }
    }
} 
```
В классе PutThread отправляет в буфер сообщение "Hello Java!":
```java
message=exchanger.exchange(message);
```
Причем в ответ метод exchange возвращает данные, которые отправил в буфер другой поток. То есть происходит обмен данными. Хотя нам необязательно получать данные, мы можем просто их отправить:
```java
exchanger.exchange(message);
```
Логика класса GetThread аналогична - также отправляется сообщение.

В итоге консоль выведет следующий результат:
<p style="background-color:navy; color: yellow">
PutThread has received: Hello World!<br>
GetThread has received: Hello Java!</p>
##### [Пример использования Exchanger](https://habr.com/ru/articles/277669/) #####

Рассмотрим следующий пример. Есть два грузовика: один едет из пункта A в пункт D, другой из пункта B в пункт С. Дороги AD и BC пересекаются в пункте E. Из пунктов A и B нужно доставить посылки в пункты C и D. Для этого грузовики в пункте E должны встретиться и обменяться соответствующими посылками.
```java
import java.util.concurrent.Exchanger;

public class Delivery {
    //Создаем обменник, который будет обмениваться типом String
    private static final Exchanger<String> EXCHANGER = new Exchanger<>();

    public static void main(String[] args) throws InterruptedException {
	    //Формируем груз для 1-го грузовика
        String[] p1 = new String[]{"{посылка A->D}", "{посылка A->C}"};
        //Формируем груз для 2-го грузовика
        String[] p2 = new String[]{"{посылка B->C}", "{посылка B->D}"};
        //Отправляем 1-й грузовик из А в D
        new Thread(new Truck(1, "A", "D", p1)).start();
        Thread.sleep(100);
        //Отправляем 2-й грузовик из В в С
        new Thread(new Truck(2, "B", "C", p2)).start();
    }

    public static class Truck implements Runnable {
        private int number;
        private String dep;
        private String dest;
        private String[] parcels;

        public Truck(int number, String departure, String destination, String[] parcels) {
            this.number = number;
            this.dep = departure;
            this.dest = destination;
            this.parcels = parcels;
        }

        @Override
        public void run() {
            try {
                System.out.printf("В грузовик №%d погрузили: %s и %s.\n", number, parcels[0], parcels[1]);
                System.out.printf("Грузовик №%d выехал из пункта %s в пункт %s.\n", number, dep, dest);
                Thread.sleep(1000 + (long) Math.random() * 5000);
                System.out.printf("Грузовик №%d приехал в пункт Е.\n", number);
                parcels[1] = EXCHANGER.exchange(parcels[1]);//При вызове exchange() поток блокируется и ждет
                //пока другой поток вызовет exchange(), после этого произойдет обмен посылками
                System.out.printf("В грузовик №%d переместили посылку для пункта %s.\n", number, dest);
                Thread.sleep(1000 + (long) Math.random() * 5000);
                System.out.printf("Грузовик №%d приехал в %s и доставил: %s и %s.\n", number, dest, parcels[0], parcels[1]);
            } catch (InterruptedException e) {
            }
        }
    }
}
```
Результат работы программы:
<p style="background-color:navy; color: yellow">
В грузовик №1 погрузили: {посылка A->D} и {посылка A->C}.  <br>
Грузовик №1 выехал из пункта A в пункт D.  <br>
В грузовик №2 погрузили: {посылка B->C} и {посылка B->D}.  <br>
Грузовик №2 выехал из пункта B в пункт C.  <br>
Грузовик №1 приехал в пункт Е.  <br>
Грузовик №2 приехал в пункт Е.  <br>
В грузовик №2 переместили посылку для пункта C.  <br>
В грузовик №1 переместили посылку для пункта D.  <br>
Грузовик №2 приехал в C и доставил: {посылка B->C} и {посылка A->C}.  <br>
Грузовик №1 приехал в D и доставил: {посылка A->D} и {посылка B->D}.</p>
Как мы видим, когда один грузовик (один поток) приезжает в пункт Е (достигает точки синхронизации), он ждет пока другой грузовик (другой поток) приедет в пункт Е (достигнет точки синхронизации). После этого происходит обмен посылками (String) и оба грузовика (потока) продолжают свой путь (работу).