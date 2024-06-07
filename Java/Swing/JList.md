#Java #Swing #JList

## Класс Swing

2024-06-07 11:04

**_JList_** является частью пакета Java [Swing](Swing). **_JList_** — это компонент, который отображает набор объектов и позволяет пользователю выбрать один или несколько элементов. **_JList_** наследует класс JComponent. **_JList_** — это простой способ отображения массива векторов.

### Конструктором для JList являются
 
1. **JList()**: создание рабочего списка
2. **JList(E [ ] l)**: создаёт новый список с массивом массива.
3. **JList (ListModel d)**: создает новый список, указанную с указанной моделью списка
4. **JList (Vector l)**: создаёт новый список с элементами вектора

### Обычно используют методы

| method                                                     | explanation                                                                                                                                                                                                                                                                                      |
| ---------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **int getSelectedIndex()**                                 | вернуть индекс элемента строки                                                                                                                                                                                                                                                                   |
| **Object[] getSelectedValue()**                            | вернуть выбранное значение элемента списка                                                                                                                                                                                                                                                       |
| **void setSelectedIndex(int i)**                           | устанавливает для индекса индекса числовое значение i                                                                                                                                                                                                                                            |
| **void setSelectionBackground(Color c)**                   | задает цвет фонаря списка                                                                                                                                                                                                                                                                        |
| **void setSelectionForeground(Color c)**                   | Изменяет цвет переднего плана списка                                                                                                                                                                                                                                                             |
| **void setListData(E [ ] l)**                              | Изменяет элементы списка элементов l .                                                                                                                                                                                                                                                           |
| **void setVisibleRowCount(int v)**                         | Устанавливает `visibleRowCount` свойство, которое имеет разные значения в зависимости от ориентации макета: для `VERTICAL` ориентации макета это устанавливает предпочтительное количество строк для отображения без необходимости прокрутки; для других ориентаций это влияет на перенос ячеек. |
| **void setSelectedValue(Object a, boolean s)**             | Выбирает указанный объект из списка.                                                                                                                                                                                                                                                             |
| **void setSelectedIndices(int[] i)**                       | Изменяет выделение на набор индексов, указанных в данном массиве.                                                                                                                                                                                                                                |
| **void setListData(Vector l)**                             | Создает доступ только для чтения `ListModel` из `Vector` и вызывает `setModel` с помощью этой модели.                                                                                                                                                                                            |
| **void setLayoutOrientation(int l)**                       | Определяет способ расположения ячеек списка.                                                                                                                                                                                                                                                     |
| **void setFixedCellWidth(int w)**                          | Устанавливает фиксированное значение, которое будет использоваться для ширины каждой ячейки в списке.                                                                                                                                                                                            |
| **void setFixedCellHeight(int h)**                         | Устанавливает фиксированное значение, которое будет использоваться для высоты каждой ячейки в списке.                                                                                                                                                                                            |
| **boolean isSelectedIndex(int i)**                         | возвращает true, если выбран указанный индекс, в противном случае — false.                                                                                                                                                                                                                       |
| **Point indexToLocation(int i)**                           | возвращает начало координат указанного элемента в списке координат системы.                                                                                                                                                                                                                      |
| **String getToolTipText(MouseEvent e)**                    | Возвращает текст всплывающей подсказки, который будет использоваться для данного события.                                                                                                                                                                                                        |
| **`List<E> getSelectedValuesList()`**                      | Возвращает список всех выбранных элементов в порядке возрастания на основе их индексов в списке.                                                                                                                                                                                                 |
| **int[] getSelectedIndices()**                             | Возвращает массив всех выбранных индексов в порядке возрастания.                                                                                                                                                                                                                                 |
| **int getMinSelectionIndex()**                             | Возвращает наименьший индекс выбранной ячейки или `-1` если выделенная ячейка пуста.                                                                                                                                                                                                             |
| **int getMaxSelectionIndex()**                             | Возвращает наибольший индекс выбранной ячейки или `-1` если выделенная ячейка пуста.                                                                                                                                                                                                             |
| **ListSelectionListener[]  getListSelectionListeners()**   | вернуть список прослушивателей                                                                                                                                                                                                                                                                   |
| **int getLastVisibleIndex()**                              | Возвращает самый большой индекс списка, который виден в данный момент.                                                                                                                                                                                                                           |
| **boolean getDragEnabled()**                               | Возвращает, включена ли автоматическая обработка перетаскивания.                                                                                                                                                                                                                                 |
| **void addListSelectionListener(ListSelectionListener l)** | Добавляет в список прослушиватель, который будет получать уведомления каждый раз, когда происходит изменение выбора; предпочтительный способ прослушивания изменений состояния выбора.                                                                                                           |

