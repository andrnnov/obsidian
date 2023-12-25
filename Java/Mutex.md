#Java #Mutex

### Мьютекс ###

2023-12-25 15:53

Мьютекс — это специальный объект для синхронизации потоков. Он «прикреплен» к каждому объекту в Java. Неважно, пользуешься ли ты стандартными классами или создал собственные классы, скажем, `Cat` и `Dog`: **у всех объектов всех классов есть мьютекс**. 

Название «мьютекс» происходит от английского «MUTual EXclusion» — «взаимное исключение», и это отлично отражает его предназначение. **Задача мьютекса — обеспечить такой механизм, чтобы доступ к объекту в определенное время был только у одного потока**.

Один поток в определенное время может работать с общими ресурсами. Попытки других потоков получить доступ к занятым ресурсам будут неудачными. 
У мьютекса есть несколько важных особенностей. 

**Во-первых**, возможны только два состояния — «свободен» и «занят». Это упрощает понимание принципа работы: можно провести параллели с булевыми переменными _true/false_ или двоичной системой счисления 1/0. 

**Во-вторых**, состояниями нельзя управлять напрямую. В Java нет механизмов, которые позволили бы явно взять объект, получить его мьютекс и присвоить ему нужный статус.
Таким образом освободить мьютекс объекта нельзя. Прямой доступ к нему есть только у Java-машины. Программисты же работают с мьютексами с помощью средств языка.

Mutex - это Semaphore со счетчиком доступа 1.
```java
import java.util.concurrent.Semaphore;

public class SemaphoreTest {
    // max 1 people
    static Semaphore semaphore = new Semaphore(1);

    static class MyLockerThread extends Thread {
        String name = "";

        MyLockerThread(String name) {
            this.name = name;
        }

        public void run() {
            try {
                System.out.println(name + " : acquiring lock...");
                System.out.println(name + " : available Semaphore permits now: "
                                + semaphore.availablePermits());
                semaphore.acquire();
                System.out.println(name + " : got the permit!");
                try {
                    for (int i = 1; i <= 5; i++) {
                        System.out.println(name + " : is performing operation " + i
                                + ", available Semaphore permits : "
                                + semaphore.availablePermits());
                        // sleep 1 second
                        Thread.sleep(1000);
                    }
                } finally {
                    // calling release() after a successful acquire()
                    System.out.println(name + " : releasing lock...");
                    semaphore.release();
                    System.out.println(name + " : available Semaphore permits now: "
                                + semaphore.availablePermits());
                }
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }

    public static void main(String[] args) {
        System.out.println("Total available Semaphore permits : "
                + semaphore.availablePermits());

        MyLockerThread t1 = new MyLockerThread("A");
        t1.start();

        MyLockerThread t2 = new MyLockerThread("B");
        t2.start();

        MyLockerThread t3 = new MyLockerThread("C");
        t3.start();

        MyLockerThread t4 = new MyLockerThread("D");
        t4.start();

        MyLockerThread t5 = new MyLockerThread("E");
        t5.start();

        MyLockerThread t6 = new MyLockerThread("F");
        t6.start();
    }
}
```
Выходные данные могут отличаться, но процесс блокировки и разблокировки должен быть одинаковым.
<p style="background-color: navy; color: yellow">Total available Semaphore permits : 1<br>
A : acquiring lock...<br>
B : acquiring lock...<br>
A : available Semaphore permits now: 1<br>
C : acquiring lock...<br>
B : available Semaphore permits now: 1<br>
C : available Semaphore permits now: 0<br>
A : got the permit!<br>
D : acquiring lock...<br>
E : acquiring lock...<br>
A : is performing operation 1, available Semaphore permits : 0<br>
E : available Semaphore permits now: 0<br>
D : available Semaphore permits now: 0<br>
F : acquiring lock...<br>
F : available Semaphore permits now: 0<br>
A : is performing operation 2, available Semaphore permits : 0<br>
A : is performing operation 3, available Semaphore permits : 0<br>
A : is performing operation 4, available Semaphore permits : 0<br>
A : is performing operation 5, available Semaphore permits : 0<br>
A : releasing lock...<br>
A : available Semaphore permits now: 1<br>
B : got the permit!<br>
B : is performing operation 1, available Semaphore permits : 0<br>
B : is performing operation 2, available Semaphore permits : 0<br>
B : is performing operation 3, available Semaphore permits : 0<br>
B : is performing operation 4, available Semaphore permits : 0<br>
B : is performing operation 5, available Semaphore permits : 0<br>
B : releasing lock...<br>
B : available Semaphore permits now: 1<br>
C : got the permit!<br>
C : is performing operation 1, available Semaphore permits : 0<br>
C : is performing operation 2, available Semaphore permits : 0<br>
C : is performing operation 3, available Semaphore permits : 0<br>
C : is performing operation 4, available Semaphore permits : 0<br>
C : is performing operation 5, available Semaphore permits : 0<br>
C : releasing lock...<br>
C : available Semaphore permits now: 1<br>
E : got the permit!<br>
E : is performing operation 1, available Semaphore permits : 0<br>
E : is performing operation 2, available Semaphore permits : 0<br>
E : is performing operation 3, available Semaphore permits : 0<br>
E : is performing operation 4, available Semaphore permits : 0<br>
E : is performing operation 5, available Semaphore permits : 0<br>
E : releasing lock...<br>
E : available Semaphore permits now: 1<br>
D : got the permit!<br>
D : is performing operation 1, available Semaphore permits : 0<br>
D : is performing operation 2, available Semaphore permits : 0<br>
D : is performing operation 3, available Semaphore permits : 0<br>
D : is performing operation 4, available Semaphore permits : 0<br>
D : is performing operation 5, available Semaphore permits : 0<br>
D : releasing lock...<br>
D : available Semaphore permits now: 1<br>
F : got the permit!<br>
F : is performing operation 1, available Semaphore permits : 0<br>
F : is performing operation 2, available Semaphore permits : 0<br>
F : is performing operation 3, available Semaphore permits : 0<br>
F : is performing operation 4, available Semaphore permits : 0<br>
F : is performing operation 5, available Semaphore permits : 0<br>
F : releasing lock...<br>
F : available Semaphore permits now: 1</p>
Как видно, здесь одновременно выполняется только один поток. Это роль мьютекса.