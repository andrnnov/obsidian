#Java #Swing #JTextField

## Класс JTextField

2024-06-04 15:51

Класс **_JTextField_** является частью пакета javax.swing. **_JTextField_** — это компонент, позволяющий редактировать одну строку текста. **_JTextField_** наследует класс JTextComponent и использует интерфейс SwingConstants.

### Конструкторs класса 
 
1. **JTextField()**: конструктор, создающий новое TextField.
2. **JTextField(int columns)**: конструктор, создающий новый пустой **_TextField_** с указанным количеством столбцов.
3. **JTextField(String text)**: конструктор, который создает новое пустое текстовое поле, инициализированное заданной строкой.
4. **JTextField(String text, int columns): конструктор, который создает новый пустой textField с заданной строкой и указанным количеством столбцов.
5. **JTextField(Document doc, String text, int columns)**: конструктор, создающий текстовое поле, использующее заданную модель хранения текста и заданное количество столбцов.

### Методы JTextField

| N   | Методы и описание                                                                                                                                                                                                                          |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1   | **protected void actionPropertyChanged(Action action, String propertyName)**<br>Обновляет состояние текстового поля в ответ на изменения свойств в соответствующем действии.                                                               |
| 2   | **void addActionListener(ActionListener l)**<br>Добавляет указанный прослушиватель действий для получения событий действий из этого текстового поля.                                                                                       |
| 3   | **protected void configurePropertiesFromAction(Action a)**<br>Устанавливает свойства этого текстового поля в соответствии со свойствами указанного действия.                                                                               |
| 4   | **protected PropertyChangeListener createActionPropertyChangeListener(Action a)**<br>Создает и возвращает PropertyChangeListener, который отвечает за прослушивание изменений от указанного действия и обновление соответствующих свойств. |
| 5   | **protected Document createDefaultModel()**<br>Создает реализацию модели по умолчанию, которая будет использоваться при построении, если она явно не задана.                                                                               |
| 6   | **protected void fireActionPerformed()**<br>Уведомляет всех слушателей, которые зарегистрировали интерес к уведомлению об этом типе события.                                                                                               |
| 7   | **AccessibleContext getAccessibleContext()**<br>Получает AccessibleContext, связанный с этим JTextField.                                                                                                                                   |
| 8   | **Action getAction()**<br>Возвращает текущее установленное действие для этого источника ActionEvent или null, если действие не задано.                                                                                                     |
| 9   | **ActionListener[] getActionListeners()**<br>Возвращает массив всех ActionListeners, добавленных в это JTextField с помощью addActionListener().                                                                                           |
| 10  | **Action[] getActions()**<br>Извлекает список команд для редактора.                                                                                                                                                                        |
| 11  | **int getColumns()**<br>Возвращает количество столбцов в этом текстовом поле.                                                                                                                                                              |
| 12  | **protected int getColumnWidth()**<br>Возвращает ширину столбца.                                                                                                                                                                           |
| 13  | **int getHorizontalAlignment()**<br>Возвращает выравнивание текста по горизонтали.                                                                                                                                                         |
| 14  | **BoundedRangeModel getHorizontalVisibility()**<br>Обеспечивает видимость текстового поля.                                                                                                                                                 |
| 15  | **Dimension getPreferredSize()**<br>Возвращает предпочтительный размер, необходимый для этого текстового поля.                                                                                                                             |
| 16  | **int getScrollOffset()**<br>Возвращает смещение прокрутки в пикселях.                                                                                                                                                                     |
| 17  | **String getUIClassID()**<br>Получает идентификатор класса для пользовательского интерфейса.                                                                                                                                               |
| 18  | **boolean isValidateRoot()**<br>Вызовы revalidate, исходящие из самого текстового поля, будут обрабатываться путем проверки текстового поля, если только текстовое поле не содержится в JViewport , и в этом случае это возвращает false . |
| 19  | **protected String paramString()**<br>Возвращает строковое представление этого JTextField.                                                                                                                                                 |
| 20  | **void postActionEvent()**<br>Обрабатывает события action, происходящие в этом текстовом поле, отправляя их любым зарегистрированным объектам ActionListener.                                                                              |
| 21  | **void removeActionListener(ActionListener l)**<br>Удаляет указанный прослушиватель действий, так что он больше не получает события действий из этого текстового поля.                                                                     |
| 22  | **void scrollRectToVisible(Rectangle r)**<br>Прокручивает поле влево или вправо.                                                                                                                                                           |
| 23  | **void setAction(Action a)**<br>Задает действие для источника ActionEvent.                                                                                                                                                                 |
| 24  | **void setActionCommand(String command)**<br>Задает командную строку, используемую для событий action.                                                                                                                                     |
| 25  | **void setColumns(int columns)**<br>Устанавливает количество столбцов в этом текстовом поле, а затем делает макет недействительным.                                                                                                        |
| 26  | **void setDocument(Document doc)**<br>Связывает редактор с текстовым документом.                                                                                                                                                           |
| 27  | **void setFont(Font f)**<br>установите шрифт текста, отображаемого в текстовом поле.                                                                                                                                                       |
| 28  | **void setHorizontalAlignment(int alignment)**<br>Задает выравнивание текста по горизонтали.                                                                                                                                               |
| 29  | **void setScrollOffset(int scrollOffset)**<br>Задает смещение прокрутки в пикселях.                                                                                                                                                        |