#### Пример 1. Программа для создания простого JList

```java
// java Program to create a simple JList
import java.awt.event.*;
import java.awt.*;
import javax.swing.*;
class solve extends JFrame {
    //frame
    static JFrame f;
    //lists
    static JList b;

    //main class
    public static void main(String[] args) {
        //create a new frame
        f = new JFrame("frame");
        f.setDefaultCloseOperation(EXIT_ON_CLOSE);
        //create a object
        solve s=new solve();
        //create a panel
        JPanel p =new JPanel();
        //create a new label
        JLabel l= new JLabel("select the day of the week");
        //String array to store weekdays
        String week[]= { "Monday","Tuesday","Wednesday",
                "Thursday","Friday","Saturday","Sunday"};

        //create list
        b= new JList(week);

        //set a selected index
        b.setSelectedIndex(2);
        //add list to panel
        p.add(b);
        f.add(p);

        //set the size of frame
        f.setSize(200,200);

        f.setVisible(true);
    }
}
```
**Вывод:**
![[Ex1-JList.png]]

#### Пример 2. Программа для создания списка и добавления в него itemListener (программа для выбора дня рождения с помощью списков).

```java
// java Program to create a list and add itemListener to it
// (program to select your birthday using lists) .
import javax.swing.event.*;
import java.awt.*;
import javax.swing.*;
class solve extends JFrame implements ListSelectionListener {
    //frame
    static JFrame f;
    //lists
    static JList b,b1,b2;
    //label
    static JLabel l1;

    //main class
    public static void main(String[] args) {
        //create a new frame
        f = new JFrame("frame");
        f.setDefaultCloseOperation(EXIT_ON_CLOSE);
        //create a object
        solve s=new solve();
        //create a panel
        JPanel p =new JPanel();
        //create a new label
        JLabel l= new JLabel("select your birthday");
        l1= new JLabel();
        //String array to store weekdays
        String month[]= { "January", "February", "March",
                "April", "May", "June", "July", "August",
                "September", "October", "November", "December"};

        //create a array for months and year
        String date[]=new String[31],year[]=new String[31];

        //add month number and year to list
        for(int i=0; i<31; i++) {
            date[i]=""+(int)(i+1);
            year[i]=""+(int)(2018-i);
        }

        //create lists
        b= new JList(date);
        b1= new JList(month);
        b2= new JList(year);

        //set a selected index
        b.setSelectedIndex(2);
        b1.setSelectedIndex(1);
        b2.setSelectedIndex(2);

        l1.setText(b.getSelectedValue()+" "+b1.getSelectedValue()
                +" "+b2.getSelectedValue());

        //add item listener
        b.addListSelectionListener(s);
        b1.addListSelectionListener(s);
        b2.addListSelectionListener(s);

        //add list to panel
        p.add(l);
        p.add(b);
        p.add(b1);
        p.add(b2);
        p.add(l1);
        f.add(p);
        //set the size of frame
        f.setSize(500,600);

        f.setVisible(true);
    }
    
    public void valueChanged(ListSelectionEvent e) {
        //set the text of the label to the selected value of lists
        l1.setText(b.getSelectedValue()+" "+b1.getSelectedValue()
                +" "+b2.getSelectedValue());
    }
}
```
**Вывод:**
![[Ex2-JList.png]]

**JList** имеет двух поставщиков данных (модели данных). Первая модель, реализующая интерфейс _ListModel_, содержит элементы списка. Вторая модель _ListSelectionModel_ реализует интерфейс ListSelectionModel и следит за выделенными элементами. По умолчанию в списке JList используется стандартная реализация модели DefaultListSelectionModel, поддерживающая все самые важные режимы выделения.

