#Java #Swing #JCheckBox

## Класс JCheckBox

2024-05-31 11:20

**_JCheckBox_** является частью пакета Java [Swing](Swing). **_JCheckBox_** можно выбрать или снять с выбора. Он отображает свое состояние пользователю. **_JCheckBox**_ — это реализация флажка. **_JCheckBox_** наследует класс [JToggleButton](JToggleButton).

### Конструкторы класса

1. **JCheckBox()** : создает новый флажок без текста или значка.
2. **JCheckBox(Icon i)** : создает новый флажок с указанным значком.
3. **JCheckBox(Icon i, boolean s)** : создает новый флажок с указанным значком, а логическое значение указывает, выбран он или нет.
4. **JCheckBox(String t)** : создает новый флажок с указанной строкой.
5. **JCheckBox(String t, boolean s)** : создает новый флажок с указанной строкой, а логическое значение указывает, выбран он или нет.
6. **JCheckBox(String t, Icon i)** : создает новый флажок с указанной строкой и значком.
7. **JCheckBox(String t, Icon i, boolean s)** : создает новый флажок с указанной строкой и значком, а логическое значение указывает, выбран он или нет.

### Методы добавления слушателя элементов в флажок

1. **addActionListener(ItemListener l)** : добавляет прослушиватель элементов к компоненту.
2. **itemStateChanged(ItemEvent e)** : абстрактная функция, вызываемая при изменении состояния элемента, к которому применяется прослушиватель.
3. **GetItem()** : возвращает объект, специфичный для компонента, связанный с элементом, состояние которого изменилось.
4. **getStateChange()** : возвращает новое состояние элемента. Класс ItemEvent определяет два состояния: SELECTED и DESELECTED.
5. **getSource()** : возвращает компонент, вызвавший событие элемента.

### Часто используемые методы

1. **setIcon(Icon i)** : устанавливает значок флажка на заданный значок.
2. **setText(String s)** : устанавливает текст флажка в заданный текст
3. **setSelected(boolean b)** : устанавливает флажок выбранным, если переданное логическое значение истинно или наоборот
4. **getIcon()** : возвращает изображение флажка.
5. **getText()** : возвращает текст флажка
6. **updateUI()** : сбрасывает свойство пользовательского интерфейса со значением текущего внешнего вида.
7. **getUI()** : возвращает внешний вид объекта, который отображает этот компонент.
8. **paramString()** : возвращает строковое представление этого JCheckBox.
9. **getUIClassID()** : возвращает имя класса внешнего вида, который отображает этот компонент.
10. **getAccessibleContext()** : получает AccessibleContext, связанный с этим JCheckBox.
11. **isBorderPaintedFlat()** : получает значение свойства borderPaintedFlat.
12. **setBorderPaintedFlat(boolean b)** : устанавливает свойство borderPaintedFlat.

#### Пример 1. Программа для создания простого флажка с помощью JCheckBox.

```java
// java Program to create a simple checkbox using JCheckBox 
import java.awt.event.*;
import java.awt.*;
import javax.swing.*;
class solve extends JFrame {

    // frame 
    static JFrame f;

    // main class 
    public static void main(String[] args) {
        // create a new frame 
        f = new JFrame("frame");
        // set layout of frame 
        f.setLayout(new FlowLayout());
        // create checkbox 
        JCheckBox c1 = new JCheckBox("checkbox 1");
        JCheckBox c2 = new JCheckBox("checkbox 2");
        // create a new panel 
        JPanel p = new JPanel();

        // add checkbox to panel 
        p.add(c1);
        p.add(c2);

        // add panel to frame 
        f.add(p);
        // set the size of frame 
        f.setSize(300, 100);
        f.setVisible(true);
    }
} 
```
**Вывод:**
![[Ex1-JCheckBox.png]]

#### Пример 2. Программа для создания флажка со значком 

```java
// java Program to create a checkbox with a icon .
import java.awt.event.*;
import java.awt.*;
import javax.swing.*;

class solve extends JFrame {
    // frame
    static JFrame f;
    // main class
    public static void main(String[] args) {
        // create a new frame
        f = new JFrame("frame");
        f.setDefaultCloseOperation(EXIT_ON_CLOSE);
        // set layout of frame
        f.setLayout(new FlowLayout());

        // create checkbox
        JCheckBox c1 = new JCheckBox("checkbox with image", new ImageIcon("c:\\book\\Icon.jpg"), true);
        JCheckBox c2 = new JCheckBox("checkbox 2");

        // create a new panel
        JPanel p = new JPanel();

        // add checkbox to panel
        p.add(c1);
        p.add(c2);

        // add panel to frame
        f.add(p);

        // set the size of frame
        f.setSize(300, 300);
        f.setVisible(true);         
    }
}
```

#### Пример 3. Программа для создания чекбокса и ItemListener к нему

```java
// java Program to create a checkbox and ItemListener to it.
import java.awt.event.*;
import java.awt.*;
import javax.swing.*;
class solve extends JFrame implements ItemListener {

    // frame
    static JFrame f;
    // label
    static JLabel l, l1;
    // checkbox
    static JCheckBox c1, c2;

    // main class
    public static void main(String[] args) {
        // create a new frame
        f = new JFrame("frame");
        f.setDefaultCloseOperation(EXIT_ON_CLOSE);
        // create a object
        solve s = new solve();

        // set layout of frame
        f.setLayout(new FlowLayout());

        // create checkbox
        c1 = new JCheckBox("checkbox 1", false);
        c2 = new JCheckBox("checkbox 2", false);

        // add ItemListener
        c1.addItemListener(s);
        c2.addItemListener(s);

        // create labels
        l = new JLabel("checkbox1 not selected");
        l1 = new JLabel("checkbox2 not selected");

        // set color of text
        l.setForeground(Color.red);
        l1.setForeground(Color.blue);

        // create a new panel
        JPanel p = new JPanel();

        // add checkbox to panel
        p.add(c1);
        p.add(c2);
        p.add(l);
        p.add(l1);

        // add panel to frame
        f.add(p);

        // set the size of frame
        f.setSize(500, 100);

        f.setVisible(true);
    }
    public void itemStateChanged(ItemEvent e)
    {
        // if the state of checkbox1 is changed
        if (e.getSource() == c1) {
            if (e.getStateChange() == 1)
                l.setText("checkbox 1 selected");
            else
                l.setText("checkbox 1 not selected");
        }

        // if the state of checkbox2 is changed
        else {
            if (e.getStateChange() == 1)
                l1.setText("checkbox 2 selected");
            else
                l1.setText("checkbox 2 not selected");
        }
    }
}
```
**Вывод:**
![[Ex3-JCheckBox.png]]
