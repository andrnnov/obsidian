#Java #Swing #JComboBox

## Класс JComboBox

2024-06-07 12:29

JComboBox является частью пакета Java [Swing](Swing). Для выбора одного элемента из нескольких доступных вариантов можно использовать раскрывающиеся списки **JComboBox**, который в нормальном состоянии отображает только один выбранный элемент. Возможные альтернативы появляются в специальном всплывающем окне при открытии списка. Раскрывающиеся списки допускают редактирование текущего элемента. Пользователь может не только выбрать определенный элемент из списка, но и ввести свое собственное значение. Список **JComboBox** обладает возможностью поиска элементов с клавиатуры, что значительно упрощает работу с большими наборами.

Раскрывающийся список **JComboBox** использует только одну модель, предоставляющую информацию об элементах списка. Свойства модели JComboBox определены интерфейсом **ComboBoxModel**, унаследованным от простой модели списка ListModel. Интерфейс ComboBoxModel включает дополнительно два новых метода : getSelectedItem() — для получения выбранного элемента и setSelectedItem() — для смены выбранного элемента. Помимо интерфейса модели ComboBoxModel можно использовать унаследованный от нее интерфейс MutableComboBoxModel, поддерживающий вставку и удаление произвольных элементов списка.

### Конструкторы JComboBox

1. **JComboBox()**: Создает `JComboBox` с моделью данных по умолчанию.
2. **JComboBox(ComboBoxModel M)**: Создаём новый JComboBox с элементами из указанной ComboBoxModel.
3. **JComboBox(E [] l)**: Создаёт новый JComboBox с элементами из указанного массива.
4. **JComboBox (Vector v)**: Создаёт новый JComboBox с элементами из указанного вектора.

### Обычно используют методы
 
1. **void addItem(Item E)**: добавить элемент в JComboBox
2. **void addItemListener(ItemListener l)**: добавление ItemListener в JComboBox
3. **E getItemAt(int index)**: Возвращает элемент списка с указанным индексом.
4. **int getItemCount()**: возвращает количество элементов из списка
5. **Object getSelectedItem()**: возврат выбранного элемента
6. **void removeItemAt(int i)**: сохранить элемент с индексом i
7. **void setEditable(boolean b)**: логическое значение b определено, доступно ли поле со списком для редактирования или нет. Если передано значение true, то поле со списком доступно для редактирования или наоборот.
8. **void setSelectedIndex (int i)**: выбирает элемент JComboBox с индексом i.
9. **void showPopup()**: Вызывает отображение всплывающего окна в поле со списком.
10. **void setUI(ComboBoxUI ui)**: задает объект L & F, который отображает этот компонент.
11. **void setSelectedItem(Object a)**: соответствует выбранному элементу в области отображения поля со списком значения аргумента.
12. **void setSelectedIndex (int anIndex)**: выбирает элемент по индексу anIndex.
13. **void setPopupVisible(boolean v)**: Задает видимость всплывающего окна.
14. **void setModel (ComboBoxModel а)**: задает данные модели, которые JComboBox использует для получения элементов списка.
15. **void setMaximumRowCount(int count)**: устанавливает максимальное количество строк, отображаемых JComboBox.
16. **void setEnabled(boolean b)**: включает поле со списком, чтобы можно было выбирать элементы.
17. **void removeItem(Object anObject)**: удаляет элемент из списка элементов.
18. **void removeAllItems()** : удаляет все элементы из списка элементов.
19. **void removeActionListener(ActionListener l)** : удаляет ActionListener.
20. **boolean isPopupVisible()** : определяет видимость всплывающего окна.
21. **void addPopupMenuListener(PopupMenuListener l)** : добавляет прослушиватель PopupMenu, который будет прослушивать сообщения уведомлений из всплывающей части поля со списком.
22. **getActionCommand()** : возвращает команду действия, включенную в событие, отправляемое прослушивателям действий.
23. **ComboBoxEditor getEditor()** : возвращает редактор, используемый для рисования и редактирования выбранного элемента в поле JComboBox.
24. **int getItemCount()** : возвращает количество элементов в списке.
25. **ItemListener[] getItemListeners()** : возвращает массив всех ItemListeners, добавленных в этот JComboBox с помощью addItemListener().
26. **protected JComboBox.KeySelectionManager createDefaultKeySelectionManager()**: возвращает экземпляр менеджера выбора ключей по умолчанию.
27. **fireItemStateChanged(ItemEvent e)** : уведомляет всех прослушивателей, которые зарегистрировали интерес к уведомлению об этом типе событий.
28. **protected void firePopupMenuCanceled()** : уведомляет PopupMenuListeners о том, что всплывающая часть поля со списком была отменена.
29. **void firePopupMenuWillBecomeInvisible()** : уведомляет PopupMenuListeners о том, что всплывающая часть поля со списком стала невидимой.
30. **void firePopupMenuWillBecomeVisible()** : уведомляет PopupMenuListeners о том, что всплывающая часть поля со списком станет видимой.
31. **void setEditor(ComboBoxEditor a)**: устанавливает редактор, используемый для рисования и редактирования выбранного элемента в поле JComboBox.
32. **void setActionCommand(String aCommand)** : устанавливает команду действия, которая должна быть включена в событие, отправляемое в actionListeners.
33. **ComboBoxUI getUI()** : возвращает внешний вид объекта, который отображает этот компонент.
34. **protected String paramString()** : возвращает строковое представление этого JComboBox.
35. **String getUIClassID()** : возвращает имя класса внешнего вида, который отображает этот компонент.
36. **AccessibleContext getAccessibleContext()** : получает AccessibleContext, связанный с этим JComboBox.

