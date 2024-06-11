#Java #Swing #JTable

## Класс JTable

2024-06-10 09:43

Таблица **_JTable_** является частью пакета Java [Swing](Swing) и позволяет отображать двухмерную информацию в виде строк и столбцов, настраивать и сортировать данные, выводить их в любом подходящем виде, управлять заголовками таблицы и ее выделенными элементами.

**_JTable_** использует три модели, поставляющие ей данные и сохраняющие изменения при изменении этих данных. Первая и самая важная модель реализует интерфейс _TableModel_ и хранит данные ячеек таблицы и дополнительную служебную информацию об этих ячейках. Вторая модель реализует интерфейс _TableColumnModel_ и управляет столбцами таблицы. _TableColumnModel_ позволяет добавлять, перемещать и находить столбцы, узнавать об изменениях в их расположении, с ее помощью можно изменить расстояние между столбцами и находящимися в них ячейками. Третья модель таблицы _SelectionModel_ используется для выделения списка. Она управляет выделением строк таблицы и не затрагивает столбцы. Модель _TableColumnModel_ имеет собственную модель выделения списка _ListSelectionModel_. Так что можно формально говорить о четырех моделях таблицы **_JTable_**. Просто одна из этих моделей вызывается неявно, через другую модель. Помимо моделей таблица **_JTable_** предоставляет еще несколько удобных механизмов выделения строк, столбцов и ячеек.

В модели данных таблицы можно хранить не только простые элементы, но и объекты. Для отображения в ячейке таблицы одного из атрибутов объекта используются специальные отображающие объекты, наследующие свойства _DefaultTableCellRenderer_. Отображающие объекты позволяет настраивать стиль и формат представления значения ячейки.

Можно реализовать собственные модели таблицы, используя для каждой из них соответствующий абстрактный класс, начинающийся со слова Abstract, в котором реализованы поддержка слушателей и рассылка событий. Для каждой из моделей **_JTable_** имеется стандартная реализация, наименование класса которого начинается со слова Default.

При работе с таблицами необязательно использовать модели. **_JTable_** включает конструкторы, в которые можно передать массивы или векторы с информацией о ячейках таблицы и при необходимости о названиях ее столбцов. Для простых программ и незатейливых таблиц такой подход удобнее. Значение любой ячейки таблицы в этом случае можно получить с использованием метода getValueAt(), а изменить значение ячейки можно методом setValueAt().

Таблица **_JTable_** реализует интерфейс _Scrollable_ и ее можно добавлять в панель прокрутки [JScrollPane](JScrollPane). При прокрутке полностью появляются следующий столбец или следующая строка таблицы. Заголовок таблицы, реализованный классом _JTableHeader_, будет виден только при помещении таблицы в панель прокрутки, поскольку таблица размещает компонент _JTableHeader_ в виде заголовка панели прокрутки.

### Конструкторы в JTable

| Конструктор                                                       | Описание                                                                                                                                                                                   |
| ----------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| JTable()                                                          | Конструктор таблицы с инициализацией объекта моделями по умолчанию : моделью данных, моделью колонок, моделью выделения.                                                                   |
| JTable(int numRows, int numColumns)                               | Конструктор таблицы с определением количества колонок и строк и с использованием модели по умолчанию DefaultTableModel. Колонки будут иметь наименования "A", "B", "C" и т.д.              |
| JTable(Object[][] rowData, Object[] columnNames)                  | Конструктор определяет количество и наименования колонок согласно columnNames. Количество строк определены размером массива данных rowData, который используется и для заполнения таблицы. |
| JTable(TableModel dm)                                             | Конструктор таблицы с инициализацией данных согласно модели dm; модель колонок и модель выделения по умолчанию.                                                                            |
| JTable(TableModel dm, TableColumnModel cm)                        | Конструктор таблицы с инициализацией данных согласно модели dm, колонок согласно модели cm и модели выделения по умолчанию.                                                                |
| JTable(TableModel dm, TableColumnModel cm, ListSelectionModel sm) | Конструктор таблицы с инициализацией данных согласно модели dm, колонок согласно модели cm и модели выделения sm.                                                                          |
| JTable(Vector rowData, Vector columnNames)                        | Конструктор таблицы с инициализацией колонок согласно columnNames. Количество строк определены параметром rowData, имеющего тип [Vector](Vector)                                           |

#### Пример 1. Простые конструкторы JTable

В следующем примере создаются три таблицы. Первая таблица _table1_ создается конструктором, принимающим два массива с данными. Первый массив хранит строки таблицы. Второй массив определяет названия столбцов таблицы. Вторая таблица _table2_ создается с помощью конструктора, которому требуется указать лишь количество строк и столбцов в таблице. Все ячейки будут пустыми, а в качестве названий столбцов использованы латинские буквы, как в электронных таблицах Excel.

Третий конструктор получает в качестве параметров данные типа [Vector](Vector) из пакета java.util. Первый вектор в качестве данных содержит такие же векторы, в которых, хранятся данные строк таблицы. Второй вектор хранит названия столбцов таблицы. В примере данные векторов заполняются в цикле.

```java
// Пример работы с простыми таблицами JTable
import javax.swing.*;
import java.awt.*;
import java.util.*;

public class Main extends JFrame {
    // Данные для таблиц
    private Object[][] array = new String[][] {{ "Сахар" , "кг", "1.5" },
            { "Мука"  , "кг", "4.0" },
            { "Молоко", "л" , "2.2" }};
    // Заголовки столбцов
    private Object[] columnsHeader = new String[] {"Наименование", "Ед.измерения",
            "Количество"};
    public Main() {
        super("Простой пример с JTable");
        setDefaultCloseOperation(EXIT_ON_CLOSE);
        // Простая таблица
        JTable table1 = new JTable(array, columnsHeader);
        // Таблица с настройками
        JTable table2 = new JTable(3, 5);
        // Настройка таблицы
        table2.setRowHeight(30);
        table2.setRowHeight(1, 20);
        table2.setIntercellSpacing(new Dimension(10, 10));
        table2.setGridColor(Color.blue);
        table2.setShowVerticalLines(false);

        // Данные для таблицы на основе Vector
        Vector<Vector<String>> data = new Vector<Vector<String>>();
        // Вектор с заголовками столбцов
        Vector<String> header = new Vector<String>();
        // Формирование в цикле массива данных
        for (int j = 0; j < array.length; j++) {
            header.add((String)columnsHeader[j]);
            Vector<String> row = new Vector<String>();
            for (int i = 0; i < array[j].length; i++) {
                row.add((String)array[j][i]);
            }
            data.add(row);
        }
        // Таблица на основе вектора
        JTable table3 = new JTable(data, header);
        // Размещение таблиц в панели с блочным расположением
        Box contents = new Box(BoxLayout.Y_AXIS);
        contents.add(new JScrollPane(table1));
        contents.add(new JScrollPane(table2));

        // Настройка таблицы table3 - цвет фона, цвет выделения
        table3.setForeground(Color.red);
        table3.setSelectionForeground(Color.yellow);
        table3.setSelectionBackground(Color.blue);
        // Скрытие сетки таблицы
        table3.setShowGrid(false);
        // contents.add(new JScrollPane(table3));
        contents.add(table3);
        // Вывод окна на экран
        setContentPane(contents);
        setSize(500, 400);
        setVisible(true);
    }
    public static void main(String[] args) {
        new Main();
    }
}
```
Созданные в примере три таблицы добавляются в панель _Box_ с вертикальным блочным расположением. Первые две таблицы помещаются в панели прокрутки [JScrollPane](JScrollPane).

