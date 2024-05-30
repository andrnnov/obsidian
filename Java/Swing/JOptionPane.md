#Java #Swing #JOptionPane

## Диалоговые окна JOptionPane

2024-05-30 11:59

Библиотека [Swing](Swing) включает богатый выбор стандартных диалоговых окон, существенно упрощающих и ускоряющих вывод простой информации типа сообщений о работе программы, ошибках и нестандартных ситуациях. Для вывода в графический интерфейс приложения разнообразной информации и выбора простых данных предназначен класс **JOptionPane**, работа с которым связана с вызовом одного из многочисленных статических методов, создающих и выводящих на экран модальное диалоговое окно стандартного вида. В диалоговых окнах _JOptionPane_ можно выводить самую разнообразную информацию и, при необходимости, размещать в них дополнительные компоненты.

_JOptionPane_ унаследован от базового класса JComponent библиотеки [Swing](Swing), так что можно работать с ним напрямую, т.е. создавать экземпляры класса _JOptionPane_ и настраивать их свойства. Использование стандартных диалоговых окон существенно упрощает разработку приложения и позволяет ускорить процесс освоения пользователем интерфейса.

Все стандартные диалоговые окна [Swing](Swing) имеют собственные UI-представители, отвечающие за интерфейс окна в используемом приложении. Это особенно важно для внешних видов окон, имитирующих известные платформы, пользователи которых не должны ощущать значительной разницы при переходе от «родных» приложений к Java-приложениям.

### Класс JOptionPane

### Поля JOptionPane

| Поля                     | Описание                                                                  |
| ------------------------ | ------------------------------------------------------------------------- |
| int ERROR_MESSAGE        | Постоянный код, отображающий значок сообщения об ошибке.                  |
| int INFORMATION_MESSAGE  | Постоянный код, отображающий значок информационного сообщения.            |
| int WARNING_MESSAGE      | Постоянный код для отображения значка предупреждающего сообщения.         |
| int YES_NO_OPTION        | Константа для создания диалогового окна с параметрами “Yes,” и “No”.      |
| int YES_NO_CANCEL_OPTION | Константа для создания диалогового окна с опциями “Yes,” “No” и “Cancel”. |
| int OK_CANCEL_OPTION     | Константа для создания диалогового окна с опциями “OK” and “Cancel”.      |

### Конструкторы

| Конструктор                                                                                                    | Описание                                                                                                                                                               |
| -------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| JOptionPane()                                                                                                  | Создает JOptionPane с тестовым сообщением.                                                                                                                             |
| JOptionPane(Object message)                                                                                    | Создает экземпляр JOptionPane для отображения сообщения, используя тип сообщения plain-message и параметры по умолчанию, предоставляемые пользовательским интерфейсом. |
| JOptionPane(Object message, int messageType)                                                                   | Создает экземпляр JOptionPane для отображения сообщения с указанным типом сообщения и параметрами по умолчанию                                                         |
| JOptionPane(Object message, int messageType, int optionType)                                                   | Создает экземпляр JOptionPane для отображения сообщения с указанным типом сообщения и параметрами.                                                                     |
| JOptionPane(Object message, int messageType, int optionType, Icon icon)                                        | Создает экземпляр JOptionPane для отображения сообщения с указанным типом сообщения, параметрами и значком.                                                            |
| JOptionPane(Object message, int messageType, int optionType, Icon icon, Object[] options)                      | Создает экземпляр JOptionPane для отображения сообщения с указанным типом сообщения, значком и параметрами.                                                            |
| JOptionPane(Object message, int messageType, int optionType, Icon icon, Object[] options, Object initialValue) | Создает экземпляр JOptionPane для отображения сообщения с указанным типом сообщения, значком и параметрами, при этом указывается изначально выбранный параметр.        |

### Основные диалоговые методы JOptionPane

| Наименование метода | Описание                                                              |
| ------------------- | --------------------------------------------------------------------- |
| showMessageDialog   | Диалоговое окно вывода сообщения                                      |
| showConfirmDialog   | Диалоговое окно подтверждения, с включением кнопок типа yes/no/cancel |
| showInputDialog     | Диалоговое окно с выбором                                             |

## Методы JOptionPane

| Методы                                                       | Описание                                                                                                       |
| ------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------- |
| createDialog(String title)                                   | Это помогает нам создать [JDialog](JDialog) с указанным заголовком, но без родительского элемента.             |
| showMessageDialog(Component parentComponent, Object message) | Этот метод отображает диалоговое окно сообщения с указанным сообщением.                                        |
| showInputDialog(Component parentComponent, Object message)   | Этот метод отображает диалоговое окно ввода с указанным сообщением.                                            |
| setMessageType(int MessageType)                              | Этот метод для установки типа сообщения диалогового окна                                                       |
| setOptionType (int optionType)                               | Этот метод позволяет вам установить тип опции для диалога.                                                     |
| setOptions(Object[] options)                                 | Здесь мы можем установить список пользовательских опций.                                                       |
| setInitialValue(Object initialValue)                         | Этот метод устанавливает первоначальный выбор при использовании пользовательских параметров в диалоговом окне. |

