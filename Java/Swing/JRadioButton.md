#Java #Swing #JRadioButton

## Класс JRadioButton

2024-05-31 14:55

Переключатель **_JRadioButton_** унаследован от выключателя [JToggleButton](JToggleButton) и отличается от него только внешним видом. **_JRadioButton_** используют, как правило, при объединении нескольких переключателей в группу и реализации выбора «один из многих». По одиночке в интерфейсе их практически не используют; обычно эту роль исполняют флажки.

Мы добавляем переключатели в группу кнопок, чтобы мы могли выбирать только по одному переключателю одновременно. Мы используем класс ButtonGroup для создания группы кнопок и добавления переключателей в группу.

### Конструкторы JRadioButton

|                         Конструктор                         |                                                            Описание                                                             |
| :---------------------------------------------------------: | :-----------------------------------------------------------------------------------------------------------------------------: |
|                  **public JRadioButton()**                  |                                               Создает невыбранный переключатель.                                                |
|            **public JRadioButton(String text)**             |                                      Создает невыбранный переключатель с заданным текстом.                                      |
|       **public JRadioButton(String text, boolean b)**       |          Создает переключатель с заданным текстом, который выбирается или невыбираемый на основе логического значения.          |
| **public JRadioButton(String text, Icon image, boolean b)** | Создает переключатель с заданным текстом и значком, который выбирается или не выбирается в зависимости от логического значения. |

### Методы класса JRadioButton
  
| Методы                               | Описание                                                                  |
| :----------------------------------- | :------------------------------------------------------------------------ |
| **public void setName(String text)** | Задает имя для JRadioButton, это имя отображаться не будет.               |
| **public String getName()**          | Получает строковое сообщение JRadioButton, это имя отображаться не будет. |
| **public void setIcon(Icon _icon_)** | Устанавливает значок или изображение поверх JRadioButton.                 |
| **public Icon getIcon()**            | Возвращает значок или изображение JRadioButton.                           |

#### Пример 1. JRadioButton Без ActionListener

```java
// Java program to show JRadioButton Example.
// in java. Importing different Package.
import java.awt.*;
import javax.swing.*;
import java.awt.event.*;

class Demo extends JFrame {

    // Declaration of object of JRadioButton class.
    JRadioButton jRadioButton1;
    // Declaration of object of JRadioButton class.
    JRadioButton jRadioButton2;
    // Declaration of object of JButton class.
    JButton jButton;
    // Declaration of object of ButtonGroup class.
    ButtonGroup G1;
    // Declaration of object of  JLabel  class.
    JLabel L1;

    // Constructor of Demo class.
    public Demo() {
        this.setDefaultCloseOperation(EXIT_ON_CLOSE);
        // Setting layout as null of JFrame.
        this.setLayout(null);
        // Initialization of object of "JRadioButton" class.
        jRadioButton1 = new JRadioButton();
        // Initialization of object of "JRadioButton" class.
        jRadioButton2 = new JRadioButton();
        // Initialization of object of "JButton" class.
        jButton = new JButton("Click");
        // Initialization of object of "ButtonGroup" class.
        G1 = new ButtonGroup();
        // Initialization of object of " JLabel" class.
        L1 = new JLabel("Qualification");
        // setText(...) function is used to set text of radio button.
        // Setting text of "jRadioButton2".
        jRadioButton1.setText("Under-Graduate");
        // Setting text of "jRadioButton4".
        jRadioButton2.setText("Graduate");
        // Setting Bounds of "jRadioButton2".
        jRadioButton1.setBounds(120, 30, 120, 50);
        // Setting Bounds of "jRadioButton4".
        jRadioButton2.setBounds(250, 30, 80, 50);
        // Setting Bounds of "jButton".
        jButton.setBounds(125, 90, 80, 30);
        // Setting Bounds of JLabel "L2".
        L1.setBounds(20, 30, 150, 50);

        // "this" keyword in java refers to current object.
        // Adding "jRadioButton2" on JFrame.
        this.add(jRadioButton1);
        // Adding "jRadioButton4" on JFrame.
        this.add(jRadioButton2);
        // Adding "jButton" on JFrame.
        this.add(jButton);
        // Adding JLabel "L2" on JFrame.
        this.add(L1);

        // Adding "jRadioButton1" and "jRadioButton3" in a Button Group "G2".
        G1.add(jRadioButton1);
        G1.add(jRadioButton2);
    }
}

class RadioButton {
    // Driver code.
    public static void main(String args[])
    { // Creating object of demo class.
        Demo f = new Demo();

        // Setting Bounds of JFrame.
        f.setBounds(100, 100, 400, 200);
        // Setting Title of frame.
        f.setTitle("RadioButtons");
        // Setting Visible status of frame as true.
        f.setVisible(true);
    }
}
```
**Вывод:**
![[Ex1-JRadioButton.png]]

#### Пример 2. JRadioButton с ActionListener

