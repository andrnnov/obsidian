#Java #Swing #JComponents #JLabel

## JLabel Java Swing

2024-05-13 16:00

**_JLabel_** — это класс Java [Swing](Swing). **_JLabel_** используется для отображения короткой строки или значка изображения. **_JLabel_** может отображать текст, изображение или и то, и другое. JLabel — это всего лишь отображение текста или изображения, и он не может получить фокус. **_JLabel_** неактивен для ввода событий, таких как фокус мыши или фокус клавиатуры. По умолчанию метки центрируются по вертикали, но пользователь может изменить выравнивание метки.  

### Конструктор класса
 
1. **JLabel():** создает пустую метку без текста или изображения.
2. **JLabel(String s) :** создает новую метку с указанной строкой.
3. **JLabel (Icon i):** создает новую метку с изображением на ней.
4. **JLabel(String s, Icon i, int align):** создает новую метку со строкой, изображением и заданным горизонтальным выравниванием.

### Обычно используемые методы класса
 
1. **getIcon():** возвращает изображение, отображаемое меткой.
2. **setIcon(Icon i):** устанавливает значок, который будет отображаться на метке, для изображения i.
3. **getText():** возвращает текст, который будет отображаться на метке.
4. **setText(String s):** устанавливает текст, который будет отображаться на метке, в строку s.

#### Пример 1. Программа для создания пустой этикетки и добавления к ней текста

```java
// Java Program to create a 
// blank label and add text to it.
import java.awt.event.*;
import java.awt.*;
import javax.swing.*;

class text extends JFrame {
    // frame
    static JFrame f;
    // label to display text
    static JLabel l;
    // default constructor
    text() {
    }
 
    // main class
    public static void main(String[] args) {
        // create a new frame to store text field and button
        f = new JFrame("label");
        // create a label to display text
        l = new JLabel();
        // add text to label
        l.setText("label text");
        // create a panel
        JPanel p = new JPanel();
        // add label to panel
        p.add(l);
        // add panel to frame
        f.add(p);
        // set the size of frame
        f.setSize(300, 300);
        f.setVisible(true);
    }
}
```
**Вывод:**
![[Ex1-JLabel.png]]

#### Пример 2. Программа для создания новой метки с помощью конструктора – JLabel(String s)

```java
// Java Program to create a new label
// using constructor - JLabel(String s)
import java.awt.event.*;
import java.awt.*;
import javax.swing.*;
class text extends JFrame {
     // frame
    static JFrame f;
     // label to display text
    static JLabel l;
     // default constructor
    text() {
    }
 
    // main class
    public static void main(String[] args) {
        // create a new frame to store text field and button
        f = new JFrame("label");
         // create a label to display text
        l = new JLabel("new text ");
         // create a panel
        JPanel p = new JPanel();
         // add label to panel
        p.add(l);
         // add panel to frame
        f.add(p);
         // set the size of frame
        f.setSize(300, 300);
		f.setVisible(true);
    }
}
```
**Вывод:**
![[Ex2-JLabel.png]]

#### Пример 3. Программа для создания этикетки и добавления к ней изображения

```java
// Java Program to create  a label 
// and add image to it .
import java.awt.event.*;
import java.awt.*;
import javax.swing.*;
class text extends JFrame {
    // frame
    static JFrame f;
    // label to display text
    static JLabel l;
    // default constructor
    text() {
    }
 
    // main class
    public static void main(String[] args) {
        // create a new frame to store text field and button
        f = new JFrame("label");
        // create a new image icon
        ImageIcon i = new ImageIcon("C:\\Users\\minipc\\OneDrive\\Документы\\Obsidian Vault\\Java\\Swing\\files\\Icon.jpg");
        // create a label to display image
        l = new JLabel(i);
        // create a panel
        JPanel p = new JPanel();
        // add label to panel
        p.add(l);
        // add panel to frame
        f.add(p);
        // set the size of frame
        f.setSize(500, 500);
        f.setVisible();
    }
}
```
**Вывод:**
![[Ex3-JLabel.png]]

#### Пример 4. Программа для добавления изображений и строк к ярлыку

```java
// Java Program to add a image and string  
// to a label with horizontal alignment  
import java.awt.event.*;  
import java.awt.*;  
import javax.swing.*;  
class text extends JFrame {  
    // frame  
    static JFrame f;  
    // label to display text  
    static JLabel l;  
    // default constructor  
    text() {  
    }  
  
    // main class  
    public static void main(String[] args) {  
        // create a new frame to store text field and button  
        f = new JFrame("label");  
        // create a new image icon  
	    ImageIcon i = new ImageIcon("C:\\Users\\minipc\\OneDrive\\Документы\\Obsidian Vault\\Java\\Swing\\files\\Icon.jpg");  
        // create a label to display text and image  
        l = new JLabel("new image text ", i, SwingConstants.HORIZONTAL);  
        // create a panel  
        JPanel p = new JPanel();  
        // add label to panel  
        p.add(l);  
        // add panel to frame  
        f.add(p);  
        // set the size of frame  
        f.setSize(400, 300);  
        f.setVisible(true);  
    }  
}
```
**Вывод:**
![[Ex4-JLabel.png]]

