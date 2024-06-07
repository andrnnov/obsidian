#Java #Swing #JSpinner

## Счетчик JSpinner

2024-06-06 15:40

Счетчики JSpinner позволяют выбирать значение из набора данных путем «прокручивания» списка вперед и назад. Внешне счетчик похож на раскрывающийся список [JComboBox](JComboBox) с выбранным одним элементом списка. Но раскрывающийся список позволяет просматривать набор данных в выпадающем окне, а счетчик вообще не показывает набора своих элементов. Данное свойство счетчика позволяет использовать неограниченное количество элементов.

Данные JSpinner хранит в модели, реализующей интерфейс SpinnerModel, которая позволяет узнать текущее, предыдущее и следующее значения счетчика, сменить текущее значение новым и также поддерживает слушателя событий ChangeListener, оповещаемый при смене текущего значения модели. Модель SpinnerModel содержит только три значения. Благодаря такой структуре данных счетчик позволяет организовать выбор из произвольного диапазона данных.

Счетчики JSpinner могут использовать одну из трех стандартных моделей:

    SpinnerListModel - модель содержит определенный набор элементов;
    SpinnerNumberModel - модель определяет набор числовых значений;
    SpinnerDateModel - модель хранения/выбора дат.

Модель можно передать конструктору счетчика или подключить отдельно с использованием метода setModel().

Модель SpinnerListModel в качестве данных может принимать список типа [List](List) (к примеру [ArrayList](Class-ArrayList)). Список элементов можно сменить после того, как модель создана или даже подключена. Для этого следует использовать метод модели setList().

Модель для выбора чисел SpinnerNumberModel в качестве параметров принимает начальное значение, минимальное значение, максимальное значения и приращение, на которое будет увеличиваться или уменьшаться текущее значение. SpinnerNumberModel имеет несколько перегруженных конструкторов для выбора целых чисел (int), чисел с плавающей запятой (double), произвольных чисел, представленных объектами [Number](Number). Сравнение этих объектов выполняется с помощью задаваемых в конструкторе объектов [Comparable](Comparable).

Модель SpinnerDateModel позволяет организовать гибкий выбор дат из определенного диапазона. Принимая во внимание, что в [Swing](Swing) отсутствует стандартный компонент «календаря», данная модель находит в некоторых случаях применение. Для использования модели выбора дат необходимо понимать, как можно манипулировать датами. Модель SpinnerDateModel использует класс [Date](Date), который описывает момент во времени с точностью до миллисекунды, и класс [Calendar](Calendar), позволяющий менять даты по любому из параметров (день недели, день месяца, год, месяц или даже эра). Конструктору SpinnerDateModel необходимо передать текущее значение даты и минимальную и максимальную даты, реализующие интерфейс [Comparable](Comparable). Если минимальное и максимальное значения задать нулевыми (null), то диапазон будет неограниченным.

### Конструкторы

**JSpinner()** - создает счетчик с помощью Integer SpinnerNumberModel с начальным значением 0 и без минимальных или максимальных ограничений.

**JSpinner(SpinnerModel model)** - создает счетчик для данной модели.

### Методы

