#Java #awt #FlowLayout

## Класс [AWT](AWT) FlowLayout

Класс **FlowLayout** состоит из компонентов в потоке слева направо.
### Объявление класса

Ниже приводится объявление для класса **java.awt.FlowLayout**:
```java
public class FlowLayout extends Object implements LayoutManager, Serializable
```

Поля для класса **java.awt.BorderLayout**:
- **static int CENTER** - Это значение указывает, что каждая строка компонентов должна быть центрирована.
- **static int LEADING** - Это значение указывает, что каждая строка компонентов должна быть выровнена по переднему краю ориентации контейнера, например, слева при ориентации слева направо.
- **static int LEFT** - Это значение указывает, что каждая строка компонентов должна быть выровнена по левому краю.
- **static int RIGHT** - это значение указывает, что каждая строка компонентов должна быть выровнена по правому краю.
- **static int TRAILING** - Это значение указывает, что каждая строка компонентов должна быть выровнена по заднему краю ориентации контейнера, например, справа при ориентации слева направо.

### Конструкторы

| N   | Конструктор и описание                                                                                                                                                         |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1   | **FlowLayout()**<br>Создает новую FlowLayout с выравниванием по центру и зазором по умолчанию в 5 единиц по горизонтали и вертикали.                                           |
| 2   | **FlowLayout(int align)**<br>Создает новую FlowLayout с указанным выравниванием и зазором по умолчанию в 5 единиц по горизонтали и вертикали.                                  |
| 3   | **FlowLayout(int align, int hgap, int vgap)**<br>Создает новый диспетчер компоновки потока с указанным выравниванием и указанными горизонтальными и вертикальными промежутками |

### Методы класса

| N   | Метод и описание                                                                                                                                                                  |
| --- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | **void addLayoutComponent(String name, Component comp)**<br>Добавляет указанный компонент в макет.                                                                                |
| 2   | **int getAlignment()**<br>Получает выравнивание для этого макета.                                                                                                                 |
| 3   | **int getHgap()**<br>Определяет горизонтальный зазор между компонентами.                                                                                                          |
| 4   | **int getVgap()**<br>Определяет вертикальный зазор между компонентами.                                                                                                            |
| 5   | **void layoutContainer(Container target)**<br>Устанавливает контейнер.                                                                                                            |
| 6   | **Dimension minimumLayoutSize(Container target)**<br>Возвращает минимальные размеры, необходимые для компоновки видимых компонентов, содержащихся в указанном целевом контейнере. |
| 7   | **Dimension preferredLayoutSize(Container target)**<br>Возвращает предпочтительные размеры для этого макета с учетом видимых компонентов в указанном целевом контейнере.          |
| 8   | **void removeLayoutComponent(Component comp)**<br>Удаляет указанный компонент из макета.                                                                                          |
| 9   | **void setAlignment(int align)**<br>Задает выравнивание для этого макета.                                                                                                         |
| 10  | **void setHgap(int hgap)**<br>Задает горизонтальный зазор между компонентами.                                                                                                     |
| 11  | **void setVgap(int vgap)**<br>Задает вертикальный зазор между компонентами.                                                                                                       |
| 12  | **String toString()**<br>Возвращает строковое представление этого объекта FlowLayout и его значений.                                                                              |

#### Пример 1.

```java
import java.awt.*;
import java.awt.event.*;

public class Main {
    private Frame mainFrame;
    private Label headerLabel;
    private Label statusLabel;
    private Panel controlPanel;
    private Label msglabel;

    public Main(){
        prepareGUI();
    }

    public static void main(String[] args){
        Main  awtLayoutDemo = new Main();
        awtLayoutDemo.showFlowLayoutDemo();
    }

    private void prepareGUI(){
        mainFrame = new Frame("Java AWT Examples");
        mainFrame.setSize(300,200);
        mainFrame.setLayout(new GridLayout(3, 1));
        mainFrame.addWindowListener(new WindowAdapter() {
            public void windowClosing(WindowEvent windowEvent){
                System.exit(0);
            }
        });
        headerLabel = new Label();
        headerLabel.setAlignment(Label.CENTER);
        statusLabel = new Label();
        statusLabel.setAlignment(Label.CENTER);
        statusLabel.setSize(350,100);

        msglabel = new Label();
        msglabel.setAlignment(Label.CENTER);
        msglabel.setText("Welcome to TutorialsPoint AWT Tutorial.");

        controlPanel = new Panel();
        controlPanel.setLayout(new FlowLayout());

        mainFrame.add(headerLabel);
        mainFrame.add(controlPanel);
        mainFrame.add(statusLabel);
        mainFrame.setVisible(true);
    }

    private void showFlowLayoutDemo(){
        headerLabel.setText("Layout in action: FlowLayout");

        Panel panel = new Panel();
        panel.setBackground(Color.darkGray);
        panel.setSize(200,200);
        FlowLayout layout = new FlowLayout();
        layout.setHgap(10);
        layout.setVgap(10);
        panel.setLayout(layout);
        panel.add(new Button("OK"));
        panel.add(new Button("Cancel"));

        controlPanel.add(panel);

        mainFrame.setVisible(true);
    }
}
```
**Вывод:**
![[Ex1-FlowLayout.png]]
