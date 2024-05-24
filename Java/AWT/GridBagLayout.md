#Java #awt #GridBagLayout

## Класс AWT GridBagLayout

2024-05-24 15:18

Менеджер расположения **GridBagLayout** подобно табличному ([GridLayout](GridLayout)) менеджеру устанавливает компоненты в таблицу. Но он дает возможность определять для компонентов разную ширину и высоту колонок и строк таблицы. Фактически GridBagLayout позволяет получить абсолютно любое расположение компонентов.

### Объявление класса

Ниже приводится объявление для класса **java.awt.GridBagLayout**:
```java
public class GridBagLayout extends Object implements LayoutManager2, Serializable
```

**Ниже приведены поля для java.awt.BorderLayout класс:**
- **double[] columnWeights** - это поле содержит переопределения весов столбцов.
- **int[] ColumnWidths** - в этом поле содержатся переопределения минимальной ширины столбца.
- **protected Hashtable comptable** - эта хэш-таблица поддерживает связь между компонентом и его ограничениями gridbag.
- **protected GridBagConstraints defaultConstraints** - это поле содержит экземпляр ограничений gridbag, содержащий значения по умолчанию, поэтому, если у компонента нет связанных с ним ограничений gridbag, компоненту будет назначена копия defaultConstraints.
- **protected java.awt.GridBagLayoutInfo layoutInfo** - в этом поле содержится информация о макете для gridbag.
- **protected static int MAXGRIDSIZE** - максимальное количество позиций сетки (как по горизонтали, так и по вертикали), которые могут быть размещены с помощью макета сетки.
- **protected static int MINSIZE** - наименьшая сетка, которая может быть нанесена с помощью макета пакета grid.
- **protected static int PREFERREDSIZE** - предпочтительный размер сетки, который может быть задан макетом пакета сетки.
- **int[] rowHeights** - в этом поле содержатся переопределения минимальной высоты строки.
- **double[] rowWeights** - в этом поле содержатся переопределения весов строк.

### Конструктор

| S.N. | Конструктор и описание                                            |
| ---- | ----------------------------------------------------------------- |
| 1    | **GridBagLayout()**<br>Создает менеджер компоновки GridBagLayout. |

### Методы класса

| N   | Методы и описание                                                                                                                                                                                                                                |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1   | **void addLayoutComponent(Component comp, Object constraints)**<br>Добавляет указанный компонент в макет, используя указанный объект constraints.                                                                                                |
| 2   | **void addLayoutComponent(String name, Component comp)**<br>Добавляет указанный компонент с указанным именем в макет.                                                                                                                            |
| 3   | **protected void adjustForGravity(GridBagConstraints constraints, Rectangle r)**<br>Настраивает поля x, y, width и height на правильные значения в зависимости от геометрии ограничения                                                          |
| 4   | **protected void AdjustForGravity(GridBagConstraints constraints, Rectangle r)**<br><p style="color: red">Этот метод устарел и предоставляется только для обратной совместимости; новый код должен вызывать adjustForGravity вместо этого.</p>   |
| 5   | **protected void arrangeGrid(Container parent)**<br>Создает таблицу.                                                                                                                                                                             |
| 6   | **protected void ArrangeGrid(Container parent)**<br><p style="color: red">Этот метод устарел и предоставляется только для обратной совместимости; вместо этого новый код должен вызывать arrangeGrid.</p>                                        |
| 7   | **GridBagConstraints getConstraints(Component comp)**<br>Получает ограничения для указанного компонента.                                                                                                                                         |
| 8   | **float getLayoutAlignmentX(Container parent)**<br>Возвращает выравнивание по оси x.                                                                                                                                                             |
| 9   | **float getLayoutAlignmentY(Container parent)**<br>Возвращает выравнивание по оси y.                                                                                                                                                             |
| 10  | **`int[][] getLayoutDimensions()`**<br>Определяет ширину столбцов и высоту строк для таблицы макета.                                                                                                                                             |
| 11  | **protected java.awt.GridBagLayoutInfo getLayoutInfo(Container parent, int sizeflag)**<br>Заполняет экземпляр GridBagLayoutInfo для текущего набора управляемых дочерних элементов.                                                              |
| 12  | **protected java.awt.GridBagLayoutInfo GetLayoutInfo(Container parent, int sizeflag)**<br><p style="color: red">Этот метод устарел и предоставляется только для обратной совместимости; вместо этого новый код должен вызывать getLayoutInfo</p> |
| 13  | **Point getLayoutOrigin()**<br>Определяет начало координат области макета в графическом координатном пространстве целевого контейнера.                                                                                                           |
| 14  | **`double[][] getLayoutWeights()`**<br>Определяет веса столбцов и строк таблицы макета.                                                                                                                                                          |
| 15  | **protected Dimension getMinSize(Container parent, java.awt.GridBagLayoutInfo info)**<br>Определяет минимальный размер шаблона на основе информации из getLayoutInfo().                                                                          |
| 16  | **protected Dimension GetMinSize(Container parent, java.awt.GridBagLayoutInfo info)**<br><p style="color: red">Этот метод устарел и предоставляется только для обратной совместимости; вместо этого новый код должен вызывать getMinSize .</p>   |
| 17  | **void invalidateLayout(Container target)**<br>Делает макет недействительным, указывая, что если диспетчер компоновки имеет кэшированную информацию, ее следует удалить.                                                                         |
| 18  | **void layoutContainer(Container parent)**<br>Размещает указанный контейнер, используя этот макет сетки.                                                                                                                                         |
| 19  | **Point location(int x, int y)**<br>Определяет, какая ячейка в сетке макета содержит точку, указанную с помощью (x, y).                                                                                                                          |
| 20  | **protected GridBagConstraints lookupConstraints(Component comp)**<br>Извлекает ограничения для указанного компонента.                                                                                                                           |
| 21  | **Dimension maximumLayoutSize(Container target)**<br>Возвращает максимальные размеры для этого макета с учетом компонентов в указанном целевом контейнере.                                                                                       |
| 22  | **Dimension minimumLayoutSize(Container parent)**<br><br>Определяет минимальный размер родительского контейнера, используя этот GridBagLayout.                                                                                                   |
| 23  | **Dimension preferredLayoutSize(Container parent)**<br>Определяет предпочтительный размер родительского контейнера, используя этот GridBagLayout.                                                                                                |
| 24  | **void removeLayoutComponent(Component comp)**<br>Удаляет указанный компонент из этого макета.                                                                                                                                                   |
| 25  | **void setConstraints(Component comp, GridBagConstraints constraints)**<br>Устанавливает ограничения для указанного компонента в этом макете.                                                                                                    |
| 26  | **String toString()**<br>Возвращает строковое представление значений этого GridBagLayout.                                                                                                                                                        |

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
        awtLayoutDemo.showGridBagLayoutDemo();
    }

    private void prepareGUI(){
        mainFrame = new Frame("Java AWT Examples");
        mainFrame.setSize(250,250);
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

    private void showGridBagLayoutDemo(){
        headerLabel.setText("Layout in action: GridBagLayout");

        Panel panel = new Panel();
        panel.setBackground(Color.darkGray);
        panel.setSize(300,300);
        GridBagLayout layout = new GridBagLayout();

        panel.setLayout(layout);
        GridBagConstraints gbc = new GridBagConstraints();

        gbc.fill = GridBagConstraints.HORIZONTAL;
        gbc.gridx = 0;
        gbc.gridy = 0;
        panel.add(new Button("Button 1"),gbc);

        gbc.gridx = 1;
        gbc.gridy = 0;
        panel.add(new Button("Button 2"),gbc);

        gbc.fill = GridBagConstraints.HORIZONTAL;
        gbc.ipady = 20;
        gbc.gridx = 0;
        gbc.gridy = 1;
        panel.add(new Button("Button 3"),gbc);

        gbc.gridx = 1;
        gbc.gridy = 1;
        panel.add(new Button("Button 4"),gbc);

        gbc.gridx = 0;
        gbc.gridy = 2;
        gbc.fill = GridBagConstraints.HORIZONTAL;
        gbc.gridwidth = 2;
        panel.add(new Button("Button 5"),gbc);

        controlPanel.add(panel);

        mainFrame.setVisible(true);
    }
}
```
**Вывод:**
![[Ex1-GridBagLayout.png]]

#### Пример 2. С использованием [Swing](Swing)

```java
// Пример использования менеджера расположения GridBagLayoutTest
import java.awt.*;
import javax.swing.JButton;
import javax.swing.JFrame;

