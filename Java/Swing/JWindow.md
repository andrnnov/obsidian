#Java #Swing #JWindow

## Окно JWindow

2024-05-15 15:47

**_JWindow_** является частью Java [Swing](Swing) и может отображаться в любой части рабочего стола пользователя. Он отличается от [JFrame](JFrame) тем, что в **_JWindow_** нет строки заголовка или кнопок управления окнами, таких как свернуть, развернуть и закрыть, которые есть в [JFrame](JFRAme). **_JWindow_** может содержать несколько компонентов, таких как кнопки и метки.

### Конструктор класса

1. **JWindow()** : создает пустое окно без указания владельца.
2. **JWindow(Frame o)** : создает пустое окно с указанным фреймом в качестве его владельца.
3. **JWindow(Frame o)** : создает пустое окно с указанным фреймом в качестве его владельца.
4. **JWindow(Window o)** : создает пустое окно с указанным окном в качестве его владельца.
5. **JWindow(Window o, GraphicsConfiguration g)** : создает пустое окно с указанным окном в качестве владельца и указанной графической конфигурацией.
6. **JWindow(GraphicsConfiguration g)** : создает пустое окно с указанной конфигурацией графики g.

### Часто используемые методы

1. **setLayout(LayoutManager m)** : устанавливает макет окна в соответствии с указанным менеджером макета.
2. **setContentPane(Container c)** : устанавливает свойство ContentPane окна.
3. **getContentPane()** : получить контейнер, который является ContentPane для этого окна.
4. **add(Component c)** : добавляет компонент в окно.
5. **isVisible(boolean b)** : устанавливает видимость окна, если значение логического значения истинно, то оно видимо, иначе невидимо.
6. **update(Graphics g)** : вызывает функцию Paint(g)
7. **Remove(Component c)** : удаляет компонент c.
8. **getGraphics()** : возвращает графический контекст компонента.
9. **getLayeredPane()** : возвращает многоуровневую панель окна.
10. **setContentPane(Container c)** : устанавливает панель содержимого для окна.
11. **setLayeredPane(JLayeredPane l)** : установить многоуровневую панель для окна.
12. **setRootPane(JRootPane r)** : устанавливает rootPane для окна.
13. **setTransferHandler(TransferHandler n)** : устанавливает свойство TransferHandler, которое представляет собой механизм поддержки передачи данных в этот компонент.
14. **setRootPaneCheckingEnabled (логическое значение включено)** : устанавливает, пересылаются ли вызовы add и setLayout в contentPane.
15. **setRootPane(JRootPane root)** : устанавливает свойство rootPane окна.
16. **setGlassPane(Component glass)** : устанавливает свойство glassPane окна.
17. **repaint(long time, int x, int y, int width, int height)** : перерисовывает указанный прямоугольник этого компонента в течение миллисекунд.
18. **Remove(Component c)** : удаляет указанный компонент из окна.
19. **isRootPaneCheckingEnabled()** : Возвращает, пересылаются ли вызовы add и setLayout в contentPane или нет.
20. **getTransferHandler()** : возвращает свойство TransferHandler.
21. **getRootPane()** : возвращает объект rootPane для этого окна.
22. **getGlassPane()** : Возвращает объект glassPane для этого окна.
23. **createRootPane()** : вызывается методами конструктора для создания rootPane по умолчанию.
24. **addImpl(Component co, Object c, int i)** : добавляет указанный дочерний компонент в окно.

### Следующие программы проиллюстрируют использование JWindow

#### Пример 1. программа для создания простого JWindow

```java
// java Program to create a simple JWindow 
import java.awt.event.*; 
import java.awt.*; 
import javax.swing.*; 
  
class solveit extends JFrame implements ActionListener { 
    // frame 
    static JFrame f; 
    // main class 
    public static void main(String[] args) { 
        // create a new frame 
        f = new JFrame("frame"); 
        // create a object 
        solveit s = new solveit(); 
        // create a panel 
        JPanel p = new JPanel(); 
        JButton b = new JButton("click"); 
        // add actionlistener to button 
        b.addActionListener(s); 
        // add button to panel 
        p.add(b); 
        f.add(p); 
        // set the size of frame 
        f.setSize(400, 300); 
        f.setVisible(true); 
    } 
  
    // if button is pressed 
    public void actionPerformed(ActionEvent e) { 
        String s = e.getActionCommand(); 
        if (s.equals("click")) { 
            // create a window 
            JWindow w = new JWindow(f); 
            // set panel 
            JPanel p = new JPanel(); 
            // create a label 
            JLabel l = new JLabel("this is a window"); 
            // set border 
            p.setBorder(BorderFactory.createLineBorder(Color.black)); 
            p.add(l); 
            w.add(p); 
            // set background 
            p.setBackground(Color.red); 
            // setsize of window 
            w.setSize(200, 100); 
            // set visibility of window 
            w.setVisible(true); 
            // set location of window 
            w.setLocation(100, 100); 
        } 
    } 
} 
```
**Выход :**
![[Ex1-JWindow.png]]

#### Пример 2. Программа для создания нескольких JWindow(где одно окно является владельцем другого)

