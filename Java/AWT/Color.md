#Java #awt #Color

## Работа с цветом. Класс Color

2024-05-20 16:06

Цвет инкапсулируется в классе **_Color_**.  Основная цель [AWT](AWT) Color - позволить разработчикам создавать новые цвета с помощью кода Java с использованием пакетов RGB (красный, зеленый, синий), RGBA (красный, зеленый, синий, альфа) или HSB (оттенок, насыщенность, компоненты BRI). Альфа указывает, насколько непрозрачен каждый пиксель, и позволяет комбинировать изображение поверх других с помощью альфа-компоновки с прозрачными областями и сглаживанием краев непрозрачных областей.Класс содержит два значения - код оттенка и значение непрозрачности / transparency.

Вот как вы объявляете класс java.awt.Color:
```java
public class Color extends Object implements Paint, Serializable
```

### AWT. Конструкторы Color в Java

В зависимости от параметра цвета, который вы хотите создать, вам нужно будет использовать определенный тип цветового конструктора. Их несколько. Давайте рассмотрим их один за другим:
- `Color(float r, float g, float b)` - это класс, который вы используете для определения непрозрачного цвета в цветовой схеме RGB. Вы можете указать цветовой диапазон в любом диапазоне от 0.0 до 0.1.
- `Color(float r, float b, float g, float a)` - это класс, который определяет цвет RGBA (диапазон доступных значений равен 0.0 и 0.1).
- `Color(ColorSpace c, float[], co, float a)` - определяет цвет в цветовом пространстве, которое вы указываете заранее. Разработчик определяет диапазон цветовых компонентов в массиве float определенного alpha.
- `Color(int, rgb)` это класс, создающий цвет RGB (непрозрачный). Обязательно обратите внимание на значение компонента конструктора - 16-23 для красного, 8-15 для зеленого, 0-7 для синего.
- `Color(int r, int g, int b)` - метод, используемый для определения непрозрачного цвета RGB. Значение цвета должно находиться в диапазоне от 0 до 255.
- `Color(int r, int g, int b, int a)` - создает цвет в схеме RGBA (0-255).
- `Color(int rgba, boolean b)` используется для создания цветов sRGB в пределах определенного комбинированного значения. Диапазон значений составляет 24-31 для alpha, 16-23 для красного, 8-15 для зеленого и 0-7 для синего.

Кроме этого, class.awt.color оперирует полями, унаследованными от `Java.awt.Transparency`:
- `TRANSLUCENT` показывает, содержит ли цвет альфа-значения или нет, и имеет два значения - 0 и 1.
- `OPAQUE` присваивает объекту альфа-значение 1, гарантирующее его полную непрозрачность.
- `BITMASK` представляет абсолютную непрозрачность или значение прозрачности и находится в диапазоне (0; 1), где 0 - полная прозрачность, а 1 - крайняя непрозрачность.

### Методы класса Color

Цветовая модель HSB (hue-saturation-brightness - оттенок-насыщенность­-яркость) является альтернативой модели RGB (red-green-Ыue - красный-зе­леный-синий) для указания конкретных цветов. Образно говоря, оттенок представляет собой цветовой круг. Оттенок можно указывать с помощью чис­ла от 0.0 до 1.0, которое применяется для получения угла в цветовом круге. (Главные цвета приблизительно соответствуют красному, оранжевому, желто­му, зеленому, синему, сине-фиолетовому и темно-лиловому.) Насыщенность -
еще одна шкала в диапазоне от 0.0 до 1.0, представляющая цвета от светлых пастельных тонов до интенсивных оттенков. Значения яркости также варьи­руются от 0.0 до 1.0, где 1.0 - яркий белый цвет, а 0.0 - черный. 

