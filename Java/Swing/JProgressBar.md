#Java #Swing #JProgressBar

## Класс JProgressBar

2024-06-06 11:05

Индикаторы процесса _JProgressBar_ позволяют наглядно отображать выполнение некоторого процесса, чтобы можно было оценить, когда же он завершится. Такие индикаторы в интерфейсе представлены в виде непрерывно меняющейся полосы со значением (в процентах), насколько выполнен процесс, или каким-либо другим образом поясняющиеся, что в данный момент происходит.

Данные _JProgressBar_ черпает из модели [[JSlider#Модель BoundedRangeModel|BoundedRangeModel]]. В отличие от ползунков JSlider индикаторы процесса JProgressBar используют лишь три значения: минимальное и максимальное значения задаются сразу же, а текущее значение должно обновляться по мере выполнения процесса.

При использовании индикатора **JProgressBar** необходимо создать отдельный поток [Thread](Thread), в который помещается обработка процесса, чтобы значение индикатора можно было непрерывно обновлять и интерфейс программы не «страдал», если процесс окажется требовательным к загрузке процессора и других ресурсов.
```java
public class JProgressBar extends JComponent implements SwingConstants, Accessible;
```

### Поля

Ниже приведены поля для **javax.swing.Класс JProgressBar** −
- **protected ChangeEvent changeEvent** − Для каждого экземпляра требуется только одно ChangeEvent, поскольку единственным интересным свойством события является неизменяемый источник, которым является индикатор выполнения.
- **protected ChangeListener changeListener** − прослушивает события изменения, отправляемые моделью индикатора выполнения, повторно отправляя их прослушивателям событий изменения, зарегистрированным на этом индикаторе выполнения.
- **protected BoundedRangeModel model** - объект, который содержит данные для индикатора выполнения.
- **protected int orientation** − является ли индикатор выполнения горизонтальным или вертикальным.
- **protected boolean paintBorder** − отображать ли границу вокруг индикатора выполнения.
- **protected boolean paintString** − отображать ли строку текста на индикаторе выполнения.
- **protected String progressString** - необязательная строка, которая может отображаться на индикаторе выполнения.

### Конструкторы

| N   | Конструктор и описание                                                                                                                                                          |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | **JProgressBar()**<br>Создает горизонтальный индикатор выполнения, который отображает границу, но не строку выполнения.                                                         |
| 2   | **JProgressBar(BoundedRangeModel NewModel)**<br>Создает горизонтальный индикатор выполнения, который использует указанную модель для хранения данных индикатора выполнения.     |
| 3   | **JProgressBar(int orient)**<br>Создает индикатор выполнения с указанной ориентацией, которая может быть либо SwingConstants. ВЕРТИКАЛЬНОЙ, либо SwingConstants.ГОРИЗОНТАЛЬНОЙ. |
| 4   | **JProgressBar(int min, int max)**<br>Создает горизонтальный индикатор выполнения с заданными минимумом и максимумом.                                                           |
| 5   | **JProgressBar(int orient, int min, int max)**<br>Создает индикатор выполнения, используя указанную ориентацию, минимум и максимум.                                             |
Ориентация индикатора процесса может быть горизонтальной SwingConstants.VERTICAL и вертикальной SwingConstants.VERTICAL. По умолчанию используется горизонтальное расположение. Если значение ориентации окажется неопределенным, то будет вызвано исключение IllegalArgumentException. Конструктор использует следующие значения индикатора процесса по умолчанию - минимальное 0, максимальное 100; текстовое значение в полосе не отображается.

### Методы класса

| N   | Метод и описание                                                                                                                                                                                                                   |
| --- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | **void addChangeListener(ChangeListener l)**<br>Добавляет указанный список изменений в индикатор выполнения.                                                                                                                       |
| 2   | **protected ChangeListener createChangeListener()**<br>Подклассы, которые хотят по-другому обрабатывать события изменения из модели, могут переопределить это, чтобы вернуть экземпляр пользовательской реализации ChangeListener. |
| 3   | **protected void fireStateChanged()**<br>Отправьте ChangeEvent, источником которого является JProgressBar, всем пользователям списка изменений, которые зарегистрировали интерес к ChangeEvents.                                   |
| 4   | **AccessibleContext getAccessibleContext()**<br>Получает AccessibleContext, связанный с этим JProgressBar.                                                                                                                         |
| 5   | **ChangeListener[] getChangeListeners()**<br>Возвращает массив всех списков изменений, добавленных в этот индикатор выполнения с помощью addChangeListener .                                                                       |
| 6   | **int getMaximum()**<br>Возвращает максимальное значение индикатора выполнения из BoundedRangeModel.                                                                                                                               |
| 7   | **int getMinimum()**<br>Возвращает минимальное значение индикатора выполнения из BoundedRangeModel.                                                                                                                                |
| 8   | **BoundedRangeModel getModel()**<br>Возвращает модель данных, используемую этим индикатором выполнения.                                                                                                                            |
| 9   | **int getOrientation()**<br>Возвращает SwingConstants.VERTICAL или SwingConstants.HORIZONTAL, в зависимости от ориентации индикатора выполнения.                                                                                   |
| 10  | **double getPercentComplete()**<br>Возвращает процент завершения для индикатора выполнения.                                                                                                                                        |
| 11  | **String getString()**<br>Возвращает строковое представление текущего прогресса.                                                                                                                                                   |
| 12  | **ProgressBarUI getUI()**<br>Возвращает объект внешнего вида, который отображает этот компонент.                                                                                                                                   |
| 13  | **String getUIClassID()**<br>Возвращает имя класса внешнего вида, который отображает этот компонент.                                                                                                                               |
| 14  | **int GetValue()**<br>Возвращает текущее значение индикатора выполнения из BoundedRangeModel.                                                                                                                                      |
| 15  | **boolean isBorderPainted()**<br>Возвращает свойство borderPainted .                                                                                                                                                               |
| 16  | **boolean isIndeterminate()**<br>Возвращает значение свойства `indeterminate`.                                                                                                                                                     |
| 17  | **boolean isStringPainted()**<br>Возвращает значение свойства stringPainted .                                                                                                                                                      |
| 18  | **protected void paintBorder(Graphics g)**<br>Закрашивает границу индикатора выполнения, если свойство borderPainted имеет значение true.                                                                                          |
| 19  | **protected String paramString()**<br>Возвращает строковое представление этого JProgressBar.                                                                                                                                       |
| 20  | void removeChangeListener(ChangeListener l)**<br>Удаляет список изменений из индикатора выполнения.                                                                                                                                |
| 21  | **void setBorderPainted(boolean b)**<br>Устанавливает свойство borderPainted, которое имеет значение true, если индикатор выполнения должен закрасить свою границу.                                                                |
| 22  | **void setIndeterminate(boolean newValue)**<br>Устанавливает свойство indeterminate индикатора выполнения, которое определяет, находится ли индикатор выполнения в определенном или неопределенном режиме.                         |
| 23  | **void setMaximum(int n)**<br>Устанавливает максимальное значение индикатора выполнения (сохраненное в модели данных индикатора выполнения) равным n.                                                                              |
| 24  | **void setMinimum(int n)**<br>Устанавливает минимальное значение индикатора выполнения (сохраненное в модели данных индикатора выполнения) равным n.                                                                               |
| 25  | **void setModel(BoundedRangeModel NewModel)**<br>Задает модель данных, используемую JProgressBar.                                                                                                                                  |
| 26  | **void setOrientation(int newOrientation)**<br><br>Устанавливает ориентацию индикатора выполнения на новое направление, которое должно быть SwingConstants.VERTICAL или SwingConstants.HORIZONTAL.                                 |
| 27  | **void setString(String s)**<br>Задает значение строки выполнения.                                                                                                                                                                 |
| 28  | **void setStringPainted(boolean b)**<br>Устанавливает значение свойства stringPainted, которое определяет, должен ли индикатор выполнения отображать строку выполнения.                                                            |
| 29  | **void setUI(ProgressBarUI ui)**<br>Задает внешний вид объекта, который отображает этот компонент.                                                                                                                                 |
| 30  | **void setValue(int n)**<br>Устанавливает текущее значение индикатора выполнения равным **n**.                                                                                                                                     |
| 31  | **void updateUI()**<br>Сбрасывает свойство пользовательского интерфейса на значение, соответствующее текущему внешнему виду.                                                                                                       |

#### Пример 1.  Пример использования JProgressBar

```java
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;

public class Main {
    private JFrame mainFrame;
    private JLabel headerLabel;
    private JLabel statusLabel;
    private JPanel controlPanel;

    public Main(){
        prepareGUI();
    }
    public static void main(String[] args){
        Main  swingControlDemo = new Main();
        swingControlDemo.showProgressBarDemo();
    }
    private void prepareGUI(){
        mainFrame = new JFrame("Java Swing Examples");
        mainFrame.setSize(300,400);
        mainFrame.setLayout(new GridLayout(3, 1));

        mainFrame.addWindowListener(new WindowAdapter() {
            public void windowClosing(WindowEvent windowEvent){
                System.exit(0);
            }
        });
        headerLabel = new JLabel("", JLabel.CENTER);
        statusLabel = new JLabel("",JLabel.CENTER);
        statusLabel.setSize(350,100);

        controlPanel = new JPanel();
        controlPanel.setLayout(new FlowLayout());

        mainFrame.add(headerLabel);
        mainFrame.add(controlPanel);
        mainFrame.add(statusLabel);
        mainFrame.setVisible(true);
    }
    private JProgressBar progressBar;
    private Task task;
    private JButton startButton;
    private JTextArea outputTextArea;

    private void showProgressBarDemo(){
        headerLabel.setText("Control in action: JProgressBar");
        progressBar = new JProgressBar(0, 100);
        progressBar.setValue(0);
        progressBar.setStringPainted(true);
        startButton = new JButton("Start");
        outputTextArea = new JTextArea("",5,20);
        JScrollPane scrollPane = new JScrollPane(outputTextArea);

        startButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                task = new Task();
                task.start();
            }
        });
        controlPanel.add(startButton);
        controlPanel.add(progressBar);
        controlPanel.add(scrollPane);
        mainFrame.setVisible(true);
    }
    private class Task extends Thread {
        public Task(){
        }
        public void run(){
            for(int i =0; i<= 100; i+=10){
                final int progress = i;

                SwingUtilities.invokeLater(new Runnable() {
                    public void run() {
                        progressBar.setValue(progress);
                        outputTextArea.setText(outputTextArea.getText()
                                + String.format("Completed %d%% of task.\n", progress));
                    }
                });
                try {
                    Thread.sleep(100);
                } catch (InterruptedException e) {}
            }
        }
    }
}
```
**Вывод:**
![[Ex1-JProgressBar.png]]

#### Пример 2. Пример использования JProgressBar

В примере создаются четыре индикатора процесса **JProgressBar**. Три индикатора используют модель _BoundedRangeModel_, поэтому в них синхронно отображается выполнение некоторого процесса _ThreadProcess_. В качестве модели используется DefaultBoundedRangeModel со следующими параметрами : текущее значение равно пяти, внутренний диапазон равен нулю (не используется), минимальное значение — равно нулю, а максимальное значение — 100.

Для первого индикатора используется конструктор с определением вертикальной ориентации. Если не указывать ориентацию индикатора процесса явно, то устанавливается горизонтальная ориентация. Модель к первому индикатору подключается с использованием метода _setModel()_. Второй и третий индикаторы создаются с использованием конструктора с моделью.

```java
// Пример использования JProgressBar
import javax.swing.*;

public class Main extends JFrame {
    // Общая модель 
    private BoundedRangeModel model;
    public Main() {
        super("Пример использования JProgressBar");
        setDefaultCloseOperation(EXIT_ON_CLOSE);
        // Создание стандартной модели
        model = new DefaultBoundedRangeModel(5, 0, 0, 100);
        // Вертикальный индикатор
        JProgressBar pbVertical = new JProgressBar(JProgressBar.VERTICAL);
        pbVertical.setModel(model);
        pbVertical.setStringPainted(true);
        pbVertical.setString("Процесс ...");

        // Горизонтальный индикатор
        JProgressBar pbHorizontal = new JProgressBar(model);
        pbHorizontal.setStringPainted(true);

        // Настройка параметрой UI-представителя
        UIManager.put("ProgressBar.cellSpacing", 2);
        UIManager.put("ProgressBar.cellLength", 6);
        // Создание индикатора
        JProgressBar pbUIManager = new JProgressBar(model);

        // Неопределенный индикатор
        JProgressBar pbUndefined = new JProgressBar(0, 100);
        pbUndefined.setIndeterminate(true);
        pbUndefined.setStringPainted(true);

        // Размещение индикаторов в окне
        JPanel contents = new JPanel();
        contents.add(pbVertical  );
        contents.add(pbHorizontal);
        contents.add(pbUIManager );
        contents.add(pbUndefined );

        // Вывод окна на экран
        setContentPane(contents);
        setSize(360, 220);
        setVisible(true);
        // Старт "процесса"
        new ThreadProcess().start();
    }
    // Поток эмуляции некоторого процесса
    class ThreadProcess extends Thread {
        public void run() {
            // Проверка завершения процесса
            while ( model.getValue() < model.getMaximum() ) {
                try {
                    // Увеличение текущего значение
                    model.setValue(model.getValue() + 1);
                    // Случайная временная задержка
                    sleep((int)(Math.random() * 1000));
                } catch (Exception e) {
                    e.printStackTrace();
                }
            }
        }
    }
    public static void main(String[] args) {
        new Main();
    }
}
```
**Вывод:**
![[Ex2-JProgressBar.png]]
По умолчанию индикатор процесса текст не прорисовывает. Чтобы в индикаторе отображать текст необходимо вызвать метод _setStringPainted(true)_. В этом случае будет прорисовываться строка, показывающая текущее значение в процентах. Чтобы прорисовывать нестандартный текст необходимо применить метод _setString(String text)_. Текст прорисовывается в той же ориентации, как располагается сам индикатор. Для 1-го индикатора текст отображается вертикально.

Внешний вид индикатора **JProgressBar** можно изменить с помощью некоторых незамысловатых свойств UI-представителя, не попавших в класс самого компонента. UI-представители индикаторов процесса выполняют фактическую прорисовку компонента на экране. Свойства UI-представителей всех компонентов [Swing](Swing) для любого внешнего вида хранятся в специальной таблице класса UIManager, и их можно менять с использованием метода put().

С помощью внутренних свойств UI-представителей индикаторов процесса можно тонко настроить внешний вид перемещающейся в них полосы. Свойство _cellLength_ управляет размером полосы индикатора. Полоса индикатора не обязательно прорисовывается сплошной, она может состоять из набора ячеек одинакового размера, а свойство _cellSpacing_ задает расстояние между ячейками. Если cellSpacing приравнять нулю, то полоса будет сплошной. 3-ий индикатор создан с использованием «тонкой настройки внешнего вида».

Иногда возникают ситуации, когда нельзя сказать, сколько потребуется времени или ресурсов до завершения процесса и на каком этапе процесс находится. В этом случае можно показать, что программа не зависла и процесс продолжается. Для таких ситуаций индикаторы процесса **JProgressBar** поддерживают состояние «неопределенности», при котором происходит периодическое движение регулятора на полосе вперед и назад. Для этого необходимо вызвать метод _setIndeterminate(true)_, как это представлено в 4-ом индикаторе. Данный индикатор создается с использованием конструктора, которому передается минимальное и максимальное значения, а стандартная модель создается автоматически. Дополнительно включена прорисовка текста методом _setStringPainted(true)_, в результате чего в полосе отобразится текущее значение процесса «0%».