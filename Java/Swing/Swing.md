#java #GUI #Swing 

## Библиотека Swing

2024-05-07 10:58

### Java AWT

Первой попыткой Sun создать графический интерфейс для Java была библиотека **AWT** (Abstract Window Toolkit) — инструментарий для работы с различными оконными средами. Sun сделал прослойку на Java, которая вызывает методы из библиотек, написанных на С. Библиотечные методы AWT создают и используют графические компоненты операционной среды. С одной стороны, это хорошо, так как программа на Java похожа на остальные программы в рамках одной ОС. Но при запуске ее на другой платформе могут возникнуть различия в размерах компонентов и шрифтов, которые будут портить внешний вид программы.

Чтобы обеспечить мультиплатформенность **AWT** интерфейсы вызовов компонентов были унифицированы, вследствие чего их функциональность получилась немного урезанной. Да и набор компонентов получился довольно небольшой. Так например, в AWT нет таблиц, а в кнопках не поддерживается отображение иконок. Тем не менее пакет **java.awt** входит в Java с самого первого выпуска и его можно использовать для создания графических интерфейсов.

Таким образом, компоненты **AWT** не выполняют никакой "работы". Это просто «Java-оболочка» для элементов управления той операционной системы, на которой они работают. Все запросы к этим компонентам перенаправляются к операционной системе, которая и выполняет всю работу.

Использованные ресурсы **AWT** старается освобождать автоматически. Это немного усложняет архитектуру и влияет на производительность. Написать что-то серьезное с использованием AWT будет несколько затруднительно. Сейчас ее используют разве что для апплетов.

### Java Swing

Swing в Java — это инструментарий графического интерфейса пользователя (GUI), включающий компоненты GUI.

Swing предоставляет богатый выбор виджетов и пакетов для создания изысканных компонентов GUI для Java-приложений.

Swing является частью **Java Foundation Classes** (JFC). **JFC** представляет собой API для программирования GUI на Java, обеспечивающий графический интерфейс пользователя.

Библиотека **Java Swing** построена поверх **Java Abstract Widget Toolkit** (AWT). Можно использовать простые компоненты программирования графического интерфейса Java:
- кнопки;
- метки;
- выпадающие списки;
- текстовые поля и т.д.,

### Иерархия Swing

![[java-Swing.jpg]]

### Контейнерный класс

Любой класс, в котором есть другие компоненты, называется контейнерным классом. Для создания приложений с графическим интерфейсом необходим как минимум один класс контейнеров.

Ниже приведены три типа контейнерных классов:
1. Панель – используется для организации компонентов в окне.
2. Рамка – полностью функционирующее окно со значками и заголовками.
3. Диалог – это как всплывающее окно, но не полностью функциональное, как рамка.

### Разница между AWT и Swing

|                                                       |                                         |
| ----------------------------------------------------- | --------------------------------------- |
| AWT                                                   | SWING                                   |
| - платформо-зависимая                                 | - не зависит                            |
| - не соответствует MVC                                | - соответствует MVC                     |
| - меньше компонентов                                  | - Более мощные компоненты               |
| - Не поддерживает подключаемый внешний вид и ощущение | - Поддержка подключаемого внешнего вида |
| - тяжеловесный                                        | - легкий                                |

### Элементы пользовательского интерфейса SWING

Ниже приведен список часто используемых элементов управления при разработке графического интерфейса с использованием SWING.

