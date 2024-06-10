#Java #Swing #JColorChooser

## Класс JColorChooser

2024-06-10 15:54

**_JColorChooser_** обеспечивает панель элементов управления, предназначенную для того, чтобы пользователь мог манипулировать цветом и выбирать его. Этот класс обеспечивает_API трех уровней_:
1. Статический удобный метод, который показывает модное окно выбора цвета и возвращает цвет, выбранный пользователем.
2. Статический удобный метод для создания окна выбора цвета, в котором _слушатели действий_ могут быть включены для вызова, когда пользователь нажимает одну из кнопок диалога.
3. Возможность создания экземпляров панелей **_JColorChooser_** напрямую (в любом контейнере). Можно добавить слушивателей _изменения свойств_, чтобы определить, когда изменяется текущее свойство «цвет».

### Конструкторы класса

1. **JColorChooser():** Создана панель выбора цвета с начальным белым цветом.
2. **JColorChooser (Color initialColor):** Создает панель выбора цвета с таким исходным цветом.
3. **JColorChooser (ColorSelectionModel model):** Создает панель выбора цвета указанной моделью ColorSelectionModel.

### Часто используют методы

| Метод                                                                  | Описание                                                                                                          |
| ---------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| void setColor(Color color)                                             | Устанавливает текущий цвет средства выбора цвета на указанный цвет.                                               |
| void setColor(int c)                                                   | Устанавливает текущий цвет средства выбора цвета на указанный цвет.                                               |
| void setColor(int r, int g, int b)                                     | Устанавливает текущий цвет средства выбора цвета в указанный цвет RGB.                                            |
| static Color showDialog(Component cmp, String title, Color init_Color) | Показывает модальное диалоговое окно выбора цвета и блокируется до тех пор, пока диалоговое окно не будет скрыто. |
| void updateUI()                                                        | Уведомление от `UIManager` о том, что L & F изменился.                                                            |
| void setChooserPanels(AbstractColorChooserPanel[] panels)              | Определяет цветовые панели, используемые для выбора значения цвета.                                               |
| void addChooserPanel(AbstractColorChooserPanel panel)                  | Добавляет панель выбора цвета к панели выбора цвета.                                                              |
| void setUI(ColorChooserUI ui)                                          | Задает объект L & F, который отображает этот компонент.                                                           |
| void setSelectionModel(ColorSelectionModel newModel)                   | Устанавливает модель, содержащую выбранный цвет.                                                                  |
| void setPreviewPanel(JComponent preview)                               | Устанавливает текущую панель предварительного просмотра.                                                          |
#### Пример 1. Программа Java для реализации класса JColorChooser с использованием ChangeListener.

```java
// Java program to implement JColorChooser
// class using ChangeListener
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;
import javax.swing.event.*;
import javax.swing.colorchooser.*;

public class Main extends JPanel implements ChangeListener {
    protected JColorChooser Jcc;
    protected JLabel label;

    public Main() {
        super(new BorderLayout());

        // Set up the Label at the top of the window
        label = new JLabel("Example", JLabel.CENTER);

        // set the foreground color of the text
        label.setForeground(Color.green);

        // set background color of the field
        label.setBackground(Color.WHITE);
        label.setOpaque(true);

        // set font type and size of the text
        label.setFont(new Font("SansSerif", Font.BOLD, 30));

        // set size of the label
        label.setPreferredSize(new Dimension(100, 65));

        // create a Panel and set its layout
        JPanel bannerPanel = new JPanel(new BorderLayout());
        bannerPanel.add(label, BorderLayout.CENTER);
        bannerPanel.setBorder(BorderFactory.createTitledBorder("Label"));

        // Set up color chooser for setting text color
        Jcc = new JColorChooser(label.getForeground());
        Jcc.getSelectionModel().addChangeListener(this);
        Jcc.setBorder(BorderFactory.createTitledBorder("Choose Text Color"));

        add(bannerPanel, BorderLayout.CENTER);
        add(Jcc, BorderLayout.PAGE_END);
    }

    public void stateChanged(ChangeEvent e) {
        Color newColor = Jcc.getColor();
        label.setForeground(newColor);
    }

    // Create the GUI and show it.  For thread safety,
    // this method should be invoked from the
    // event-dispatching thread.
    private static void createAndShowGUI() {
        // Create and set up the window.
        JFrame frame = new JFrame("ColorChooserDemo");

        // set default close operation of the window.
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        // Create and set up the content pane.
        JComponent newContentPane = new Main();

        // content panes must be opaque
        newContentPane.setOpaque(true);

        // add content pane to the frame
        frame.setContentPane(newContentPane);

        // Display the window.
        frame.pack();
        frame.setVisible(true);
    }

    // Main Method
    public static void main(String[] args) {
        // Schedule a job for the event-dispatching thread:
        // creating and showing this application's GUI.
        javax.swing.SwingUtilities.invokeLater(new Runnable() {
            public void run() {
                createAndShowGUI();
            }
        });
    }
}
```
**Вывод:**
![[Ex1-JColorChooser.png]]

#### Пример 2. Программа Java для реализации класса JColorChooser с использованием ActionListener

```java
// Java program to implement JColorChooser
// class using ActionListener
import java.awt.event.*;
import java.awt.*;
import javax.swing.*;

public class Main extends JFrame implements ActionListener {
    // create a button
    JButton b = new JButton("color");
    Container c = getContentPane();

    // Constructor
    Main() {
        // set Layout
        c.setLayout(new FlowLayout());

        // add Listener
        b.addActionListener(this);
        // add button to the Container
        c.add(b);
    }

    public void actionPerformed(ActionEvent e) {
        Color initialcolor = Color.RED;
        // color chooser Dialog Box
        Color color = JColorChooser.showDialog(this,
                "Select a color", initialcolor);

        // set Background color of the Container
        c.setBackground(color);
    }

    // Main Method
    public static void main(String[] args) {
        Main ch = new Main();
        ch.setSize(400, 400);
        ch.setVisible(true);
        ch.setDefaultCloseOperation(EXIT_ON_CLOSE);
    }
}
```
**Вывод:
![[Ex2-JColorChooser.png]]**
