#Java #Swing #JButton

## Класс JButton

2024-05-14 11:13

Класс **_JButton_** является реализацией кнопки. Этот компонент имеет метку и генерирует событие при нажатии. Он также может иметь изображение.
Объявление класса **_javax.swing.JButton_**:
```java
public class JButton extends AbstractButton implements Accessible
```

### Конструкторы класса

| №   | Конструктор и описание                                                                          |
| --- | ----------------------------------------------------------------------------------------------- |
| 1   | **JButton()**<br>Создает кнопку без установленного текста или значка.                           |
| 2   | **JButton(Action a)**<br>Создает кнопку, свойства которой берутся из предоставленного действия. |
| 3   | **JButton (Icon icon)**<br>Создает кнопку со значком.                                           |
| 4   | **JButton(String text)**<br>Создает кнопку с текстом.                                           |
| 5   | **JButton(String text, Icon icon)**<br>Создает кнопку с начальным текстом и значком.            |

### Методы класса 

Класс **_JButton_** наследует методы от следующих классов:
- javax.swing.AbstractButton
- javax.swing.JComponent
- java.awt.Container
- java.awt.Component
- java.lang.Object

Распространенные методы, используемые для JButton:
- **void setText(String s):** устанавливает предоставленный текст в созданную кнопку.
- **String getText():** Возвращает текст на кнопке.
- **void setAction(Action a):** Устанавливает свойства кнопки в соответствии с предоставленным действием.
- **Action getAction():** Возвращает свойства кнопки, относящиеся к представленному в ней действию.
- **void setIcon (Icon i):** Задает значок или изображение, которое отображается на кнопке, когда она не нажата. Чтобы установить значок для нажатой кнопки, используйте void setPressedIcon (Icon i)
- **Icon getIcon():** Кнопка отображает значок, когда она не нажата или не выбрана. Чтобы получить значок от нажатой или выбранной кнопки, используйте Icon getPressedIcon().
- **void addActionListener(ActionListener a):** Добавляет объекты, которые прослушивают события действия, генерируемые кнопкой.
- **ActionListener removeActionListener():** Удаляет объекты, которые прослушивают события действия, генерируемые кнопкой.
- **void addItemListener(ItemListener a):** Добавляет объекты, которые прослушивают события элемента, генерируемые кнопкой.
- **ItemListener removeItemListener():** Удаляет объекты, которые прослушивают события элемента, генерируемые кнопкой.
- **void setSelected(boolean):** переводит кнопку в режим выбора или нажатия.
- boolean isSelected():** мы получаем значение кнопки, независимо от того, выбрано оно или нет. AbstractButton предоставляет методы для выравнивания положения значка и текста на кнопке.
- **void setHorizontalAlignment(int alignment):** Устанавливает горизонтальное выравнивание значка и текста. AbstractButton по умолчанию использует SwingConstants.CENTER. Некоторые другие настройки, которые могут быть предоставлены: SwingConstants.RIGHT, SwingConstants.LEFT, SwingConstants.LEADING, SwingConstants.TRAILING.
- **void setVerticalAlignment(int alignment):** - Устанавливает вертикальное выравнивание значков и текста. Некоторые другие настройки, которые могут быть предоставлены: SwingConstants.TOP, SwingConstants.BOTTOM, SwingConstants.CENTER(default).
- **int getHorizontalAlignment():** возвращает выравнивание значка и текста по горизонтали.
- **int getVerticalAlignment():** возвращает выравнивание значка и текста по вертикали.
- **void setHorizontalTextPosition(int)** и **void setVerticalTextPosition(int):** Используются для установки горизонтального и вертикального положения кнопки.
- **int getHorizontalTextPosition() и int getVerticalTextPosition():** Мы получили горизонтальное и вертикальное положение кнопки.

#### Пример 1. Применение JButton

```java
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;
 
public class SwingControlDemo {
   private JFrame mainFrame;
   private JLabel headerLabel;
   private JLabel statusLabel;
   private JPanel controlPanel;

   public SwingControlDemo(){
      prepareGUI();
   }
   public static void main(String[] args){
      SwingControlDemo  swingControlDemo = new SwingControlDemo();      
      swingControlDemo.showButtonDemo();
   }
   private void prepareGUI(){
      mainFrame = new JFrame("Java Swing Examples");
      mainFrame.setSize(400,400);
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
   private static ImageIcon createImageIcon(String path, String description) {
      java.net.URL imgURL = SwingControlDemo.class.getResource(path);
      if (imgURL != null) {
         return new ImageIcon(imgURL, description);
      } else {            
         System.err.println("Couldn't find file: " + path);
         return null;
      }
   }   
   private void showButtonDemo(){
      headerLabel.setText("Control in action: Button"); 

      //resources folder should be inside SWING folder.
      ImageIcon icon = createImageIcon("/resources/icon.png","Java");

      JButton okButton = new JButton("OK");        
      JButton javaButton = new JButton("Submit", icon);
      JButton cancelButton = new JButton("Cancel", icon);
      cancelButton.setHorizontalTextPosition(SwingConstants.LEFT);   

      okButton.addActionListener(new ActionListener() {
         public void actionPerformed(ActionEvent e) {
            statusLabel.setText("Ok Button clicked.");
         }          
      });
      javaButton.addActionListener(new ActionListener() {
         public void actionPerformed(ActionEvent e) {
            statusLabel.setText("Submit Button clicked.");
         }
      });
      cancelButton.addActionListener(new ActionListener() {
         public void actionPerformed(ActionEvent e) {
            statusLabel.setText("Cancel Button clicked.");
         }
      });
      controlPanel.add(okButton);
      controlPanel.add(javaButton);
      controlPanel.add(cancelButton);       

      mainFrame.setVisible(true);  
   }
}
```
**Вывод:**
![[Ex1-JButton.png]]

