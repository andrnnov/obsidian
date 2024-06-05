#Java #Swing #JTextArea

## Многострочное поле JTextArea

2024-06-05 12:03

Многострочное текстовое поле **_JTextArea_** предназначено для ввода простого неразмеченного различными атрибутами текста. В отличие от обычных полей, позволяющих вводить только одну строку текста, многострочные поля дают пользователю возможность вводить произвольное количество строк текста.

Для многострочных полей необходимо задавать не только ширину (максимальное количество символов), но и высоту(максимальное количество строк). _JTextArea_ следует размещать в панелях прокрутки [JScrollPane](JScrollPane).

### Конструкторы JTextArea

1. **JTextArea():** создает новую пустую текстовую область.  
2. **JTextArea(String s):** создает новую текстовую область с заданным исходным текстом.  
3. **JTextArea(int row, int columns):** создает новую текстовую область с заданным количеством строк и столбцов.  
4. **JTextArea(String s, int row, int columns):** создает новую текстовую область с заданным количеством строк и столбцов и заданным исходным текстом.

### Часто используемые методы

1. **add(String s):** добавляет заданную строку к тексту текстовой области.  
2. **void append(String str):** добавляет указанный текст в конец документа.
3. **int getColumns():** возвращает количество столбцов в текстовой области.
4. **int getLineCount():** получить количество строк в тексте текстовой области.  
5. **void setFont(Font f):** устанавливает заданный шрифт текстовой области.  
6. **void setColumns(int c):** устанавливает количество столбцов текстовой области равным заданному целому числу.  
7. **void setRows(int r):** устанавливает количество строк текстовой области в заданное целое число.  
8. **void setTabSize(int size):** задает количество символов для табуляции.
9. **void getRows():** получить количество строк текстовой области.
10. **void setLineWrap(boolean wrap):** устанавливает политику переноса строк в текстовой области.
11. **setWrapStyleWord(boolean word):** задает стиль переноса, используемый, если текстовая область представляет собой перенос строк.

#### Пример 1. Программа для создания простой JTextArea

```java
// Java Program to create a simple JTextArea
import java.awt.event.*;
import java.awt.*;
import javax.swing.*;
class text extends JFrame implements ActionListener {
    // JFrame
    static JFrame f;
    // JButton
    static JButton b;
    // label to display text
    static JLabel l;
    // text area
    static JTextArea jt;
    // default constructor
    text() {
    }

    // main class
    public static void main(String[] args) {
        // create a new frame to store text field and button
        f = new JFrame("textfield");
        f.setDefaultCloseOperation(EXIT_ON_CLOSE);
        // create a label to display text
        l = new JLabel("nothing entered");
        // create a new button
        b = new JButton("submit");
        // create a object of the text class
        text te = new text();

        // addActionListener to button
        b.addActionListener(te);

        // create a text area, specifying the rows and columns
        jt = new JTextArea(10, 10);

        JPanel p = new JPanel();

        // add the text area and button to panel
        p.add(jt);
        p.add(b);
        p.add(l);

        f.add(p);
        // set the size of frame
        f.setSize(300, 300);
        f.setVisible(true);
    }

    // if the button is pressed
    public void actionPerformed(ActionEvent e) {
        String s = e.getActionCommand();
        if (s.equals("submit")) {
            // set the text of the label to the text of the field
            l.setText(jt.getText());
        }
    }
}
```
**Вывод:**
![[Ex1-FTextArea.png]]

#### Пример 2. Программа для создания JTextArea и задания начального текста, а также добавление кнопок для изменения шрифта текстовой области.

