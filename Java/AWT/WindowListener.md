#Java #awt #WindowListener

## Интерфейс - WindowListener

2024-05-29 11:00

Инструментарий Abstract Window Toolkit ([AWT](AWT)) Java предоставляет набор компонентов графического интерфейса пользователя (GUI) для создания настольных приложений. Когда дело доходит до управления событиями, связанными с окнами, используется интерфейс **_WindowListener_**. Интерфейс **_WindowListener_** предоставляет методы реагирования на события, связанные с окном, такие как открытие, закрытие, активация или деактивация, и другие подобные методы.

### WindowListener в [AWT](AWT)

Интерфейс **_WindowListener_** в Java [AWT](AWT) импортирован из пакета java.awt.event. Это основное соединение между вашим приложением и действиями окна. Реализуя этот интерфейс и переопределяя его методы в своем классе, вы можете реагировать на широкий спектр событий окна.

### Синтаксис WindowListener

```java
public interface WindowListener extends EventListener;
```

Интерфейс **_WindowListener_** в Java объявляется с помощью приведенного выше оператора. Он расширяет интерфейс **_EventListener_**, что указывает на то, что он помогает фиксировать различные события окна в Java-приложениях и реагировать на них.

## Методы интерфейса WindowListener

Ниже приведены **абстрактные** методы интерфейса WindowListener.

| Тип модификатора и метод               | Описание                                                                              |
| -------------------------------------- | ------------------------------------------------------------------------------------- |
| void windowActivated​(WindowEvent e)   | Этот метод вызывается, когда окно настроено как активное.                             |
| void windowClosed​(WindowEvent e)      | Запускается при закрытии окна в результате вызова dispose в окне.                     |
| void window closing​(WindowEvent e)    | Вызывается всякий раз, когда пользователь пытается закрыть окно через системное меню. |
| void windowDeactivated​(WindowEvent e) | Вызывается, когда окно больше не является активным.                                   |
| void windowDeiconified​(WindowEvent e) | Вызывается при преобразовании окна из свернутого в обычное состояние.                 |
| void windowIconified (WindowEvent e)   | Запускается при переходе окна из его обычного свернутого состояния.                   |
| windowOpened​(WindowEvent e)           | Он вызывается при первом появлении окна.                                              |

> **Примечание:** Методы интерфейса **_WindowListener_** унаследованы от интерфейса **_EventListener_**.

#### Пример 1. Демонстрация работы интерфейса WindowListener

```java
// Java program to demonstrate the use of WindowListener 
// interface and its methods 
import java.awt.*; 
import java.awt.event.*; 
import java.awt.event.WindowListener; 
  
// Driver CLass 
public class Window implements WindowListener { 
    public Window() { 
        // Create a frame 
        Frame f = new Frame("WindowListener Example"); 
  
        // Create a label 
        Label l = new Label("WindowListener Example"); 
  
        // Set properties of label 
        l.setBounds(100, 90, 140, 20); 
        l.setForeground(Color.GREEN); 
        l.setFont(new Font("Serif", Font.BOLD, 22)); 
  
        // Add it to the frame 
        f.add(l); 
  
        // Add windowListener to the frame 
        f.addWindowListener(this); 
  
        // Set properties of frame 
        f.setSize(400, 300); 
        f.setLayout(null); 
        f.setVisible(true); 
    } 
  
    // Override all the abstract methods of WindowListener 
    // interface 
    public void windowOpened(WindowEvent e) 
    { 
        System.out.println("Window is opened!"); 
    } 
  
    public void windowClosing(WindowEvent e) 
    { 
        System.out.println("Window is closing..."); 
        System.exit(0); 
    } 
  
    public void windowClosed(WindowEvent e) 
    { 
        System.out.println("Window is closed!"); 
    } 
  
    public void windowIconified(WindowEvent e) 
    { 
        System.out.println("Window is iconified!"); 
    } 
  
    public void windowDeiconified(WindowEvent e) 
    { 
        System.out.println("Window is deiconified!"); 
    } 
  
    public void windowActivated(WindowEvent e) 
    { 
        System.out.println("Window is activated!"); 
    } 
  
    public void windowDeactivated(WindowEvent e) 
    { 
        System.out.println("Window is deactivated!"); 
    } 
  
    // Main method 
    public static void main(String[] args) { 
	    new Window(); 
	} 
}
```
**Вывод:**