#### Пример 1. Программа для создания простого JComboBox и добавления в него элементов.

```java
// Java Program to create a simple JComboBox
// and add elements to it
import java.awt.event.*;
import java.awt.*;
import javax.swing.*;
class solve extends JFrame implements ItemListener {
    // frame
    static JFrame f;
    // label
    static JLabel l, l1;
    // combobox
    static JComboBox c1;

    // main class
    public static void main(String[] args) {
        // create a new frame
        f = new JFrame("frame");
        f.setDefaultCloseOperation(EXIT_ON_CLOSE);
        // create a object
        solve s = new solve();
        // set layout of frame
        f.setLayout(new FlowLayout());
        // array of string containing cities
        String s1[] = { "Jalpaiguri", "Mumbai", "Noida", "Kolkata", "New Delhi" };
        // create checkbox
        c1 = new JComboBox(s1);
        // add ItemListener
        c1.addItemListener(s);
        // create labels
        l = new JLabel("select your city ");
        l1 = new JLabel("Jalpaiguri selected");
        // set color of text
        l.setForeground(Color.red);
        l1.setForeground(Color.blue);
        // create a new panel
        JPanel p = new JPanel();
        p.add(l);
        // add combobox to panel
        p.add(c1);
        p.add(l1);
        // add panel to frame
        f.add(p);
        // set the size of frame
        f.setSize(400, 100);
        f.setVisible(true);
    }

    public void itemStateChanged(ItemEvent e) {
        // if the state combobox is changed
        if (e.getSource() == c1) {
            l1.setText(c1.getSelectedItem() + " selected");
        }
    }
}
```
**Вывод:**
![[Ex1-JComboBox.png]]

#### Пример 2. Программа для создания двух флажков: один редактируемый, другой только для чтения

```java
// Java Program to create two  checkbox
// one editable and other read only
import java.awt.event.*;
import java.awt.*;
import javax.swing.*;
class solve extends JFrame implements ItemListener {
    // frame
    static JFrame f;
    // label
    static JLabel l, l1, l3, l4;
    // combobox
    static JComboBox c1, c2;

    // main class
    public static void main(String[] args) {
        // create a new frame
        f = new JFrame("frame");
        f.setDefaultCloseOperation(EXIT_ON_CLOSE);
        // create a object
        solve s = new solve();

        // array of string containing cities
        String s1[] = { "Jalpaiguri", "Mumbai", "Noida", "Kolkata", "New Delhi" };
        String s2[] = { "male", "female", "others" };

        // create checkbox
        c1 = new JComboBox(s1);
        c2 = new JComboBox(s2);

        // set Kolkata and male as selected items
        // using setSelectedIndex
        c1.setSelectedIndex(3);
        c2.setSelectedIndex(0);

        // add ItemListener
        c1.addItemListener(s);
        c2.addItemListener(s);

        // set the checkbox as editable
        c1.setEditable(true);

        // create labels
        l = new JLabel("select your city ");
        l1 = new JLabel("Jalpaiguri selected");
        l3 = new JLabel("select your gender ");
        l4 = new JLabel("Male selected");

        // set color of text
        l.setForeground(Color.red);
        l1.setForeground(Color.blue);
        l3.setForeground(Color.red);
        l4.setForeground(Color.blue);

        // create a new panel
        JPanel p = new JPanel();
        p.add(l);
        // add combobox to panel
        p.add(c1);
        p.add(l1);
        p.add(l3);
        // add combobox to panel
        p.add(c2);
        p.add(l4);
        // set a layout for panel
        p.setLayout(new FlowLayout());
        // add panel to frame
        f.add(p);
        // set the size of frame
        f.setSize(400, 120);
        f.setVisible(true);
    }
    public void itemStateChanged(ItemEvent e) {
        // if the state combobox 1is changed
        if (e.getSource() == c1) {
            l1.setText(c1.getSelectedItem() + " selected");
        }
        // if state of combobox 2 is changed
        else
            l4.setText(c2.getSelectedItem() + " selected");
    }
}
```
**Вывод:**
![[Ex2-JComboBox.png]]

#### Пример 3. Программа для создания флажка и добавления или удаления из него элементов

