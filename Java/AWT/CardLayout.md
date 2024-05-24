#Java #awt 

## Класс [AWT](AWT) CardLayout

2024-05-24 14:17

Класс **_CardLayout_** упорядочивает каждый компонент в контейнере в виде карточки. Одновременно видна только одна карточка, а контейнер действует как стопка карточек.

### Объявление класса

Ниже приводится объявление для класса **java.awt.CardLayout**:
```java
public class CardLayout extends Object implements LayoutManager2, Serializable
```

### Конструкторы

| S.N. | Конструктор и описание                                                                                                    |
| ---- | ------------------------------------------------------------------------------------------------------------------------- |
| 1    | **CardLayout()**<br>Создает новый макет карты с пробелами нулевого размера.                                               |
| 2    | **CardLayout(int hgap, int vgap)**<br>Создает новый макет карты с заданными горизонтальными и вертикальными промежутками. |

### Методы класса

| S.N. | Метод и описание                                                                                                                                                                                              |
| ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1    | **void addLayoutComponent(Component comp, Object constraints)**<br>Добавляет указанный компонент во внутреннюю таблицу имен этого макета карты.                                                               |
| 2    | **void addLayoutComponent(String name, Component comp)**<br>Если менеджер компоновки использует строку для каждого компонента, добавляет компонент comp в макет, связывая его со строкой, указанной по имени. |
| 3    | **void first(Container parent)**<br>Переходит к первой карте контейнера.                                                                                                                                      |
| 4    | **int getHgap()**<br>Определяет горизонтальный зазор между компонентами.                                                                                                                                      |
| 5    | **float getLayoutAlignmentX(Container parent)**<br>Возвращает выравнивание по оси x.                                                                                                                          |
| 6    | **float getLayoutAlignmentY(Container parent)**<br>Возвращает выравнивание по оси y.                                                                                                                          |
| 7    | **int getVgap()**<br>Определяет вертикальный зазор между компонентами.                                                                                                                                        |
| 8    | **void invalidateLayout(Container target)**<br>Делает макет недействительным, указывая, что если диспетчер макетов имеет кэшированную информацию, ее следует удалить.                                         |
| 9    | **void last(Container parent)**<br>Переходит к последней карте контейнера.                                                                                                                                    |
| 10   | **void layoutContainer(Container parent)**<br>Размещает указанный контейнер, используя этот макет карты.                                                                                                      |
| 11   | **Dimension maximumLayoutSize(Container target)**<br>Возвращает максимальные размеры для данного макета с учетом компонентов в указанном целевом контейнере.                                                  |
| 12   | **Dimension minimumLayoutSize(Container parent)**<br>Вычисляет минимальный размер для указанной панели.                                                                                                       |
| 13   | **void next(Container parent)**<br>Переходит к следующей карте указанного контейнера.                                                                                                                         |
| 14   | **Dimension preferredLayoutSize(Container parent)**<br>Определяет предпочтительный размер аргумента контейнера, используя этот макет карты.                                                                   |
| 15   | **void previous(Container parent)**<br>Переходит к предыдущей карте указанного контейнера.                                                                                                                    |
| 16   | **void removeLayoutComponent(Component comp)**<br>Удаляет указанный компонент из макета.                                                                                                                      |
| 17   | **void setHgap(int hgap)**<br>Устанавливает горизонтальный зазор между компонентами.                                                                                                                          |
| 18   | **void setVgap(int vgap)**<br>Устанавливает вертикальный зазор между компонентами.                                                                                                                            |
| 19   | **void show(Container parent, String name)**<br>Переходит к компоненту, который был добавлен в этот макет с указанным именем, используя addLayoutComponent.                                                   |
| 20   | **String toString()**<br>Возвращает строковое представление состояния этого макета карты.                                                                                                                     |

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
        awtLayoutDemo.showCardLayoutDemo();
    }

    private void prepareGUI(){
        mainFrame = new Frame("Java AWT Examples");
        mainFrame.setSize(400,200);
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

    private void showCardLayoutDemo(){
        headerLabel.setText("Layout in action: CardLayout");

        final Panel panel = new Panel();
        panel.setBackground(Color.CYAN);
        panel.setSize(300,300);

        CardLayout layout = new CardLayout();
        layout.setHgap(10);
        layout.setVgap(10);
        panel.setLayout(layout);

        Panel buttonPanel = new Panel(new FlowLayout());

        buttonPanel.add(new Button("OK"));
        buttonPanel.add(new Button("Cancel"));

        Panel textBoxPanel = new Panel(new FlowLayout());

        textBoxPanel.add(new Label("Name:"));
        textBoxPanel.add(new TextField(20));

        panel.add("Button", buttonPanel);
        panel.add("Text", textBoxPanel);

        Choice choice = new Choice();
        choice.add("Button");
        choice.add("Text");

        choice.addItemListener(new ItemListener() {
            public void itemStateChanged(ItemEvent e) {
                CardLayout cardLayout = (CardLayout)(panel.getLayout());
                cardLayout.show(panel, (String)e.getItem());
            }
        });
        controlPanel.add(choice);
        controlPanel.add(panel);

        mainFrame.setVisible(true);
    }
}
```
**Вывод:**
![[Ex1-CardLayout.png]]

#### Пример 3. С использованием [Swing](Swing)

Менеджер **CardLayout** можно использовать для создания так называемых вкладок (tabs), выбирая которые будут избранно открываться разные панели, занимающие одно и то же место в интерфейсе окна. В библиотеке Swing данную задачу можно решить с использованием класса JTabbedPane, организовывающего управление панелями с вкладками.
```java
// Пример использования менеджера расположения CardLayoutTest