#### Пример 1. Программа для создания пустого текстового поля с определенным количеством столбцов

```java
/ Java program to create a blank text
// field of definite number of columns.
import java.awt.event.*;
import javax.swing.*;
class text extends JFrame implements ActionListener {
    // JTextField
    static JTextField t;
    // JFrame
    static JFrame f;
    // JButton
    static JButton b;
    // label to display text
    static JLabel l;
    // default constructor
    text() { }

    // main class
    public static void main(String[] args) {
    // create a new frame to store text field and button
        f = new JFrame("textfield");
        f.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        // create a label to display text
        l = new JLabel("nothing entered");
        // create a new button
        b = new JButton("submit");
        // create a object of the text class
        text te = new text();
        // addActionListener to button
        b.addActionListener(te);
        // create a object of JTextField with 16 columns
        t = new JTextField(16);
        // create a panel to add buttons and textfield
        JPanel p = new JPanel();

        // add buttons and textfield to panel
        p.add(t);
        p.add(b);
        p.add(l);

        // add panel to frame
        f.add(p);

        // set the size of frame
        f.setSize(300, 200);
        f.setVisible(true);
    }

    // if the button is pressed
    public void actionPerformed(ActionEvent e) {
        String s = e.getActionCommand();
        if (s.equals("submit")) {
            // set the text of the label to the text of the field
            l.setText(t.getText());
            // set the text of field to blank
            t.setText("  ");
        }
    }
}
```
**Вывод:**
![[Ex1-JTextField.png]]

Текстовое поле **_JTextField_** является самым простым компонентом и наиболее часто встречающимся в пользовательских интерфейсах. Как правило, поле является однострочным и служит для ввода текста. В библиотеке [Swing](Swing) имеется два текстовых поля. Первое, представленное классом _JTextField_, позволяет вводить однострочный текст. Второе поле, реализованное классом **JPasswordField** и унаследованное от поля **_JTextField_**, дает возможность организовать ввод «закрытой» информации (чаще всего паролей), которая не должна напрямую отображаться на экране.

Оба текстовых поля **_JTextField_, JPasswordField** просты. Работа с ними чаще всего сводится к заданию количества отображаемых в поле символов и начального текста, если таковой требуется. После чего остается только поместить поле в контейнер и в нужный момент получить из него набранный пользователем текст.

#### Пример 2. Использование текстовых полей JTextField

```java
/// Использование текстовых полей JTextField  
import javax.swing.*;  
  
import java.awt.Font;  
import java.awt.event.*;  
import java.awt.FlowLayout;  
  
public class Main extends JFrame {  
    // Текстовые поля  
    JTextField smallField, bigField;  
  
    public Main() {  
        super("Текстовые поля");  
        setDefaultCloseOperation(EXIT_ON_CLOSE);  
        // Создание текстовых полей  
        smallField = new JTextField(15);  
        smallField.setToolTipText("Короткое поле");  
        bigField = new JTextField("Текст поля", 25);  
        bigField.setToolTipText("Длиное поле");  
        // Настройка шрифта  
        bigField.setFont(new Font("Dialog", Font.PLAIN, 14));  
        bigField.setHorizontalAlignment(JTextField.RIGHT);  
        // Слушатель окончания ввода  
        smallField.addActionListener(new ActionListener() {  
            public void actionPerformed(ActionEvent e) {  
                // Отображение введенного текста  
                JOptionPane.showMessageDialog(Main.this,  
                        "Ваше слово: " + smallField.getText());  
            }  
        });  
        // Поле с паролем  
        JPasswordField password = new JPasswordField(12);  
        password.setEchoChar('*');  
        // Создание панели с текстовыми полями  
        JPanel contents = new JPanel(new FlowLayout(FlowLayout.LEFT));  
        contents.add(smallField);  
        contents.add(bigField  );  
        contents.add(password  );  
        setContentPane(contents);  
        // Определяем размер окна и выводим его на экран  
        setSize(400, 130);  
        setVisible(true);  
    }  
    public static void main(String[] args) {  
        new Main();  
    }  
}
```
**Вывод:**
![[Ex2-JTextField.png]]
В примере создается окно с несколькими текстовыми полями. Первое поле создается с помощью конструктора класса **_JTextField_**, которому передается максимальное количество символов в поле. Для однострочных текстовых полей прокрутка не нужна, и размер поля в символах должен примерно соответствовать объему информации, которую пользователь вводит в поле. Второе поле создается более функциональным конструктором: ему передается текст, который будет записан в поле, и максимальное количество символов. Далее определяется шрифт и вариант выравнивания текста в поле. По умолчанию текст выравнивается по левому краю, в примере - по правому краю.

