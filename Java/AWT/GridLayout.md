#Java #awt #GridLayout

## Класс [AWT](AWT) GridLayout

2024-05-24 11:53

Класс **GridLayout** упорядочивает компоненты в виде прямоугольной сетки.
### Объявление класса

Ниже приводится объявление для класса **java.awt.GridLayout**:
```java
public class GridLayout extends Object implements LayoutManager, Serializable
```

### Конструкторы класса

| N   | Конструктор и описание                                                                                                  |
| --- | ----------------------------------------------------------------------------------------------------------------------- |
| 1   | **GridLayout()**<br>Создает макет сетки с по умолчанию одним столбцом для каждого компонента в одной строке.            |
| 2   | **GridLayout(int rows, int cols)**<br>Создает макет сетки с заданным количеством строк и столбцов.                      |
| 3   | **GridLayout (int rows, int cols, int hgap, int vgap)**<br>Создает макет сетки с заданным количеством строк и столбцов. |

### Методы класса

| S.N. | Метод и описание                                                                                                                            |
| ---- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| 1    | **void addLayoutComponent(String name, Component comp)**<br>Добавляет указанный компонент с указанным именем в макет.                       |
| 2    | **int getColumns()**<br>Получает количество столбцов в этом макете.                                                                         |
| 3    | **int getHgap()**<br>Определяет горизонтальный зазор между компонентами.                                                                    |
| 4    | **int GetRows()**<br>Получает количество строк в этом макете.                                                                               |
| 5    | **int getVgap()**<br>Определяет вертикальный зазор между компонентами.                                                                      |
| 6    | **void layoutContainer(Container parent)**<br>Размещает указанный контейнер с использованием этого макета.                                  |
| 7    | **Dimension minimumLayoutSize(Container parent)**<br>Определяет минимальный размер аргумента контейнера, используя этот макет сетки.        |
| 8    | **Dimension preferredLayoutSize(Container parent)**<br>Определяет предпочтительный размер аргумента контейнера, используя этот макет сетки. |
| 9    | **void removeLayoutComponent(Component comp)**<br>Удаляет указанный компонент из макета.                                                    |
| 10   | **void setColumns(int cols)**<br>Устанавливает количество столбцов в этом макете равным указанному значению.                                |
| 11   | **void setHgap(int hgap)**<br>Устанавливает горизонтальный зазор между компонентами на указанное значение.                                  |
| 12   | **void setRows(int rows)**<br>Устанавливает количество строк в этом макете равным указанному значению.                                      |
| 13   | **void setVgap(int vgap)**<br>Устанавливает вертикальный зазор между компонентами на указанное значение.                                    |
| 14   | **String toString()**<br>Возвращает строковое представление значений этого макета сетки.                                                    |
#### Пример 1

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
        awtLayoutDemo.showGridLayoutDemo();
    }

    private void prepareGUI(){
        mainFrame = new Frame("Java AWT Examples");
        mainFrame.setSize(300,300);
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

    private void showGridLayoutDemo(){
        headerLabel.setText("Layout in action: GridLayout");

        Panel panel = new Panel();
        panel.setBackground(Color.darkGray);
        panel.setSize(250,250);
        GridLayout layout = new GridLayout(0,3);
        layout.setHgap(10);
        layout.setVgap(10);

        panel.setLayout(layout);
        panel.add(new Button("Button 1"));
        panel.add(new Button("Button 2"));
        panel.add(new Button("Button 3"));
        panel.add(new Button("Button 4"));
        panel.add(new Button("Button 5"));
        controlPanel.add(panel);
        mainFrame.setVisible(true);
    }
}
```
**Вывод:**
![[Ex1-GridLayout.png]]

#### Пример 2. С использованием [Swing](Swing)

```java
import java.awt.GridLayout;
import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JPanel;

public class Main{
    public static void main(String[] args) {
        JFrame jf = new JFrame();
        jf.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        jf.setSize(300, 200);
        jf.setVisible(true);
        // создаем  панель.
        JPanel  p = new JPanel();
        jf.add(p);
        // к панели добавляем менеджер GridLayout и устанавливаем размеры таблицы 3*3.
        p.setLayout(new GridLayout(3,3));
        // к панели добавляем кнопку и устанавливаем для нее менеджер в верхнее расположение.
        p.add(new JButton("start 1"));
        p.add(new JButton("start 2"));
        p.add(new JButton("start 3"));
        p.add(new JButton("start 4"));
        p.add(new JButton("start 6"));
        p.add(new JButton("Okay"));
        // Открываем окно
        jf.setVisible(true);
    }
}
```
**Вывод:**
![[Ex2-GridLayout.png]]