Таблицы без панелей прокрутки занимают ровно столько места, сколько им требуется для отображения своих данных. Третья таблица добавлена в панель напрямую, поэтому в этой таблице заголовок не отображается.

**Вывод:**
![[Ex1-JTable.png]]

С помощью полезных свойств **_JTable_** можно раскрасить таблицу, определить цвета для текста и выделения, размеры сетки таблицы, задать расстояния между ячейками. Настройка таблицы _table2_ демонстрирует свойства _JTable_, позволяющие управлять расстоянием между ячейками, высотой строк таблицы, а также цветом и стилем сетки таблицы. Настройка таблицы _table3_ показывает, как можно изменить цвета, используемые для текста и выделенных элементов, а также как отключить прорисовку сетки таблицы.

#### Свойства определения внешнего вида таблицы JTable

| Свойства                                      | Описание                                                                                                                                                                                                                                             |
| --------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| selectionBackground,  <br>selectionForeground | Управление выделением цвета прорисовки фона выделенной ячейки и текста выделенной ячейки. Вместе со стандартными свойствами background и foreground, отвечающими за фон и цвет компонента [Swing](Swing), позволяют настроить цветовую гамму таблицы |
| rowHeight                                     | Определение высоты всех строк таблицы. С помощью перегруженного метода set можно отдельно задать высоту некоторой строки таблицы. Данный метод используется в примере.                                                                               |
| intercellSpacing                              | Управление расстоянием между ячейками как по оси X, так и по оси Y. В примере расстояние задается в виде объекта [[Dimension\|Dimension]].                                                                                                           |
| showVerticalLines,  <br>showHorizontalLines,  | Управление прорисовкой вертикальных и горизонтальных линий сетки таблицы.                                                                                                                                                                            |
| showGrid                                      | Управление прорисовкой (показать или скрыть) сетки таблицы.                                                                                                                                                                                          |
| gridColor                                     | Определение цвета сетки таблицы **_JTable_**.                                                                                                                                                                                                        |

### Модель данных TableModel

Модель таблицы **TableModel** позволяет подробно описать каждую ячейку таблицы **_JTable_**. Определенные в модели методы позволяют получить значение произвольной ячейки и изменить его, узнать о возможности редактирования ячейки, получить информацию о столбцах (количество, наименование, тип) и строках.

В предыдущем примере были созданы простые таблицы **JTable**, которая неявно создавала стандартную модель _DefaultTableModel_ и наполняла ее данными, переданными в конструктор. Модель _DefaultTableModel_ хранит переданные ей данные в двух векторах [Vector](Vector): в одном из векторов хранятся такие же векторы с данными строк, а во втором векторе хранятся названия столбцов таблицы. К недостаткам DefaultTableModel относят низкую производительность. Это связано с тем, что данный класс появился еще в самом первом выпуске [Swing](Swing) для JDK 1.1 и использует для хранения данных класс [Vector](Vector), устаревший и уступающий по многим показателям новым контейнерам данных типа [ArrayList](Class-ArrayList).

В следующем примере создается две таблицы. Для первой таблицы используется **DefaultTableModel**. В конструктор второй таблицы передается разработанная модель _SimpleModel_, наследующая свойства _AbstractTableModel_.

#### Пример 2

```java
// Пример работы со стандартной моделью таблицы JTable  
import javax.swing.*;  
import javax.swing.table.DefaultTableModel;  
import javax.swing.table.AbstractTableModel;  
import java.awt.event.ActionEvent;  
import java.awt.event.ActionListener;  
  
public class Main extends JFrame {  
    // Модель данных таблицы  
    private DefaultTableModel tableModel;  
    private JTable table1;  
    // Данные для таблиц  
    private Object[][] array = new String[][] {{ "Сахар" , "кг", "1.5" },  
            { "Мука"  , "кг", "4.0" },  
            { "Молоко", "л" , "2.2" }};  
    // Заголовки столбцов  
    private Object[] columnsHeader = new String[] {"Наименование", "Ед.измерения", "Количество"};  
  
    public Main() {  
        super("Пример использования TableModel");  
        setDefaultCloseOperation(EXIT_ON_CLOSE);  
        // Создание стандартной модели  
        tableModel = new DefaultTableModel();  
        // Определение столбцов  
        tableModel.setColumnIdentifiers(columnsHeader);  
        // Наполнение модели данными  
        for (int i = 0; i < array.length; i++)  
            tableModel.addRow(array[i]);  
  
        // Создание таблицы на основании модели данных  
        table1 = new JTable(tableModel);  
        // Создание кнопки добавления строки таблицы  
        JButton add = new JButton("Добавить");  
        add.addActionListener(new ActionListener() {  
            public void actionPerformed(ActionEvent e) {  
                // Номер выделенной строки  
                int idx = table1.getSelectedRow();  
                // Вставка новой строки после выделенной  
                tableModel.insertRow(idx + 1, new String[] {  
                        "Товар №" + String.valueOf(table1.getRowCount()),  
                        "кг", "Цена"});  
            }  
        });  
        // Создание кнопки удаления строки таблицы  
        JButton remove = new JButton("Удалить");  
        remove.addActionListener(new ActionListener() {  
            public void actionPerformed(ActionEvent e) {  
                // Номер выделенной строки  
                int idx = table1.getSelectedRow();  
                // Удаление выделенной строки  
                tableModel.removeRow(idx);  
            }  
        });  
        // Создание таблицы на основе модели данных  
        JTable table2 = new JTable(new SimpleModel());  
        // Определение высоты строки  
        table2.setRowHeight(24);  
  
        // Формирование интерфейса  
        Box contents = new Box(BoxLayout.Y_AXIS);  
        contents.add(new JScrollPane(table1));  
        contents.add(new JScrollPane(table2));  
        getContentPane().add(contents);  
  
        JPanel buttons = new JPanel();  
        buttons.add(add);  
        buttons.add(remove);  
        getContentPane().add(buttons, "South");  
        // Вывод окна на экран  
        setSize(400, 300);  
        setVisible(true);  
    }  
    // Модель данных  
    class SimpleModel extends AbstractTableModel {  
        // Количество строк  
        @Override  
        public int getRowCount() {  
            return 10;  
        }  
        // Количество столбцов  
        @Override  
        public int getColumnCount() {  
            return 3;  
        }  
        // Тип хранимых в столбцах данных  
        @Override  
        public Class<?> getColumnClass(int column) {  
            switch (column) {  
                case 1: return Boolean.class;  
                case 2: return Icon.class;  
                default: return Object.class;  
            }  
        }  
        // Функция определения данных ячейки  
        @Override  
        public Object getValueAt(int row, int column) {  
            boolean flag = ( row % 2 == 1 ) ? true : false;  
            // Данные для стобцов  
            switch (column) {  
                case 0: return "" + row;  
                case 1: return flag;  
                case 2: return new ImageIcon("images/copy.png");  
            }  
            return "Не определена";  
        }  
    }  
  
    public static void main(String[] args) {  
        new Main();  
    }  
}
```
При создании стандартной модели _DefaultTableModel_ был использован конструктор без параметров, который после создания хранит нулевое количество строк и столбцов. Прежде, чем вводить в модель данные необходимо определить колонки таблицы (названия и количество) с использованием метода _setColumnIdentifiers()_.