#### Конструкторы окна сообщений showMessageDialog

```java
// Простое диалоговое окно с заголовком «Message»
public static void showMessageDialog(Component parent,
                                     Object message) 
                                            throws HeadlessException
// Диалоговое окно с заголовком и типом сообщения
public static void showMessageDialog(Component parent,
                                     Object message, 
                                     String title,
                                     int messageType) 
                                            throws HeadlessException
// Диалоговое окно с заголовком, типом сообщения и иконкой
public static void showMessageDialog(Component parent,
                                     Object message,
                                     String title,
                                     int messageType,
                                     Icon icon)
                                            throws HeadlessException
```

#### Конструкторы окна подтверждения showConfirmDialog

```java
// Простое диалоговое окно подтверждения с кнопками Yes, No, Cancel и
// с заголовком «Select an Option»
public static void showConfirmDialog(Component parent,
                                     Object message) 
                                         throws HeadlessException
// Окно подтверждения с заголовком и кнопками, определенными 
// опцией optionType
public static void showConfirmDialog(Component parent, 
                                     Object message, 
                                     String title, 
                                     int optionType) 
                                         throws HeadlessException
// Окно подтверждения с заголовком, кнопками, определенными 
// опцией optionType, и иконкой
public static void showConfirmDialog(Component parent, 
                                     Object message,
                                     String title,
                                     int optionType,
                                     Icon icon) 
                                         throws HeadlessException
```

#### Конструкторы окна выбора showInputDialog

```java
// Диалоговое окно с полем ввода
public static void showInputDialog(Component parent,
                                   Object message) 
                                          throws HeadlessException
// Диалоговое окно с полем ввода, инициализируемое initialSelectionValue
public static void showInputDialog(Component parent, 
                                   Object message, 
                                   Object initialSelectionValue) 
                                          throws HeadlessException
// Диалоговое окно с полем выбора из списка selectionValues
public static void showInputDialog(Component parent, 
                                   Object message,
                                   String title, 
                                   int messageType,
                                   Icon icon,  
                                   Object[] selectionValues,
                                   Object initialSelectionValue) 
                                          throws HeadlessException
```
Параметры:
- parent - родительское окно.
- message - отображаемый в окне текст сообщения. В большинстве случаев это строка, но может быть использован массив строк String[], компонент Component, иконка Icon, представленная меткой JLabel, объект Object, конвертируемый в строку методом toString().
- title - заголовок окна.
- messageType - тип диалогового окна:
	- INFORMATION_MESSAGE - стандартное диалоговое окно для вывода информации со значком соответствующего вида;
	-  WARNING_MESSAGE - стандартное диалоговое окно для вывода предупреждающей информации со значком соответствующего вида;
	- QUESTION_MESSAGE - стандартное диалоговое окно для вывода информации. Как правило, не используется для информационных сообщений;
	- ERROR_MESSAGE - стандартное диалоговое окно для вывода информации об ошибке со значком соответствующего вида;
	- PLAIN_MESSAGE - стандартное диалоговое окно для вывода информации без значка.
- optionType - опция определения кнопок управления:
	- DEFAULT_OPTION
	- YES_NO_OPTION
	- YES_NO_CANCEL_OPTION
	- OK_CANCEL_OPTION
- selectionValues - список возможных значений. В диалоговом окне InputDialog список будет представлен в компоненте JComboBox или JList. Если selectionValues = null, то в окне будет определено поле JTextField, в которое пользователь может ввести любое значение.
- initialSelectionValue - инициализируемое значение.
- icon - отображаемая в диалоговом окне иконка.

#### Локализация кнопок JOptionPane

Кнопки управления, как правило, имеют заголовки «Yes», «No», «Cancel». Для локализации кнопок диалогового компонента _JOptionPane_ можно использовать _UIManager_ следующим образом :
```java
UIManager.put("OptionPane.yesButtonText"   , "Да"    );
UIManager.put("OptionPane.noButtonText"    , "Нет"   );
UIManager.put("OptionPane.cancelButtonText", "Отмена");
UIManager.put("OptionPane.okButtonText"    , "Готово");
```

#### Пример 1. Java-программа для создания showMessageDialog в JOptionPane