![[Ex1-WindowListener.png]]
**Вывод в консоли:**
<p style="background-color: navy; color: yellow">
Window is activated!<br>
Window is opened!<br>
Window is closing...<br>
<br>
Process finished with exit code 0</p>


#### Объяснение примера:

- В приведенном выше коде создается простая рамка или окно с меткой в нем.
- Класс **Window** реализует интерфейс **_WindowListener_**. В этом классе переопределены все методы интерфейса.
- Когда запускается каждое из этих событий window, переопределенные методы выводят сообщения на консоль.
- Например, он выводит "Window is opened!", когда окно открыто, и "Window is closing...", когда пользователь пытается закрыть окно.

#### Пример 2. Мониторинг через WindowAdapter

Если вам нужно только прослушать событие закрытия окна сейчас, мы вообще не заботимся о других операциях, нет необходимости отслеживать события путем реализации интерфейса, потому что, реализуя интерфейс, мы должны реализовать все методы.  

Для решения вышеуказанных проблем вводится шаблон проектирования адаптер и добавляется переходная абстракция между реализацией класса и интерфейсом. Абстрактный класс наследования байтов может покрывать метод события в соответствии с его собственными потребностями. Взяв WindowAdapter в качестве примера, пользователям нужно только унаследовать класс WindowAdapter, и они могут переопределить методы в соответствии со своими потребностями. Если они заботятся только о методе закрытия события формы, то переопределяют только метод windowClosing() в подклассе.
```java
import java.awt.event.WindowAdapter;  
import java.awt.event.WindowEvent;  
import java.awt.Color;  
import javax.swing.JFrame;  
  
class MyWindowEventHandle1 extends WindowAdapter {  
    public void windowClosing(WindowEvent e) {  
        System.out.println("windowClosing -> окно закрыто");  
        System.exit(1);  
    }  
}  
  
public class Main {  
    public static void main(String args[]) {  
        JFrame frame = new JFrame("Прослушивание и обработка событий через адаптер");  
        frame.addWindowListener(new MyWindowEventHandle1()); // Присоединяйся к событию  
        frame.setSize(300, 150);  
        frame.getContentPane().setBackground(Color.yellow);  
        frame.setLocation(300, 200);  
        frame.setVisible(true);  
    }  
}
```
Закройте форму, вывод консоли:
<p style="background-color: navy; color: yellow">
windowClosing --> Окно закрыто</p>

#### Пример 3. Используем анонимный внутренний класс

Если этот процесс прослушивания необходимо выполнить только один раз, нет необходимости устанавливать его в отдельный класс, в настоящее время вы можете использовать анонимный внутренний класс для управления событием.
```java
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;
import java.awt.Color;
import javax.swing.JFrame;

public class Main {
    public static void main(String args[]) {
        JFrame frame = new JFrame(«Используйте анонимно внутри, чтобы прийти»);
        // Присоединяйся к событию
        frame.addWindowListener(
        // Анонимный метод внутреннего класса для мониторинга событий.
        new WindowAdapter() {
            public void windowClosing(WindowEvent e)
            {
                System.out.println("windowClosing -> окно закрыто");
                System.exit(1);
            }
        }); 
        frame.setSize(300, 150);
        frame.getContentPane().setBackground(Color.green);
        frame.setLocation(300, 200);
        frame.setVisible(true);
    }
}
```
Закройте форму, вывод консоли:
<p style="background-color: navy; color: yellow">
windowClosing --> Окно закрыто</p>

### Приложения интерфейса WindowListener

Существует множество вариантов использования интерфейса WindowListener, который мы можем использовать в нашем Java-приложении для выполнения различных действий.

1. ****Подтверждение при выходе:**** Перед завершением работы приложения вы можете запросить у пользователя подтверждение, используя метод windowClosing.
2. ****Сохранение данных:**** Когда окно закроется, вы можете захотеть сохранить любые несохраненные конфигурации или данные.
3. ****Динамические обновления пользовательского интерфейса:**** Когда окно включено или деактивировано, могут быть инициированы определенные действия, такие как обновление пользовательского интерфейса или данных.
4. ****Взаимодействие с медиаплеером:**** Когда пользователь переходит к другому окну или программе в медиаплеере, событие windowDeactivated может использоваться для запуска автоматической остановки воспроизведения.
5. ****Обновления статуса:**** Событие windowDeactivated в приложении чата может использоваться для изменения статуса пользователя на “Отсутствует” или “Неактивен”, если он переходит в другую программу.

  