Для добавления данных в _DefaultTableModel_ используется метод addRow(), в который передается массив со значениями. Перегруженная версия метода addRow() обеспечивает добавление строки, данные которой хранятся в векторе [Vector](Vector).

Общее правило работы со стандартной моделью таблицы _DefaultTableModel_ : при вызове методов, изменяющих количество строк или столбцов, данные могут теряться, так что нужно следить за тем, чтобы новое количество строк или столбцов было достаточным для хранимых в модели данных.

Скриншот примера использования моделей данных таблицы **JTable**:
![[Ex2-JTable.png]]

#### Основные методы модели данных TableModel

| Метод                                 | Описание                                                                                                                                                                                                                                                 |
| ------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int getRowCount()                     | Метод возвращает количество строк в таблице.                                                                                                                                                                                                             |
| int getColumnCount()                  | Метод возвращает количество столбцов в таблице.                                                                                                                                                                                                          |
| Object getValueAt(строка, столбец)    | Чтение данных ячейки таблицы. Данные могут иметь определенный тип. Метод возвращает ссылку на базовый тип [Object](Object).                                                                                                                              |
| setColumnName(столбец)                | Метод определения имени столбца, которое будет отображаться в заголовке таблицы JTableHeader. Заголовок таблицы появляется при размещении таблицы в панели прокрутки.                                                                                    |
| isCellEditable(строка, столбец)       | Метод определения возможности редактирования ячейки таблицы.                                                                                                                                                                                             |
| setValueAt(значениe, строка, столбец) | Метод используется для определения значения ячейки таблицы. Реализуйте этот метод, если в таблице есть редактируемые ячейки, иначе их значение невозможно будет поменять.                                                                                |
| getColumnClass(столбец)               | Метод определения типа данных, хранимых в столбце. Тип задается в виде объекта Class. На основе типа данных определяется, как следует отображать и редактировать эти данные. Таблица JTable стандартно поддерживает несколько типов данных для столбцов. |

### Модель столбцов таблицы TableColumnModel

Модель **TableColumnModel** позволяет настраивать столбцы таблицы _JTable_ : устанавливать размеры столбцов, менять их местами, настраивать объекты для отображения в столбце и для редактирования ячеек столбца, управлять заголовком столбца и т.д.

Таблица _JTable_ отображает в интерфейсе порядок столбцов согласно параметрам, определенным в **TableColumnModel**. Каждый столбец таблицы представлен объектом _TableColumn_, c помощью которого указываются:
- размеры столбца - _столбец TableColumn, как обычный компонент, имеет предпочтительный, максимальный и минимальный размеры;_
- индекс столбца - _в модели данных TableModel по этому индексу таблица определяет, какой набор данных отображает столбец;_
- объекты - _для отображения и редактирования данных, хранящихся в столбце._

С помощью **TableColumn** можно настроить и другие параметры, в том числе и модель выделения столбцов.

В **JTable** для хранения информации о столбцах по умолчанию используется стандартная модель _DefaultTableColumnModel_. В подавляющем большинстве случаев ее возможностей хватает. Модель столбцов таблицы хранит список _TableColumn_ и при смене какого-либо свойства столбца или его расположения оповещает об этом событии слушателей _TableColumnModelListener_. В следующем примере демонстрируется обработка различных событий модели столбцов с использованием слушателя _TableColumnModelListener_.

#### Пример 3. Использование модели столбцов таблицы TableColumnModel

