#Java #awt #Lebal

## Метка Java AWT

2024-05-23 11:06

**_Label_** в Java [AWT](AWT) — это компонент для размещения текста в контейнере. Текст, отображаемый в контейнере **_Label_** Java [AWT](AWT), не может быть отредактирован непосредственно пользователем. **_Label_** Java [AWT](AWT) также называется **пассивным компонентом управлением**, поскольку при доступе к ней не создается никаких событий.

Синтаксис:
```java
public class Label extends Component implements Accessible
```

### Конструкторы

1. **_Label()_**: создает пустую метку.
2. **_Label(String str):_** создает метку с именем str.
3. **_Label(String str, int x):_** создает метку с указанной строкой и x заданным горизонтальным выравниванием.

### Методы класса Label Java AWT

Существует несколько предопределенных методов, связанных с Label Java AWT

| N   | Метод                                    | Описание                                                                                                      |
| --- | ---------------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| 1.  | void setText(String text)                | Устанавливает текст метки.                                                                                    |
| 2.  | String getText()                         | Получает текст метки.                                                                                         |
| 3.  | void setAlignment(int alignment)         | Задает выравнивание текста в метке.  <br>Возможные значения: `Label.LEFT`, `Label.RIGHT`, `Label.CENTER`.<br> |
| 4.  | int getAlignment()                       | GetПолучает выравнивание текста в метке.                                                                      |
| 5.  | void addNotify()                         | Creates the peer for the label.                                                                               |
| 6.  | AccessibleContext getAccessibleContext() | Gets the AccessibleContext associated with the label.                                                         |
| 7.  | void addNotify()                         | Creates the peer (native window) for the label.                                                               |
### Примеры Label Java AWT

#### Пример 1

```java

// Java AWT Program to
// demonstrate Use of Label
// Hello World Program in AWT
import java.awt.*;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;
 
// Driver Class
class Main {
    // Main Function
    public static void main(String[] args) {
        // Declaring Frame
        Frame frame = new Frame("Basic");
        // All the components will be
        // inserted in this frame
        // Declaring Label
        Label label = new Label("Hello World!");
        // Adding Label into Frame
        frame.add(label);
        // Setting Frame Size
        frame.setSize(200, 200);
        // Setting Visibility of Frame
        frame.setVisible(true);
 
        // Using WindowListener for closing the window
        frame.addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
                System.exit(0);
            }
        });
    }
}
```
**Вывод:**
![[Ex1-Label.png]]

#### Пример 2. Печать текста, выровненного по центру

```java

// Java AWT Program to
// demonstrate Use of
// setAlignment
import java.awt.*;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;
 
// Driver Class
class Main {
    // Main Function
    public static void main(String[] args) {
        // Declaring Frame
        Frame frame = new Frame("Basic");
        // All the components will be
        // inserted in this frame
        // Declaring Label
        Label label = new Label("Change is Here");
        // Setting the Aligment to CENTER
        label.setAlignment(Label.CENTER);
        // Adding Label into Frame
        frame.add(label);
        // Setting Frame Size
        frame.setSize(200, 200);
        // Setting Visibility of Frame
        frame.setVisible(true);
 
        // Using WindowListener for closing the window
        frame.addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
                System.exit(0);
            }
        });
    }
}
```
**Вывод:**
![[Ex2-Label.png]]

#### Пример 3

В этом примере мы создаем объекты классов **_Label_** и Button, которые добавляются во фрейм. Используя метод actionPerformed(), над кнопкой генерируется событие. Когда мы нажмем кнопку, мы получим результат, если число нечетное или четное.
```java
// Java AWT Label Program to Check
// if a number is Odd or event
// Using ActionListener
import java.awt.*;
import java.awt.event.*;

// Driver Class
public class Main
        extends Frame implements ActionListener {
    // Frame Label and Button Initialised
    private Frame frame;
    private Label label;
    private Button button;
    public int count = 0;

    // Constructor
    public Main() {
        // Memory Allocated to frame
        frame = new Frame("Example 3 of AWT Label");

        // Memory Allocated to label
        label = new Label("Check if a Number is Even or Odd");

        // Memory Allocated to button
        button = new Button("Calculate");

        // Register ActionListener
        button.addActionListener(this);

        // Add components to the frame
        frame.add(label, BorderLayout.CENTER);
        frame.add(button, BorderLayout.SOUTH);

        // Dimensions of Frame
        frame.setSize(300, 300);
        frame.setVisible(true);

        // Using WindowListener for closing the window
        frame.addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
                System.exit(0);
            }
        });
    }

    // Action Listener checks when
    // Button is Pressed
    @Override public void actionPerformed(ActionEvent e) {
        if (e.getSource() == button) {
            String str;
            if (count % 2 == 0)
                str = count + " is even";
            else
                str = count + " is odd";

            label.setText(str);
            count++;
        }
    }

    // main function
    public static void main(String[] args) {
        Main example = new Main();
    }
}
```
**Вывод:**
	![[Ex3_1-Label.png]]  ![[Ex3_2-Label.png]]