| S.No. | Класс и описание                                                                                                                                                                                                                 |
| ----- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1     | [JLabel](JLabel)<br>Объект JLabel - это компонент для размещения текста в контейнере.                                                                                                                                            |
| 2     | [JButton](https://www.tutorialspoint.com/swing/swing_jbutton.htm)<br>Этот класс создает кнопку с надписью.                                                                                                                       |
| 3     | [JColorChooser](https://www.tutorialspoint.com/swing/swing_jcolorchooser.htm)<br>JColorChooser предоставляет панель элементов управления, предназначенную для того, чтобы пользователь мог манипулировать цветом и выбирать его. |
| 4     | [Флажок JCheck Box](https://www.tutorialspoint.com/swing/swing_jcheckbox.htm)<br>JCheckBox - это графический компонент, который может находиться либо в состоянии **включено** (true), либо в состоянии **выключено** (false).   |
| 5     | [JRadioButton](https://www.tutorialspoint.com/swing/swing_jradiobutton.htm)<br>The JRadioButton class is a graphical component that can be in either an **on** (true) or **off** (false) state. in a group.                      |
| 6     | [JList](https://www.tutorialspoint.com/swing/swing_jlist.htm)<br>A JList component presents the user with a scrolling list of text items.                                                                                        |
| 7     | [JComboBox](https://www.tutorialspoint.com/swing/swing_jcombobox.htm)<br>Компонент JComboBox предоставляет пользователю доступное меню выбора.                                                                                   |
| 8     | [JTextField](https://www.tutorialspoint.com/swing/swing_jtextfield.htm)<br>Объект JTextField - это текстовый компонент, который позволяет редактировать одну строку текста.                                                      |
| 9     | [JPasswordField](https://www.tutorialspoint.com/swing/swing_jpasswordfield.htm)<br>Объект JPasswordField - это текстовый компонент, предназначенный для ввода пароля.                                                            |
| 10    | [JTextArea](https://www.tutorialspoint.com/swing/swing_jtextarea.htm)<br>Объект JTextArea - это текстовый компонент, который позволяет редактировать несколько строк текста.                                                     |
| 11    | [ImageIcon](https://www.tutorialspoint.com/swing/swing_imageicon.htm)<br>Элемент управления ImageIcon - это реализация интерфейса Icon, который рисует значки из изображений                                                     |
| 12    | [JScrollBar](https://www.tutorialspoint.com/swing/swing_jscrollbar.htm)<br>Элемент управления полосой прокрутки представляет собой компонент полосы прокрутки, позволяющий пользователю выбирать из диапазона значений.          |
| 13    | [JOptionPane](https://www.tutorialspoint.com/swing/swing_joptionpane.htm)<br>JOptionPane предоставляет набор стандартных диалоговых окон, которые запрашивают у пользователей значение или информируют их о чем-либо.            |
| 14    | [JFileChooser](https://www.tutorialspoint.com/swing/swing_jfilechooser.htm)<br>Элемент управления JFileChooser представляет собой диалоговое окно, в котором пользователь может выбрать файл.                                    |
| 15    | [JProgressBar](https://www.tutorialspoint.com/swing/swing_jprogressbar.htm)<br>По мере продвижения задачи к завершению на индикаторе выполнения отображается процент выполнения задачи.                                          |
| 16    | [JSlider](https://www.tutorialspoint.com/swing/swing_jslider.htm)<br>JSlider позволяет пользователю графически выбирать значение, перемещая ручку в пределах ограниченного интервала.                                            |
| 17    | [JSpinner](https://www.tutorialspoint.com/swing/swing_jspinner.htm)<br>JSpinner - это однострочное поле ввода, которое позволяет пользователю выбрать число или значение объекта из упорядоченной последовательности.            |

**Пример 1.** В примере реализуется простейший GUI непосредственно в главном методе _main_():
```java
import javax.swing.*; // подключаем все средства java Swing
 
public class Program { // класс с методом main()
    public static void main(String[] args) {
        JFrame frame = new JFrame("My First GUI"); 
        // Для окна нужна "рама" - Frame
        // стандартное поведение при закрытии окна - завершение приложения
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setSize(300, 300); // размеры окна
        frame.setLocationRelativeTo(null); // окно - в центре экрана
        JButton button = new JButton("Press"); // Экземпляр класса JButton
        // getContentPane() - клиентская область окна
        frame.getContentPane().add(button); // Добавляем кнопку на Frame
        frame.setVisible(true); // Делаем окно видимым
    }
}
```
Вывод:
![[Ex1-Swing.png]]
После запуска можно увидеть, что кнопка «Press» заполнила всю клиентскую область окна. 
Как это исправить? Для этого служит менеджер компоновки. Он используется для компоновки (или расположения) компонентов GUI Java внутри контейнера. Существует множество менеджеров компоновки, но наиболее часто используемые из них — это **BorderLayout**, который размещает компоненты в пяти областях:
- cверху (NORTH);
- снизу (SOUTH);
- слева (WEST);
- справа (EAST);
- по центру (CENTER).

**Пример 2.** Добавим ещё одну кнопку. Теперь их будет две. Первую переименуем в «Старт», а вторую назовём «Стоп»:
```java
import java.awt.BorderLayout; // подключаем BorderLayout
import javax.swing.*; // подключаем все средства java Swing
 
public class Program { // класс с методом main()
 
    public static void main(String[] args) {
        JFrame frame = new JFrame("My First GUI");
        // добавляем панель
        JPanel buttonsPanel = new JPanel(); 
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setSize(300, 300);
        frame.setLocationRelativeTo(null); // окно в центре экрана
        JButton start = new JButton("Старт");
        JButton stop = new JButton(("Стоп");
        // добавляем кнопки на панель
        buttonsPanel.add(start);
        buttonsPanel.add(stop);
        // размещаем панель на Frame (верхняя часть)
        frame.getContentPane().add(BorderLayout.NORTH, buttonsPanel);
        frame.setVisible(true);
    }
}
```
Вывод:
![[Ex2-Swing.png]]
Таким образом можно создавать нужное количество невидимых панелей и размещать (add) на них необходимое число компонентов.

Пример 3. 
```java
import javax.swing.*;  
  
class SwingDemo {  
    SwingDemo() {  
        JFrame frame = new JFrame("A simple swing program");  
        frame.setSize(275, 100);  
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);  
        JLabel label = new JLabel("Swing");  
        frame.getContentPane().add(label);  
        frame.setVisible(true);  
    }  
    public static void main(String[] args) {  
        SwingUtilities.invokeLater(new Runnable() {  
            public void run() {  
                new SwingDemo();  
            }  
        });  
    }  
}
```
Вывод:
![[Ex3-Swing.png]]
В программе SwingDemo присутствует строка
```java
frame.getContentPane().add(label);
```
В JDK5 и более поздних версиях ее можно заменить на
```java
frame.add(label);
```
В методе main конструктор SwingDemo вызывается с помощью следующего фрагмента кода:
```java
    public static void main(String[] args) {  
        SwingUtilities.invokeLater(new Runnable() {  
            public void run() {  
                new SwingDemo();  
            }  
        });  
    }  
```
Этот фрагмент кода создает объект SwingDemo не в основном потоке приложения, а в потоке обработки событий.

Метод main выполняется в основном потоке событий. Следовательно, в нем нельзя непосредственно создавать объект. Следует сначала создать объект [Runnable](Runnable), выполняемый в потоке обработки событий, а затем предоставить данному объекту возможность создавать окно интерфейса программы.