```java
// Java Program  to create a JTextArea and
// set a initial text and add buttons to change
// the font of text area.
import java.awt.event.*;
import java.awt.*;
import javax.swing.*;
class text11 extends JFrame implements ActionListener {
    // JFrame
    static JFrame f;
    // JButton
    static JButton b, b1, b2, b3;
    // label to display text
    static JLabel l, l1;
    // text area
    static JTextArea jt;

    // default constructor
    text11() {
    }

    // main class
    public static void main(String[] args) {
        // create a new frame to store text field and button
        f = new JFrame("textfield");
        f.setDefaultCloseOperation(EXIT_ON_CLOSE);
        // create a label to display text
        l = new JLabel("nothing entered");
        l1 = new JLabel("0 lines");
        // create a new buttons
        b = new JButton("submit");
        b1 = new JButton("plain");
        b2 = new JButton("italic");
        b3 = new JButton("bold");
        // create a object of the text class
        text11 te = new text11();

        // addActionListener to button
        b.addActionListener(te);
        b1.addActionListener(te);
        b2.addActionListener(te);
        b3.addActionListener(te);

        // create a text area, specifying the rows and columns
        jt = new JTextArea("please write something ", 10, 10);
        JPanel p = new JPanel();

        // add the text area and button to panel
        p.add(jt);
        p.add(b);
        p.add(b1);
        p.add(b2);
        p.add(b3);
        p.add(l);
        p.add(l1);

        f.add(p);
        // set the size of frame
        f.setSize(300, 300);
        f.setVisible(true);
    }

    // if the button is pressed
    public void actionPerformed(ActionEvent e) {
        String s = e.getActionCommand();
        if (s.equals("submit")) {
            // set the text of the label to the text of the field
            l.setText(jt.getText() + ", ");
            l1.setText(jt.getLineCount() + " lines");
        }
        else if (s.equals("bold")) {
            // set bold font
            Font f = new Font("Serif", Font.BOLD, 15);
            jt.setFont(f);
        }
        else if (s.equals("italic")) {
            // set italic font
            Font f = new Font("Serif", Font.ITALIC, 15);
            jt.setFont(f);
        }
        else if (s.equals("plain")) {
            // set plain font
            Font f = new Font("Serif", Font.PLAIN, 15);
            jt.setFont(f);
        }
    }
}
```
**Вывод:**
![[Ex2-FTextArea.png]]

#### Пример 3. Использования многострочных полей JTextArea

```java
// Пример использования многострочных полей JTextArea
import javax.swing.*;
import java.awt.Font;

public class Main extends JFrame
{
    public Main() {
        super("Пример JTextArea");
        setDefaultCloseOperation(EXIT_ON_CLOSE);

        // Cоздание многострочных полей
        JTextArea area1 = new JTextArea("Многострочное поле", 8, 10);
        // Шрифт и табуляция
        area1.setFont(new Font("Dialog", Font.PLAIN, 14));
        area1.setTabSize(10);

        JTextArea area2 = new JTextArea(15, 10);
        area2.setText("Второе многострочное поле");
        // Параметры переноса слов
        area2.setLineWrap(true);
        area2.setWrapStyleWord(true);

        // Добавим поля в окно
        JPanel contents = new JPanel();
        contents.add(new JScrollPane(area1));
        contents.add(new JScrollPane(area2));
        setContentPane(contents);

        // Выводим окно на экран
        setSize(400, 300);
        setVisible(true);
    }
    public static void main(String[] args) {
        new Main();
    }
}
```
**Вывод:**
![[Ex3-FTextArea.png]]
В примере создается два многострочных текстовых полей **JTextArea**, для которых были изменены некоторые наиболее часто используемых свойства. Первое текстовое поле создается с помощью конструктора, заполняещего поле текстом и определяющего количество строк и символов. Следует обратить внимание, что количество строк идет в списке параметров перед количеством символов. Задаваемые в конструкторе количество строк и символов поля определяют его размер в контейнере, но не накладывают ограничений на объем вводимого текста. Для первого поля был изменен шрифт и определено нестандартное значение для табуляции вызывом метода _setTabSize()_. Данный метод позволяет указать, какое количество символов пробела будет замещать символ табуляции, вставляемый нажатием клавиши `<Tab>`.

Второе текстовое поле создается с помощью конструктора, которому в качестве параметров передается количество строк и символов. После этого с использованием метода _setText()_ определяется содержимое поля и меняются свойства, управляющие процессом переноса текста на новые строки. По умолчанию текст в поле **JTextArea** не переносится на новую строку. Изменить данное поведение позволяет метод setLineWrap(). Метод setWrapStyleWord() изменяет стиль переноса длинных слов на новые строки. Если вы передадите в этот метод значение true, то слова, не умещающиеся в строке, будут целиком переноситься на новую строку. По умолчанию значение этого свойства равно false. Это означает, что текст переносится, как только ему перестает хватать места в строке, независимо от того, в каком месте слова приходится делать перенос.

Текстовые поля добавляются в панель содержимого окна с использованием полос прокрутки **JScrollPane**. Необходимо отметить, что текстовое поле **JTextArea** не имеет собственной рамки. Полосы прокрутки решают данную проблему.

Обратите внимание на разницу реализации переноса текста в двух компонентах **JTextArea**. Для переноса текста в левом поле приходится вручную нажимать клавишу _Enter_, а в правом поле перенос выполняется автоматически.