import java.awt.*;
import java.awt.event.*;
import javax.swing.*;

public class Main implements ItemListener
{
    private static JPanel cards;

    final   static String BUTTONPANEL = "Панель с кнопками"       ;
    final   static String TEXTPANEL   = "Панель с текстовым полем";

    /**
     * Метод определения интерфейса панели
     * @param container - панель содержимого
     */
    public void createPanelUI(Container container)
    {
        // Создание компонента с выпадающим списком 
        JComboBox<String> combobox = new JComboBox<String>(
                new String[] {BUTTONPANEL, TEXTPANEL});
        combobox.setEditable    (false);
        combobox.addItemListener(this );

        // Помещаем JComboBox в JPanel для наглядности.
        JPanel cbPanel = new JPanel();
        cbPanel.add(combobox);

        // Создание "cards". 
        JPanel card1 = new JPanel();
        card1.add(new JButton("Продукты"));
        card1.add(new JButton("Одежда"  ));
        card1.add(new JButton("Обувь"   ));

        JPanel card2 = new JPanel();
        card2.add(new JTextField("TextField", 15));

        // Создаем панель с менеджером расположения CardLayout
        cards = new JPanel(new CardLayout());
        // Добавляем вкладки
        cards.add(card1, BUTTONPANEL);
        cards.add(card2, TEXTPANEL);

        container.add(cbPanel, BorderLayout.PAGE_START);
        container.add(cards  , BorderLayout.CENTER    );
    }
    // Обработчик события
    public void itemStateChanged(ItemEvent event)
    {
        CardLayout layout = (CardLayout)(cards.getLayout());
        layout.show(cards, (String)event.getItem());
    }

    public static void main(String[] args)
            throws ClassNotFoundException, InstantiationException,
            IllegalAccessException, UnsupportedLookAndFeelException
    {
        // Создание и настройка окна 
        final JFrame frame = new JFrame("CardLayoutTest");
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        javax.swing.SwingUtilities.invokeLater(new Runnable() {
            public void run() {
                (new Main()).createPanelUI(frame.getContentPane());

                // Открытие окна 
                frame.pack();
                frame.setVisible(true);
            }
        });
    }
}
```
**Вывод:**
![[Ex2-CardLayout.png]]
![[Ex2_1-CardLayout.png]]