```java
// Использование модели столбцов таблицы TableColumnModel
import java.awt.BorderLayout;
import java.awt.event.*;
import javax.swing.*;
import javax.swing.table.*;
import javax.swing.event.ChangeEvent;
import javax.swing.event.ListSelectionEvent;
import javax.swing.event.TableColumnModelEvent;
import javax.swing.event.TableColumnModelListener;
import java.util.Enumeration;

public class Main extends JFrame {
    // Модель столбцов таблицы
    private TableColumnModel columnModel;
    // Данные для таблиц
    private Object[][] array = new String[][] {{ "Сахар" , "кг", "1.5", "44" },
            { "Мука"  , "кг", "4.0", "32" },
            { "Молоко", "л" , "2.2", "45" }};
    // Заголовки столбцов
    private Object[] columnsHeader = new String[] {"Наименование", "Ед.измерения", "Количество"};
    public Main() {
        super("Пример использования TableColumnModel");
        setDefaultCloseOperation(EXIT_ON_CLOSE);
        // Создание таблицы
        final JTable table1 = new JTable(array, columnsHeader);
        // Получаем стандартную модель
        columnModel = table1.getColumnModel();
        // Определение минимального и максимального размеров столбцов
        Enumeration<TableColumn> e = columnModel.getColumns();
        while ( e.hasMoreElements() ) {
            TableColumn column = (TableColumn)e.nextElement();
            column.setMinWidth(50);
            column.setMaxWidth(200);
        }
        // Таблица с автонастройкой размера последней колонки
        JTable table2 = new JTable(3, 5);
        table2.setAutoResizeMode(JTable.AUTO_RESIZE_LAST_COLUMN);
        // Размещение таблиц в панели с блочным расположением
        Box contents = new Box(BoxLayout.Y_AXIS);
        contents.add(new JScrollPane(table1));
        contents.add(new JScrollPane(table2));

        // Кнопка добавления колонки в модель TableColumnModel
        JButton add = new JButton("Добавить колонку");
        // Слушатель обработки события
        add.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                // Добавление столбца к модели TableColumnModel
                TableColumn сolumn = new TableColumn(3, 50);
                сolumn.setHeaderValue("<html><b>Цена</b></html>");
                columnModel.addColumn(сolumn);
            }
        });
        // Кнопка перемещения колонки
        JButton move = new JButton("Переместить колонку");
        // Слушатель обработки события
        move.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                // Индекс первой колоки
                int first = table1.getSelectedColumn();
                // Индекс второй колонки
                int last = (first == columnModel.getColumnCount()) ? first + 1 : 0;
                // Перемещение столбцов
                columnModel.moveColumn(first, last);
            }
        });
        // Панель кнопок
        JPanel pnlButtons = new JPanel();
        pnlButtons.add(add);
        pnlButtons.add(move);
        // Слушатель событий модели столбцов таблицы
        columnModel.addColumnModelListener(new TableColumnModelListener() {
            @Override
            public void columnAdded(TableColumnModelEvent arg0) {
                System.out.println ("TableColumnModelListener.columnAdded()");
            }
            @Override
            public void columnMarginChanged(ChangeEvent arg0) {
                System.out.println ("TableColumnModelListener.columnMarginChanged()");
            }
            @Override
            public void columnMoved(TableColumnModelEvent arg0) {
                System.out.println ("TableColumnModelListener.columnMoved()");
            }
            @Override
            public void columnRemoved(TableColumnModelEvent arg0) {}
            @Override
            public void columnSelectionChanged(ListSelectionEvent arg0) {
                System.out.println ("TableColumnModelListener.columnSelectionChanged()");
            }
        });

        // Вывод окна на экран
        getContentPane().add(contents);
        getContentPane().add(pnlButtons, BorderLayout.SOUTH);
        setSize(480, 300);
        setVisible(true);
    }
    public static void main(String[] args) {
        new Main();
    }
}
```
В примере создаются две таблицы. В первой таблице для модели столбцов определяются минимальный и максимальный размеры с использованием методов setMinWidth(int), setMaxWidth (int) объекта **TableColumn**. По умолчанию минимальный размер столбца составляет 15 пикселов, предпочтительный — 75 пикселов, максимальный размер не ограничен.

В интерфейс примера включены две кнопки для добавления и перемещения колонок. При создании новой колонки используется конструктор _TableColumn(int modelIndex, int width)_, в котором определен идентификатор модели данных и размер колонки.

Следует обратить внимание, что первая таблица создается с использованием конструктора, которому в качестве параметров передаются данные и заголовки столбцов. При этом массив данных определен для 4-х колонок, а количество столбцов всего 3. При добавлении новой колонки в модель столбцов в качестве первого параметра определен "неиспользуемый" индекс (3) модели данных.

При перемещении колонки в новую позицию используется метод _moveColumn(int columnIndex, int newIndex)_, в котором в качестве первого параметрам индекс колонки, а вторым параметром указывается ее новое положение.

Скриншот примера использования модели таблицы **TableColumnModel**.
![[Ex3-JTable.png]]

### Свойства модели TableColumnModel

|Методы и свойства|Описание|
|---|---|
|addColumn(),  <br>removeColumn()|Методы динамического управления количеством хранимых в модели TableColumnModel столбцов. Первый метод добавляет к модели новый столбец, второй удаляет из модели заданный столбец.|
|addColumnModelListener(),  <br>removeColumnModelListener()|Методы подключения и отключения слушателей TableColumnModelListener.|
|getColumnCount()|Функция получения количества столбцов модели.|
|getColumn(int idx)|Функция получения столбца по его порядковому номеру.|
|Enumeration getColumns()|Функция получения всех содержащихся в модели столбцов.|
|moveColumn(int columnIndex, int newIndex)|Метод изменения позиции столбца.|
|columnMargin (методы get/set)|Свойство управления расстоянием между столбцами таблицы (в пикселах).|

### Свойства столбца TableColumn

|Свойства|Описание|
|---|---|
|modelIndex|Индекс столбца в модели данных TableModel. Данные столбца отображает объект TableColumn.|
|preferredWidth, minWidth, maxWidth|Предпочтительный, минимальный и максимальный размеры столбца таблицы.|
|cellRenderer, cellEditor, headerRenderer|Объекты для отображения и редактирования ячеек столбца, а также объект, отображающий заголовок столбца.|
|headerValue, identifier|Первое свойство хранит отображаемое в заголовке столбца значение, а второе позволяет связать со столбцом уникальный идентификатор.|

Еще одним полезным свойством модели колонок таблицы явлется режим распределения пространства. По умолчанию таблица **JTable** устанавливает режим AUTO_RESIZE_SUBSEQUENT_COLUMNS.  
JTable предлагает к использованию 5 режимов :
- AUTO_RESIZE_OFF - в данном режиме пространство не перераспределяется, т.е. размеры столбцов таблицей не меняются. По умолчанию размер столбца равен его предпочтительному размеру. Если меняется размер какого-либо столбца, то остальные столбцы не затрагиваются. При недостаточном месте в таблице для столбца появляется горизонтальная полоса прокрутки, если таблица была размещена в панели прокрутки JScrollPane, в противном случае крайние столбцы просто исчезают с экрана;
- AUTO_RESIZE_NEXT_COLUMN - при изменении размеров столбца пространство перераспределяется только между ним и следующим за ним столбцом. Если размер столбца увеличивается, то размер следующего столбца уменьшается, и наоборот;
- AUTO_RESIZE_LAST_COLUMN - столбцы можно увеличивать или уменьшать только за счет последнего столбца таблицы, все остальные столбцы остаются неизменными;
- AUTO_RESIZE_SUBSEQUENT_COLUMNS - при изменении размера какого-либо столбца перераспределение пространства происходит равномерно между всеми следующими за ним столбцами. Последний столбец нельзя отдельно уменьшить или увеличить, разве что меняя размеры предпоследнего столбца. Данный режим используется таблицей по умолчанию.
- AUTO_RESIZE_ALL_COLUMNS - перераспределение пространства в этом режиме происходит между всеми столбцами таблицы. Если увеличивается размер некоторого столбца, то требуемое для этого пространство «отнимается» у всех остальных столбцов в равном соотношении. Если столбец достигает минимального размера или изначально не допускает изменения своих размеров, он перестает участвовать в «жертвовании» пространства.

