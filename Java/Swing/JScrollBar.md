#Java #Swing #JScrollBar

## Класс JScrollBar

2024-06-05 14:44

Библиотека [Swing](Swing) Java предоставляет различные компоненты графического пользовательского интерфейса для создания графических интерфейсов. Среди этих компонентов есть класс **_JScrollBar_**, который позволяет пользователям прокручивать такой важный компонент, как **_JScrollPane_**. **_JScrollBar_** является частью пакета javax.swing.

### Конструкторы JScrollBar

| Конструктор                                                          | Описание                                                                                                              |
| -------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| JScrollBar()                                                         | Создает вертикальную полосу прокрутки со следующими начальными значениями: JScrollBar.HORIZONTAL, JScrollBar.VERTICAL |
| JScrollBar(int orientation)                                          | Создает полосу прокрутки с указанной ориентацией                                                                      |
| JScrollBar(int orientation, int value, int extent, int min, int max) | Создает полосу прокрутки с указанной ориентацией, значением, экстентом, минимумом и максимумом.<br>                   |

### Некоторые методы работы с JScrollBar


1. **setValue(значение int):** Устанавливает текущее значение полосы прокрутки в указанное значение.
2. **GetValue():** извлекает текущее значение полосы прокрутки, которое указывает текущее положение большого пальца.
3. **setMinimum(int minimum):** устанавливает минимальное значение полосы прокрутки, определяя нижнюю границу диапазона.
4. **getMinimum():** возвращает минимальное значение, позволяющее получить нижнюю границу диапазона.
5. **setMaximum(int maximum):** устанавливает максимальное значение полосы прокрутки, определяя верхнюю границу диапазона.
6. **getMaximum():** извлекает максимальное значение, указывающее верхнюю границу диапазона.

#### Пример 1. Программа реализации полос прокрутки

```java
import java.awt.*;  
import java.awt.event.*;  
import javax.swing.*;  
  
public class Main {  
    private JFrame mainFrame;  
    private JLabel headerLabel;  
    private JLabel statusLabel;  
    private JPanel controlPanel;  
  
    public Main(){  
        prepareGUI();  
    }  
    public static void main(String[] args){  
        Main  swingControlDemo = new Main();  
        swingControlDemo.showScrollbarDemo();  
    }  
    private void prepareGUI(){  
        mainFrame = new JFrame("Java Swing Examples");  
        mainFrame.setSize(300,300);  
        mainFrame.setLayout(new GridLayout(3, 1));  
  
        mainFrame.addWindowListener(new WindowAdapter() {  
            public void windowClosing(WindowEvent windowEvent){  
                System.exit(0);  
            }  
        });  
        headerLabel = new JLabel("", JLabel.CENTER);  
        statusLabel = new JLabel("",JLabel.CENTER);  
        statusLabel.setSize(350,100);  
  
        controlPanel = new JPanel();  
        controlPanel.setLayout(new FlowLayout());  
  
        mainFrame.add(headerLabel);  
        mainFrame.add(controlPanel);  
        mainFrame.add(statusLabel);  
        mainFrame.setVisible(true);  
    }  
    private void showScrollbarDemo() {  
        headerLabel.setText("Control in action: JScrollbar");  
  
        final JScrollBar horizontalScroller = new JScrollBar(JScrollBar.HORIZONTAL);  
        final JScrollBar verticalScroller = new JScrollBar();  
        verticalScroller.setOrientation(JScrollBar.VERTICAL);  
        horizontalScroller.setMaximum (100);  
        horizontalScroller.setMinimum (1);  
        verticalScroller.setMaximum (100);  
        verticalScroller.setMinimum (1);  
  
        horizontalScroller.addAdjustmentListener(new AdjustmentListener() {  
            @Override  
            public void adjustmentValueChanged(AdjustmentEvent e) {  
                statusLabel.setText("Horozontal: " + horizontalScroller.getValue()  
                        +" ,Vertical: " + verticalScroller.getValue());  
            }  
        });  
        verticalScroller.addAdjustmentListener(new AdjustmentListener() {  
            @Override  
            public void adjustmentValueChanged(AdjustmentEvent e) {  
                statusLabel.setText("Horozontal: " + horizontalScroller.getValue()  
                        +" ,Vertical: "+ verticalScroller.getValue());  
            }  
        });  
        controlPanel.add(horizontalScroller);  
        controlPanel.add(verticalScroller);  
  
        mainFrame.setVisible(true);  
    }  
}
```
**Вывод:**
![[Ex1-JScrollBar.png]]