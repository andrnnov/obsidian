#Java #awt #Component #Font

## Шрифты, доступные в Java [AWT](AWT)

2024-05-21 15:37

Шрифт предоставляет информацию, необходимую для сопоставления последовательностей символов с последовательностями глифов и для отображения последовательностей глифов на объектах **[Graphics](Graphics)** и **[Component](Component)**. Глиф - это форма, используемая для отображения символа или последовательности символов.

### Константы

Для отображения шрифтов в Java существует четыре стиля: обычный, жирный, курсивный и bold italic.

Три константы класса используются для представления стилей шрифтов:
 - _public static final int BOLD_ - константа представляет собой шрифт, выделенный жирным шрифтом.
- _public static final int ITALIC_- константа ITALIC представляет курсивный шрифт.
- _public static final int PLAIN_ - константа PLAIN представляет обычный шрифт.

## Конструкторы

Для шрифта существует единый конструктор. 

public Font (String name, int style, int size) 

```java
setFont(new Font("TimesRoman", Font.BOLD | Font.ITALIC, 20));
```
Для него требуется название, стиль и размер. Имя представляет собой название создаваемого шрифта без учета регистра.

### Методы

**_public String getName()_**

Метод getName() возвращает логическое имя шрифта. Это имя, передаваемое конструктору для конкретного экземпляра шрифта. Помните, что системные свойства могут использоваться для псевдонимов имен шрифтов, поэтому имя, используемое в конструкторе, не обязательно является фактическим именем шрифта в системе.

**_public String getFamily()_**

Метод getFamily() возвращает фактическое название шрифта, который используется для отображения символов. Если шрифту присвоен псевдоним другого шрифта, метод getFamily() возвращает имя шрифта, зависящего от платформы, а не псевдоним. Например, если конструктором был `new Font ("AvantGarde", Font.PLAIN, 10)` и свойство `awt.font.avantgarde=Helvetica` установлено, затем getName() возвращает AvantGarde, а getFamily(), возвращает Helvetica. Если свойство никто не задавал, оба метода возвращают AvantGarde, и система использует шрифт по умолчанию (поскольку AvantGarde - нестандартный шрифт).

**_public int getStyle()_**

Метод getStyle() возвращает текущий стиль шрифта в виде целого числа. Сравните это значение с константами Font.BOLD, Font.PLAIN и Font.ITALIC, чтобы увидеть, какой стиль имеется в виду. Для определения текущего стиля проще использовать методы isPlain(), isBold() и isItalic(). Функция getStyle() полезнее, если вы хотите скопировать стиль какого-либо шрифта при создании другого.

**_public int getSize()_**

Метод getSize() извлекает размер шрифта в виде точки, установленный параметром size в конструкторе. Фактический отображаемый размер может отличаться.

**_public boolean isPlain()_**

Метод isPlain() возвращает true, если текущий шрифт не является ни жирным, ни курсивным. В противном случае он возвращает false.

**_public boolean isBold()_**

Метод isBold() возвращает true, если текущий шрифт либо выделен жирным шрифтом, либо жирным шрифтом и курсивом. В противном случае возвращается false.

**_public boolean isItalic()_**

Метод isItalic() возвращает true, если текущий шрифт либо курсивный, либо жирный и выделенный курсивом. В противном случае возвращается false.

**_public static Font getFont(String name)_**

Метод getFont() получает шрифт, указанный в системном свойстве name. Если name не является допустимым системным свойством, возвращается null. Этот метод реализуется вызовом следующей версии getFont(), для параметра DefaultFont установлено значение null.

**_public static Font getFont(String name, Font defaultFont)_**

Метод getFont() получает шрифт, указанный в системном свойстве name. Если name не является допустимым системным свойством, эта версия getFont() возвращает шрифт, указанный в DefaultFont. Эта версия позволяет вам указывать значения по умолчанию в случае, если пользователь не желает предоставлять свои собственные настройки шрифта.

#### Пример 1. Пример показывает как пользоваться Font 
```java
import java.awt.Color;  
import java.awt.Font;  
  
import javax.swing.JFrame;  
import javax.swing.JLabel;  
  
public class Main {  
    public static void main(String[] args) {  
        JFrame frame = new JFrame("JLabel Test");  
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);  
        JLabel label = new JLabel("First Name");  
        label.setFont(new Font("Courier New", Font.ITALIC, 18));  
        label.setForeground(Color.RED);  
  
        frame.add(label); 
        frame.pack();  
        frame.setVisible(true);  
    }  
}
```
**Вывод:**
![[Ex1-Font.png]]

#### Пример 2. Программа для получения названий семейств шрифтов в AWT

Используя _**getAvailableFontFamilyNames()**_, вы можете получить массив всех доступных шрифтов в AWT, которые были отображены на консоли.
```java
// Java Program to extract the list of Fonts  
import java.awt.*;  
  
// Driver class to check available Fonts in AWT  
class Main {  
    // Main Function  
    public static void main(String[] args) {  
        System.out.println("To Know the available font family names");  
        GraphicsEnvironment ge = raphicsEnvironment.getLocalGraphicsEnvironment();    
        System.out.println("Getting the font family names");  
        // Array of all the fonts available in AWT  
        String fonts[] = ge.getAvailableFontFamilyNames();  
  
        // Getting the font family names  
        for (String i : fonts) {  
            System.out.println(i + " ");  
        }  
    }  
}
```
**Пояснение к вышеуказанной программе:**
- Использование экземпляра _**GraphicsEnvironment.getLocalGraphicsEnvironment().**_
- Извлечение массива доступных шрифтов в String fonts[] с помощью _**getAvailableFontFamilyNames()**_.

**Вывод:**
![[Ex2-Font.png]]

#### Пример 3. Использование класса шрифта с помощью названий семейств шрифтов в AWT

```java
// Java program to test  
// Custom available font in AWT  
import java.awt.*;  
import java.awt.Color;  
import java.awt.event.WindowAdapter;  
import java.awt.event.WindowEvent;  
  
public class Main extends Frame {  
    //class to close the AWT frame  
    Main(){  
        // To close the AWT frame we use the WindowAdapter class  
        this.addWindowListener(new WindowAdapter() {  
            public void windowClosing(WindowEvent we) {  
                System.exit(0);  
            }  
        });  
    }  
  
    // Here to draw the string we use the  
    // Graphics class in java    
    public void paint(Graphics g){  
        g.setColor(Color.GREEN);  
        // Algerian font family is present in the above  
        // mentioned program output        
        g.setFont(new Font("Algerian", Font.BOLD, 50));  
        g.drawString("Example", 100, 100);  
    }  
  
    //Main Method  
    public static void main(String args[]){  
        Main obj = new Main();  
        obj.setTitle("GeeksForGeeks");  
        obj.setSize(400, 150);  
        obj.setVisible(true);  
    }  
}
```
**Пояснение к вышеуказанной программе:**
- _**Main obj**_ для создания макета окна для отображения данных.
- Установите различные параметры, такие как заголовок, размер, видимость и т. д.
- _**Paint()**_ для создания графики текста «Example».

**Вывод:**
![[Ex3-Font.png]]