### Модель выделения SelectionModel

Ячейки таблицы можно выделять разными способами : строками, столбцами, интервалами, единичными ячейками и т.д. Эту задачу решают модели выделения **SelectionModel**, которые хранят выделенные строки и столбцы таблицы. Следует отметить, что и для столбцов, и для строк таблицы имеются собственные модели выделения, представленные интерфейсом _ListSelectionModel_. Таким образом таблица имеет две модели выделения. Первая модель хранится непосредственно в **JTable** и отвечает за выделение строк таблицы. Вторая модель отвечает за выделение столбцов таблицы и хранится в модели столбцов таблицы _TableColumnModel_.

Модель выделения списка использует один из трех режимов выделения :
- **SINGLE_SELECTION** - режим выделения одиночных элементов;
- **SINGLE_INTERVAL_SELECTION** - режим выделения непрерывными интервалами;
- **MULTIPLE_INTERVAL_SELECTION** - режим выделения произвольного набора строк или столбцов.

Таким образом, для строк и для столбцов имеется по три режима выделения. То есть, таблица предоставляет девять комбинаций. По умолчанию в таблице и для строк, и для столбцов используется стандартная реализация интерфейса _ListSelectionModel_ — класс _DefaultListSelectionModel_.

#### Пример 4. Использование модели SelectionModel

```java
// Пример выделения ячеек таблицы с использованием SelectionModel
import javax.swing.*;
import javax.swing.table.*;

public class Main extends JFrame {
    // Данные для таблиц
    private Object[][] array = new String[][] {{ "Сахар" , "кг", "1.5", "44" },
            { "Мука"  , "кг", "4.0", "32" },
            { "Молоко", "л" , "2.2", "45" }};
    // Заголовки столбцов
    private Object[] columnsHeader = new String[] {"Наименование", "Ед.измерения", "Количество"};
    public Main() {
        super("Пример использованием SelectionModel");
        setDefaultCloseOperation(EXIT_ON_CLOSE);

        // Таблица с выделение по столбцам
        JTable tableColumn = new JTable(array, columnsHeader);
        // Блокирование выделения по строкам
        tableColumn.setRowSelectionAllowed(false);
        // Модель столбцов
        TableColumnModel columnModel = tableColumn.getColumnModel();
        // Разрешение выделения столбца
        columnModel.setColumnSelectionAllowed(true);
        // Режим одиночного выделения
        columnModel.getSelectionModel().setSelectionMode(ListSelectionModel.SINGLE_SELECTION);

        // Таблица с выделением по строкам
        JTable tableRow = new JTable(array, columnsHeader);
        // Режим выделения интервала по строкам
        tableRow.getSelectionModel().setSelectionMode(ListSelectionModel.SINGLE_INTERVAL_SELECTION);

        // Размещение таблиц в панели с блочным расположением
        Box contents = new Box(BoxLayout.Y_AXIS);
        contents.add(new JScrollPane(tableColumn));
        contents.add(new JScrollPane(tableRow));
        setContentPane(contents);

        // Вывод окна на экран
        setSize(480, 300);
        setVisible(true);
    }
    public static void main(String[] args) {
        new Main();
    }
}
```
В примере создаётся две таблицы с одинаковыми данными, но с разными режимами выделения. В первой таблице используется выделение по столбцам. Чтобы решить данную задачу сначала было отключено выделение по строкам методом _rowSelectionAllowed(boolean)_, затем для модели столбцов **TableColumnModel** определен режим выделения. Свойство _columnSelectionAllowed_ позволяет включить выделение столбцов. Модель выделения столбцов, полученная через вызов метода _getSelectionModel()_, позволяет определить для столбцов любой из трех режимов выделения.

Во второй таблице примера установлен режим выделения непрерывных интервалов строк.

Интерфейс примера использования модели выделения таблицы **SelectionModel** представлен на следующем скриншоте.
![[Ex4-JTable.png]]

### Основные методы и свойства SelectionModel

|Методы или свойства|Описание|
|---|---|
|selectionModel|Свойство хранит модель выделения в JTable. По умолчанию используется стандартная реализация DefaultListSelectionModel.|
|rowSelectionAllowed,  <br>columnSelectionAllowed|Первое свойство - включение и отключение выделения строк. Второе свойство - включает или отключает выделение столбцов (имеется и в модели выделения столбцов и в классе JTable). По умолчанию выделение по столбцам отключено.|
|selectionMode|Свойство моделей выделения таблицы JTable.|
|selectAll()|Выделение всех ячеек таблицы.|
|clearSelection()|Снятие выделения со всех ячеек.|
|cellSelectionAllowed|Метод разрешения или запрещения выделять отдельные ячейки таблицы.|
|rowSelectionInterval,  <br>columnSelectionInterval  <br>(add, set, remove)|Методы выделения строк или столбцов. Методы «add» присоединяют к уже имеющемуся выделению новые строки и столбцы, методы «set» заменяют имеющееся выделение новым. Методы «remove» удаляют из выделения указанные строки или столбцы.|

### Методы получения информации о выделениях модели SelectionModel

|Методы|Описание|
|---|---|
|isSelectedIndex()|Функция проверки выделения элемента в некоторой позиции.|
|isRowSelected(),  <br>isColumnSelected()|Методы определения, выделена ли строка или столбец или нет.|
|isCellSelected()|Метод определения, выделена ли ячейка или нет.|
|getSelectedRows(),  <br>getSelectedColumns()|Методы получения массивов индексов выделенных строк и столбцов.|

Модели выделения, методы и свойства **JTable** позволяют управлять работой механизмов выделения ячеек таблицы и получать информацию о выделенных элементах. Следует помнить, что модели выделения строк и столбцов действуют независимо друг от друга. К примеру, если в таблице используется режим выделения строк и пользователь щелкает на некоторой ячейке, то выделяется вся строка, которой принадлежит выделенная ячейка. То есть все ячейки в данной строке выглядят как выделенные. Но выделенными будут только та строка и тот столбец, которым принадлежит ячейка, на которой щелкнули мышью.