К текстовому полю можно присоединить слушателя событий **ActionListener**. Такие слушатели оповещаются о нажатии пользователем специальной клавиши, сигнализирующей об окончании ввода. Обычно это клавиша Enter. Использовать слушателя особенно удобно в случае текстовых полей, предназначенных для ввода важной информации. Присоединение к полю слушателя _ActionListener_ позволяет ускорить процесс работы с интерфейсом, избавляя пользователя от необходимости по окончании ввода данных щелкать на подтверждающих кнопках подобных кнопке ОК. Помимо прямого присоединения к полю слушателя ActionListener можно также воспользоваться методом setAction(), присоединяющего к полю объект-команду Action. Применение этого метода не удаляет уже присоединенных к полю слушателей, все они также будут оповещаться о завершении ввода.

В примере также используется поле для ввода «закрытых» данных **JPasswordField**. Это поле унаследовано от обычного поля JTextField. Из собственных методов поля JPasswordField можно упомянуть лишь метод _setEchoChar()_, служащий для смены символа-заменителя. По умолчанию в качестве такого символа используется звездочка '*'. Разработчики класса JPasswordField не рекомендуют применять для получения введенного в поле значения (пароля) обычный метод getText(). Дело в том, что создаваемая данным методом строка String может кэшироваться (объекты String в Java максимально оптимизируются компилятором и виртуальной машиной), и злоумышленник сможет похитить ваш пароль сканированием памяти приложения. Для получения данных предоставляется более безопасный метод getPassword(), возвращающий массив символов char, значения которого после проверки имеет смысл обнулить и при желании вызвать [сборщик мусора](GarbageCollection). Поле JPasswordField особым образом копирует данные в буфер обмена — оно переопределяет методы cut() и сору(), определенные в базовом классе JTextComponent, запрещая копировать набранный текст в буфер обмена.

Метод setToolTipText() позволяет для каждого поля установить всплывающую "подсказку".

### Свойства текстовых полей

| Свойства и методы get/set            | Описание                                                                                                                       |
| ------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------ |
| text                                 | Чтение введенного в поле текста или его замена. Для поля с конфиденциальной информацией лучше использовать метод getPassword() |
| columns                              | Определение количества символов в поле; можно получить размер поля или изменить его                                            |
| font                                 | Определение используемого в текстовом поле шрифта.                                                                             |
| horizontalAlignment                  | Управление выравниванием текста в поле. По умолчанию текст выравнивается по левой границе поля.                                |
| echoChar (только для JPasswordField) | Определение символа-заменителя для ввода закрытой информации. По умолчанию используется символ звездочки (*)                   |

#### Пример 3

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
        swingControlDemo.showTextFieldDemo();
    }
    private void prepareGUI(){
        mainFrame = new JFrame("Java Swing Examples");
        mainFrame.setSize(400,300);
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
    private void showTextFieldDemo(){
        headerLabel.setText("Control in action: JTextField");

        JLabel  namelabel= new JLabel("User ID: ", JLabel.RIGHT);
        JLabel  passwordLabel = new JLabel("Password: ", JLabel.CENTER);
        final JTextField userText = new JTextField(6);
        final JPasswordField passwordText = new JPasswordField(6);

        JButton loginButton = new JButton("Login");
        loginButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                String data = "Username " + userText.getText();
                data += ", Password: " + new String(passwordText.getPassword());
                statusLabel.setText(data);
            }
        });
        controlPanel.add(namelabel);
        controlPanel.add(userText);
        controlPanel.add(passwordLabel);
        controlPanel.add(passwordText);
        controlPanel.add(loginButton);
        mainFrame.setVisible(true);
    }
}
```
**Вывод:**
![[Ex3-JTextField.png]]