```java
// Java program to show JRadioButton Example.
// in java. Importing different Package.
import java.awt.*;
import javax.swing.*;
import java.awt.event.*;

class Demo extends JFrame {
    // Declaration of object of JRadioButton class.
    JRadioButton jRadioButton1;
    // Declaration of object of JRadioButton class.
    JRadioButton jRadioButton2;
    // Declaration of object of JButton class.
    JButton jButton;
    // Declaration of object of ButtonGroup class.
    ButtonGroup G1;
    // Declaration of object of  JLabel  class.
    JLabel L1;
    // Constructor of Demo class.
    public Demo() {
        this.setDefaultCloseOperation(EXIT_ON_CLOSE);
        // Setting layout as null of JFrame.
        this.setLayout(null);
        // Initialization of object of "JRadioButton" class.
        jRadioButton1 = new JRadioButton();
        // Initialization of object of "JRadioButton" class.
        jRadioButton2 = new JRadioButton();
        // Initialization of object of "JButton" class.
        jButton = new JButton("Click");
        // Initialization of object of "ButtonGroup" class.
        G1 = new ButtonGroup();
        // Initialization of object of " JLabel" class.
        L1 = new JLabel("Qualification");

        // setText(...) function is used to set text of radio button.
        // Setting text of "jRadioButton2".
        jRadioButton1.setText("Under-Graduate");
        // Setting text of "jRadioButton4".
        jRadioButton2.setText("Graduate");
        // Setting Bounds of "jRadioButton2".
        jRadioButton1.setBounds(120, 30, 120, 50);
        // Setting Bounds of "jRadioButton4".
        jRadioButton2.setBounds(250, 30, 80, 50);
        // Setting Bounds of "jButton".
        jButton.setBounds(125, 90, 80, 30);
        // Setting Bounds of JLabel "L2".
        L1.setBounds(20, 30, 150, 50);

        // "this" keyword in java refers to current object.
        // Adding "jRadioButton2" on JFrame.
        this.add(jRadioButton1);
        // Adding "jRadioButton4" on JFrame.
        this.add(jRadioButton2);
        // Adding "jButton" on JFrame.
        this.add(jButton);
        // Adding JLabel "L2" on JFrame.
        this.add(L1);

        // Adding "jRadioButton1" and "jRadioButton3" in a Button Group "G2".
        G1.add(jRadioButton1);
        G1.add(jRadioButton2);

        // Adding Listener to JButton.
        jButton.addActionListener(new ActionListener() {
            // Anonymous class.
            public void actionPerformed(ActionEvent e) {
                // Override Method
                // Declaration of String class Objects.
                String qual = " ";

                // If condition to check if jRadioButton2 is selected.
                if (jRadioButton1.isSelected()) {
                    qual = "Under-Graduate";
                }
                else if (jRadioButton2.isSelected()) {
                    qual = "Graduate";
                }
                else {
                    qual = "NO Button selected";
                }
                // MessageDialog to show information selected radio buttons.
                JOptionPane.showMessageDialog(Demo.this, qual);
            }
        });
    }
}

class RadioButton {
    // Driver code.
    public static void main(String args[])
    { // Creating object of demo class.
        Demo f = new Demo();

        // Setting Bounds of JFrame.
        f.setBounds(100, 100, 400, 200);
        // Setting Title of frame.
        f.setTitle("RadioButtons");
        // Setting Visible status of frame as true.
        f.setVisible(true);
    }
}
```
**Вывод:**
![[Ex2-JRadioButton.png]]

#### Пример 3 Программа для создания простой группы переключателей и добавления к ним слушателя элементов

```java
// Java Program to create a simple group of radio buttons
// and add item listener to them
import java.awt.event.*;
import java.awt.*;
import javax.swing.*;
class solve extends JFrame implements ItemListener {
    // frame
    static JFrame f;
    // radiobuttons
    static JRadioButton b, b1;
    // create a label
    static JLabel l1;

    // main class
    public static void main(String[] args) {
        // create a new frame
        f = new JFrame("frame");
        f.setDefaultCloseOperation(EXIT_ON_CLOSE);
        // create a object
        solve s = new solve();
        // create a panel
        JPanel p = new JPanel();
        // create a new label
        JLabel l = new JLabel("which website do you like?");
        l1 = new JLabel("www.game.com selected");
        // create Radio buttons
        b = new JRadioButton("www.game.com");
        b1 = new JRadioButton("others");

        // create a button group
        ButtonGroup bg = new ButtonGroup();

        // add item listener
        b.addItemListener(s);
        b1.addItemListener(s);

        // add radio buttons to button group
        bg.add(b);
        bg.add(b1);

        b.setSelected(true);

        // add button and label to panel
        p.add(l);
        p.add(b);
        p.add(b1);
        p.add(l1);

        f.add(p);

        // set the size of frame
        f.setSize(400, 100);

        f.setVisible(true);
    }

    public void itemStateChanged(ItemEvent e) {
        if (e.getSource() == b) {
            if (e.getStateChange() == 1) {
                l1.setText("www.game.com selected");
            }
        }
        else {
            if (e.getStateChange() == 1) {
                l1.setText("others selected");
            }
        }
    }
}
```
**Вывод:**
![[Ex3-JRadioButton.png]]