### Заголовок таблицы JTableHeader

Заголовок таблицы **JTableHeader** позволяет отображать названия столбцов, менять столбцы местами, изменять размеры столбцов. Таблица **JTable** автоматически добавляет заголовок таблицы в панель прокрутки, если таблица размещается в панели прокрутки. Если таблица будет размещаться в любом другом контейнере, то для заголовка таблицы места не найдется.

Данные _JTableHeader_ получает из модели столбцов таблицы _TableColumnModel_, которая передается в конструктор класса JTableHeader или присоединяется к заголовку позже. Фактически заголовок таблицы играет роль дополнительной модели столбцов. Никаких данных в самом заголовке не хранится — все находится в модели TableColumnModel.

Возможности стандартного **JTableHeader** ограничены. Можно разрешить или запретить перетаскивание столбцов, изменение их размеров, а также определить внешний интерфейс.

#### Пример 5. Использование JTableHeader

```java
// Настройка заголовка таблицы JTableHeader
import java.awt.*;
import javax.swing.*;
import javax.swing.table.*;
import javax.swing.border.*;

public class Main extends JFrame {
    // Данные для таблицы
    private String[][] data = {{ "2016.04.05", "68.6753", "78.1662" },
            { "2016.04.06", "68.8901", "78.2798" },
            { "2016.04.07", "68.5215", "78.1662" }};
    // Названия столбцов
    private String[] columnNames = {"Дата", "Курс USD", "Курс EUR"};

    public Main() {
        super("Пример использования TableHeader");
        setDefaultCloseOperation(EXIT_ON_CLOSE);
        // Создание таблицы
        JTable table = new JTable(data, columnNames);
        // Настройка заголовков таблицы
        JTableHeader header = table.getTableHeader();
        header.setReorderingAllowed(false);
        header.setResizingAllowed(false);
        // Подключение заголовка таблицыHeaderRenderer
        header.setDefaultRenderer(new HeaderRenderer());
        // Размещение таблицы в панели прокрутки
        getContentPane().add(new JScrollPane(table));
        // Вывод окна на экран
        setSize(400, 150);
        setVisible(true);
    }
    // Модифицируемый заголовок таблицы
    class HeaderRenderer extends DefaultTableCellRenderer {
        // Границы заголовков колонок
        Border border = BorderFactory.createBevelBorder(BevelBorder.RAISED);

        // Метод возвращает визуальный компонент для прорисовки
        public Component getTableCellRendererComponent(JTable table, Object value,
                                                       boolean isSelected, boolean hasFocus,
                                                       int row, int column) {
            // Надпись из базового класса
            JLabel label = (JLabel)super.getTableCellRendererComponent(
                    table, value, isSelected, hasFocus, row, column);
            // Выравнивание строки заголовка
            label.setHorizontalAlignment(SwingConstants.CENTER);
            // Размещение изображения в заголовке
            if (column == 1)
                label.setIcon(new ImageIcon("c://users//minipc//onedrive//документы//obsidian vault//java//swing//icon//usd.png"));
            else if (column == 2)
                label.setIcon(new ImageIcon("c:/users/minipc/onedrive/документы/obsidian vault/java/swing/icon/eur.png"));
            else if (column == 0)
                label.setIcon(null);
            // Настройка цвет фона метки
            float[] hsb = Color.RGBtoHSB(224, 224, 224, null);
            label.setBackground(Color.getHSBColor(hsb[0], hsb[1], hsb[2]));

            label.setBorder(border);
            return label;
        }
    }
    public static void main(String[] args) {
        new Main();
    }
}
```
В примере создается небольшое окно, в центре которого размещается таблица JTable в панели прокрутки. Таблица создается на основе двух массивов: двухмерный массив data с данными, одномерный columnNames — названия столбцов. После создания таблицы с помощью метода getTableHeader() извлекается её заголовок.

В заголовке таблицы блокируются возможности перетаскивания столбцов методом reorderingAllowed() и смены положения столбцов методом resizingAllowed(). Для определения интерфейса заголовков подключается класс HeaderRenderer, унаследованный от стандартного отображающего объекта DefaultTableCellRenderer (метод setDefaultRenderer()). Настройка интерфейса заголовка таблицы реализована во внутреннем классе HeaderRenderer.

Интерфейс примера использования заголовка таблицы JTableHeader представлен на следующем скриншоте.
![[Ex5-JTable.png]]

Внешний вид границы заголовков таблицы можно изменить. Следующий код демонстрирует возможность определения границы заголовка таблицы с иконкой, либо определенного цвета. В примере используется BevelBorder.
```java
// Границы заголовков колонок с отступами и иконками
Border border1 = BorderFactory.createMatteBorder(
                      16, 16, 16, 16, new ImageIcon("images/star.png"));
// Границы заголовков колонок с отступами и определенным цветом
float[] hsb = Color.RGBtoHSB(224, 224, 224, null);
Color color = Color.getHSBColor(hsb[0], hsb[1], hsb[2]);
Border border2 = BorderFactory.createMatteBorder(16, 16, 16, 16, color);
```
Часто заголовок таблицы JTableHeader используется для подключения возможности сортировки данных по столбцам. Для этого к заголовку таблицы присоединяется слушатель событий от мыши, следящий за щелчками на заголовках столбцов. После щелчка можно определить, какой столбец был выделен (метод columnAtPoint() класса JTableHeader), отсортировать данные по какому-либо признаку и дать сигнал таблице о том, что данные изменились и вид таблицы следует обновить.

### Отображение значения, DefaultTableCellRenderer

Каждая ячейка таблицы прорисовывается с помощью отдельного отображающего объекта, который должен реализовывать особый интерфейс. Все поддерживаемые таблицей типы данных прорисовываются с помощью стандартного объекта **DefaultTableCellRenderer**. Можно регистрировать отображающие объекты собственной разработки для своих типов данных или же заменять стандартные отображающие объекты собственными. Отображающие объекты могут быть определены и для отдельных столбцов независимо от типа хранящейся в них информации.

Все стандартные отображающие объекты наследуют свойства и методы надписи JLabel. Поэтому для отображения значения ячейки можно применять все возможности HTML и загружать изображения.