#### Пример 3. Пример использования списка JList и модели DefaultListModel

```java
// Использование списков JList и модели списка DefaultListModel
import javax.swing.*;
import java.awt.event.*;
import java.util.Vector;

public class Main extends JFrame {
    // Модель списка
    private DefaultListModel<String> dlm = new DefaultListModel<String>();

    private final String[] data1 = { "Чай" ,"Кофе"  ,"Минеральная","Морс"};
    private final String[] data2 = { "Ясли","Детсад", "Школа"     , "Институт",
            "Университет"};

    public Main() {
        super("Пример со списком JList");
        setDefaultCloseOperation(EXIT_ON_CLOSE);
        // Создание панели
        JPanel contents = new JPanel();

        // Наполнение модели данными
        for (String string : data2) {
            dlm.add(0, string);
        }
        // Создание кнопки
        JButton add = new JButton("Добавить");
        add.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                dlm.add(dlm.getSize(), "-- Новая запись --");
                validate();
            }
        });
        JList<String> list1 = new JList<String>(data1);
        JList<String> list2 = new JList<String>(dlm);

        // Вектор данных
        Vector<String> big = new Vector<String>();
        for (int i=0; i < 15; i++) {
            big.add("~ " + i + ". ~");
        }
        JList<String> bigList = new JList<String>(big);
        bigList.setPrototypeCellValue("12345");

        // Размещение компонентов в панели
        contents.add(add);
        contents.add(new JScrollPane(list1));
        contents.add(new JScrollPane(list2));
        contents.add(new JScrollPane(bigList));

        setContentPane(contents);
        // Вывод окна
        setSize(400, 200);
        setVisible(true);
    }
    public static void main(String[] args) {
        new Main();
    }
}
```
**Вывод:**
![[Ex3-JList.png]]
В примере создается небольшое окно, в котором размещаются три списка **JList**. Первый список создается на основе массива строк. Второй список использует в качестве модели данных DefaultListModel типа [String](String). Третий список формируется динамически на основе объекта [Vector](Vector). Следует отметить, что списки вставляются в панель прокрутки [JScrollPane](JScrollpane). Компоненты Swing по умолчанию не предоставляют возможностей прокрутки содержимого и их необходимо помещать в панель прокрутки. Списки JList не являются исключением.

В примере используется полезный метод setPrototypeCellValue() для определения ширины визуального списка. Элементы списка, как правило, имеют разные размеры, поэтому перед их выводом на экран компонент **JList** проверяет их размеры и выбирает ширину самого большого элемента в списке. Метод setPrototypeCellValue() позволяет определить ширину JList по длине указанной строки.

### Модели списка

С данными списков, как и с данными других компонентов [Swing](Swing), лучше всего работать с использованием моделей. Списки включают модель данных и модель выделения элементов. Модели позволяют отделить обработку данных от их представления на экране.

#### Модель данных AbstractListModel

Свойства моделей данных списков **JList** описаны в интерфейсе ListModel и включают четыре метода. Два метода служат для присоединения и удаления слушателей событий, происходящих при обновлении данных списка; один метод возвращает элемент, находящийся в некоторой позиции списка; последний метод позволяет узнать количество элементов модели.

Для работы со списками в библиотеке [Swing](Swing) имеется стандартная модель данных **DefaultListModel**. В рассмотренном выше примере представлен код добавления строк в модель и создание списка на основе данных модели. Модель позволяет добавлять и удалять данные, вставлять их в любые позиции, производить перебор элементов. Модели и виды (View) компонентов [Swing](Swing) сами заботятся о том, чтобы всё вовремя и правильно появлялось на экране. Для демонстрации динамического поведения данных модели в примере размещена кнопка [JButton](JButton) "Добавить". В методе обработки нажатия кнопки _actionPerformed_ в модель данных добавляется строка, после чего вызывается метод validate(), чтобы привести интерфейс в соответствие с новыми данными списка.