| Метод                                                 | Описание                                                                                                                           |
| ----------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| void	addChangeListener(ChangeListener listener)       | Добавляет в список прослушиватель, который получает уведомления каждый раз, когда происходит изменение модели.                     |
| void	commitEdit()                                     | Фиксирует измененное в данный момент значение в SpinnerModel.                                                                      |
| protected JComponent	createEditor(SpinnerModel model) | Этот метод вызывается конструкторами для создания JComponent который отображает текущее значение последовательности.               |
| protected void fireStateChanged()                     | Отправляет ChangeEvent, источником которого является this JSpinner, каждому ChangeListener.                                        |
| AccessibleContext getAccessibleContext()              | Получает AccessibleContext для JSpinner                                                                                            |
| ChangeListener[]	getChangeListeners()                 | Возвращает массив всех ChangeListenerфайлов, добавленных в этот JSpinner с помощью addChangeListener().                            |
| JComponent getEditor()                                | Возвращает компонент, который отображает и потенциально изменяет значение модели.                                                  |
| SpinnerModel	getModel()                               | Возвращает SpinnerModel, который определяет эту последовательность значений spinners.                                              |
| Object	getNextValue()                                 | Возвращает объект в последовательности, которая следует за объектом, возвращенным с помощью getValue().                            |
| Object	getPreviousValue()                             | Возвращает объект в последовательности, предшествующей объекту, возвращенному с помощью getValue().                                |
| SpinnerUI getUI()                                     | Возвращает объект look and feel (L & F), который отображает этот компонент.                                                        |
| String	getUIClassID()                                 | Возвращает суффикс, используемый для создания имени класса look and feel (L & F), используемого для визуализации этого компонента. |
| Object	getValue()                                     | Возвращает текущее значение модели, обычно это значение отображается с помощью editor.                                             |
| void	removeChangeListener(ChangeListener listener)    | Удаляет ChangeListener из этого счетчика.                                                                                          |
| void	setEditor(JComponent editor)                     | Изменяет , JComponent который отображает текущее значение SpinnerModel.                                                            |
| void	setModel(SpinnerModel model)                     | Изменяет модель, представляющую значение этого счетчика.                                                                           |
| void	setUI(SpinnerUI ui)                              | Задает внешний вид объекта (L & F), который отображает этот компонент.                                                             |
| void	setValue(Object value)                           | Изменяет текущее значение модели, обычно это значение отображается с помощью editor.                                               |
| void	updateUI()                                       | Возвращает свойству пользовательского интерфейса значение из текущего внешнего вида.                                               |

#### Пример 1. Программа для создания простого JSpinner

```java
// java Program to create a
// simple JSpinner
import java.awt.event.*;
import javax.swing.*;
import java.awt.*;
class spinner extends JFrame {
    // frame
    static JFrame f;

    // default constructor
    spinner() {  }

    // main class
    public static void main(String[] args) {
        // create  a new frame
        f = new JFrame("spinner");
        f.setDefaultCloseOperation(EXIT_ON_CLOSE);
        // create a JSpinner
        JSpinner s = new JSpinner();

        // set Bounds for spinner
        s.setBounds(70, 70, 50, 40);

        // set layout for frame
        f.setLayout(null);

        // add panel to frame
        f.add(s);

        // set frame size
        f.setSize(200, 200);

        f.setVisible(true);
    }
}
```
**Вывод:**
![[Ex1-JSpinner.png]]

#### Пример 2. Программа для создания JSpinner и добавления в него списка изменений (Программа для выбора даты вашего рождения с помощью JSpinner)

```java
// Java program to select your
// date of birth using JSpinner
import java.awt.event.*;
import javax.swing.*;
import java.awt.*;
import javax.swing.event.*;
class spinner1 extends JFrame implements ChangeListener {
    // frame
    static JFrame f;

    // label
    static JLabel l, l1;

    // spinner
    static JSpinner s, s1, s2;

    // default constructor
    spinner1()
    {
    }

    // main class
    public static void main(String[] args) {
        // create an object of the class
        spinner1 sp1 = new spinner1();

        // create  a new frame
        f = new JFrame("spinner");
        f.setDefaultCloseOperation(EXIT_ON_CLOSE);
        // create a label
        l = new JLabel("select your date of birth");
        l1 = new JLabel("1 January 2000");

        // create a JSpinner with a minimum, maximum and step value
        s = new JSpinner();
        s1 = new JSpinner(new SpinnerNumberModel(1, 1, 31, 1));

        // setvalue of year
        s.setValue(2000);

        // store the months
        String months[] = { "January", "February", "March",
                "April", "May", "June", "July", "August",
                "September", "October", "Novemeber", "December" };

        // create a JSpinner with list values
        s2 = new JSpinner(new SpinnerListModel(months));

        // add change listener to spinner
        s.addChangeListener(sp1);
        s1.addChangeListener(sp1);
        s2.addChangeListener(sp1);

        // set Bounds for spinner
        s.setBounds(70, 70, 50, 40);
        s1.setBounds(70, 130, 50, 40);
        s2.setBounds(70, 200, 90, 40);

        // setbounds for label
        l.setBounds(10, 10, 150, 20);
        l1.setBounds(10, 300, 150, 20);

        // set layout for frame
        f.setLayout(null);

        // add label
        f.add(l);
        f.add(l1);
        f.add(s);
        f.add(s1);
        f.add(s2);

        // add panel to frame
        f.add(s);

        // set frame size
        f.setSize(300, 400);

        f.setVisible(true);
    }

    // if the state is changed
    public void stateChanged(ChangeEvent e) {
        l1.setText(s1.getValue() + " " + s2.getValue() + " " + s.getValue());
    }
}
```
**Вывод:**
![[Ex2-JSpinner.png]]

