#Java #awt #KeyListener

## Java KeyListener в AWT

2024-05-27 12:46

Интерфейс **_KeyListener_** находится в пакете «java.awt.event». Порт **_KeyListener_** в Java [AWT](AWT) широко используется для прослушивания событий клавиатуры, таких как нажатие и отпускание клавиш. Это позволяет вашей программе реагировать на ввод пользователя с клавиатуры, что имеет решающее значение для создания интерактивных приложений.
```java
interface KeyListener {
    //клавиша нажата, но не отпущена
    public void keyPressed(KeyEvent event);
    //клавиша отпущена
    public void keyReleased(KeyEvent event);
    //клавиша нажата и отпущена
    public void keyTyped(KeyEvent event);
}
```
Каждый метод, реализованный интерфейсом KeyListener, вызывается определенным событием, вместе с которым передается экземпляр [KeyEvent](KeyEvent). [KeyEvent](KeyEvent) содержит в себе всю информацию о нажатой клавише и о модификаторах, таких как Alt, Ctrl, Shift:
```java
int keyCode = event.getKeyCode(); //цифровой код нажатой клавиши
boolean isAltDown = event.isAltDown();
boolean isControlDown = event.isControlDown();
boolean isShiftDown = event.isShiftDown();
```
У каждой клавиши есть свой цифровой код, например, код **пробела** 32, клавиша **вправо** имеет код 39. Всегда можно посмотреть эти коды, выполнив команду:
```java
System.out.println(event.getKeyCode());
```
Кроме того, класс [KeyEvent](KeyEvent) содержит коды всех клавиш в статических переменных, все они начинаются на VK_:
```java
KeyEvent.VK_SPACE;//32
KeyEvent.VK_RIGHT;//39
```
Можно и нужно использовать эти переменные для сравнения:
```java
If (event.getKeyCode()==KeyEvent.VK_SPACE) {
    System.out.println(Нажат пробел);
}
```

### Объявление KeyListener
```java
public interface KeyListener extends EventListener
```
 
### Методы Java KeyListener в [AWT](AWT)

Порт KeyListener определяет три метода, которые необходимо реализовать:

| Метод                   | Описание                                                                   |
| ----------------------- | -------------------------------------------------------------------------- |
| keyPressed(KeyEvent e)  | Вызывается при нажатии клавиши.                                            |
| keyReleased(KeyEvent e) | Вызывается при отпускании клавиши.                                         |
| keyTyped(KeyEvent e)    | Вызывается, когда нажатие/отпускание клавиши приводит к появлению символа. |

### Короткие нажатия

Когда дело касается только обработки нажатой клавиши, достаточно поместить необходимый код в метод keyTyped() интерфейса **_KeyListener_**.
```java
@Override
public void keyTyped(KeyEvent event) {
    //клавиша нажата и отпущена
}
```

### Длинные одновременные нажатия

Другое дело, когда нам необходимо обрабатывать не только нажатие, но еще и его длительность и скорее всего сразу у нескольких клавиш одновременно. В этом случае приходится вводить дополнительные переменные, на каждую отслеживаемую клавишу:
```java
private boolean isLeft = false;
private boolean isRight = false;
private boolean isUp = false;
private boolean isDown = false;
```
Такой подход позволяет реализовывать составные действия, например, длительное движение вправо-вверх одновременно. Необходимо правильно отлавливать события с клавиатуры. Когда зажата клавиша, мы получаем событие в метод **keyPressed** и записываем эту информацию в переменную. С этого момента мы считаем, что клавиша непрерывно нажата. Если клавиша будет отпущена, мы получим событие в метод **keyReleased** и обновим об этом информацию в переменной.
```java
@Override
public void keyPressed(KeyEvent event) {
    if (e.getKeyCode()==KeyEvent.VK_LEFT) isLeft = true;
    if (e.getKeyCode()==KeyEvent.VK_RIGHT) isRight = true;
    if (e.getKeyCode()==KeyEvent.VK_UP) isUp = true;
    if (e.getKeyCode()==KeyEvent.VK_DOWN) isDown = true;
}
 
@Override
public void keyReleased(KeyEvent event) {
    if (e.getKeyCode()==KeyEvent.VK_LEFT) isLeft = false;
    if (e.getKeyCode()==KeyEvent.VK_RIGHT) isRight = false;
    if (e.getKeyCode()==KeyEvent.VK_UP) isUp = false;
    if (e.getKeyCode()==KeyEvent.VK_DOWN) isDown = false;
}
```

Некий движок, управляющий нашей программой и живущий в отдельном потоке не слушает нажатия клавиш напрямую. Вместо этого, он работает с переменными, которые мы любезно для него подготовили.

### Подключаем слушатель

Остается только повесить наш класс слушателя нажатий на какой-нибудь компонент [Swing](Swing), например на **[JFrame](JFrame)**:
```java
frame.addKeyListener(keyListener);
```


### Пример Java KeyListener

#### Пример 1. Ниже приведена реализация Java KeyListener