Стандартная модель DefaultListModel очень удобна и позволяет гибко хранить и изменять любые данные. Однако иногда лучше определить собственную модель данных; особенно там, где данные хранятся в нестандартных структурах или их необходимо получить из сетевого соединения или базы данных. Полностью реализовывать модель «с нуля» не нужно. Создатели [Swing](Swing) уже позаботились о поддержке любыми моделями механизма оповещения (встроили списки слушателей и обеспечили рассылку событий) в абстрактном классе AbstractListModel. Нужно лишь унаследовать от этого класса и получить данные списка.

#### Пример использования AbstractListModel для создания модели данных

```java
public class DatabaseListModel extends AbstractListModel<String>  
{  
    // Коллекция для хранения данных  
    private ArrayList<String> data = new ArrayList<String>();  
    // Загрузка данных из БД  
    public void setDataSource(ResultSet rs, String column)  
    {  
        try {  
            // Очистка коллекции  
            data.clear();  
            // Перебор в цикле данных  
            while ( rs.next() ) {  
                synchronized ( data ) {  
                    // Добавление данных в коллекцию  
                    data.add(rs.getString(column));  
                }  
                // Оповещение видов о добавлении, если они есть  
                fireIntervalAdded(this, 0, data.size());  
            }  
            rs.close();  
            // Оповещение видов об изменении  
            fireContentsChanged(this, 0, data.size());  
        } catch (Exception ex) {  
            throw new RuntimeException(ex);  
        }  
    }  
    // Функция размера массива данных в списке  
    public int getSize() {  
        synchronized ( data ) {  
            return data.size();  
        }  
    }  
    // Функция извлечения элемента  
    public String getElementAt(int idx) {  
        synchronized ( data ) {  
            return data.get(idx);  
        }  
    }  
}
```

Модель _DatabaseListModel_ наследуется от абстрактного класса моделей списков AbstractListModel и хранит данные в динамическом массиве [ArrayList](Class-ArrayList). Основной код определен в методе setDataSource(), который позволяет модели получать данные из соединения с базой данных. Для правильной работы этому методу необходимо передать результат запроса к базе данных ResultSet, а также название столбца column, данные которого будут использованы для заполнения списка.

При получении очередной записи из базы данных модель данных оповещает об этом своих слушателей. Для оповещения присоединенных к модели слушателей, а это чаще всего виды, отображающие ее данные, используются возможности базового класса AbstractListModel: вызываются методы fireXXX(), каждый из которых сообщает о некотором событии. Для ускорения работы с коллекциями в классе [ArrayList](Class-ArrayList) отключена синхронизация. Поэтому методы коллекции add(), size(), get() синхронизируются "в ручную".

Можно было бы сначала загрузить из БД данные, а затем поместить их в стандартную модель DefaultListModel. Но в созданной в примере модели демонстрируется способность оповещать слушателей при изменении данных.

## Модель выделения DefaultListSelectionModel

Список **JList** включает используемую по умолчанию модель выделения **DefaultListSelectionModel**. Данная модель поддерживает три режима выделения элементов списка и предоставляет полную информацию о текущем выделении. В следующей таблице представлены режимы выделения элементов списка.

| Режим                       | Описание                                                      |
| --------------------------- | ------------------------------------------------------------- |
| SINGLE_SELECTION            | Выделение одного элемента списка.                             |
| SINGLE_INTERVAL_SELECTION   | Выделение нескольких смежных элементов списка.                |
| MULTIPLE_INTERVAL_SELECTION | Выделение нескольких элементов списка в произвольном порядке. |

Наиибольшее распространение получили следующие методы модели выделения элементов списка :
- setSelectedIndex (int idx) - выделение элемента списка;
- setSelectionInterval (int anchor, int lead) - выделение нескольких смежных элементов;
- addSelectionInterval (int anchor, int lead) - добавление к уже имеющемуся выделению еще одного интервала выделения;
- setSelectedIndices (int[] rows) - выделение нескольких элементов списка в произвольном порядке.

Методы setSelectionInterval() и addSelectionInterval() в качестве параметров используют позиции первого и последнего выделяемых элементов. Если они совпадают, то выделяется один элемент. Необязательно, чтобы первое число было бы больше второго. В модели выделения хранятся начало интервала выделения anchor и конец интервала выделения lead.