public class Main
{
    /**
     * Метод определения интерфейса панели
     * @param container
     */
    public static void createPanelUI(Container container)
    {
        JButton button;

        container.setComponentOrientation(ComponentOrientation.LEFT_TO_RIGHT);

        container.setLayout(new GridBagLayout());
        GridBagConstraints constraints = new GridBagConstraints();

        // По умолчанию натуральная высота, максимальная ширина
        constraints.fill = GridBagConstraints.HORIZONTAL;
        constraints.weightx = 0.5;
        constraints.gridy   = 0  ;  // нулевая ячейка таблицы по вертикали

        button = new JButton("Школа");

        constraints.gridx = 0;      // нулевая ячейка таблицы по горизонтали
        container.add(button, constraints);

        button = new JButton("Институт");
        constraints.gridx = 1;      // первая ячейка таблицы по горизонтали
        container.add(button, constraints);

        button = new JButton("Академия");
        constraints.gridx = 2;      // вторая ячейка таблицы по горизонтали
        container.add(button, constraints);

        button = new JButton("Высокая кнопка размером в 2 ячейки");
        constraints.ipady     = 45;   // кнопка высокая
        constraints.weightx   = 0.0;
        constraints.gridwidth = 2;    // размер кнопки в две ячейки
        constraints.gridx     = 0;    // нулевая ячейка по горизонтали
        constraints.gridy     = 1;    // первая ячейка по вертикали
        container.add(button, constraints);

        button = new JButton("Семья");
        constraints.ipady     = 0;    // установить первоначальный размер кнопки
        constraints.weighty   = 1.0;  // установить отступ
        // установить кнопку в конец окна
        constraints.anchor    = GridBagConstraints.PAGE_END;
        constraints.insets    = new Insets(5, 0, 0, 0);  // граница ячейки по Y
        constraints.gridwidth = 2;    // размер кнопки в 2 ячейки
        constraints.gridx     = 1;    // первая ячейка таблицы по горизонтали
        constraints.gridy     = 2;    // вторая ячейка по вертикали
        container.add(button, constraints);
    }

    public static void main(String[] args)
    {
        // Создание окна
        JFrame frame = new JFrame("GridBagLayoutTest");
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        // Определить панель содержания
        createPanelUI(frame.getContentPane());

        // Показать окно
        frame.pack();
        frame.setVisible(true);
    }
}
```
**Вывод:**
![[Ex2-GridBagLayout.png]]