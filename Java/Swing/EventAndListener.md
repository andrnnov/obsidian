#Java #Event #Listener

## События и слушатели

2024-05-16 15:52

Событие **_Event_** - это объект, описывающий изменение состояния источника, с которым оно связано. Примером события, в котором участвует пользователь, являются нажатие кнопки, выбор элемента из списка, ввод символа с клавиатуры и т.д. Событие может происходить и без участия пользователя при использовании таймера.

**Слушатель _Listener_** - это уведомляемый о некотором событии объект. Чтобы слушатель смог реагировать на определенное событие источника он должен быть им зарегистрирован, т.е. подключен к источнику. **_Listener_** должен реализовывать определенные методы для получения и обработки уведомлений о событии.

**_Listener_** находится в постоянном ожидании, пока в источнике, в котором он зарегистрирован, не наступит соответствующее событие. При его возникновении слушатель получает управление. Также слушателю передается объект события (источник), чтобы он смог правильно на него отреагировать. Таким образом, источник вызывает метод-обработчик события, определенный в классе, являющемся блоком прослушивания. В качестве блоков прослушивания иногда используют внутренние классы. В этом случае в методе, регистрирующем блок прослушивания в качестве параметра, используется объект этого внутреннего класса.

После обработки события _слушатель_ возвращает управление. Таким образом, для обработки события вызываются только те слушатели, которые на него "подписались", т.е. были зарегистрированы источником.

### Типы событий и слушателей

В пакете java.awt.event определены интерфейсы слушателей для каждого из определенных в нем типов событий (например, для событий MouseEvent определено два интерфейса слушателей: MouseListener и MouseMotionListener). Все интерфейсы слушателей событий являются расширениями интерфейса java.util.EventListener. В этом интерфейсе не определяется ни один из методов, но он играет роль базового интерфейса, в котором однозначно определены все слушатели событий как таковые. Т.е. слушатель наследуется от интерфейса **_EventListener_** и предназначен для обработки определенного типа событий. При этом **_Listener_** содержит один или несколько методов, которые принимают объект события в качестве единственного параметра и вызываются в определенных ситуациях.

Интерфейс слушателя событий **_Listener_** может включать несколько методов. Например, класс событий, подобный MouseEvent, описывает несколько событий, связанных с мышью, таких как события нажатия и отпускания кнопки мыши. Эти события вызывают различные методы соответствующего слушателя.

В таблице приведены определенные в пакете java.awt.event типы событий, соответствующие им слушатели, а также методы, определенные в каждом интерфейсе слушателя.

