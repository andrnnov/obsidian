#Java #Callback

## Интерфейсы в механизме обратного вызова

2024-06-25 15:06

Одним из распространенных способов использования интерфейсов в Java является создание обратного вызова. Суть обратного вызова состоит в том, что мы создаем действия, которые вызываются при других действиях. То есть одни действия вызываются другими действиями. Стандартный пример - нажатие на кнопку. Когда мы нажимаем на кнопку, мы производим действие, но в ответ на это нажатие запускаются другие действия. Например, нажатие на значок принтера запускает печать документа на принтере и т.д.

Рассмотрим следующий пример:
```java
public class EventsApp {
 
    public static void main(String[] args) {       
        Button button = new Button(new ButtonClickHandler());
        button.click();
        button.click();
        button.click();
    }
}
 
class ButtonClickHandler implements EventHandler{
     
    public void execute() {
        System.out.println("Кнопка нажата!");
    }
}
 
interface EventHandler {
    void execute();
}
 
class Button {
    EventHandler handler;
    Button(EventHandler action) {
        this.handler=action;
    }
    public void click() {
        handler.execute();
    }
}
```
Итак, здесь у нас определен класс Button, который в конструкторе принимает объект интерфейса EventHandler и в методе click (имитация нажатия) вызывает метод execute этого объекта.

Далее определяется реализация EventHandler в виде класса ButtonClickHandler. И в основной программе объект этого класса передается в конструктор Button. Таким образом, через конструктор мы устанавливаем обработчик нажатия кнопки. И при каждом вызове метода button.click() будет вызываться этот обработчик.

В итоге программа выведет на консоль следующий результат:
<p style="background-color: navy; color: yellow">
Кнопка нажата!<br>
Кнопка нажата!<br>
Кнопка нажата!</p>

Но казалось бы, зачем нам выносить все действия в интерфейс, его реализовать, почему бы не написать проще сразу в классе Button:
```java
class Button{
    public void click(){
        System.out.println("Кнопка нажата!");
    }
}
```
Дело в том, что на момент определения класса нам не всегда бывают точно известны те действия, которые должны производиться. Особенно если класс Button и класс основной программы находятся в разных пакетах, библиотеках и могут проектироваться разными разработчиками. К тому же у нас может быть несколько кнопок - объектов Button и для каждого объекта надо определить свое действие. Например, изменим главный класс программы:
```java
public class EventsApp {
 
    public static void main(String[] args) {  
        Button tvButton = new Button(new EventHandler(){
            private boolean on = false;
            public void execute(){
                if(on) {
                    System.out.println("Телевизор выключен..");
                    on=false;
                }   
                else {
                    System.out.println("Телевизор включен!");
                    on=true;
                }
            }
        });
         
        Button printButton = new Button(new EventHandler() {
            public void execute() {
                 
                System.out.println("Запущена печать на принтере...");
            }
        });
         
        tvButton.click();
        printButton.click();
        tvButton.click();
    }
}
```
Здесь у нас две кнопки - одна для включения-выключения телевизора, а другая для печати на принтере. Вместо того, чтобы создавать отдельные классы, реализующие интерфейс EventHandler, здесь обработчики задаются в виде анонимных объектов, которые реализуют интерфейс EventHandler. Причем обработчик кнопки телевизора хранит дополнительное состояние в виде логической переменной on.

В итоге консоль выведет нам следующий результат:
<p style="background-color: navy; color: yellow">
Телевизор включен!<br>
Запущена печать на принтере...<br>
Телевизор выключен..</p>
И в завершении надо сказать, что интерфейсы в данном качестве особенно широко используются в различных графических API - [AWT](AWT), [Swing](Swing), JavaFX, где обработка событий объектов - элементов графического интерфейса особенно актуальна.

#### Пример

В пакет **[javax.swing](Swing)** входит класс **Timer**, который можно использовать для отсечения интервалов времени. Так, если в программе предусмотрены часы, то с помощью класса **Timer** можно отсчитывать каждую секунду и обновлять циферблат часов. При установке таймера задается интервал времени и указывается, что именно должно произойти по его истечении.

