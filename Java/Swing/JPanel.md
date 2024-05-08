#Java #Swing #JPanel

## Java Swing – JPanel с примерами

2024-05-08 12:01

**_JPanel_** - часть пакета Java [Swing](Swing), представляет собой контейнер, в котором может храниться группа компонентов. Основная задача **_JPanel_** - организовать компоненты, в **_JPanel_** можно установить различные макеты, которые обеспечивают лучшую организацию компонентов, однако у него нет строки заголовка.

### **Конструкторы JPanel** 

1. **JPanel()**: создает новую панель с потоковым макетом
2. **JPanel(LayoutManager l)**: создает новую JPanel с указанным LayoutManager
3. **JPanel(boolean isDoubleBuffered)**: создает новую JPanel с указанной стратегией буферизации
4. **JPanel(LayoutManager l, boolean isDoubleBuffered)**: создает новую JPanel с указанным LayoutManager и указанной стратегией буферизации

### **Часто используемые функции JPanel** 

1. **add(Component c)**: добавляет компонент в указанный контейнер
2. **setLayout(LayoutManager l)**: устанавливает макет контейнера в соответствии с указанным менеджером макетов
3. **updateUI()**: возвращает свойству пользовательского интерфейса значение, соответствующее текущему внешнему виду.
4. **setUI(PanelUI ui)**: задает внешний вид объекта, который отображает этот компонент.
5. **getUI()**: возвращает объект внешнего вида, который отображает этот компонент.
6. **paramString()**: возвращает строковое представление этой **_JPanel_**.
7. **getUIClassID()**: возвращает имя класса внешнего вида, который отображает этот компонент.
8. **getAccessibleContext()**: возвращает AccessibleContext, связанный с этой **_JPanel_**.

#### Пример 1. Программа создает простую JPanel и добавляет в нее компоненты.

```java
// Java Program to Create a Simple JPanel 
// and Adding Components to it 
  
// Importing required classes 
import java.awt.*; 
import java.awt.event.*; 
import javax.swing.*; 
  
// Class 1 
// Helper class extending JFrame class 
class solution extends JFrame { 
    // JFrame 
    static JFrame f; 
    // JButton 
    static JButton b, b1, b2; 
    // Label to display text 
    static JLabel l; 
  
    // Main class 
    public static void main(String[] args) { 
        // Creating a new frame to store text field and 
        // button 
        f = new JFrame("panel"); 
        // Creating a label to display text 
        l = new JLabel("panel label"); 
        // Creating a new buttons 
        b = new JButton("button1"); 
        b1 = new JButton("button2"); 
        b2 = new JButton("button3"); 
        // Creating a panel to add buttons 
        JPanel p = new JPanel(); 
  
        // Adding buttons and textfield to panel 
        // using add() method 
        p.add(b); 
        p.add(b1); 
        p.add(b2); 
        p.add(l); 
  
        // setbackground of panel 
        p.setBackground(Color.red); 
        // Adding panel to frame 
        f.add(p); 
        // Setting the size of frame 
        f.setSize(300, 300); 
        f.show(); 
    } 
}
```
Вывод:
![[Ex1-JPanel.png]]

#### Пример 2

```java
// Java Program to Create a JPanel with a Border Layout 
// and Adding Components to It 
  
// Importing required classes 
import java.awt.*; 
import java.awt.event.*; 
import javax.swing.*; 
  
// Main class 
// Extending JFrame class 
class solution extends JFrame { 
    // JFrame 
    static JFrame f; 
    // JButton 
    static JButton b, b1, b2, b3; 
    // Label to display text 
    static JLabel l; 
  
    // Main driver method 
    public static void main(String[] args) { 
        // Creating a new frame to store text field and 
        // button 
        f = new JFrame("panel"); 
        // Creating a label to display text 
        l = new JLabel("panel label"); 
        // Creating a new buttons 
        b = new JButton("button1"); 
        b1 = new JButton("button2"); 
        b2 = new JButton("button3"); 
        b3 = new JButton("button4"); 
        // Creating a panel to add buttons 
        // and a specific layout 
        JPanel p = new JPanel(new BorderLayout()); 
  
        // Adding buttons and textfield to panel 
        // using add() method 
        p.add(b, BorderLayout.NORTH); 
        p.add(b1, BorderLayout.SOUTH); 
        p.add(b2, BorderLayout.EAST); 
        p.add(b3, BorderLayout.WEST); 
        p.add(l, BorderLayout.CENTER); 
  
        // setbackground of panel 
        p.setBackground(Color.red); 
        // Adding panel to frame 
        f.add(p); 
        // Setting the size of frame 
        f.setSize(300, 300); 
        f.show(); 
    } 
}
```
Вывод:
![[Ex2-JPanel.png]]

#### Пример 3.

```java
// Java Program to Create a JPanel with a Box layout 
// and Adding components to it 
  
// Importing required classes 
import java.awt.*; 
import java.awt.event.*; 
import javax.swing.*; 
  
// Main class 
// Extending JFrame class 
class solution extends JFrame { 
    // JFrame 
    static JFrame f; 
    // JButton 
    static JButton b, b1, b2, b3; 
    // Label to display text 
    static JLabel l; 
  
    // Main drive method 
    public static void main(String[] args) { 
        // Creating a new frame to store text field and 
        // button 
        f = new JFrame("panel"); 
        // Creating a label to display text 
        l = new JLabel("panel label"); 
        // Creating a new buttons 
        b = new JButton("button1"); 
        b1 = new JButton("button2"); 
        b2 = new JButton("button3"); 
        b3 = new JButton("button4"); 
        // Creating a panel to add buttons and 
        // textfield and a layout 
        JPanel p = new JPanel(); 
  
        // Setting box layout 
        p.setLayout(new BoxLayout(p, BoxLayout.Y_AXIS)); 
  
        // Adding buttons and textfield to panel 
        p.add(b); 
        p.add(b1); 
        p.add(b2); 
        p.add(b3); 
        p.add(l); 
  
        // Setting background of panel 
        p.setBackground(Color.red); 
        // Adding panel to frame 
        f.add(p); 
        // Setting the size of frame 
        f.setSize(300, 300); 
        f.show(); 
    } 
}
```
Вывод:
![[Pasted image 20240508123839.png]]


