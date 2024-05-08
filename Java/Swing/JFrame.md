#Java #Swing #JFrame

## Java JFrame

2024-05-08 10:34

Java **_JFramе_** является важным компонентом Java [Swing](Swing), который является частью Java SWT (Standard Widget Toolkit). **_JFrame_** в Java — это класс, который позволяет создавать и управлять окном верхнего уровня в Java-приложении. Он служит главным окном для Java-приложений с графическим интерфейсом и обеспечивает независимый от платформы способ создания графических пользовательских интерфейсов. В Java **_JFrame_** является частью пакета javax.swing.

### Конструктор Java JFrame

| Конструктор                                         | Описание                                                                                            |
| --------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| **JFrame()**                                        | Это конструктор по умолчанию для JFrame. Создается новый кадр без заголовка.                        |
| **JFrame (String title)**                           | Этот конструктор создает новый кадр с указанным заголовком.                                         |
| **JFrame (GraphicsConfiguration gc)**               | Этот конструктор создает JFrame, который использует указанную графическую конфигурацию.             |
| **JFrame (String title, GraphicsConfiguration gc)** | Этот конструктор создает JFrame с указанным заголовком и использует указанную конфигурацию графики. |
| **JFrame(Rectangle bounds)**                        | Этот конструктор создает JFrame с указанными границами.                                             |
| **JFrame (String title, Rectangle bounds)**         | Этот конструктор создает JFrame с указанным заголовком и границами.                                 |

### Методы Java JFrame

| Методы                                      | Описание                                                                                                                                                   |
| ------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **setTitle(String title)**                  | Устанавливает заголовок JFrame.                                                                                                                            |
| **setSize(int width, int height)**          | Устанавливает размер JFrame.                                                                                                                               |
| **setDefaultCloseOperation(int operation)** | Устанавливает операцию закрытия по умолчанию для JFrame. Общие параметры включают JFrame.EXIT_ON_CLOSE, JFrame.HIDE_ON_CLOSE и JFrame.DO_NOTHING_ON_CLOSE. |
| **setVisible(boolean b)**                   | Устанавливает видимость JFrame. Передайте true, чтобы сделать его видимым, и false, чтобы скрыть его.                                                      |
| **setLayout(LayoutManager manager)**        | Устанавливает менеджер макета для JFrame, который управляет расположением компонентов внутри фрейма.                                                       |
| **add(Component comp)**                     | Добавляет компонент Swing в JFrame.                                                                                                                        |
| **remove(Component comp)**                  | Удаляет компонент из JFrame.                                                                                                                               |
| **validate()**                              | Заставляет менеджер компоновки пересчитать компоновку компонентов внутри JFrame.                                                                           |
| **setResizable(boolean resizable)**         | Определяет, может ли пользователь изменять размер JFrame.                                                                                                  |
| **setIconImage(Image image)**               | Устанавливает значок (изображение) для окна JFrame.                                                                                                        |

### Родительские классы методов JFrame

Java JFrame является частью Java [Swing](Swing), и классы, от которых наследуются все методы, связанные с JFrame, упомянуты ниже:
1. java.awt.Frame
2. java.awt.Container
3. java.awt.Window
4. javax.swing.JFrame

### Некоторые поля для Java JFrame
 
| Поля                          | Описание                                                                                                                                                  |
| ----------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **EXIT_ON_CLOSE (int)**       | Поле, определяющее операцию по умолчанию, выполняемую, когда пользователь закрывает JFrame. Обычно он используется с методом setDefaultCloseOperation().  |
| **DISPOSE_ON_CLOSE (int)**    | Это константа, определяющая операцию, которую необходимо выполнить, когда пользователь закрывает JFrame. Она удаляет JFrame, но не выходит из приложения. |
| **HIDE_ON_CLOSE (int)**       | Указывает, что JFrame должен быть скрыт, но не удален, когда пользователь его закрывает.                                                                  |
| **DO_NOTHING_ON_CLOSE (int)** | Указывает, что не следует предпринимать никаких действий, когда пользователь закрывает JFrame.                                                            |

### Программы для реализации JFrame

#### 1. Java-программа для демонстрации простого JFrame.

Ниже приведена демонстрация простого JFrame:
```java
// Java Swing Program to demonstrate
// a simple JFrame
import javax.swing.JFrame;
import javax.swing.JLabel;
 
// Driver Class
public class MyJFrame {
    // main function
    public static void main(String[] args) {
        // Create a new JFrame
        JFrame frame = new JFrame("My First JFrame");
        // Create a label
        JLabel label = new JLabel("Geeks Premier League 2023");
        // Add the label to the frame
        frame.add(label);
        // Set frame properties
        frame.setSize(300, 200); // Set the size of the frame
        // Close operation
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        // Make the frame visible
        frame.setVisible(true);
    }
}
```
Вывод:
![[Ex1-JFrame.png]]

#### 2. Java-программа для добавления JMenuBar и JButton внутри JFrame.

Ниже приведена реализация добавления JMenuBar и JButton внутри примера JFrame:
```java
// Java Swing Program to Add 
// JMenuBar and JButton inside the JFrame 
import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
 
// Driver Class
public class JFrameExample {
      // Main function
    public static void main(String[] args) {
        // Create the main frame
        JFrame frame = new JFrame("JFrame Example");
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setSize(800, 600);
 
        // Create a menu bar
        JMenuBar menuBar = new JMenuBar();
        JMenu fileMenu = new JMenu("File");
        JMenuItem openItem = new JMenuItem("Open");
        JMenuItem exitItem = new JMenuItem("Exit");
        fileMenu.add(openItem);
        fileMenu.addSeparator();
        fileMenu.add(exitItem);
        menuBar.add(fileMenu);
 
        // Create a panel with a button
        JPanel panel = new JPanel();
        JButton button = new JButton("Click Me");
        panel.add(button);
 
        // Add action to the button
        button.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                JOptionPane.showMessageDialog(frame, "Button Clicked!");
            }
        });
 
        // Create another panel with text
        JPanel textPanel = new JPanel();
        JLabel label = new JLabel("Geeks Premier League 2023");
        textPanel.add(label);
 
        // Set layout for the main frame
        frame.setLayout(new BorderLayout());
        frame.setJMenuBar(menuBar);
        frame.add(panel, BorderLayout.CENTER);
        frame.add(textPanel, BorderLayout.SOUTH);
 
        frame.setVisible(true);
    }
}
```
Вывод:
![[Ex2-JFrame.png]]