Возникает вопрос: Как же указать таймеру, что именно он должен делать? Во многих языках программирования для этого задается имя функции, которую таймер должен периодически вызывать. Но в классах из стандартной библиотеки **Java** применяется объектно-ориентированный подход: таймеру нужно передать объект некоторого класса. После этого таймер вызывает один из методов для данного объекта. Передача объекта - более гибкий механизм, чем вызов функции, поскольку объект может нести дополнительную информацию.

Разумеется, таймер должен знать, какой именно метод следует вызвать. Для этого таймеру нужно указать объект класса, реализующего интерфейс **ActionListener** из пакета **java.awt.event**. Содержимое этого интерфейса представлено ниже:
```java
public interface ActionListener {
    void actionPerformed(ActionEvent event);
}
```
По истечении заданного интервала времени таймер вызывает метод actionPerformed(). Допустим, что через каждые десять секунд требуется выводить на экран сообщение о текущем времени, сопровождаемое звуковым сигналом. Для этого нужно сначала определить класс, реализующий интерфейс ActionListener, а затем ввести операторы, которые должны быть выполнены, в тело метода actionPerformed():
```java
class TimerPrinter implements ActionListener {
    public void actionPerformed(ActionEvent event) {
        Date now = new Date();
        System.out.println("now: " + now);
        Toolkit.getDefaultToolkit().beep();
    }
}
```
Обратите внимание на параметр ActionEvent метода actionPerformed(). Он содержит сведения о событии, например, об инициировавшем его объекте. 

Затем нужно сконструировать объект данного класса и передать его конструктору класса Timer следующим образом:
```java
ActionListener listener = new TimerPrinter();
Timer timer = new Timer(10000, listener);
```
Первый параметр конструктора Timer представляет собой измеряемый в миллисекундах интервал времени между последовательными уведомлениями. Сообщение о текущем времени должно выводиться каждые десять секунд. А второй параметр является объектом класса ActionListener.

И наконец, таймер запускается следующим образом:
```java
timer.start();
```
Приведем ниже исходный текст программы демонстрирующий использование обратных вызовов.
```java
import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.util.Date;

/**
 * <p>Класс TimerTest для тестирования таймера</p>
 * <p>Функция showMessageDialog класса JOptionPane создает диплоговое окно, в котором
 * предлагается завершить программу</p>
 * */
public class TimerTest {
    public static void main(String[] args) {
        ActionListener listener = new TimerPrinter();
        Timer timer = new Timer(10000, listener);
        timer.start();

        JOptionPane.showMessageDialog(null, "Quit program?");
    }
}

/**
 * <p>Класс TimerPrinter реализует интерфейс ActionListener</p>
 * */
class TimerPrinter implements ActionListener {
    /**
     * <p>Функция actionPerformed будет вызываться таймером каждые 10 секунд</p>
     * */
    @Override
    public void actionPerformed(ActionEvent e) {
        Date now = new Date();
        System.out.println("At the tone, the time is " + now);
        Toolkit.getDefaultToolkit().beep();
    }
}
```
**Вывод:**
![[Callback.png]]
<p style="background-color: navy; color: yellow">
At the tone, the time is Tue Jun 25 15:00:52 MSK 2024<br>
At the tone, the time is Tue Jun 25 15:01:02 MSK 2024<br>
At the tone, the time is Tue Jun 25 15:01:12 MSK 2024<br>
At the tone, the time is Tue Jun 25 15:01:22 MSK 2024<br>
At the tone, the time is Tue Jun 25 15:01:32 MSK 2024<br>
At the tone, the time is Tue Jun 25 15:01:42 MSK 2024<br>
At the tone, the time is Tue Jun 25 15:01:52 MSK 2024<br>
At the tone, the time is Tue Jun 25 15:02:02 MSK 2024<br>
<br>
Process finished with exit code 0</p>




