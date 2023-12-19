#Java  #Runnable
### Интерфейс Runnable ###

 2023-12-19 16:46

Интерфейс _Runnable_ содержит только один метод _run()_ :
```java
interface Runnable
{
    void run();
}
```
Метод _run()_ выполняется при запуске потока. После определения объекта Runnable он передается в один из конструкторов класса [Thread](Thread).
#### Пример класса RunnableExample, реализующего интерфейс Runnable ####
```java
class MyThread implements Runnable
{
    Thread thread;
    MyThread() {
        thread = new Thread(this, "Дополнительный поток");
        System.out.println("Создан дополнительный поток " + thread);
        thread.start();
    }
    @Override
    public void run() {
        try {
            for (int i = 5; i > 0; i--) {
                System.out.println(
                           "\tдополнительный поток: " + i);
                Thread.sleep(500);
            }
        } catch (InterruptedException e) {
            System.out.println(
                         "\tдополнительный поток прерван");
        }
        System.out.println(
                        "\tдополнительный поток завершён");
    }
}
public class RunnableExample
{
    public static void main(String[] args)
    {
        new MyThread();
        try {
            for (int i = 5; i > 0; i--) {
                System.out.println("Главный поток: " + i);
                Thread.sleep(1000);
            }
        } catch (InterruptedException e) {
            System.out.println("Главный поток прерван");
        }
        System.out.println("Главный поток завершён");
    }
}
```
При выполнении программы в консоль было выведено следующее сообщение.
<p style="background-color: navy; color: yellow">Создан дополнительный поток <br>Thread[Дополнительный поток,5,main]<br>
Главный поток: 5<br>
	дополнительный поток: 5<br>
	дополнительный поток: 4<br>
Главный поток: 4<br>
	дополнительный поток: 3<br>
	дополнительный поток: 2<br>
Главный поток: 3<br>
	дополнительный поток: 1<br>
	дополнительный поток завершён<br>
Главный поток: 2<br>
Главный поток: 1<br>
Главный поток завершён</p>
