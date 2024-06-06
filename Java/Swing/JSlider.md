#Java #Swing #JSlider

## Класс JSlider

2024-06-06 14:16

### Ползунки JSlider

Ползунок _JSlider_ позволяет изменять в заданном диапазоне значение изменением положения некоторого регулятора мышью. Для работы ползунка используется модель _BoundedRangeModel_, которая хранит информацию об ограниченном наборе данных в виде четырех целочисленных значений: минимальное значение (minimum), максимальное значение (maximum), текущее значение (value) и внутренний диапазон (extent). При изменении любого из четырех значений модель вызывает событие _ChangeEvent_ для обновления вида или выполнения каких-либо действий.

Ползунки используют внутренний диапазон для того, чтобы определить, на сколько должен «прыгнуть» регулятор, если пользователь щелкает на шкале ползунка, не трогая регулятор. Если диапазон данных велик, то можно сделать внутренний диапазон большим, чтобы можно было быстро менять его, щелкая на полосе.

### Модель BoundedRangeModel

Модель _BoundedRangeModel_ очень проста и нет смысла реализовывать ее. Лучше использовать стандартную модель _DefaultBoundedRangeModel_, поставляемую вместе с библиотекой [Swing](Swing). Стандартная модель позволяет определять и изменять все четыре значения и взаимодействует со слушателями. Именно _DefaultBoundedRangeModel_ используют конструкторы ползунка JSlider по умолчанию.

#### Конструктор модели DefaultBoundedRangeModel

```java
public DefaultBoundedRangeModel(int value, int extent, int min, int max)
```

Конструктор _DefaultBoundedRangeModel_ принимает параметры для инициализации значений и вызывает исключение IllegalArgumentException, если не выполняется следующее условие :  
min <= value <= value+extent <= max

Модель _BoundedRangeModel_ поддерживает специальный режим _valueIsAdjusting_, в котором она перестает оповещать слушателей об изменениях в данных. Этот режим включается UI-представителем при перетаскивании пользователем регулятора, чтобы не замедлять программу запуском событий на каждое изменение положения указателя мыши. При завершении перетаскивания модель возвращается в обычное состояние и сообщает слушателям об изменении в данных, вызывая событие ChangeEvent.

### Конструкторы ползунков JSlider

| N   | Конструктор и описание                                                                                                                                                   |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1   | **JSlider()**<br>Создает горизонтальный ползунок с диапазоном от 0 до 100 и начальным значением 50.                                                                      |
| 2   | **JSlider(BoundedRangeModel brm)**<br>Создает горизонтальный слайдер, используя указанную BoundedRangeModel.                                                             |
| 3   | **JSlider (внутренняя ориентация)**<br><br>Создает слайдер, используя указанную ориентацию с диапазоном от 0 до 100 и начальным значением 50.                            |
| 4   | **JSlider(int min, int max)**<br><br>Создает горизонтальный слайдер, используя указанные min и max с начальным значением, равным среднему значению min плюс max.         |
| 5   | **JSlider(int min, int max, int value)**<br><br>Создает горизонтальный ползунок, используя указанные минимальные, максимальные и значения.                               |
| 6   | **JSlider(int orientation, int min, int max, int value)**<br><br>Создает ползунок с указанной ориентацией и указанными минимальным, максимальным и начальным значениями. |

### Методы класса

