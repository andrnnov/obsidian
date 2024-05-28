#Java #awt #MouseEvent

## Класс MouseEvent Java

2024-05-28 10:15

Объявление класса **_MouseEvent_**:
```java
public class MouseEvent extends InputEvent;
```

Событие **MouseEvent** возникает в компоненте по любой из семи причин:
- нажатие кнопки мыши – идентификатор **MOUSE_PRESSED**;
- отпускание кнопки мыши – идентификатор **MOUSE_RELEASED**;
- щелчок кнопкой мыши – идентификатор **MOUSE_CLICKED** (нажатие и отпускание не различаются);
- перемещение мыши – идентификатор **MOUSE_MOVED**;
- перемещение мыши с нажатой кнопкой – идентификатор **MOUSE_DRAGGED**;
- появление курсора мыши в компоненте – идентификатор **MOUSE_ENTERED**;
- выход курсора мыши из компонента – идентификатор **MOUSE_EXITED**.

Для их обработки есть семь методов в двух интерфейсах [MouseListener](MouseListener) и MouseMotionListener:
```java
public interface MouseListener extends EventListener{
public void mouseClicked(MouseEvent e);
public void mousePressed(MouseEvent e);
public void mouseReleased(MouseEvent e);
public void mouseEntered(MouseEvent e);
public void mouseExited(MouseEvent e);
}
public interface MouseMotionListener extends EventListener{
public void mouseDragged(MouseEvent e);
public void mouseMoved(MouseEvent e);
}
```
Эти методы могут получить от аргумента е координаты курсора мыши в системе координат компонента методами **e.getx()**, **e.getv()**, или одним методом **e.getPoint()**, возвращающим экземпляр класса [[Component#Положение. Класс Point|Point]].

Двойной щелчок кнопкой мыши можно отследить методом **e.getclickcount()**, возвращающим количество щелчков. При перемещении мыши возвращается 0.

Узнать, какая кнопка была нажата, можно с помощью метода **e.getModifiers()** класса inputEvent сравнением со следующими статическими константами класса inputEvent:
- **BUTTON1_MASK** – нажата первая кнопка, обычно левая;
- **BUTTON2_MASK** – нажата вторая кнопка, обычно средняя, или одновременно нажаты обе кнопки на двухкнопочной мыши;
- **BUTTON3_MASK** – нажата третья кнопка, обычно правая.

### Поля

| Модификатор и тип         | Поле и описание                                                             |
| ------------------------- | --------------------------------------------------------------------------- |
| static int	BUTTON1        | Указывает кнопку мыши №1; используется getButton().                         |
| static int	BUTTON2        | Указывает кнопку мыши №2; используется getButton().                         |
| static int	BUTTON3        | Указывает кнопку мыши №3; используется getButton().                         |
| static int	MOUSE_CLICKED  | Событие "щелчок мышью".                                                     |
| static int	MOUSE_DRAGGED  | Событие "перетаскивания мышью".                                             |
| static int	MOUSE_ENTERED  | Событие "Мышь введена".                                                     |
| static int	MOUSE_EXITED   | Событие "Мышь завершила работу".                                            |
| static int	MOUSE_FIRST    | Первое число в диапазоне идентификаторов, используемых для событий мыши.    |
| static int	MOUSE_LAST     | Последнее число в диапазоне идентификаторов, используемых для событий мыши. |
| static int	MOUSE_MOVED    | Событие "Мышь перемещена".                                                  |
| static int	MOUSE_PRESSED  | Событие "Нажата мышь".                                                      |
| static int	MOUSE_RELEASED | Событие "Мышь выпущена".                                                    |
| static int	MOUSE_WHEEL    | Событие "Колесико мыши".                                                    |
| static int	NOBUTTON       | Указывает на отсутствие кнопок мыши; используется getButton().              |

### Конструкторы

- public MouseEvent(Component source, int id, long when, int modifiers, int x, int y, int clickCount, boolean popupTrigger, int button);
- public MouseEvent (Component source, int id, long when, int modifiers, int x, int y, int clickCount, boolean popupTrigger);

Создают `MouseEvent` объект с указанным исходным компонентом, типом, модификаторами, координатами и количеством кликов.

>Обратите внимание, что передача недопустимого значения `id` приводит к неопределенному поведению. Создание недопустимого события (например, при использовании более чем одной из старых `_MASKs` или значений модификатора / кнопки, которые не совпадают) приводит к неопределенному поведению. Этот метод выдает значение `IllegalArgumentException` if `source` is `null`.

Параметры:
- source - тот, Component который вызвал событие
- id - целое число, идентифицирующее событие
- when - длинный int, указывающий время, когда произошло событие
- modifiers - во время события модификатор нажимается вниз (например, shift, ctrl, alt, meta). Следует использовать либо расширенные модификаторы `_DOWN_MASK`, либо старые `_MASK`, но обе модели не должны смешиваться в одном событии. Предпочтительно использовать расширенные модификаторы.
- x - горизонтальная координата x для местоположения мыши
- y - вертикальная координата y для местоположения мыши
- clickCount - количество щелчков мыши, связанных с событием
- popupTrigger - логическое значение, true, если это событие является триггером для всплывающего меню
- button - какая из кнопок мыши изменила состояние. NOBUTTON, BUTTON1, BUTTON2 или BUTTON3.

### Методы

| Модификатор и тип | Метод и описание                                                                                                                                                                                |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int               | getButton()<br>Возвращает, какая из кнопок мыши, если таковая имеется, изменила состояние.                                                                                                      |
| int               | getClickCount()<br>Возвращает количество щелчков мыши, связанных с этим событием.                                                                                                               |
| Point             | getLocationOnScreen()<br>Возвращает абсолютную позицию события по x, y.                                                                                                                         |
| int               | getModifiersEx()<br>Возвращает расширенную маску-модификатор для этого события.                                                                                                                 |
| static String     | getMouseModifiersText(int modifiers)<br>Возвращает String экземпляр, описывающий клавиши-модификаторы и кнопки мыши, которые были нажаты во время события, такие как "Shift" или "Ctrl+ Shift". |
| Point             | getPoint()<br>Возвращает положение события по x, y относительно исходного компонента.                                                                                                           |
| int               | getX()<br>Возвращает горизонтальное положение x события относительно исходного компонента.                                                                                                      |
| int               | getXOnScreen()<br>Возвращает абсолютную горизонтальную позицию x события.                                                                                                                       |
| int               | getY()<br>Возвращает вертикальное положение y события относительно исходного компонента.                                                                                                        |
| int               | getYOnScreen()<br>Возвращает абсолютную вертикальную позицию y события.                                                                                                                         |
| boolean           | isPopupTrigger()<br>Возвращает, является ли это событие мыши событием запуска всплывающего меню для платформы.                                                                                  |
| String            | paramString()<br>Возвращает строку параметра, идентифицирующую это событие.                                                                                                                     |
| void              | translatePoint(int x, int y)<br>Преобразует координаты события в новую позицию, добавляя указанные x (горизонтальное) и y (вертикальное) смещения.                                              |

`MouseEvent` передается каждому `MouseListener` или `MouseAdapter` объекту, который зарегистрирован для получения  событий мыши с использованием `addMouseListener` метода компонента. (`MouseAdapter` объекты реализуют `MouseListener` интерфейс.) Каждый такой объект-прослушиватель получает `MouseEvent` событие мыши.

`MouseEvent` также передается каждому объекту `MouseMotionListener` или `MouseMotionAdapter`, который зарегистрирован для получения событий движения мыши с использованием `addMouseMotionListener` метода компонента. (`MouseMotionAdapter` объекты реализуют `MouseMotionListener` интерфейс.) Каждый такой объект-прослушиватель получает `MouseEvent` содержащий событие движения мыши.

При нажатии кнопки мыши генерируются события, которые отправляются зарегистрированным `MouseListener` пользователям. Состояние модальных ключей можно получить с помощью `InputEvent.getModifiers()` и `InputEvent.getModifiersEx()`. Маска кнопки, возвращаемая `InputEvent.getModifiers()`, отражает только кнопку, которая изменила состояние, а не текущее состояние всех кнопок. (Примечание: Из-за совпадения значений ALT_MASK / BUTTON2_MASK и META_MASK / BUTTON3_MASK это не всегда верно для событий мыши, связанных с ключами-модификаторами). Чтобы получить состояние всех кнопок и клавиш-модификаторов, используйте `InputEvent.getModifiersEx()`. Кнопка, состояние которой изменилось, возвращается с помощью `getButton()`

Например, при нажатии первой кнопки мыши события отправляются в следующем порядке:

    модификаторы идентификатора     кнопки 
    `MOUSE_PRESSED`: `BUTTON1_MASK` `BUTTON1`
    `MOUSE_RELEASED`: `BUTTON1_MASK` `BUTTON1`
    `MOUSE_CLICKED`: `BUTTON1_MASK` `BUTTON1`
 

При нажатии нескольких кнопок мыши каждое нажатие, отпускание и щелчок приводят к отдельному событию.

Например, если пользователь нажимает **кнопку 1**, за которой следует **кнопка 2**, а затем отпускает их в том же порядке, генерируется следующая последовательность событий:

    модификаторы    идентификатора  кнопки 
    `MOUSE_PRESSED`: `BUTTON1_MASK` `BUTTON1`
    `MOUSE_PRESSED`: `BUTTON2_MASK` `BUTTON2`
    `MOUSE_RELEASED`: `BUTTON1_MASK` `BUTTON1`
    `MOUSE_CLICKED`: `BUTTON1_MASK` `BUTTON1`
    `MOUSE_RELEASED`: `BUTTON2_MASK` `BUTTON2`
    `MOUSE_CLICKED`: `BUTTON2_MASK` `BUTTON2`
 

Если сначала отпустить **кнопку 2**, то сначала появится пара `MOUSE_RELEASED`/`MOUSE_CLICKED` для `BUTTON2_MASK`, а затем пара для `BUTTON1_MASK`.

#### Пример 1. Простейшая программа рисования.

```java
import java.awt.*;
import java.awt.event.*;

public class Main extends Frame {
    public Main(String s){
        super(s);
        ScrollPane pane = new ScrollPane();
        pane.setSize(300, 300);
        add(pane, BorderLayout.CENTER);
        Scribble scr = new Scribble(this, 300, 300);
        pane.add(scr);
        Panel p = new Panel();
        add(p, BorderLayout.SOUTH);
        Button bl = new Button("Красный");
        p.add(bl);
        bl.addActionListener(scr);
        Button b2 = new Button("Зеленый");
        p.add(b2);
        b2.addActionListener(scr);
        Button b3 = new Button("Синий");
        p.add(b3);
        b3.addActionListener(scr);
        Button b4 = new Button("Черный");
        p.add(b4);
        b4.addActionListener(scr);
        Button b5 = new Button("Очистить");
        p.add(b5);
        b5.addActionListener(scr);
        addWindowListener(new WindowAdapter() {
            public void windowClosing(WindowEvent e){
                System.exit(0);
            }
        });
        pack();
        setVisible(true);
    }

    public static void main(String[] args) {
        new Main(" \"Рисовалка\"");
    }
}

class Scribble extends Component implements ActionListener, MouseListener, MouseMotionListener {
    protected int lastX, lastY, w, h;
    protected Color currColor = Color.black;
    protected Frame f;
    public Scribble(Frame frame, int width, int height){
        f = frame;
        w = width;
        h = height;
        enableEvents(AWTEvent.MOUSE_EVENT_MASK | AWTEvent.MOUSE_MOTION_EVENT_MASK);
        addMouseListener(this);
        addMouseMotionListener(this);
    }

    public Dimension getPreferredSize() {
        return new Dimension(w, h);
    }

    public void actionPerformed(ActionEvent event) {
        String s = event.getActionCommand();
        if (s.equals ("Очистить"))
            repaint();
        else if (s.equals ("Красный"))
            currColor = Color.red;
        else if (s.equals("Зеленый"))
            currColor = Color.green;
        else if (s.equals("Синий"))
            currColor = Color.blue;
        else if (s.equals("Черный"))
            currColor = Color.black;
    }

    public void mousePressed(MouseEvent e) {
        if(e.getButton()==MouseEvent.BUTTON1) return;
        lastX = e.getX();
        lastY = e.getY();
    }

    public void mouseDragged(MouseEvent e) {
        if(e.getButton()==MouseEvent.BUTTON1) return;
        Graphics g = getGraphics();
        g.setColor(currColor);
        g.drawLine(lastX, lastY, e.getX(), e.getY());
        lastX = e.getX();
        lastY = e.getY();
    }

    public void mouseReleased(MouseEvent e){}
    public void mouseClicked(MouseEvent e){}
    public void mouseEntered(MouseEvent e){}
    public void mouseExited(MouseEvent e){}
    public void mouseMoved(MouseEvent e){}
}
```
**Вывод:**
![[Ex1-MouseEvent.png]]

#### Пример 2.  Фиксация события мыши в Java [Swing](Swing)

```java
import java.awt.BorderLayout;
import java.awt.Dimension;
import java.awt.event.MouseEvent;
import java.awt.event.MouseListener;
import java.awt.event.MouseMotionListener;

import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.SwingConstants;
import javax.swing.SwingUtilities;

public class Main extends JFrame implements MouseListener, MouseMotionListener {
    private JLabel label;

    public Main() {
        super("MouseEvent Demo");
        label = new JLabel("No mouse event captured yet.", SwingConstants.CENTER);
        label.setPreferredSize(new Dimension(300, 100));
        add(label, BorderLayout.CENTER);
        addMouseListener(this);
        addMouseMotionListener(this);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        pack();
        setLocationRelativeTo(null);
        setVisible(true);
    }

    @Override
    public void mouseClicked(MouseEvent e) {
        label.setText("Mouse clicked at (" + e.getX() + ", " + e.getY() + ")");
    }

    @Override
    public void mousePressed(MouseEvent e) {
        label.setText("Mouse pressed at (" + e.getX() + ", " + e.getY() + ")");
    }

    @Override
    public void mouseReleased(MouseEvent e) {
        label.setText("Mouse released at (" + e.getX() + ", " + e.getY() + ")");
    }

    @Override
    public void mouseEntered(MouseEvent e) {
        label.setText("Mouse entered at (" + e.getX() + ", " + e.getY() + ")");
    }

    @Override
    public void mouseExited(MouseEvent e) {
        label.setText("Mouse exited at (" + e.getX() + ", " + e.getY() + ")");
    }

    @Override
    public void mouseDragged(MouseEvent e) {
        label.setText("Mouse dragged at (" + e.getX() + ", " + e.getY() + ")");
    }

    @Override
    public void mouseMoved(MouseEvent e) {
        label.setText("Mouse moved at (" + e.getX() + ", " + e.getY() + ")");
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> new Main());
    }

}
```
**Вывод:**
![[Ex2-MouseEvent.png]]
