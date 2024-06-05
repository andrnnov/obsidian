#Java #Swing #JScrollPane

### Класс JScrollPane

2024-06-05 15:29

Java **_JScrollPane_** - это компонент библиотеки Java [Swing](Swing), который предоставляет прокручиваемый вид другого компонента, обычно это [JPanel](JPanel) или [JTextArea](JTextArea). Он предоставляет функциональность прокрутки дисплея, размер которой изменяется динамически. Полезно отображать содержимое, которое превышает видимую область окна.

### Конструкторы JScrollPane

| Конструкторы                              | Описания                                                                                                           |
| ----------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| JScrollPane()                             | Это конструктор по умолчанию, который создает пустую JScrollPane.                                                  |
| JScrollPane(Component comp)               | Этот конструктор создает JScrollPane с указанным компонентом представления в качестве прокручиваемого содержимого. |
| JScrollPane(int vertical, int horizontal) | Этот конструктор создает пустую JScrollPane с указанной вертикальной и горизонтальной полосой прокрутки.           |
| JScrollPane(LayoutManager layout)         | Этот конструктор создает JScrollPane с указанным менеджером компоновки.                                            |

### Методы JScrollPane

| Методы                                            | Описание                                                                                                                                   |
| ------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| void setVerticalScrollBarPolicy(int vertical)     | Устанавливает политику вертикальной полосы прокрутки                                                                                       |
| void setHorizontalScrollBarPolicy(int horizontal) | Устанавливает политику горизонтальной полосы прокрутки                                                                                     |
| void setColumnHeaderView(Component comp)          | задает заголовок столбца для JScrollPane                                                                                                   |
| void setRowHeaderView(Component comp)             | устанавливает rowheader для JScrollPane                                                                                                    |
| setCorner(String key, Component corner)           | Используется для настройки компонента, который будет отображаться в одном из углов области прокрутки                                       |
| Component getCorner(String key)                   | Используется для извлечения компонента, который был ранее установлен в одном из углов области прокрутки, с использованием метода setCorner |
| void setViewportView(Component comp)              | Используется для настройки компонента, который будет отображаться в окне просмотра области прокрутки                                       |

#### Пример 1. Программа на Java для демонстрации простой JScrollPane

```java
// Java Program to demonstrate  
// Simple JscrollPane 
import javax.swing.*; 
import java.awt.*; 
  
// Driver Class 
public class SimpleJScrollPaneExample { 
      // main function 
    public static void main(String[] args) { 
        
        JFrame frame = new JFrame("Simple JScrollPane Example"); 
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE); 
        frame.setSize(300, 200); 
        
        // Create a JPanel to hold a list of labels. 
        JPanel panel = new JPanel(); 
        panel.setLayout(new BoxLayout(panel, BoxLayout.Y_AXIS)); 
        
        // Add a large number of labels to the panel. 
        for (int i = 1; i <= 50; i++) { 
            JLabel label = new JLabel("Label " + i); 
            panel.add(label); 
        } 
        
        // Create a JScrollPane and set the panel as its viewport. 
        JScrollPane scrollPane = new JScrollPane(panel); 
        
        // Add the JScrollPane to the frame. 
        frame.add(scrollPane); 
        frame.setVisible(true); 
    } 
} 
```
**Вывод:**
![[Ex1-JScrollPane.png]]

#### Пример 2. Программа Java для реализации JTextArea в JScrollPane

```java
// Java Program to Implementing
// JTextArea to JScrollPane
import javax.swing.*;

// Driver Class
public class Main {
    // main function
    public static void main(String[] args)
    {
        JFrame frame = new JFrame("Java JTextArea in JScrollPane");
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setSize(300, 200);

        // Creating an JTextArea with 10 rows, 30 columns
        JTextArea textArea = new JTextArea(5, 10);

        // Creating an JScrollPane
        JScrollPane scrollPane = new JScrollPane(textArea);

        frame.add(scrollPane);
        frame.setVisible(true);
    }
}
```
**Вывод:**
![[Ex2-JScrollPane.png]]