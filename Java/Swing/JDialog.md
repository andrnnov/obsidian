#Java #Swing #JDialog

## Диалоговое окно JDialog

2024-05-29 15:23

Диалоговые окна чаще всего используются в приложениях для получения дополнительной информации с целью установки параметров приложения, вывода важной вспомогательной/отладочной информации. Диалоговые окна, как правило, создаются модальными (modal), блокирующими доступ к остальным окнам приложения, пока пользователь не закончит работу с модальным диалоговым окном. Модальные диалоговые окна располагаются поверх основного окна приложения. Внешний вид диалоговых окон мало отличается от окон с рамкой [JFrame](JFrame), но обычно у них меньше элементов управления окна (чаще всего, имеется только кнопка закрытия окна) и отсутствует системное меню.

В [Swing](Swing) диалоговые окна реализуются классом **JDialog**, унаследованном от базового класса окон [JWindow](JWindow) и позволяющим создавать как обычные, так и модальные диалоговые окна. JDialog поддерживает, как и [JFrame](JFrame) закрытие окна, а в остальном сходен с другими окнами [Swing](Swing).

При создании диалоговых окон [Swing](Swing) необходимо указать «родительское окно», которым может быть окно с рамкой [JFrame](JFrame) или другое диалоговое окно **JDialog**. Имеется также конструктор, не требующий «родительского» окна, но использующий вспомогательное прозрачное окно.

#### Пример 1. JDialog пример создания диалоговых окон

```java
/**
 * Тестовый класс создания диалоговых окон
 */
import javax.swing.*;
import java.awt.event.*;

public class JDialogTest extends JFrame {
    private static final long serialVersionUID = 1L;
    public JDialogTest() {
        super("DialogWindows");
        // Выход из программы при закрытии
        setDefaultCloseOperation(EXIT_ON_CLOSE);
        // Кнопки для создания диалоговых окон
        JButton button1 = new JButton("Немодальное окно");
        button1.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                JDialog dialog = createDialog("Немодальное", false);
                dialog.setVisible(true);
            }
        });
        JButton button2 = new JButton("Модальное окно");
        button2.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                JDialog dialog = createDialog("Модальное", true);
                dialog.setVisible(true);
            }
        });
        // Создание панели содержимого с размещением кнопок
        JPanel contents = new JPanel();
        contents.add(button1);
        contents.add(button2);
        setContentPane(contents);
        // Определение размера и открытие окна
        setSize(350, 100);
        setVisible(true);
    }
    /** Функция создания диалогового окна.
     * @param title - заголовок окна
     * @param modal - флаг модальности
     */
    private JDialog createDialog(String title, boolean modal) {
        JDialog dialog = new JDialog(this, title, modal);
        dialog.setDefaultCloseOperation(DISPOSE_ON_CLOSE);
        dialog.setSize(180, 90);
        return dialog;
    }

    public static void main(String[] args) {
        new JDialogTest();
    }
}
```
В примере создаем окно с рамкой [JFrame](JFrame), в панели содержимого которого размещается две кнопки [JButton](JButton). По нажатию на кнопки создаются диалоговые окна в отдельном методе createDialog(). Диалоговое окно с заданным заголовком **JDialog** может быть модальным и немодальным. Программа позволяет создать несколько немодальных окон одновременно, но только одно модальное. Немодальные окна не блокируют работу с основным окном приложения. При закрытии диалогового окна используется константа DISPOSE_ON_CLOSE, удаляющую окно после закрытия.
**Вывод:**
![[Ex1-JDialog.png]]

### Конструкторы класса
 
1. **JDialog()**: создает пустой диалог без заголовка или указанного владельца.
2. **JDialog(Frame o)**: создает пустой диалог с указанным фреймом в качестве его владельца.
3. **JDialog(Frame o, String s)**: создает пустой диалог с указанным фреймом в качестве его владельца и указанным заголовком.
4. **JDialog(Window o)**: создает пустой диалог с указанным окном в качестве его владельца.
5. **JDialog(Window o, String t)**: создает пустой диалог с указанным окном в качестве владельца и указанным заголовком.
6. **JDialog(Dialog o)** : создает пустой диалог с указанным диалогом в качестве его владельца.
7. **JDialog(Dialog o, String s)** : создает пустой диалог с указанным диалогом в качестве его владельца и указанным заголовком.