В следующем примере создадим таблицу с тремя столбцами и определим объект _ImageTextCell_, который нужно будет отобразить в двух колонках таблицы. В одной колонке будет отображаться текст с иконкой, а в другой только текст. В тетьей колонке отобразим текст в формате HTML.
```java
class ImageTextCell
{
    public Icon   icon;
    public String text;
    // Конструкторы
    public ImageTextCell(String text) {
        this (text, null);
    }
    public ImageTextCell(String text, Icon icon) {
        this.icon = icon;
        this.text = text;
    }
}
```
Для отображения объекта _ImageTextCell_ создадим унаследованный от DefaultTableCellRenderer класс ImageTextCellRenderer и переопределим метод getTableCellRendererComponent(), который будет прорисовывать данные, хранящиеся в ячейках таблицы.
```java
// Класс отображения объекта в ячейке таблицы
class ImageTextCellRenderer extends DefaultTableCellRenderer 
{
    // Метод получения компонента для прорисовки
	public Component getTableCellRendererComponent(JTable table, Object value,
			boolean isSelected, boolean hasFocus, int row, int column) {
        // Объект прорисовки
        ImageTextCell objectCell = (ImageTextCell)value;
        // Надпись от базового класса
        JLabel label = (JLabel)super.getTableCellRendererComponent(table, 
            objectCell.text, isSelected, hasFocus, row, column);
        // Размещение значка
        label.setIcon(objectCell.icon);
        // Выравнивание
        if (column == 2)
            label.setHorizontalAlignment(JLabel.RIGHT);
        else
            label.setHorizontalAlignment(JLabel.LEFT);
        return label;
    }
}
```
В методе getTableCellRendererComponent() для каждой ячейки определяется текстовое значение и иконка. Текстовое значение выравнивается по правому или по левому краю.

В примере _TableCellTest_ для подключения объекта отображения используется метод setDefaultRenderer. Кроме этого, переопределяется модель таблицы TableModel для работы с объектами.
```java
// Создание таблицы на основе модели данных
JTable table = new JTable(new DataModel(data, columnNames));
// Регистрация объекта для прорисовки данных
table.setDefaultRenderer(ImageTextCell.class, new ImageTextCellRenderer());
```

#### Пример 6. Полный исходный код примера

```java
import java.awt.*;
import javax.swing.*;
import javax.swing.table.*;
import javax.swing.Icon;

public class Main extends JFrame {
    private static final long serialVersionUID = 1L;

    // Значки
    private Icon manIcon   = new ImageIcon("c://users//minipc//onedrive//документы//obsidian vault//java//swing//icon//man.png"),
            womanIcon = new ImageIcon("c://users//minipc//onedrive//документы//obsidian vault//java//swing//icon//woman.png");
    // Названия столбцов
    private String[] columnNames = {"Роль", "Образ", "Актер"};
    // Данные таблицы
    private Object[][] data = {{ new ImageTextCell("Остап Бендер" , manIcon),
            "<html><b>Великий комбинатор",
            new ImageTextCell("Арчил Гомиашвили") },
            { new ImageTextCell("Киса Воробьянинов", manIcon),
                    "<html><i>Предводитель дворянства",
                    new ImageTextCell("Сергей Филиппов")},
            { new ImageTextCell("Мадам Грицацуева", womanIcon),
                    "<html><font color=\"red\">Знойная женщина",
                    new ImageTextCell("Наталья Крачковская")}};
    public Main()
    {
        super("Пример использования TableCellRenderer");
        setDefaultCloseOperation(EXIT_ON_CLOSE);
        // Создание таблицы на основе модели данных
        JTable table = new JTable(new DataModel(data, columnNames));
        // Регистрация объекта для прорисовки данных
        table.setDefaultRenderer(ImageTextCell.class, new ImageTextCellRenderer());
        // Вывод окна на экран
        getContentPane().add(new JScrollPane(table));
        setSize(500, 150);
        setVisible(true);
    }

    // Объект, включающий значок и текст
    class ImageTextCell
    {
        public Icon   icon;
        public String text;
        // Конструкторы
        public ImageTextCell(String text)
        {
            this (text, null);
        }
        public ImageTextCell(String text, Icon icon) {
            this.icon = icon;
            this.text = text;
        }
    }

    // Класс отображения объекта в ячейке таблицы
    class ImageTextCellRenderer extends DefaultTableCellRenderer {
        private static final long serialVersionUID = 1L;

        // Метод получения компонента для прорисовки
        public Component getTableCellRendererComponent(JTable table, Object value, boolean isSelected,
                                                       boolean hasFocus, int row, int column) {
            // Объект прорисовки
            ImageTextCell objectCell = (ImageTextCell)value;
            // Надпись от базового класса
            JLabel label = (JLabel)super.getTableCellRendererComponent(table,
                    objectCell.text, isSelected, hasFocus, row, column);
            // Размещение значка
            label.setIcon(objectCell.icon);
            // Выравнивание
            if (column == 2)
                label.setHorizontalAlignment(JLabel.RIGHT);
            else
                label.setHorizontalAlignment(JLabel.LEFT);
            return label;
        }
    }
    // Модель данных таблицы
    class DataModel extends AbstractTableModel {
        private static final long serialVersionUID = 1L;
        // Названия столбцов
        private String[] columnNames = null;
        // Данные таблицы
        private Object[][] data = null;
        DataModel(Object[][] data, String[] columnNames) {
            this.data        = data;
            this.columnNames = columnNames;
        }
        // Количество столбцов
        public int getColumnCount() {
            return columnNames.length;
        }
        // Названия столбцов
        public String getColumnName(int column) {
            return columnNames[column];
        }
        // Количество строк
        public int getRowCount() {
            return data.length;
        }
        // Тип данных столбца
        public Class<?> getColumnClass(int column) {
            return data[0][column].getClass();
        }
        // Значение ячейки
        public Object getValueAt(int row, int column) {
            return data[row][column];
        }
    }
    public static void main(String[] args) {
        new Main();
    }
}
```
Интерфейс примера _TableCellTest_ представлен на следующем скриншоте:
![[Ex6-JTable.png]]

### Редактирование ячейки, CellEditor

За редактирование ячеек таблицы отвечает объект, реализующий интерфейс **TableCellEditor**, наследующий интерфейс CellEditor. Cтандартный объект для редактирования таблицы можно настроить или создать собственный объект.

Объекты для редактирования также, как и отображающие объекты, делятся на два типа: объекты по умолчанию и объекты, используемые для конкретного столбца таблицы. При этом вторые имеют приоритет перед первыми. Объекты редактирования по умолчанию регистрируются посредством специальных методов класса **JTable** и предназначены для редактирования данных определенного типа. Тип данных столбца можно получить с использованием метода getColumnClass() модели TableModel. JTable включает редактор для текстовых данных, числовых данных и булевых переменных, в качестве редактора которого используется флажок [JCheckBox](JCheckBox).