#### Пример 3

В примере первый счетчик позволяет выбрать только целочисленное значение в диапазоне от 0 до 16. Второй счетчик определяет диапазон значений из дней недели. Для третьего счетчика используется модель _dayModel_, которая не имеет ограничений по выбору даты. При использовании модели _monthModel_ для четвертого счетчика можно выбрать только дни текущего месяца. Модели dayModel и monthModel реализуют интерфейс [Comparable](Comparable).

Прокручивая счетчик можно столкнуться с не слишком приятной ситуацией: при смене элементов разной длины поле счетчика может динамически менять свой предпочтительный размер, что оказывает влияние на интерфейс. К сожалению **JSpinner** не имеет метод типа _setPrototypeValue()_ списка [JComboBox](JComboBox). Так что в отдельных случаях лучше использовать раскрывающийся список [JComboBox](JComboBox).
```java
// Использование счетчиков JSpinner и моделей SpinnerModel 
import javax.swing.*;

import java.util.Date;
import java.util.Calendar;

public class Main extends JFrame {
    private  String[]  data     = {"Понедельник", "Вторник", "Среда", "Четверг",
            "Пятница", "Суббота", "Воскресенье"};
    private  Calendar  calendar = Calendar.getInstance();

    public Main() {
        super("Пример использования JSpinner");
        setDefaultCloseOperation(EXIT_ON_CLOSE);
        // Создание модели списка из массива строк
        SpinnerModel week = new SpinnerListModel(data);
        // Создание модели списка целых чисел
        SpinnerModel numbers = new SpinnerNumberModel(8, 0, 16, 2);

        // Модель выбора дня месяца
        SpinnerModel dayModel = new SpinnerDateModel(new Date(), null, null,
                Calendar.DAY_OF_MONTH);
        // Модель выбора дня текущего месяца
        SpinnerModel monthModel = new SpinnerDateModel(new Date(),
                new MinDate(),
                new MaxDate(),
                Calendar.MONTH);

        // Создание счетчиков
        JSpinner spinInt   = new JSpinner(numbers   );
        JSpinner spinWeek  = new JSpinner(week      );
        JSpinner spinDay   = new JSpinner(dayModel  );
        JSpinner spinMonth = new JSpinner(monthModel);

        // Размещение счетчиков в интерфейсе
        JPanel contents = new JPanel();
        contents.add(spinInt  );
        contents.add(spinWeek );
        contents.add(spinDay  );
        contents.add(spinMonth);

        setContentPane(contents);

        // Вывод окна на экран
        setSize(600, 90);
        setVisible(true);
    }
    // Проверка минимальной даты
    class MinDate extends Date implements Comparable<Date> {
        private static final long serialVersionUID = 1L;

        public int compareTo(Date o) {
            Date d = (Date)o;
            calendar.setTime(d);

            int year  = calendar.get(Calendar.YEAR );
            int month = calendar.get(Calendar.MONTH);

            Calendar prev = Calendar.getInstance();
            prev.add(Calendar.MONTH, -1);
            int year_pred  = prev.get(Calendar.YEAR );
            int month_pred = prev.get(Calendar.MONTH);
            // Только текущий месяц
            return (((year == year_pred) && (month > month_pred)) ||
                    ((year > year_pred) && (month < month_pred))) ? -1 : 1;
        }
    }
    // Проверка максимальной даты
    class MaxDate extends Date implements Comparable<Date> {
        private static final long serialVersionUID = 1L;
        public int compareTo(Date o) {
            Date d = (Date)o;
            calendar.setTime(d);

            int year = calendar.get(Calendar.YEAR);
            int month = calendar.get(Calendar.MONTH);

            Calendar next = Calendar.getInstance();
            next.add(Calendar.MONTH, 1);
            int year_next  = next.get(Calendar.YEAR );
            int month_next = next.get(Calendar.MONTH);
            // Только текущий месяц
            return (((year == year_next) && (month < month_next)) ||
                    ((year < year_next) && (month > month_next))) ? 1 : -1;
        }
    }
    public static void main(String[] args) {
        new Main();
    }
}
```
**Вывод:**
![[Ex3-JSpinner.png]]



