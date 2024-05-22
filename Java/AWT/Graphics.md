#Java #awt #Graphics

## Абстрактный класс Graphics

2024-05-22 11:59

**_Graphics_** — это абстрактный класс, предоставляемый Java [AWT](AWT), использующийся для рисования. Он состоит из различных полей, которые содержат такую ​​информацию, как окрашиваемые компоненты, шрифт, цвет, режим XOR и т. д., а также методы, позволяющие рисовать различные формы на компонентах графического интерфейса. **_Graphics_** — это абстрактный класс, поэтому его нельзя инициализировать напрямую. Объекты его дочерних классов можно получить двумя следующими способами.

### 1. Внутри метода paint() или update()

Он передается в качестве аргумента методам paint() и update() и, следовательно, доступен внутри этих методов. Методы paint() и update() присутствуют в классе [Component](Component) и, следовательно, могут быть переопределены.
```java
void paint(Graphics g)

void update(Graphics g)
```

#### Пример 1. 

```java
import java.awt.*;  
import java.awt.event.WindowAdapter;  
import java.awt.event.WindowEvent;  
  
public class Main extends Frame {  
    public Main()  
    {  
        setVisible(true);  
        setSize(200, 150);  
        addWindowListener(new WindowAdapter() {  
            @Override  
            public void windowClosing(WindowEvent e)  
            {  
                System.exit(0);  
            }  
        });  
    }  
    public void paint(Graphics g)  
    {  
        g.drawRect(50, 50, 100, 50);  
    }  
  
    public static void main(String[] args)  
    {  
        new Main();  
    }  
}
```
**Вывод:**
![[Ex1-Graphics.png]]

### **2. метод getGraphics()**

Этот метод присутствует в классе [Component](Component) и, следовательно, может быть вызван для любого компонента, чтобы получить объект **_Graphics_** для компонента.

`public Graphics getGraphics()` создает графический контекст для компонента. Этот метод вернет значение null, если компонент в данный момент не отображается.

>**Примечание**. Рисование желательно выполнять с помощью метода paint(). Графика, нарисованная с помощью объекта, полученного с помощью метода getGraphics(), является временной и теряется при повторной перерисовке компонента. Рисование может произойти сразу же, но перерисовка может занять некоторое время и, следовательно, удалить эффекты кода, выполненного с помощью getGraphics().

#### Пример 2. 

```java
import java.awt.*; 
import java.awt.event.WindowAdapter; 
import java.awt.event.WindowEvent; 
  
public class MyFrame extends Frame { 
    public MyFrame() 
    { 
        setVisible(true); 
        setSize(300, 200); 
        addWindowListener(new WindowAdapter() { 
            @Override
            public void windowClosing(WindowEvent e) 
            { 
                System.exit(0); 
            } 
        }); 
    } 
    public void paint(Graphics g) 
    { 
        System.out.println("painting..."); 
    } 
  
    public static void main(String[] args) 
    { 
        MyFrame f = new MyFrame(); 
        Graphics g = f.getGraphics(); 
        System.out.println("drawing..."); 
        g.drawRect(100, 100, 10, 10); 
        System.out.println("drawn..."); 
    } 
}
```
**Вывод:**
![[Pasted image 20240522122507.png]]
Этот код не будет отображать графику, нарисованную с помощью getGraphics(), поскольку paint() вызывается после draw().

#### Пример 3.

```java
import java.awt.*; 
import java.awt.event.WindowAdapter; 
import java.awt.event.WindowEvent; 
  
public class MyFrame extends Frame { 
    public MyFrame() 
    { 
        setVisible(true); 
        setSize(300, 200); 
        addWindowListener(new WindowAdapter() { 
            @Override
            public void windowClosing(WindowEvent e) 
            { 
                System.exit(0); 
            } 
        }); 
    } 
    public void paint(Graphics g) 
    { 
        System.out.println("painting..."); 
    } 
  
    public static void main(String[] args) 
    { 
        MyFrame f = new MyFrame(); 
        Graphics g = f.getGraphics(); 
        try { 
            Thread.sleep(1000); 
        } 
        catch (Exception e) { 
        } 
        System.out.println("drawing..."); 
        g.drawRect(100, 100, 100, 50); 
        System.out.println("drawn..."); 
    } 
}
```
**Вывод**:
![[Ex3-Graphics.png]]
Этот код будет отображать графику, нарисованную с помощью getGraphics(), поскольку draw() вызывается с задержкой после paint().