### Методы

1. **setLayout(LayoutManager m)**: устанавливает макет диалогового окна в соответствии с заданным менеджером макетов
2. **setJMenuBar(JMenuBar m)**: устанавливает в строке меню диалогового окна значение указанной строки
3. **add(Component c)**: добавляет компонент в диалоговое окно
4. **isVisible(boolean b)**: задает видимость диалогового окна, если значение логического значения равно true, то visible, иначе invisible
5. **update(Graphics g)**: вызывает функцию paint(g)
6. **remove(Component c)**: удаляет компонент c
7. **getGraphics()**: возвращает графический контекст компонента.
8. **getLayeredPane()**: возвращает многоуровневую панель для диалогового окна
9. **setContentPane(Container c)**: задает область содержимого для диалогового окна
10. **setLayeredPane(JLayeredPane l)**: задает многоуровневую панель для диалогового окна
11. **setRootPane(JRootPane r)**: задает корневую панель для диалогового окна
12. **getJMenuBar()**: возвращает строку меню компонента
13. **setTransferHandler(TransferHandler n)**: устанавливает свойство TransferHandler, которое является механизмом для поддержки передачи данных в этот компонент.
14. **setRootPaneCheckingEnabled(boolean enabled)**: задает, будут ли вызовы add и setLayout перенаправляться в ContentPane.
15. **setRootPane(JRootPane root)**: устанавливает свойство RootPane диалогового окна.
16. **setGlassPane(Component glass)**: устанавливает свойство GlassPane диалогового окна.
17. **repaint(long time, int x, int y, int width, int height)**: перерисовывает указанный прямоугольник этого компонента в течение миллисекунд.
18. **remove(Component c)**: удаляет указанный компонент из диалогового окна.
19. **isRootPaneCheckingEnabled()**: возвращает, перенаправлены ли вызовы add и setLayout в ContentPane или нет .
20. **getTransferHandler()**: возвращает свойство TransferHandler.
21. **getRootPane()**: возвращает объект RootPane для этого диалогового окна.
22. **getGlassPane()**: возвращает объект GlassPane для этого диалогового окна.
23. **createRootPane()**: вызывается методами конструктора для создания корневой области по умолчанию.
24. **addImpl(Component co, Object c, int i)**: добавляет указанный дочерний компонент в диалоговое окно.

#### Пример 2. Программа для создания простого JDialog

```java
// java Program to create a simple JDialog
import java.awt.event.*;
import java.awt.*;
import javax.swing.*;
class solve extends JFrame implements ActionListener {
    // frame
    static JFrame f;
    // main class
    public static void main(String[] args) {
        // create a new frame
        f = new JFrame("frame");
        f.setDefaultCloseOperation(EXIT_ON_CLOSE);
        // create a object
        solve s = new solve();
        // create a panel
        JPanel p = new JPanel();
        JButton b = new JButton("click");
        // add actionlistener to button
        b.addActionListener(s);
        // add button to panel
        p.add(b);
        f.add(p);
        // set the size of frame
        f.setSize(400, 400);
        f.setVisible(true);
    }
    public void actionPerformed(ActionEvent e)     {
        String s = e.getActionCommand();
        if (s.equals("click")) {
            // create a dialog Box
            JDialog d = new JDialog(f, "dialog Box");
            // create a label
            JLabel l = new JLabel("this is a dialog box");
            d.add(l);
            // setsize of dialog
            d.setSize(100, 100);
            // set visibility of dialog
            d.setVisible(true);
        }
    }
}
```
**Вывод:**
![[Ex2-JDialog.png]]

#### Пример 3. Программа для создания диалога внутри диалога

