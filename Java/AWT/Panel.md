#Java #awt #Panel

## Java AWT Panel

2024-05-23 09:53

В наборе инструментов абстрактного окна Java ([AWT](AWT)) класс **_Panel_** является фундаментальным компонентом для создания графических пользовательских интерфейсов. Он предлагает простой способ организации и группировки различных элементов графического интерфейса.
```java
public class Panel extends Container implements Accessible
```

### Конструкторы

| Конструктор                  | Описание                                                |
| ---------------------------- | ------------------------------------------------------- |
| Panel()                      | Создает новую панель с менеджером макетов по умолчанию. |
| Panel (LayoutManager layout) | Создает новую панель с указанным менеджером макетов.    |

### Методы

| Метод                                | Описание                                           |
| ------------------------------------ | -------------------------------------------------- |
| void add(Component comp)             | Добавляет указанный компонент на эту панель.       |
| Component getComponent(int n)        | Возвращает компонент по указанному индексу.        |
| void remove(Component comp)          | Удаляет указанный компонент с этой панели.         |
| void removeAll()                     | Удаляет все компоненты с этой панели.              |
| void setLayout(LayoutManager layout) | Устанавливает менеджер компоновки для этой панели. |

#### Пример 1. Пример AWT Panel

В этом примере мы создаем две панели (Panel1 и Panel2) и добавляем кнопки на Panel1. Метод setLayout используется для указания менеджера макета для Panel1, и мы устанавливаем разные цвета фона для панелей. Класс Frame используется для создания главного окна графического интерфейса.
```java
// Java Program to implement  
// AWT Panel 
import java.awt.*;
import java.awt.event.*;

// Driver Class 
public class Main {
    // main function
    public static void main(String[] args) {

        Frame frame = new Frame("Java AWT Panel Example");
        Panel panel1 = new Panel();
        Panel panel2 = new Panel();

        // Set the layout manager for panel1 
        panel1.setLayout(new FlowLayout());

        // Add components to panel1 
        Button button1 = new Button("Button 1");
        Button button2 = new Button("Button 2");

        panel1.add(button1);
        panel1.add(button2);

        // Set background colors for panels 
        panel1.setBackground(Color.CYAN);
        panel2.setBackground(Color.MAGENTA);

        // Add panels to the frame 
        frame.add(panel1);
        frame.add(panel2);

        frame.setSize(300, 100);
        frame.setLayout(new FlowLayout());
        frame.setVisible(true);

        frame.addWindowListener(new WindowAdapter() {
            public void windowClosing(WindowEvent we) {
                System.exit(0);
            }
        });
    }
} 
```
**Вывод:**
![[Ex1-Panel.png]]
