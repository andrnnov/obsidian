#Java #Swing #JToggleButton

## Класс JToggleButton

2024-05-30 15:08

Реализация кнопки с двумя состояниями. Классы [JRadioButton](JRadioButton) и [JCheckBox](JCheckBox) являются подклассами этого класса. **_JToggleButton_** — довольно необычный элемент управления, чаще всего используемый в панелях инструментов, где он играет роль флажков. Фактически, по виду это та же самая кнопка, только ее можно нажать, и она остается в этом состоянии. Можно использовать **_JToggleButton_** и в обычном интерфейсе, когда нужно сделать выбор из двух альтернатив.

### Конструкторы JToggleButton

1. **JToggleButton():** Создана изначально невыбранная кнопка переключения без установки текста или изображения.
2. **JToggleButton(Action a):** Создана кнопка переключения, свойства которой извлекаются из указанного действия.
3. **JToggleButton (Icon icon):** Изначально создана невыбранная кнопка переключения с указанным изображением, но без текста.
4. **JToggleButton (Icon icon, boolean selected):** Создана кнопка переключения с приведенным изображением и выделением состояний, но без текста.
5. **JToggleButton(String text):** Создана невыбранная кнопка переключения с приведенным ниже текстом.
6. **JToggleButton (String text, boolean selected):** Создана кнопка переключения с текстом и состоянием выделения.
7. **JToggleButton (String text, Icon icon):** Создана кнопка переключения с текстом и изображением, которые изначально не выбраны.
8. **JToggleButton (String text, Icon icon, boolean selected):** Создает кнопку переключения с текстом, изображением и выделением состояний.

### Часто используют методы

| Метод                  | Описание                                                                             |
| ---------------------- | ------------------------------------------------------------------------------------ |
| getAccessibleContext() | Получает AccessibleContext, связанный с этим JToggleButton.                          |
| getUIClassID()         | Возвращает строку, определяющую имя класса l&f, отображающего этот компонент.        |
| paramString()          | Возвращает строковое представление этого JToggleButton.                              |
| updateUI()             | Сбрасывает свойство пользовательского интерфейса на значение текущего внешнего вида. |
#### Пример 1. **1. Java-программа для реализации событий JToggleButton с помощью ItemListener.** 

В этой программе мы создаем фрейм с помощью _JFrame()_. Здесь _setDefaultCloseOperation()_ используется для установки параметра закрытия кадра. Используя _JToggleButton(),_ создается кнопка. Создайте экземпляр _ItemListener_, который содержит только метод _itemStateChanged()_ , который автоматически вызывается при нажатии кнопки. Событие генерируется на кнопке и, соответственно, вывод выводится на консоль. Прикрепите все прослушиватели и добавьте _ItemListener_ к кнопке. Добавить кнопку в рамку и задать размер рамки.
```java
import java.awt.BorderLayout;
import java.awt.event.ItemEvent;
import java.awt.event.ItemListener;
import javax.swing.JFrame;
import javax.swing.JToggleButton;

public class Main {
    // Main Method
    public static void main(String args[]) {
        // create a frame and set title
        JFrame frame = new JFrame("Selecting Toggle");
        // set the default close operation of the frame
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        // create a ToggleButton
        JToggleButton toggleButton = new JToggleButton("Toggle Button");
        // ItemListener is notified whenever you click on the Button
        ItemListener itemListener = new ItemListener() {
            // itemStateChanged() method is invoked automatically
            // whenever you click or unclick on the Button.
            public void itemStateChanged(ItemEvent itemEvent) {
                // event is generated in button
                int state = itemEvent.getStateChange();
                // if selected print selected in console
                if (state == ItemEvent.SELECTED) {
                    System.out.println("Selected");
                }
                else {
                    // else print deselected in console
                    System.out.println("Deselected");
                }
            }
        };
        // Attach Listeners
        toggleButton.addItemListener(itemListener);
        frame.add(toggleButton, BorderLayout.SOUTH);
        frame.setSize(300, 125);
        frame.setVisible(true);
    }
}
```
**Вывод:**
![[Ex1-JToggleButton.png]]

#### Пример **2. Программа Java для реализации события JToggleButton с использованием ActionListener

JToggleButton создается в [JFrame](JFrame). Затем мы определяем ActionListener. _actionPerformed()_ — единственный метод в _ActionListener()_, который вызывается при каждом щелчке по зарегистрированному компоненту. _AbstractButton.getModel().isSelected()_ возвращает true, если кнопка выбрана, иначе возвращает false. Прикрепите прослушиватель к ToggleButton.

```java
import java.awt.BorderLayout;  
import java.awt.event.ActionEvent;  
import java.awt.event.ActionListener;  
import javax.swing.AbstractButton;  
import javax.swing.JFrame;  
import javax.swing.JToggleButton;  
  
public class Main {  
    // Main Method  
    public static void main(String args[])  
    {  
        // create the JFrame  
        JFrame frame = new JFrame("Selecting Toggle");  
        // set default close operation for frame  
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);  
        // create a ToggleButton  
        JToggleButton toggleButton = new JToggleButton("Toggle Button");  
        // Define ActionListener  
        ActionListener actionListener = new ActionListener() {  
            // actionPerformed() method is invoked  
            // automatically whenever you click on            // registered component            public void actionPerformed(ActionEvent actionEvent) {  
                AbstractButton abstractButton = (AbstractButton)actionEvent.getSource();  
                // return true or false according  
                // to the selection or deselection                // of the button                boolean selected = abstractButton.getModel().isSelected();  
                System.out.println("Action - selected=" + selected + "\n");  
            }  
        };  
        // Attach Listeners  
        toggleButton.addActionListener(actionListener);  
        // add ToggleButton to the frame  
        frame.add(toggleButton, BorderLayout.NORTH);  
        // set size of the frame  
        frame.setSize(300, 125);  
        frame.setVisible(true);  
    }  
}
```
**Вывод:**
![[Ex2-JToggleButton.png]]
**Вывод в консоли:**
<p style="background-color: navy; color: yellow">
Action - selected=true<br>
Action - selected=false<br>
Process finished with exit code 0</p>