- В классе **_Color_** определены два метода, которые позволяют выполнять преобразова­ния между моделями RGB и HSB:
```java
static int HSBtoRGB (float hue, float saturation, float brightness);
static float [ ] RGBtoHSB (int red, int green, int Ыuе, float [ ] values );
```
Метод HSBtoRGB() возвращает упакованное значение RGB, совместимое с конструктором Color(int). Метод RGBtoHSB() возвращает массив типа float значений HSB, соответствующих целым числам RGB. Если values неравно null, тогда этому массиву присваиваются значения HSB и он возвра­щается. В противном случае создается новый массив и в нем возвращаются
значения HSB. В любом случае массив содержит оттенок по индексу О, насы­щенность по индексу 1 и яркость по индексу 2.

- **getRed(), getGreen(), getBlue()**
Красную, зеленую и синюю составляющие цвета можно получать неза­висимо друг от друга с использованием методов getRed(), getGreen() и getBlue():
```java
int getRed();
int getGreen();
int getBlue();
```
Каждый метод возвращает в младших восьми битах целочисленного зна­чения компонент цвета RGB, найденный в вызываемом объекте **_Color_**.

- **getRGB()** - этот метод предназначен для получения упакованного представления цвета RGB:
```java
int getRGB();
```

- **Color darker()** - этот метод используется для создания нового цвета, который является более темной версией цвета, чем который вы уже определили. Пример:
```java
Color.green.darker();
```
Если применения `darker()` одного раза недостаточно для создания нужного вам оттенка, не стесняйтесь повторно применять метод столько раз, сколько захотите:
```java
Color.green.darker().darker().darker().darker().darker();
```

- **Color brighter()** - этот метод используется для придания яркости уже имеющемуся у вас оттенку. Аналогично `darker()`, его можно использовать несколько раз для одного цвета. Пример:
```java
Color myColor = Color.RED; 
JLabel label = new JLabel("First Name"); 
label.setForeground(myColor.brighter());
```

- **int getAlpha()** - этот метод возвращает альфа-компонент вашего цвета. Имейте в виду, что альфа-значения лежат в диапазоне 0-255. Вот пример применения метода и возврата. Пример:
```java
alpha = Color.black.getAlpha(); 
return new Color(components[0], components[1], components[2], alpha);
```
- **static Color getColor(String nm)** - этот метод для определения местоположения цвета с помощью системных свойств. Существуют другие методы, решающие аналогичные задачи:
```java
static Color getColor(String nm, int v);
static Color getColor(String nm, Color v);
```

- **static Color decode (string nm)** - этот метод используется для отображения цвета в виде строки. После завершения преобразования разработчик получит определенный непрозрачный цвет. Пример:
```java
public static Color decodeColor(String hexColor) { return Color.decode(hexColor); }
```

- **getTransparency()** - этот метод возвращает значение прозрачности, указанное вами или другим разработчиком для цвета при его создании. Пример:
```java
public int getTransparency() { return myColor.getTransparency(); }
```

- **boolean equals(Object obj)** - тот метод очень полезен, если вы сравниваете два цвета друг с другом. Он позволяет разработчикам Java узнать, имеют ли два цветных объекта равные значения. Пример:
```java
import java.awt.Color;

public class Main { 
	public static void main(String[] a) { 
		Color myBlack = new Color(0, 0, 0); // Color black 
		Color myWhite = new Color(255, 255, 255); // Color white 
		System.out.println(myBlack.equals(myWhite)); 
	} 
}
```

- **hashCode() - этот метод вычисляет хэш-код для этого цвета.

#### Программа 1. Демонстрация работы с цветом