| Класс события              | Интерфейс слушателя                        | Обработчики события                                                                   |
| -------------------------- | ------------------------------------------ | ------------------------------------------------------------------------------------- |
| ActionEvent                | ActionListener                             | actionPerformed(ActionEvent e)                                                        |
| AdjustmentEvent            | AdjustmentListener                         | adjustmentValueChanged(AdjustmentEvent e)                                             |
| ComponentEvent             | ComponentListener                          | componentResized(ComponentEvent e)                                                    |
|                            |                                            | componentMoved(ComponentEvent e)                                                      |
|                            |                                            | componentShown(ComponentEvent e)                                                      |
|                            |                                            | componentHidden(ComponentEvent e)                                                     |
| ContainerEvent             | ContainerListener                          | componentAdded(ContainerEvent e)                                                      |
|                            |                                            | componentRemoved(ContainerEvent e)                                                    |
| FocusEvent                 | FocusListener                              | focusGained(FocusEvent e)                                                             |
|                            |                                            | focusLost(FocusEvent e)                                                               |
| ItemEvent                  | ItemListener                               | itemStateChanged(ItemEvent e)                                                         |
| [KeyEvent](KeyEvent)       | [KeyListener](KeyListener)                 | [[KeyListener#Длинные одновременные нажатия\|keyPressed(KeyEvent e)]]                 |
|                            |                                            | [[KeyListener#Длинные одновременные нажатия\|keyReleased(KeyEvent e)]]                |
|                            |                                            | [[KeyListener#Короткие нажатия\|keyTyped(KeyEvent e)]]                                |
| [MouseEvent](MouseEvent)   | [MouseListener](MouseListener)             | [[MouseListener#Методы интерфейса\|mouseClicked(MouseEvent e)]]                       |
|                            |                                            | [[MouseListener#Методы интерфейса\|mousePressed(MouseEvent e)]]                       |
|                            |                                            | [[MouseListener#Методы интерфейса\|mouseReleased(MouseEvent e)]]                      |
|                            |                                            | [[MouseListener#Методы интерфейса\|mouseEntered(MouseEvent e)]]                       |
|                            |                                            | [[MouseListener#Методы интерфейса\|mouseExited(MouseEvent e)]]                        |
|                            | [MouseMotionListener](MouseMotionListener) | [[MouseMotionListener#Методы интерфейса\|mouseDragged(MouseEvent e)]]                 |
|                            |                                            | [[MouseMotionListener#Методы интерфейса\|mouseMoved(MouseEvent e)]]                   |
| TextEvent                  | TextListener                               | textValueChanged(TextEvent e)                                                         |
| [WindowEvent](WindowEvent.md) | [WindowListener](WindowListener)           | [[WindowListener#Методы интерфейса WindowListener\|windowOpened(WindowEvent e)]]      |
|                            |                                            | [[WindowListener#Методы интерфейса WindowListener\|windowClosing(WindowEvent e)]]     |
|                            |                                            | [[WindowListener#Методы интерфейса WindowListener\|windowClosed(WindowEvent e)]]      |
|                            |                                            | [[WindowListener#Методы интерфейса WindowListener\|windowIconified(WindowEvent e)]]   |
|                            |                                            | [[WindowListener#Методы интерфейса WindowListener\|windowDeiconified(WindowEvent e)]] |
|                            |                                            | [[WindowListener#Методы интерфейса WindowListener\|windowActivated(WindowEvent e)]]   |
Корнем иерархии классов событий является суперкласс **_EventObject_** из пакета _java.util_. Данный класс содержит два метода: _getSource()_, возвращающий источник событий, и _toString()_, возвращающий строчный эквивалент события. Чтобы узнать, в каком объекте произошло событие, нужно вызвать метод getSource(), возвращающий значение типа [Object](Object). Следовательно, один и тот же слушатель можно подключить к разным источникам.

Для события ActionEvent регистрация проводится по форме ActionListener. Имена в ней связаны соответствующим образом, а для каждого события формы ABCEvent ассоциированным слушателем является ABCListener, где вместо ABC указывается конкретный тип события.

Регистрация происходит при вызове метода addActionListener. Каждый зарегистрированный реализатор уведомляется путем передачи (при генерации события ActionEvent) реализации интерфейса слушателя методу addActionListener. У одного события может быть несколько наблюдателей.

Весь процесс представлен следующими пунктами (хотя порядок их следования может меняться):
- Определить для заданного события класс, реализующий связанный с ним интерфейс. В существующее определение класса можно добавить строку "implements ABCListener" или создать новый класс, реализующий данный интерфейс. 
- Добавления в определение класса строки "implements ABCListener" недостаточно. Кроме этого необходимо реализовать каждый метод данного интерфейса. У одних слушателей (например, ActionListener) есть только один метод. У других (например, WindowListener, используемого при перемещении или закрытии окна) – несколько. Код можно компилировать тогда, когда определены все методы слушателей. Однако и это еще не все. Для того чтобы программа должным образом реагировала на события необходимо выполнить последнее действие.
- После определения реализации интерфейса необходимо создать экземпляр реализации и ассоциировать его с компонентом. Только после этого наблюдатель (слушатель) сможет получать уведомления о возникновении соответствующих событий.

#### Пример 1. В данной программе продемонстрирован случай обработки события «выбор кнопки»

```java
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

class MyActionListener implements ActionListener {
  public void actionPerformed(ActionEvent e) {
    System.out.println("Thank you.");
  }
}

public class SelectMe extends JFrame {

  public SelectMe() {
    super("Hello");
    setDefaultCloseOperation(EXIT_ON_CLOSE);
    JButton button = new JButton("Pick Me");
    ActionListener listener = new MyActionListener();
    button.addActionListener(listener);
    getContentPane().add(button, BorderLayout.CENTER);
    setSize(200, 200);
  }

  public static void main(String args[]) {
    JFrame frame = new SelectMe();
    frame.show();
  }
}
```
**Вывод:**
![[Ex1-EventAndListener.png]]
Вывод в консоли при нажатии кнопки: <p style="background-color: navy; color: yellow">Thank you.</p>

### Классы-адаптеры, Adapter

Для каждого интерфейса слушателей событий, содержащего несколько методов, в пакете _java.awt.event_ определен **класс-адаптер Adapter**. Когда нужен только один или два таких метода, иногда проще получить подкласс класса-адаптера, чем реализовать интерфейс самостоятельно. _При использовании адаптера требуется лишь переопределить те методы, которые нужны, а при прямой реализации интерфейса необходимо определить все методы, в том числе и ненужные в данной программе_.

Заранее определенные классы-адаптеры называются также, как и интерфейсы, которые они реализуют. Но в этих названиях **Listener** заменяется на **Adapter**; например _MouseAdapter_, _MouseMotionAdapter_, _WindowAdapter_ и т.д.

#### Описание класса-адаптера действий с мышью, MouseAdapter

```java
public abstract class MouseAdapter implements MouseListener { 
    public void mouseClicked(MouseEvent e){} 
    public void mousePressed(MouseEvent e){} 
    public void mouseReleased(MouseEvent e){} 
    public void mouseEntered(MouseEvent e){} 
    public void mouseExited(MouseEvent e){}  
}  

public abstract class MouseMotionAdapter implements MouseMotionListener { 
    public void mouseDragged(MouseEvent e){} 
    public void mouseMoved(MouseEvent e){}  
}
```
Классов-адаптеров всего семь. Кроме уже упомянутых трех классов, это классы ComponentAdapter, ContainerAdapter, FocusAdapter и KeyAdapter.

#### Пример 2. Реализация адаптера

В качестве следующего примера мы создадим приложение с двумя кнопками. При наведении на кнопку мышью в текстовом поле должно появляться имя кнопки. В данном приложении расширяется класс MouseAdapter, таким образом, вместо всех пяти в интерфейсе MouseListener реализовано только два метода:
```java
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;

public class MouseAdapterExample extends JFrame {
  JButton button1, button2;
  JTextField tf;

  public MouseAdapterExample() {
    // открыть конструктор

    // создать кнопки и добавить слушателей
    button1 = new JButton("Button 1");
    button1.setName("Button 1");
    button1.addMouseListener(new MouseHandler());
    button2 = new JButton("Button 2");
    button2.setName("Button 2");
    button2.addMouseListener(new MouseHandler());

    // Создать текстовое поле, в котором
    // пользователь не сможет вводить текст
    tf = new JTextField(25);
    tf.setEditable(false);

    // создать панели, добавить кнопки и текстовое поле
    JPanel p1 = new JPanel();
    p1.setBackground(Color.white);
    p1.add(button1);
    p1.add(button2);

    JPanel p2 = new JPanel();
    p2.setBackground(Color.white);
    p2.add(tf);

    // получить ContentPane и добавить панели
    getContentPane().setLayout(new BorderLayout());
    getContentPane().add(p1, BorderLayout.NORTH);
    getContentPane().add(p2, BorderLayout.SOUTH);

    addWindowListener(new WinClosing());
    setBounds(100, 100, 300, 100);
    setVisible(true);
  }
  // закрыть конструктор

  // MouseHandler обрабатывает события мыши и
  // расширяет класс adapter, обеспечивающий пустые
  // методы. Данный класс (MouseHandler) переопределяет
  // методы mouseEntered и mouseExit.
  class MouseHandler extends MouseAdapter {
    public void mouseEntered(MouseEvent me)
           {
             // При перемещении мыши над кнопкой
             // имя кнопки фиксируется и отображается в текстовом поле.
             tf.setText("Mouse is over" + me.getComponent().getName());
            }

    public void mouseExited(MouseEvent me) {
      // Когда мышь покидает область кнопки
      // значение в текстовом поле сбрасывается.
      tf.setText("");
    }
  }
  // закрыть MouseHandler

  public static void main(String args[]) {
    MouseAdapterExample mae = new MouseAdapterExample();
  }
}

// Данный класс расширяет класс adapter и
// переопределяет только один метод: windowClosing. Вместо
// того, чтобы использовать данный класс для закрытия окна,
// вы можете добавить в код еще одну строку:
// setDefaultCloseOperation(EXIT_ON_CLOSE);
// как показано ранее в примере SelectMe.
class WinClosing extends WindowAdapter {
  public void windowClosing(WindowEvent we) {
    System.exit(0);
  }
}
```
**Вывод:**
![[Ex2-EventAndListener.png]]

### События, связанные с визуальными компонентами AWT

В следующей таблице приведен список визуальных компонентов пакета [AWT](AWT) и событий, которые они порождают.

| Компонент              | Событие                    | Описание                                                                                                                                                                                            |
| ---------------------- | -------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Button                 | ActionEvent                | Пользователь нажал кнопку                                                                                                                                                                           |
| CheckBox               | ItemEvent                  | Пользователь установил или сбросил флажок                                                                                                                                                           |
| CheckBoxMenuItem       | ItemEvent                  | Пользователь установил или сбросил флажок рядом с пунктом меню                                                                                                                                      |
| Choice                 | ItemEvent                  | Пользователь выбрал элемент списка или отменил его выбор                                                                                                                                            |
| [Component](Component) | ComponentEvent             | Элемент либо перемещен, либо он стал скрытым, либо видимым                                                                                                                                          |
|                        | FocusEvent                 | Элемент получил или потерял фокус ввода                                                                                                                                                             |
|                        | [KeyEvent](KeyEvent)       | Пользователь нажал или отпустил клавишу                                                                                                                                                             |
|                        | [MouseEvent](MouseEvent)   | Пользователь нажал или отпустил кнопку мыши, либо курсор мыши вошел или покинул область, занимаемую элементом, либо пользователь просто переместил мышь или переместил мышь при нажатой кнопке мыши |
| Container              | ContainerEvent             | Элемент добавлен в контейнер или удален из него                                                                                                                                                     |
| List                   | ActionEvent                | Пользователь выполнил двойной щелчок мыши на элементе списка                                                                                                                                        |
|                        | ItemEvent                  | Пользователь выбрал элемент списка или отменил выбор                                                                                                                                                |
| MenuItem               | ActionEvent                | Пользователь выбрал пункт меню                                                                                                                                                                      |
| Scrollbar              | AdjustmentEvent            | Пользователь осуществил прокрутку                                                                                                                                                                   |
| TextComponent          | TextEvent                  | Пользователь внес изменения в текст элемента                                                                                                                                                        |
| TextField              | ActionEvent                | Пользователь закончил редактирование текста элемента                                                                                                                                                |
| Window                 | [WindowEvent](WindowEvent.md) | Окно было открыто, закрыто, представлено в виде пиктограммы, восстановлено или требует восстановления                                                                                               |

### Регистрация слушателя Listener

Для регистрации слушателя источник использует специальные методы. Как правило, имена методов имеют форму addXxxListener(XxxListener listener) или setXxxListener(XxxListener listener), где Xxx - это имя события, а listener - ссылка на слушателя событий.

#### Пример 3. Пример использования слушателя ActionListener

```java
import java.awt.Dimension;
import java.awt.FlowLayout;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
 
import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JPanel;
import javax.swing.JTextField;
 
public class TestFrame extends JFrame {
 	 private static final long serialVersionUID = 1L;

 	 private JTextField textField;
 	 private JButton    button1;
 	 private JButton    button2;
 	 private JButton    button3;
 	
     public TestFrame() {
          super("Test frame");
          createGUI();
     }
 
     public void createGUI() {
          setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
 
          JPanel panel = new JPanel();
          panel.setLayout(new FlowLayout());
 
          button1 = new JButton("Button 1");
          button1.setActionCommand("Button 1 was pressed!");
          panel.add(button1);
 
          button2 = new JButton("Button 2");
          button2.setActionCommand("Button 2 was pressed!");
          panel.add(button2);
 
          button3 = new JButton("Button 3");
          button3.setActionCommand("Button 3 was pressed!");
          panel.add(button3);
 
          textField = new JTextField();
          textField.setColumns(23);
          panel.add(textField);
 
          ActionListener actionListener = new TestActionListener();
           
          button1.addActionListener(actionListener);
          button2.addActionListener(actionListener);
          button3.addActionListener(actionListener);
           
          getContentPane().add(panel);
          setPreferredSize(new Dimension(320, 100));
     }
 
     public class TestActionListener implements ActionListener {
          public void actionPerformed(ActionEvent e) {
              textField.setText(e.getActionCommand());
          }
     }
 
     public static void main(String[] args) {
        javax.swing.SwingUtilities.invokeLater(new Runnable() {
             public void run() {
                  JFrame.setDefaultLookAndFeelDecorated(true);
                  TestFrame frame = new TestFrame();
                  frame.pack();
                  frame.setLocationRelativeTo(null);
                  frame.setVisible(true);
             }
        });
     }
}
```
**Вывод:**
![[Ex3-EventAndListener.png]]

### Программный вызов события

Событие вызывается автоматически, при наступлении определенных условий. Но можно событие создать и вызвать программно (fire event).

В предыдущий пример были внесены изменения во внутренний класс TestActionListener, в результате чего по нажатию на кнопку button3 создается и вызывается новое событие.

```java
import java.awt.Dimension;
import java.awt.FlowLayout;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
 
import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JPanel;
import javax.swing.JTextField;
 
public class TestFrame extends JFrame
{
 	 private static final long serialVersionUID = 1L;

 	 private JTextField textField;
 	 private JButton    button1;
 	 private JButton    button2;
 	 private JButton    button3;
 	
     public TestFrame() {
          super("Test frame");
          createGUI();
     }
 
     public void createGUI() {
          setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
 
          JPanel panel = new JPanel();
          panel.setLayout(new FlowLayout());
 
          button1 = new JButton("Button 1");
          button1.setActionCommand("Button 1 was pressed!");
          panel.add(button1);
 
          button2 = new JButton("Button 2");
          button2.setActionCommand("Button 2 was pressed!");
          panel.add(button2);
 
          button3 = new JButton("Button 3");
          button3.setActionCommand("Button 3 was pressed!");
          panel.add(button3);
 
          textField = new JTextField();
          textField.setColumns(23);
          panel.add(textField);
 
          ActionListener actionListener = new TestActionListener();
           
          button1.addActionListener(actionListener);
          button2.addActionListener(actionListener);
          button3.addActionListener(actionListener);
           
          getContentPane().add(panel);
          setPreferredSize(new Dimension(320, 100));
     }
 
public class TestActionListener implements ActionListener {
    public void actionPerformed(ActionEvent e) {
        JButton button = (JButton) e.getSource();
        System.out.println (button.getText() + ", " + 
                               e.getActionCommand());
        if (e.getSource() != button3) {
            textField.setText(e.getActionCommand());
        } else {
            ActionEvent e1 = new ActionEvent(button2,
                                    Event.MOUSE_DOWN,
                 "Button 2 was pressed programmatically!");
            ActionListener[] listeners;
            listeners = button2.getActionListeners();
            listeners[0].actionPerformed(e1);
        }
    }
} 
     public static void main(String[] args) {
        javax.swing.SwingUtilities.invokeLater(new Runnable() {
             public void run() {
                  JFrame.setDefaultLookAndFeelDecorated(true);
                  TestFrame frame = new TestFrame();
                  frame.pack();
                  frame.setLocationRelativeTo(null);
                  frame.setVisible(true);
             }
        });
     }
}
```
После нажатия на кнопку button3 в консоли будет выведена следующая информация:
<p style="background-color: navy; color: yellow">
Button 1, Button 1 was pressed!<br>
Button 2, Button 2 was pressed!<br>
Button 3, Button 3 was pressed!<br>
Button 2, Button 2 was pressed programmatically!</p>

#### Пример 4. Интерфейс KeyListener и абстрактный класс KeyAdapter

События клавиатуры также можно отслеживать. Для получения такого рода событий используется интерфейс KeyListener. Объекты-слушатели регистрируются для таких компонентов, как окно или панель, при помощи метода addKeyListener компонента.

Класс, заинтересованный в обработке событий клавиатуры, или реализует данный интерфейс вместе со всеми его методами, или же расширяет абстрактный класс KeyAdapter. В последнем случае вы можете переопределить только те методы, которые имеют значение для приложения.

В качестве примера в следующем приложении создается объект, который устанавливает, вводятся ли с клавиатуры какие-либо символы. Введенный текст отображается в метке внизу экрана:
```java
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;

public class KeyAdapterExample extends JFrame {
  // Метка, отображающая введенный текст.
  JLabel label;
  // Окно, в котором перемещается мышь и вводится текст
  JPanel p;

  public KeyAdapterExample() {
    label = new JLabel("You typed: ");

    p = new JPanel();
    p.setBackground(Color.white);
    // Зарегистрировать введенный символ
    p.addKeyListener(new KeyHandler());
    // Зарегистрировать перемещение мыши в области глухой панели
    p.addMouseListener(new MyMouseAdapter(p));

    // Получить ContentPane и отформатировать
    getContentPane().setLayout(new BorderLayout());
    getContentPane().add(p, BorderLayout.CENTER);
    getContentPane().add(label, BorderLayout.SOUTH);
    // зарегистрировать выход из программы
    addWindowListener(new WinClosing());
    setBounds(100, 100, 200, 200);
    setVisible(true);
  }
  // закрыть конструктор

  // Класс, обрабатывающий набор символов
  class KeyHandler extends KeyAdapter {
    // Метод, извлекающий набранные символы и
    // устанавливающий их в качестве значений метки
    public void keyTyped(KeyEvent ke) {
      label.setText("You typed: " + ke.getKeyChar());
      label.invalidate();
      invalidate();
      validate();
    }
  }

  // Класс, обрабатывающий перемещение мыши
  class MyMouseAdapter extends MouseAdapter {
    MyMouseAdapter(Component c) {
      this.c = c;
    }

    public void mousePressed(MouseEvent e) {
      c.requestFocus();
    }

    private Component c;
  }

  public static void main(String args[]) {
    KeyAdapterExample kae = new KeyAdapterExample();
  }
}

class WinClosing extends WindowAdapter

{
  public void windowClosing(WindowEvent we) {
    System.exit(0);
  }
}
```
**Вывод:**
![[Ex4-EventAndListener.png]]