```java
// java program to create a multiple  JWindow .( where one window is the owner of the other )< 
import java.awt.event.*; 
import java.awt.*; 
import javax.swing.*; 
class solveit extends JFrame implements ActionListener { 
    // frame 
    static JFrame f; 
    // windows 
    JWindow w, w1; 
    // object of class 
    static solveit s; 
    // main class 
    public static void main(String[] args) { 
        // create a new frame 
        f = new JFrame("frame"); 
        // create a object 
        s = new solveit(); 
        // create a panel 
        JPanel p = new JPanel(); 
        JButton b = new JButton("click"); 
        // add actionlistener to button 
        b.addActionListener(s); 
        // add button to panel 
        p.add(b); 
        f.add(p); 
        // set the size of frame 
        f.setSize(400, 400); 
        f.setVisible(true); 
    } 
  
    // if button is pressed 
    public void actionPerformed(ActionEvent e) { 
        String s1 = e.getActionCommand(); 
        if (s1.equals("click")) { 
            // create a window 
            w = new JWindow(f); 
            // set panel 
            JPanel p = new JPanel(); 
            // create a label 
            JLabel l = new JLabel("this is first window"); 
            // create a button 
            JButton b = new JButton("Click me"); 
            // add Action listener 
            b.addActionListener(s); 
            // set border 
            p.setBorder(BorderFactory.createLineBorder(Color.black)); 
            p.add(l); 
            p.add(b); 
            w.add(p); 
            // set background 
            p.setBackground(Color.red); 
            // setsize of window 
            w.setSize(200, 100); 
            // set visibility of window 
            w.setVisible(true); 
            // set location of window 
            w.setLocation(100, 100); 
        } 
        else { 
            // create a window 
            w1 = new JWindow(w); 
            // set panel 
            JPanel p = new JPanel(); 
            // create a label 
            JLabel l = new JLabel("this is the second window"); 
            // set border 
            p.setBorder(BorderFactory.createLineBorder(Color.black)); 
            p.add(l); 
            w1.add(p); 
            // set background 
            p.setBackground(Color.blue); 
            // setsize of window 
            w1.setSize(200, 100); 
            // set visibility of window 
            w1.setVisible(true); 
            // set location of window 
            w1.setLocation(210, 210); 
        } 
    } 
} 
```
**Выход:**
![[Ex2-JWindow.png]]

#### Пример 3. 

Основная идея использования окна без рамки **_JWindow_** заключается в копировании части "изображения рабочего стола" в окно приложения. Благодаря появившемуся в пакете JDK 1.3 классу Robot можно "снимать" экранную копию рабочего стола.
```java
// Пример использования окна без рамки JWindow
import javax.swing.*;
import java.awt.*;

// Класс прорисовки изображения
class ImageDraw extends JComponent {
    private Image capture;
    ImageDraw (Image capture) {
        this.capture = capture;
    }
    public void paintComponent(Graphics g) {
        // Прорисовка изображения
        g.drawImage(capture, 0, 0, this);
    }
}
public class JWindowTest extends JWindow {
    // изображение "рабочего стола"
    private Image capture;
    // Размер окна 
    private int window_w = 300, window_h = 300;

    public JWindowTest() {
        super();
        // Определение положение окна на экране
        setLocation(200, 100);
        // Определение размера окна
        setSize (window_w, window_h);
        try {
            // "Вырезаем" часть изображения "рабочего стола"
            Robot robot = new Robot();
            capture = robot.createScreenCapture(
                      new Rectangle(5, 5, window_w, window_h));
        } catch (Exception ex) { ex.printStackTrace(); }
        // Добавляем в интерфейс изображение
        getContentPane().add(new ImageDraw(capture));
        // Открываем окно
        setVisible(true);
        try {
            // Заканчиваем работу через 10 сек
            Thread.currentThread();
            Thread.sleep(10000);
        } catch (Exception e) { }
            System.exit(0);
    }
    public static void main(String[] args) {
        new JWindowTest();
    }
}
```
В этом примере приложение наследуем от окна **_JWindow_**, чтобы удобнее вызывать методы этого класса и добавлять в окно компоненты. Объект Robot необходимо создавать в блоке try ... catch, т.к. его создание может быть запрещено менеджером безопасности, используемым виртуальной машиной Java. Впрочем, нам нарушение безопасности не грозит, потому что мы создаем отдельное приложение, а не апплет.

Вырезаем часть изображения "рабочего стола" методом createScreenCapture() в стороне он местоположения нашего окна. Затем в панель содержимого окна добавляется компонент ImageDraw, который и отображает вырезанное изображения рабочего стола. После вывода окна на экран программа засыпает на 10 секунд, а потом заканчивает свою работу.

Скриншот рабочего стола с интерфейсом окна **примера _JWindow_** представлен на следующем рисунке.
![[Ex3-JWindow.png]]
Прежде чем производить настройку окна, в примере JWindowTest вызывается конструктор базового класса ключевым словом super() без параметров. На самом деле окна без рамки **_JWindow_** обязательно требуют при создании указывать своего «родителя» — окно с рамкой [JFrame](JFrame), что не всегда может быть неудобно. Специально для таких случаев в класс **_JWindow_** был добавлен конструктор без параметров, который создает вспомогательное невидимое окно [JFrame](JFrame) и использует его как «родителя». После этого все окна без рамки, созданные таким образом, задействуют только это окно и экономят ресурсы.

Следует также отметить, что с помощью конструктора без параметров создается окно **_JWindow_**, неспособное получать фокус ввода. Чаще всего именно такое поведение необходимо (ведь панелям инструментов, всплывающим заставкам и меню фокус ввода не нужен). При необходимости получения фокуса ввода, используйте метод setFocusableWindowState(true).