```java
// Java program to demonstrate textfield and  
// display typed text using KeyListener 
import java.awt.*; 
import java.awt.event.*; 
  
public class KeyListenerExample extends Frame implements KeyListener { 
  
    private TextField textField; 
    private Label displayLabel; 
  
    // Constructor 
    public KeyListenerExample() { 
        // Set frame properties 
        setTitle("Typed Text Display"); 
        setSize(400, 200); 
        setLayout(new FlowLayout()); 
  
        // Create and add a TextField for text input 
        textField = new TextField(20); 
        textField.addKeyListener(this); 
        add(textField); 
  
        // Create and add a Label to display typed text 
        displayLabel = new Label("Typed Text: "); 
        add(displayLabel); 
  
		addWindowListener(new WindowAdapter() {  
	    @Override  
		    public void windowClosing(WindowEvent e) {  
		        System.exit(0);  
		    }  
		});
		        // Ensure the frame can receive key events 
        setFocusable(true); 
        setFocusTraversalKeysEnabled(false); 
          
        // Make the frame visible 
        setVisible(true); 
    } 
  
    // Implement the keyPressed method 
    @Override
    public void keyPressed(KeyEvent e) { 
        // You can add custom logic here if needed 
    } 
  
    // Implement the keyReleased method 
    @Override
    public void keyReleased(KeyEvent e) { 
        // You can add custom logic here if needed 
    } 
  
    // Implement the keyTyped method 
    @Override
    public void keyTyped(KeyEvent e) { 
        char keyChar = e.getKeyChar(); 
        displayLabel.setText("Typed Text: " + textField.getText() + keyChar); 
    } 
  
    public static void main(String[] args) { 
        new KeyListenerExample(); 
    } 
} 
```
**Вывод:**
![[Ex1-KeyListener.png]]

#### Пример 2.

```java
//Java program to demonstrate keyPressed,
// keyReleased and keyTyped method
import java.awt.*;
import java.awt.event.*;

public class Main extends Frame implements KeyListener {

    private TextField textField;
    private Label displayLabel;

    // Constructor
    public Main() {
        // Set frame properties
        setTitle("Typed Text Display");
        setSize(400, 200);
        setLayout(new FlowLayout());

        // Create and add a TextField for text input
        textField = new TextField(20);
        textField.addKeyListener(this);
        add(textField);

        // Create and add a Label to display typed text
        displayLabel = new Label("Typed Text: ");
        add(displayLabel);

        addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
                System.exit(0);
            }
        });

        // Ensure the frame can receive key events
        setFocusable(true);
        setFocusTraversalKeysEnabled(false);

        // Make the frame visible
        setVisible(true);
    }

    // Implement the keyPressed method
    @Override
    public void keyPressed(KeyEvent e) {
        int keyCode = e.getKeyCode();
        System.out.println("Key Pressed: " + KeyEvent.getKeyText(keyCode));
    }

    // Implement the keyReleased method
    @Override
    public void keyReleased(KeyEvent e) {
        int keyCode = e.getKeyCode();
        System.out.println("Key Released: " + KeyEvent.getKeyText(keyCode));
    }

    // Implement the keyTyped method
    @Override
    public void keyTyped(KeyEvent e) {
        char keyChar = e.getKeyChar();
        System.out.println("Key Typed: " + keyChar);
        displayLabel.setText("Typed Text: " + textField.getText() + keyChar);
    }

    public static void main(String[] args) {
        new Main();
    }
}
```
**Терминал, показывающий нажатие клавиш:**
![[Ex2-KeyListener.png]]

#### Пример 3. Код, реализующий отрисовку змейки. Голова управляется "стрелками".

```java
import java.awt.*;
import java.awt.event.*;
import java.util.Random;
import javax.swing.JFrame;

public class Main extends JFrame implements KeyListener{

    private Thread thread;
    private static Random random = new Random();
    private static final int DIR_STEP = 2;
    private boolean isLeft = false;
    private boolean isRight = false;
    private boolean isUp = false;
    private boolean isDown = false;
    private int x, y;

    public Main(int width, int height) {
        this.setSize(width, height);
        x = width/2;
        y = height/2;
        this.addKeyListener(this);
        thread = new MoveThread(this);
        thread.start();
    }

    //Start point
    public static void main(String... string) {
        JFrame frame = new Main(500,500);
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setVisible(true);
    }

    //Listener
    @Override
    public void keyPressed(KeyEvent e) {
        if (e.getKeyCode()==KeyEvent.VK_LEFT) isLeft = true;
        if (e.getKeyCode()==KeyEvent.VK_RIGHT) isRight = true;
        if (e.getKeyCode()==KeyEvent.VK_UP) isUp = true;
        if (e.getKeyCode()==KeyEvent.VK_DOWN) isDown = true;
    }

    @Override
    public void keyReleased(KeyEvent e) {
        if (e.getKeyCode()==KeyEvent.VK_LEFT) isLeft = false;
        if (e.getKeyCode()==KeyEvent.VK_RIGHT) isRight = false;
        if (e.getKeyCode()==KeyEvent.VK_UP) isUp = false;
        if (e.getKeyCode()==KeyEvent.VK_DOWN) isDown = false;
    }

    @Override
    public void keyTyped(KeyEvent arg0) {}

    //Graphics
    @Override
    public void paint(Graphics gr) {
        Graphics2D g2d = (Graphics2D)gr;
        int r = random.nextInt(256);
        int g = random.nextInt(256);
        int b = random.nextInt(256);
        g2d.setColor(new Color(r,g,b));
        g2d.setStroke(new BasicStroke(4f));
        g2d.drawOval(x-25, y-25, 50, 50);
    }

    public void animate() {
        if (isLeft) x-=DIR_STEP;
        if (isRight) x+=DIR_STEP;
        if (isUp) y-=DIR_STEP;
        if (isDown) y+=DIR_STEP;
        this.repaint();
    }

    //Engine thread
    private class MoveThread extends Thread{
        Main runKeyboard;

        public MoveThread(Main runKeyboard) {
            super("MoveThread");
            this.runKeyboard = runKeyboard;
        }

        public void run(){
            while(true) {
                runKeyboard.animate();
                try {
                    Thread.sleep(10);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
```
**Вывод:**
![[Ex3-KeyListener.png]]