#### Пример 4.  Различные режимы выделения элементов списка

```java
// Пример использования различных режимов выделения
import javax.swing.*;

public class Main extends JFrame
{
    private String[] data = { "Футбол", "Хоккей", "Баскетбол",
            "Биатлон", "Лыжи"};
    public Main()
    {
        super("Пример модели выделения");
        setDefaultCloseOperation(EXIT_ON_CLOSE);
        // Модель данных
        DefaultListModel<String> dlm = new DefaultListModel<String>();
        for (String string : data)
            dlm.addElement(string);
        // Cписки для разных типов выделения
        JList<String> lst_single   = new JList<String>(dlm);
        JList<String> lst_interval = new JList<String>(dlm);
        JList<String> multiple     = new JList<String>(dlm);
        // Определение максимальной ширины списка
        lst_single.setPrototypeCellValue("Установленный размер");
        // Модели выделения
        lst_single  .setSelectionMode(
                ListSelectionModel.SINGLE_SELECTION);
        lst_interval.setSelectionMode(
                ListSelectionModel.SINGLE_INTERVAL_SELECTION  );
        multiple    .setSelectionMode(
                ListSelectionModel.MULTIPLE_INTERVAL_SELECTION);
        // Модель выделения можно установить и как в следующей
        // закомментированной строке
        // multiple .getSelectionMode().setSelectionMode(
        //                ListSelectionModel.MULTIPLE_INTERVAL_SELECTION);
        // Выделение строки списков
        lst_single  .setSelectedIndex(2);
        lst_interval.setSelectionInterval(1, 1);
        lst_interval.addSelectionInterval(2, 3);
        // Список выделяемых строк
        int[] rows = {0, 2, 4};
        multiple.setSelectedIndices(rows);
        // Добавляем компоненты в интерфейс
        JPanel contents = new JPanel();
        contents.add(new JScrollPane(lst_single  ));
        contents.add(new JScrollPane(lst_interval));
        contents.add(new JScrollPane(multiple    ));
        // Вывод окна
        setContentPane(contents);
        setSize(360, 200);
        setVisible(true);
    }
    public static void main(String[] args) {
        new Main();
    }
}
```
**Вывод:**
![[Ex4-JList.png]]
В примере заполняется стандартная модель **DefaultListModel** данными из массива и на её основе создается три списка. Для списков устанавливаются различные режимы выделения элементов. Режим выделения можно установить двумя способами: вызовом метода setSelectionMode() или вызовом метода с точно таким же названием для самой модели выделения.

дин элемент списка может быть выбран щелчком мыши или нажатием клавиш управления курсором. Интервалы и дополнительные элементы могут быть выбраны с помощью вспомогательных клавиш Shift и Ctrl.

В следующей таблице представлены методы получения информации о выделенных элементах.

|Метод|Назначение|
|---|---|
|isSelectedlndex()|Функция проверки наличия выделенных элементов списка.|
|getSelectedlndex(),  <br>getSelectedIndices()|Функции получения позиции первого выделенного элемента (если выделений нет, то возвращается -1) или массив позиций выделенных элементов.|
|getSelectedValue(),  <br>getSelectedValues()|Получение выбранного элемент списка или массива элементов.|

Как правило, возможностей стандартной модели выделения DefaultListSelectionModel вполне достаточно для большей части приложений. Но если возникнет потребность в разработке собственной модели выделения, то можно использовать следующий шаблон для создания собственной модели.
```java
class CustomListSelectionModel extends DefaultListSelectionModel
{
    // Добавление интервала выделения
    public void addSelectionInterval(int anchor, int lead)
    {
        super.addSelectionInterval(anchor, lead);
        ...
    }
    // Определение интервала выделения
	public void setSelectionInterval(int anchor, int lead)
    {
        super.setSelectionInterval(anchor, lead);
        ...
    }
}
```
### Внешний вид списка

Внешний вид списка **JList**, как и у всех унаследованных от JComponent компонентов [Swing](Swing), можно настраивать - менять цвет фона, цвет шрифта и сам шрифт, а также цвет выделенного элемента.

В таблице представлены свойства и методы определения интерфейса списка.