1. **void setOrientation(int n):** устанавливает ориентацию ползунка на указанное значение 
2. **void setValue(int v):** устанавливает значение ползунка в указанное значение 
3. **void setPaintTicks(boolean b):** логическое значение определяет, нарисованы ли галочки на ползунке или нет
4. **void setPaintTrack(boolean b):** логическое значение определяет, будут ли дорожки нарисованы на слайдере или нет
5. **void setMajorTickSpacing(int n):** устанавливает интервал между основными отметками. 
6. **void setMinorTickSpacing(int n):** устанавливает интервал между второстепенными отметками.
7. **void setFont(Font f):** задает шрифт текста для слайдера 
8. **void setMaximum(int m):** устанавливает максимальное значение для ползунка
9. **void setMinimum(int m):** устанавливает минимальное значение для ползунка 
10. **void updateUI():** возвращает свойству пользовательского интерфейса значение, соответствующее текущему внешнему виду. 
11. **void setValueIsAdjusting(boolean b):** присваивает свойству valueIsAdjusting модели значение boolean b.
12. **void setUI(SliderUI ui):** задает объект пользовательского интерфейса, который реализует внешний вид этого компонента.
13. **void setSnapToTicks(boolean b):** если передается значение true, то положение ползунка устанавливается на ближайшую галочку.  
14. **void setModel(BoundedRangeModel n):** задает BoundedRangeModel, которая обрабатывает три основных свойства слайдера: минимальное, максимальное, значение. 
15. **void setLabelTable(Dictionary l):** используется для указания того, какая метка будет отображаться при любом заданном значении.
16. **void setInverted(boolean b):** если передано значение true, то для ползунка устанавливается значение inverted.   
17. **boolean imageUpdate(Image img, int s, int x, int y, int w, int h):** перерисовывает компонент при изменении изображения.
18. **void setExtent(int extent):** устанавливает размер диапазона, “охватываемого” ручкой.
19. **void removeChangeListener(ChangeListener l):** удаляет прослушиватель изменений из слайдера. 
20. **BoundedRangeModel getModel():** возвращает BoundedRangeModel, которая обрабатывает три основных свойства слайдера: минимум, максимум, значение. 
21. **boolean getSnapToTicks():** возвращает true, если регулятор (и значение данных, которое он представляет) устанавливается на ближайшую галочку рядом с тем местом, где пользователь расположил регулятор.
22. **SliderUI getUI():** возвращает объект пользовательского интерфейса, который реализует L&F для этого компонента.
23. **boolean getPaintTrack():** возвращает, окрашены дорожки или нет.  
24. **boolean getPaintTicks():** возвращает, закрашены галочки или нет
25. **void getPaintLabels():** возвращает, закрашены метки или нет  
26. **int getOrientation():** возвращает ориентацию компонента.
27. **int getMinorTickSpacing():** возвращает незначительный интервал между галочками 
28. **int getMinimum():** возвращает минимальное значение
29. **int getMaximum():** возвращает максимальное значение
30. **int getMajorTickSpacing():** возвращает основной интервал между галочками.  
31. **void addChangeListener(ChangeListener l):** добавляет прослушиватель в слайдер.   
32. **protect ChangeListener createChangeListener():** создайте прослушиватель изменений для компонента
33. **void setUI(SliderUI ui):** задает внешний вид объекта, который отображает этот компонент.
34. **SliderUI getUI():** возвращает объект внешнего вида, который отображает этот компонент.
35. **protected String paramString():** возвращает строковое представление этого JSlider.
36. **String getUIClassID():** возвращает имя класса внешнего вида, который отображает этот компонент.
37. **AccessibleContext getAccessibleContext():** возвращает AccessibleContext, связанный с этим JSlider.

### Настройка внешнего вида ползунков

|Свойство (методы get/set)|Описание|
|---|---|
|majorTickSpacing|Определение расстояния для прорисовки больших делений или меток, если они выводятся.|
|minorTickSpacing|Определение расстояния для прорисовки промежуточных делений. Желательно выбирать значение так, чтобы между большими делениями было кратное количество маленьких делений.|
|paintTicks|Включение или отключение прорисовки делений.|
|paintLabels|Прорисовка меток под большими делениями.|
|paintTrack|Управление отображением на экране полосы (шкалы), по которой перемещается регулятор. По умолчанию шкала отображается. Это свойство полезно, если потребуется создать собственную шкалу без разработки UI-представителя ползунка «с нуля».|
|snapToTicks|Определение привязки положения ползунка к меткам, если значение true (метки должны быть включены).|

#### Пример 1. Программа для создания простого JSlider

```java
// java Program to create a simple JSlider
import javax.swing.event.*;
import java.awt.*;
import javax.swing.*;
class solve extends JFrame {
    // frame
    static JFrame f;
    // slider
    static JSlider b;

    // main class
    public static void main(String[] args) {
        // create a new frame
        f = new JFrame("frame");
        f.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        // create a object
        solve s = new solve();
        // create a panel
        JPanel p = new JPanel();
        // create a slider
        b = new JSlider();
        // add slider to panel
        p.add(b);
        f.add(p);
        // set the size of frame
        f.setSize(300, 100);
        f.setVisible(true);
    }
}
```
**Вывод:**
![[Ex1-JSlider.png]]