```java
// Демонстрация работы с цветом.  
import java.awt.*;  
import java.awt.event.*;  
  
public class ColorDemo extends Frame {  
    public ColorDemo() {  
        addWindowListener(new WindowAdapter() {  
            public void windowClosing(WindowEvent we) {  
                System.exit(0);  
            }  
        });  
    }  
  
    // Вычерчивать с использованием различных цветов.  
    public void paint(Graphics g) {  
        Color c1 = new Color(255, 100, 100);  
        Color c2 = new Color(100, 255, 100);  
        Color c3 = new Color(100, 100, 255);  
        g.setColor(c1) ;  
        g.drawLine(20, 40, 100, 100);  
        g.drawLine(20, 100, 100, 20);  
        g.setColor(c2);  
        g.drawLine(40, 45, 250, 180);  
        g.drawLine(75, 90, 400, 400);  
        g.setColor(c3);  
        g.drawLine(20, 150, 400, 40);  
        g.drawLine(25, 290, 80, 19);  
        g.setColor(Color.red);  
        g.drawOval(20, 40, 50, 50);  
        g.fillOval(70, 90, 140, 100);  
        g.setColor(Color.blue);  
        g.drawOval(190, 40, 90, 60);  
        g.drawRect(40, 40, 55, 50);  
        g.setColor(Color. cyan);  
        g.fillRect(100, 40, 60, 1);  
        g.drawRoundRect(190, 40, 60, 60, 15, 15);  
    }  
  
    public static void main (String [] args) {  
        ColorDemo appwin = new ColorDemo();  
        appwin.setSize(new Dimension(340, 260));  
        appwin.setTitle("ColorDerno");  
        appwin.setVisible(true);  
    }  
}
```
**Вывод:**
![[Ex1-Color.png]]

#### Пример 2. Программа устанавливает цвет фона панели

```java
// Java program to set the background color of panel  
// using the color specified in the constants  
// of the class.  
import java.awt.*;  
import java.awt.event.WindowAdapter;  
import java.awt.event.WindowEvent;  
import javax.swing.*;  
  
class color extends JFrame {  
  
    // constructor  
    color()  
    {  
        super("color");  
        addWindowListener(new WindowAdapter() {  
            public void windowClosing(WindowEvent we) {  
                System.exit(0);  
            }  
        });  
  
        // create a new Color  
        Color c = Color.yellow;  
  
        // create a panel  
        JPanel p = new JPanel();  
  
        // set the background of the frame  
        // to the specified Color        p.setBackground(c);  
  
        setSize(200, 200);  
        add(p);  
        setVisible(true);  
    }  
  
    // Main Method  
    public static void main(String args[])  
    {  
        color c = new color();  
    }  
}
```
**Вывод:**
![[Ex2-Color.png]]

#### Пример 3. Программа делает фон панели светлее или темнее

```java
// Java program to set the background color of panel  
// using the color specified in the constants  
// of the class.  
import java.awt.*;  
import java.awt.event.ActionEvent;  
import java.awt.event.ActionListener;  
import java.awt.event.WindowAdapter;  
import java.awt.event.WindowEvent;  
import javax.swing.*;  
  
class color extends JFrame implements ActionListener {  
  
    JPanel p;  
    // constructor  
    color()  {  
        super("color");  
        addWindowListener(new WindowAdapter() {  
            public void windowClosing(WindowEvent we) {  
                System.exit(0);  
            }  
        });  
  
        // create a new Color  
        // RGB value of Green is 0, 100, 0        
        Color c = new Color(0, 100, 0);  
        // create a panel  
        p = new JPanel();  
        // set the background of the frame  
        // to the specified Color        
        p.setBackground(c);  
  
        JButton b = new JButton("brighter");  
        JButton b1 = new JButton("darker");  
  
        b.addActionListener(this);  
        b1.addActionListener(this);  
  
        setSize(200, 200);  
        p.add(b);  
        p.add(b1);  
        add(p);  
  
        setVisible(true);  
    }  
  
    public void actionPerformed(ActionEvent evt)  {  
        String s = evt.getActionCommand();  
        Color c = p.getBackground();  
        
        if (s.equals("brighter")) {  
            // make the color brighter  
            c = c.brighter();  
        }  
        else {  
            // make the color darker  
            c = c.darker();  
        }  
		p.setBackground(c);  
	}    
    // Main Method  
    public static void main(String args[]) {  
        color c = new color();  
    }  
}
```
**Вывод:**

![[Ex3_1-Color.png]]--brighter-->![[Ex3_2-Color.png]]