Изначально встроенные в таблицу JTable редакторы реализованы в виде DefaultCellEditor. Этот редактор ячеек реализует интерфейс **TableCellEditor** и позволяет использовать для редактирования данных текстовое поле [JTextField](JTextField), флажок [JCheckBox](JCheckBox) или раскрывающийся список JComboBox.

Интерфейс **TableCellEditor** добавляет к базовым методам родительского интерфейса CellEditor метод getTableCellEditorComponent(), который возвращает Component, используемый для редактирования ячеек.

В следующем примере _TableCellEditorTest_ создается редактируемая таблица с тремя столбцами. В первом столбце размещается обычный текст. Во втором столбце используется редактор с раскрывающимся списком [JComboBox](JCheckBox). А в третьем столбце используется простенький редактор даты.

В качестве компонента для редактирования даты используется счетчик [JSpinner](JSpinner) со специальной моделью.
```java
// Редактор даты с использованием прокручивающегося списка JSpinner
class DateCellEditor extends AbstractCellEditor implements TableCellEditor
{
    // Редактор
    private JSpinner editor;
    // Конструктор
    public DateCellEditor() {
        // Настройка прокручивающегося списка
        SpinnerDateModel model = new SpinnerDateModel(new Date(), null, null, Calendar.DAY_OF_MONTH);
        editor = new JSpinner(model);
    }
    // Метод получения компонента для прорисовки
    public Component getTableCellEditorComponent(JTable table, Object value, 
                                        boolean isSelected, int row, int column) {
        // Изменение значения
        editor.setValue(value);
        return editor;
    }
    // Функция текущего значения в редакторе
    public Object getCellEditorValue() {
        return editor.getValue();
    }
}
```
Редактор _DateCellEditor_ наследует свойства класса AbstractCellEditor и реализует интерфейс TableCellEditor. Необходимо переопределить метод getTableCellEditorComponent(), который возвращает редактируемый компонент, и метод getCellEditorValue(), сообщающий текущее значение в редакторе (ячейке). Для второго редактора с раскрывающимся списком необходимо предварительно создать объект [JComboBox](JComboBox) и наполнить его элементами, прежде чем передать его в конструктор.

В следующих строках кода примера _TableCellEditorTest_ определены массивы наименований столбцов и данных, которые используются для создания модели таблицы _model_. Таблица создается уже с использованием этой _model_. Для таблицы определяется редактор данных методом setDefaultEditor. А для второго столбца создается свой редактор _editor_.
```java
// Название столбцов
private String[] columns = { "Сотрудник", "Должность", "Дата рождения" };
// Данные для таблицы
private Object[][] data = {{ "Иван"     , "Менеджер"   , new Date()}, 
                           { "Александр", "Программист", new Date()},
                           { "Петр"     , "Водитель"   , new Date()}};
...

// Создание модели таблицы
DefaultTableModel model = new DefaultTableModel(data, columns)
{
    // Функция получения типа столбца
    public Class<?> getColumnClass(int column) {
        return data[0][column].getClass();
    }
};

// Создание таблицы
JTable table = new JTable(model);

// Определение редактора ячеек
table.setDefaultEditor(Date.class, new DateCellEditor());
// Раскрывающийся список
JComboBox<String> combo = new JComboBox<String>(new String[] { "Менеджер", "Программист", "Водитель"});
// Редактор ячейки с раскрывающимся списком
DefaultCellEditor editor = new DefaultCellEditor(combo);
// Определение редактора ячеек для колонки
table.getColumnModel().getColumn(1).setCellEditor(editor);
```

#### Пример 7. Полный исходный код

```java
// Применение редактора ячеек таблицы CellEditor
import java.awt.Component;
import java.util.Calendar;
import java.util.Date;
import javax.swing.*;
import javax.swing.table.DefaultTableModel;
import javax.swing.table.TableCellEditor;

// Редактор даты с использованием прокручивающегося списка JSpinner
class DateCellEditor extends AbstractCellEditor implements TableCellEditor {
    private static final long serialVersionUID = 1L;
    // Редактор
    private JSpinner editor;
    // Конструктор
    public DateCellEditor() {
        // Настройка прокручивающегося списка
        SpinnerDateModel model = new SpinnerDateModel(new Date(), null, null, Calendar.DAY_OF_MONTH);
        editor = new JSpinner(model);
    }
    // Метод получения компонента для прорисовки
    public Component getTableCellEditorComponent(JTable table, Object value,
                                                 boolean isSelected, int row, int column) {
        // Изменение значения
        editor.setValue(value);
        return editor;
    }
    // Функция текущего значения в редакторе
    public Object getCellEditorValue() {
        return editor.getValue();
    }
}

public class Main extends JFrame {
    private static final long serialVersionUID = 1L;

    // Название столбцов
    private String[] columns = { "Сотрудник"   , "Должность", "Дата рождения" };
    // Данные для таблицы
    private Object[][] data = {{ "Сергеев С.С.", "Менеджер"   , new Date()},
            { "Петров П.П." , "Программист", new Date()},
            { "Смирнов А.С" , "Водитель"   , new Date()}};
    public Main() {
        super("Пример редактора ячеек CellEditor");
        setDefaultCloseOperation(EXIT_ON_CLOSE);

        // Создание модели таблицы
        DefaultTableModel model = new DefaultTableModel(data, columns) {
            private static final long serialVersionUID = 1L;

            // Функция получения типа столбца
            public Class<?> getColumnClass(int column) {
                return data[0][column].getClass();
            }
        };

        // Создание таблицы
        JTable table = new JTable(model);
        // Определение редактора ячеек
        table.setDefaultEditor(Date.class, new DateCellEditor());
        // Раскрывающийся список
        JComboBox<String> combo = new JComboBox<String>(new String[] { "Менеджер", "Программист", "Водитель"});
        // Редактор ячейки с раскрывающимся списком
        DefaultCellEditor editor = new DefaultCellEditor(combo);
        // Определение редактора ячеек для колонки
        table.getColumnModel().getColumn(1).setCellEditor(editor);
        // Вывод окна на экран
        getContentPane().add(new JScrollPane(table));
        setSize(400, 200);
        setVisible(true);
    }
    public static void main(String[] args) {
        new Main();
    }
}
```
Интерфейс примера _TableCellEditorTest_ представлен на следующем скриншоте.
![[Ex7_1-JTable.png]] ![[Ex7_2-JTable.png]]