Это диалоговое окно используется для отображения сообщений пользователю.
```java
//Java program to create a showMessageDialog in JOptionPane 
import javax.swing.JOptionPane;

public class Main {
    public static void main(String[] args) {
        // Create a JOptionPane to display a message dialog 
        // The first parameter (null) specifies the dialog's parent component (usually the main frame) 
        // The second parameter is the message to display ("Example" in this case)
        // The third parameter is the title of the dialog ("Example JOptionPane")
        // The fourth parameter (JOptionPane.INFORMATION_MESSAGE) specifies the message type (information icon) 
        JOptionPane.showMessageDialog(null, "Example", "Example JOptionPane",
                JOptionPane.INFORMATION_MESSAGE);
    }
} 
```
**Вывод:**
![[Ex1-JOptionPane.png]]

#### Пример 2. Java-программа для создания showInputDialog в JOptionPane

Это диалоговое окно используется для получения входных данных от пользователя.

```java
//Java Program to create a showInputDialog in JOptionPane
import javax.swing.JOptionPane;

public class Main {
    public static void main(String[] args) {
        // Prompt the user to enter their article name and store it in the 'name' variable
        String name = JOptionPane.showInputDialog("Enter your Article Name:");

        // Create a JOptionPane to display a message with a personalized greeting

        JOptionPane.showMessageDialog(null, "Example " + name + "!");
    }
} 
```
**Вывод:**
![[Ex2_1-JOptionPane.png]]
**Окончательный вывод после выбора:**
![[Ex2_2-JOptionPane.png]]

#### Пример 3. Java-программа для создания showConfirmDialog в JOptionPane

В этом диалоговом окне отображается сообщение с подтверждением и пользователь может принять решение.
```java
//Java Program to create showConfirmDialog in JOptionPane
import javax.swing.JOptionPane;

public class Main {
    public static void main(String[] args) {
        // Display a confirmation dialog with Yes, No, and Cancel options
        int choice = JOptionPane.showConfirmDialog(null, "Do you want to save changes?",
                "Confirmation", JOptionPane.YES_NO_CANCEL_OPTION);

        // Check the user's choice and display a corresponding message
        if (choice == JOptionPane.YES_OPTION) {
            // If the user chose 'Yes', show a message indicating that changes are saved
            JOptionPane.showMessageDialog(null, "Changes saved.");
        } else if (choice == JOptionPane.NO_OPTION) {
            // If the user chose 'No', show a message indicating that changes are not saved
            JOptionPane.showMessageDialog(null, "Changes not saved.");
        } else {
            // If the user chose 'Cancel' or closed the dialog, show a message indicating the operation is canceled
            JOptionPane.showMessageDialog(null, "Operation canceled.");
        }
    }
} 
```
**Вывод:**
![[Ex3_1-JOptionPane.png]]
**Окончательный вывод после выбора:**
![[Ex3_2-JOptionPane.png]]

#### Пример 4. Java-программа для создания showOptionDialog в JOptionPane

Это диалоговое окно позволяет вам создать настраиваемое диалоговое окно выбора.
```java
// Java Program to create a
// showOptionDialog in JOptionPane
import javax.swing.JOptionPane;

// Driver Class
public class Main {
    // main function
    public static void main(String[] args)
    {
        // Define an array of custom options for the dialog
        Object[] options = { "Yes", "No", "Cancel" };

        // Display an option dialog with custom options
        // The user's choice is stored in the 'choice'
        // variable
        int choice = JOptionPane.showOptionDialog(
                null, // Parent component (null means center on screen)
                "Do you want to proceed?", // Message to display
                "Custom Options", // Dialog title
                JOptionPane.YES_NO_CANCEL_OPTION, // Option type (Yes, No, Cancel)
                JOptionPane.QUESTION_MESSAGE, // Message type (question icon)
                null, // Custom icon (null means no custom icon)
                options, // Custom options array
                options[2] // Initial selection (default is "Cancel")
        );

        // Check the user's choice and display a
        // corresponding message
        if (choice == JOptionPane.YES_OPTION) {
            // If the user chose 'Yes'
            // show a message indicating that they are
            // proceeding
            JOptionPane.showMessageDialog(null,"Proceeding...");
        }
        else if (choice == JOptionPane.NO_OPTION) {
            // If the user chose 'No'
            // show a message indicating that they are not
            // proceeding
            JOptionPane.showMessageDialog(null, "Not proceeding.");
        }
        else {
            // If the user chose 'Cancel' or closed the
            // dialog
            // show a message indicating the operation is
            // canceled
            JOptionPane.showMessageDialog(null, "Operation canceled.");
        }
    }
}
```
**Вывод:**
![[Ex4_1-JOptionPane.png]]
**Окончательный вывод после выбора:**
![[Ex4_2-JOptionPane.png]]