|Свойство (и методы get/set)|Описание|
|---|---|
|background, foreground, font|Определение фона, цвета символов и шрифт соответственно.|
|selectedBackground|Определение цвета фона выделенных элементов.|
|selectedForeground|Определение цвета символов выделенных элементов.|

С помощью этих свойств можно установить определенный стиль представления списков в интерфейсе приложения.

### Слушатели событий JList

Список **JList** включает стандартные события от мыши и клавиатуры базового компонента JComponent. Дополнительные события происходят в его моделях. События в модели выделения элемента списка ListSelectionModel позволяют узнать об изменениях в выделении элементов списка.

#### Пример 5. Использование слушателя ListSelectionListener

```java
// Пример тестирования слушателя ListSelectionListener
import java.awt.event.MouseAdapter;
import java.awt.event.MouseEvent;
import javax.swing.*;
import javax.swing.event.ListSelectionEvent;
import javax.swing.event.ListSelectionListener;

public class Main extends JFrame {
    // Данные списка
    private final String[]   dataList = { "Бакалея", "Напитки", "Хлеб"};
    private final String[][] dataText = {{"Сахар", "Мука", "Соль"},
            {"Чай"  , "Кофе", "Морс"},
            {"Батон", "Пшеничный",
                    "Бородинский"}};
    private JTextArea content;

    public Main() {
        super("Слушатель событий списка");
        setDefaultCloseOperation(EXIT_ON_CLOSE);
        // Создание списка
        JPanel contents = new JPanel();
        final JList<String> list = new JList<String>(dataList);
        list.setSelectionMode(ListSelectionModel.SINGLE_SELECTION);
        list.setPrototypeCellValue("Увеличенный");
        // Создание текстового поля
        content = new JTextArea(5, 20);
        // Подключения слушателя
        list.addListSelectionListener(new listSelectionListener());
        // Подключение слушателя мыши
        list.addMouseListener(new MouseAdapter() {
            public void mouseClicked(MouseEvent e) {
                if ( e.getClickCount() == 2 ) {
                    // Получение элемента
                    int selected = list.locationToIndex(e.getPoint());
                    int i = 0;
                    String txt = "";
                    while (i < dataText[selected].length)
                        txt += dataText[selected][i++] + "\n";
                    content.setText (txt);
                }
            }
        });

        // Размещение компонентов в интерфейсе
        contents.add(new JLabel("Список разделов"));
        contents.add(new JScrollPane(list));
        contents.add(new JLabel("Содержимое разделов"));
        contents.add(new JScrollPane(content));
        // Вывод окна
        setContentPane(contents);
        setSize(600, 200);
        setVisible(true);
    }
    /*
     * Слушатель списка
     */
    class listSelectionListener implements ListSelectionListener {
        public void valueChanged(ListSelectionEvent e) {
            // Выделенная строка
            int selected = ((JList<?>)e.getSource()).
                    getSelectedIndex();
            System.out.println ("Выделенная строка : " +
                    String.valueOf(selected));
        }
    }
    public static void main(String[] args) {
        new Main();
    }
}
```
В примере в интерфейсе окна размещаются список на основе небольшого массива строк и текстовое поле JTextArea для вывода дополнительной информации. К списку подключается слушатель события _listSelectionListener_, наследуемый свойства модели выделения. Следует отметить, что слушатель подключается к списку **JList**, хотя точно такой же метод есть и в модели выделения ListSelectionModel. Отличия связаны с источником события, который возвращает слушателю источник getSource(). В слушателе события определяется выделенная строка.

Интерфейс программы представлен на следующем скриншоте.
![[Ex5-JList.png]]
Список **JList** не поддерживает двойные щелчки мыши и не предоставляет средства по их определению. Но добавить такой "сервис" не представляет никаких сложностей. В примере к списку JList дополнительно подключен слушатель обработки события клавиши мыши. При двойном нажатии клавиши мыши на списке определяется выделяемая строка и в текстовый компонент загружаются соответствующие данные. Для получения выделенного элемента используется метод locationToIndex(), который позволяет определить принадлежность точки экрана к элементу списка. Метод indexToLocation() решает обратную задачу - определяет место экрана где находится элемент списка.