```java
// java Program to create a dialog within a dialog
import java.awt.event.*;
import java.awt.*;
import javax.swing.*;
class solve extends JFrame implements ActionListener {
    // frame
    static JFrame f;
    // dialog
    static JDialog d, d1;

    // main class
    public static void main(String[] args) {
        // create a new frame
        f = new JFrame("frame");
        f.setDefaultCloseOperation(EXIT_ON_CLOSE);
        // create a object
        solve s = new solve();
        // create a panel
        JPanel p = new JPanel();
        JButton b = new JButton("click");
        // add actionlistener to button
        b.addActionListener(s);
        // add button to panel
        p.add(b);
        f.add(p);
        // set the size of frame
        f.setSize(400, 400);
        f.setVisible(true);
    }
    public void actionPerformed(ActionEvent e) {
        String s = e.getActionCommand();
        if (s.equals("click")) {
            // create a dialog Box
            d = new JDialog(f, "dialog Box");
            // create a label
            JLabel l = new JLabel("this is first dialog box");
            // create a button
            JButton b = new JButton("click me");
            // add Action Listener
            b.addActionListener(this);
            // create a panel
            JPanel p = new JPanel();
            p.add(b);
            p.add(l);
            // add panel to dialog
            d.add(p);
            // setsize of dialog
            d.setSize(200, 200);
            // set visibility of dialog
            d.setVisible(true);
        }
        else { // create a dialog Box
            d1 = new JDialog(d, "dialog Box");
            // create a label
            JLabel l = new JLabel("this is second dialog box");
            d1.add(l);
            // setsize of dialog
            d1.setSize(200, 200);
            // set location of dialog
            d1.setLocation(200, 200);
            // set visibility of dialog
            d1.setVisible(true);
        }
    }
}
```
**Вывод:**
![[Ex3-JDialog.png]]

### Оформление окон

Начиная с JDK 1.4 появилась возможность настраивать так называемое визуальное «оформление» окон: рамка, элементы управления окном (кнопки закрытия или свертывания), системное меню. Необходимость этого ощущалась с самых первых выпусков [Swing](Swing).

Сейчас создание различных интерфейсов окон возможна благодаря усовершенствованиям в UI-представителе корневой панели [[Swing#Корневая панель JRootPane|JRootPane]]. UI-представитель позволяет создавать специальные рамки, заголовок, системное меню и кнопки управления окном, и размещать их в корневой панели нужным образом, используя специализированный менеджер расположения. Менеджер расположения контролирует пространство корневой панели. Кроме этого, при новом оформлении окон отключаются системные элементы окна.

В классах [JFrame](JFrame) и JDialog имеется статический метод setDefaultLookAndFeelDecorated(), обеспечивающий возможность оформления всех создаваемых окон.

#### Пример 4. Пример оформления окон: JDialog decoration

```java
// Оформление окон Swing
import javax.swing.*;

public class JFrameDecorations {
    public static void main(String[] args) {
        // Подключение украшений для окон
        JFrame.setDefaultLookAndFeelDecorated(true);
        JDialog.setDefaultLookAndFeelDecorated(true);
        // Создание окна с рамкой
        JFrame frame = new JFrame("Oкнo с рамкой");
        // Определение способа завершения работы программы
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setSize(200, 200);
        frame.setVisible(true);
        // Создание диалогового окна
        JDialog dialog = new JDialog(frame, "Диалоговое окно");
        // Определение способа завершения работы диалогового окна
        dialog.setDefaultCloseOperation(JDialog.DISPOSE_ON_CLOSE);
        dialog.setSize(150, 100);
        // Определение типа оформления диалогового окна
        dialog.getRootPane().setWindowDecorationStyle(JRootPane.INFORMATION_DIALOG);
        dialog.setVisible(true);
    }
}
```
В примере создается простое окно с рамкой и диалоговое окно. Перед создания окон вызывается метод setDefaultLookAndFeelDecorated(), означающий, что для создаваемых окон **[JFrame](JFrame)** и **JDialog** потребуется специальное оформление. Далее определяются размеры окон и они выводятся на экран.

Следует обратить внимание на метод корневой панели setWindowDecorationStyle(), позволяющий настроить оформление окна. Если окно с рамкой имеет только один тип оформления, то диалоговые окна в зависимости от их цели (представление информации, сообщение об ошибке и т.д.) могут выглядеть по-разному. В примере было определено, что создаваемое диалоговое окно требуется для вывода информации и должно выглядеть соответствующим образом.

Интерфейс примера окон, оформленных с внешним видом Metal, представлен на следующем скриншоте.
![[Ex4-JDialog.png]]

Специальное оформление окон может быть полезно как средство, позволяющее полностью, вплоть до окон, управлять внешним видом вашего приложения. Создав собственного UI-представителя корневой панели, можно придать своему приложению уникальный вид, легко узнаваемый пользователями.