**Важные методы для настройки свойства графического контекста:**
- void setClip(int x, int y, int width, int height),
- void setClip(Shape clip),
- void setColor(Color c),
- void setFont(Font font),
- void setPaintMode(),
- void setXORMode(Color c1).

### Рисование в режиме XOR

В режиме рисования новый нарисованный результат перезаписывает предыдущий. Следовательно, если цвет, установленный в графическом объекте, соответствует цвету фона, объект будет не виден. В режиме **_Xor_** результат получается путем преобразования предоставленного цвета в цвет фона и графики. Следовательно, объект всегда виден независимо от цвета фона.

#### Пример 4. Пример рисование в режиме XOR

```java
import java.awt.*;  
import java.awt.event.WindowAdapter;  
import java.awt.event.WindowEvent;  
  
public class Main extends Frame {  
    public Main()  
    {  
        setVisible(true);  
        setSize(300, 200);  
        setBackground(Color.red);  
        addWindowListener(new WindowAdapter() {  
            @Override  
            public void windowClosing(WindowEvent e)  
            {  
                System.exit(0);  
            }  
        });  
    }  
    public void paint(Graphics g)  
    {  
        g.setColor(Color.green);  
        g.setXORMode(Color.black);  
        g.fillRect(100, 100, 100, 50);  
    }  
  
    public static void main(String[] args)  
    {  
        new Main();  
    }  
}
```
**Вывод:**
![[Ex4-Graphics.png]]
В приведенном выше коде набор цветов для графики: зеленый (00000000 11111111 00000000);
цвет фона: красный (11111111 00000000 00000000);
цвет, предусмотренный для XOR: черный (00000000 00000000 00000000);
цвет, полученный для рендеринга вывода = зеленый XOR красный XOR черный = желтый (11111111 11111111 00000000).

### Рисование фигур с использованием графического объекта

#### Линия

Для рисования линии используется следующий метод класса Graphics:
```java
void drawLine(int startX, int startY, int endX, int endY);
```

#### Прямоугольник

Для рисования прямоугольников используются следующие методы класса Graphics:
```java
void drawRect(int x, int y, int width, int height);
void drawRoundRect(int x, int y, int width, int height, int arcWidth, int arcHeight);
void fillRect(int x, int y, int width, int height);
void fillRoundRect(int x, int y, int width, int height, int arcWidth, int arcHeight);
```

#### Овал и Круг

Для рисования овалов и кругов используются следующие методы:
```java
void drawOval(int x, int y, int width, int height);
void fillOval(int x, int y, int width, int height);
```

#### Дуга

Для рисования дуг используются следующие методы класса Graphics:
```java
void drawArc(int x, int y, int width, int height, int startAngle, int arcAngle);
void fillArc(int x, int y, int width, int height, int startAngle, int arcAngle);
```

#### Полигон

Для рисования полигонов используются следующие методы:
```java
void drawPolygon(int[] xPoints, int[] yPoints, int nPoints);
void drawPolygon(Polygon p);
void fillPolygon(int[] xPoints, int[] yPoints, int nPoints);
void fillPolygon(Polygon p);
```

#### Пример 5.

```java
import java.awt.*;  
import java.awt.event.WindowAdapter;  
import java.awt.event.WindowEvent;  
  
public class Main extends Frame {  
    public Main()  
    {  
        setVisible(true);  
        setSize(250, 250);  
        addWindowListener(new WindowAdapter() {  
            @Override  
            public void windowClosing(WindowEvent e)  
            {  
                System.exit(0);  
            }  
        });  
    }  
    public void paint(Graphics g)  
    {  
        int[] x = { 50, 100, 150, 200, 150, 100 };  
        int[] y1 = { 100, 80, 80, 100, 120, 120 };  
        g.drawPolygon(x, y1, 6);  
        int[] y2 = { 160, 140, 140, 160, 180, 180 };  
        g.fillPolygon(x, y2, 6);  
    }  
  
    public static void main(String[] args)  
    {  
        new Main();  
    }  
}
```
**Вывод:**
![[Ex5-Graphics.png]]