#### Пример 2. Использования ползунков JSlider

```java
// Пример использования ползунков
import javax.swing.*;
import javax.swing.event.ChangeEvent;
import javax.swing.event.ChangeListener;

import java.awt.BorderLayout;
import java.util.Dictionary;
import java.util.Hashtable;

public class Main extends JFrame {
    private JLabel label;

    public Main() {
        super("Пример использования ползунков JSlider");
        setDefaultCloseOperation(EXIT_ON_CLOSE);

        // Таблица с надписями ползунка
        Dictionary <Integer, JLabel> labels = new Hashtable<Integer, JLabel>();
        labels.put(0, new JLabel("<html><font color=red size=3>0"));
        labels.put(60, new JLabel("<html><font color=gray size=3>30"));
        labels.put(120, new JLabel("<html><font color=blue size=4>60"));
        labels.put(180, new JLabel(new ImageIcon("images/star.png")));

        // Создание модели ползунков
        BoundedRangeModel model = new DefaultBoundedRangeModel(80, 0, 0, 200);

        // Создание ползунков
        JSlider slider1 = new JSlider(model);
        JSlider slider2 = new JSlider(model);
        JSlider slider3 = new JSlider(0, 80, 20);
        JSlider slider4 = new JSlider(model);

        // Настройка внешнего вида ползунков
        slider2.setOrientation(JSlider.VERTICAL);
        slider2.setMajorTickSpacing(50);
        slider2.setMinorTickSpacing(10);
        slider2.setPaintTicks(true);

        slider3.setPaintLabels(true);
        slider3.setMajorTickSpacing(10);

        slider4.setLabelTable(labels);
        slider4.setPaintLabels(true);

        label = new JLabel(getPercent(slider1.getValue()));
        // присоединяем слушателя
        slider1.addChangeListener(new ChangeListener() {
            public void stateChanged(ChangeEvent e) {
                // меняем надпись
                int value = ((JSlider)e.getSource()).getValue();
                label.setText(getPercent(value));
            }
        });
        // Размещение ползунков в интерфейсе
        JPanel contents = new JPanel();
        contents.add(slider1);
        contents.add(slider2);
        contents.add(slider3);
        contents.add(slider4);
        getContentPane().add(contents);
        getContentPane().add(label, BorderLayout.SOUTH);
        // Вывод окна на экран
        setSize(500, 300);
        setVisible(true);
    }
    private String getPercent(int value) {
        return "Размер : " + (int)value/2 + "%";
    }
    public static void main(String[] args) {
        new Main();
    }
}
```
**Вывод:**
![[Ex2-JSlider.png]]

В примере для второго, третьего и четвертого ползунков выполнена настройка внешнего вида. Так для второго ползунка определена прорисовка больших и малых делений, помечающих определенные значения ползунка. Для третьего ползунка определены расстояния отображения делений с прорисовкой надписей со значениями. Чтобы надписи появились, необходимо указать, промежутки для больших делений.

Внешний вид **JSlider** можно настроить с использованием собственных надписей для определенных значений. Для этого следует в метод _setLabelTable()_ передать список в виде подкласса таблицы Dictionary, сопоставляя целому числу («обернутому» в Integer) соответствующую надпись. В качестве метки (надписи) могут выступать любые компоненты, унаследованные от JComponent. В примере данная функция реализована для четвертой таблицы.

Запустив программу, можно увидеть, как одна модель поставляет данные для трех разных ползунков и положения регуляторов меняются синхронно при изменении значения в одном из них. Достоинство использования моделей наглядно показывает, что можно изменять данные не думая о правильном отображении значений в интерфейсе JSlider.

### Событие ползунков ChangeEvent

Ползунки _JSlider_ являются несложными компонентами и имеют всего одно событие **ChangeEvent**, которое вызывается моделью BoundedRangeModel при изменении текущего значения ползунка. В примере показано как подключить к ползунку данное событие, узнавать о перемещении регулятора и отображать в интерфейсе значение.

Присоединить слушателя событий **ChangeEvent** можно либо к используемой в ползунке модели _BoundedRangeModel_, либо к самому ползунку _JSlider_. Отличие связано с источником события, получаемого методом getSource() класса ChangeEvent. В первом случае источником будет модель, а во втором — ползунок. И модель, и ползунок позволяют управлять значениями.