```java
// Java  Program to create a checkbox
// and add or remove items from it
import java.awt.event.*;
import java.awt.*;
import javax.swing.*;
class solve11 extends JFrame implements ItemListener, ActionListener {
    // frame
    static JFrame f;
    // label
    static JLabel l, l1;
    // combobox
    static JComboBox c1;
    // textfield to add and delete items
    static JTextField tf;

    // main class
    public static void main(String[] args) {
        // create a new frame
        f = new JFrame("frame");
        f.setDefaultCloseOperation(EXIT_ON_CLOSE);
        // create a object
        solve11 s = new solve11();
        // set layout of frame
        f.setLayout(new FlowLayout());
        // array of string containing cities
        String s1[] = { "Jalpaiguri", "Mumbai", "Noida", "Kolkata", "New Delhi" };
        // create checkbox
        c1 = new JComboBox(s1);
        // create textfield
        tf = new JTextField(16);
        // create add and remove buttons
        JButton b = new JButton("ADD");
        JButton b1 = new JButton("REMOVE");
        // add action listener
        b.addActionListener(s);
        b1.addActionListener(s);
        // add ItemListener
        c1.addItemListener(s);
        // create labels
        l = new JLabel("select your city ");
        l1 = new JLabel("Jalpaiguri selected");
        // set color of text
        l.setForeground(Color.red);
        l1.setForeground(Color.blue);
        // create a new panel
        JPanel p = new JPanel();
        p.add(l);
        // add combobox to panel
        p.add(c1);
        p.add(l1);
        p.add(tf);
        p.add(b);
        p.add(b1);
        f.setLayout(new FlowLayout());
        // add panel to frame
        f.add(p);
        // set the size of frame
        f.setSize(700, 100);
        f.setVisible(true);
    }
    // if button is pressed
    public void actionPerformed(ActionEvent e) {
        String s = e.getActionCommand();
        if (s.equals("ADD")) {
            c1.addItem(tf.getText());
        }
        else {
            c1.removeItem(tf.getText());
        }
    }

    public void itemStateChanged(ItemEvent e) {
        // if the state combobox is changed
        if (e.getSource() == c1) {
            l1.setText(c1.getSelectedItem() + " selected");
        }
    }
}
```
**Вывод:**
![[Ex3-JComboBox.png]]

#### Пример 4. Использование JComboBox

```java
{
    private static final long serialVersionUID = 1L;
    // Массив элементов списка
    public String[] elements = new String[] {"Офис", "Склад", "Гараж",
            "Производство", "Столовая"};

    private JComboBox<String> cbFirst;
    private DefaultComboBoxModel<String> cbModel;

    public Main() {
        super("Пример JComboBox");
        setDefaultCloseOperation(EXIT_ON_CLOSE);

        // Модель данных списка
        cbModel = new DefaultComboBoxModel<String>();
        for (int i = 0; i < elements.length; i++)
            cbModel.addElement((String)elements[i]);
        // Данные для 2-го списка
        Vector<String> data = new Vector<String>();
        for (int i = 0; i < 10; i++)
            data.add(String.format("#%d элемент", i));
        // 1-й раскрывающийся список
        cbFirst = new JComboBox<String>(cbModel);
        // Меняем элемент Гараж на Автопарк
        cbModel.setSelectedItem("Гараж");
        int idx = cbModel.getIndexOf(cbModel.getSelectedItem());
        cbModel.removeElementAt(idx);
        cbModel.insertElementAt("Автопарк", idx);
        cbModel.setSelectedItem("Автопарк");
        // Определяем размер списка
        cbFirst.setPrototypeDisplayValue("Максимальный размер");
        // 2-й раскрывающийся список
        JComboBox<String> cbSecond = new JComboBox<String>(data);
        /*
         *  Определение свойств списка - редактируемый, количество
         *  элементов в раскрывающемся окне
         */
        cbSecond.setEditable(true);
        cbSecond.setMaximumRowCount(5);
        // Кнопка добавления элемента в модель данных
        JButton btnAdd = new JButton("Добавить");
        btnAdd.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                // Выбираем позицию предпоследнего элемента
                int pos = cbModel.getSize() - 1;
                cbModel.insertElementAt("~ Добавленная строка ~", pos);
            }
        });

        // Размещение компонентов в интерфейсе и вывод окна
        JPanel contents = new JPanel();
        contents.add  (cbSecond);
        contents.add  (cbFirst );
        contents.add  (btnAdd  );
        setContentPane(contents);
        setSize(450, 180);
        setVisible(true);
    }
    public static void main(String[] args) {
        new Main();
    }
}
```
**Вывод:**
![[Ex4-JComboBox.png]]
В примере 2-ой элемент списка "Гараж" меяется на "Автопарк". Для удобства работы со списком было установлено количество видимых на экране элементов с использованием метода setMaximumRowCount(int).

Данные следует добавлять в модель до присоединения к виду с использованием метода addElement. После присоединения модели к списку она начинает оповещать вид о каждом изменении в своих данных, что может замедлить работу приложения.
