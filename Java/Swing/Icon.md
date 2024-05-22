#Java #Swing #Icon #ImageIcon

## Интерфейс Icon и класс ImageIcon

2024-05-15 12:03

[Swing](Swing) представляет концепцию значка для использования в различных компонентах. Интерфейс **_Icon_** и класс **_ImageIcon_** чрезвычайно упрощают работу с простыми изображениями.

### Интерфейс Icon

Интерфейс **_Icon_** очень прост, в нем указаны всего три метода, используемых для определения размера **_Icon_** и его отображения. Разработчики этого интерфейса могут свободно хранить и отображать изображения любым способом, обеспечивая большую гибкость. Другими словами, иконки не обязательно должны быть растровыми или GIF-изображениями, они могут отображаться любым выбранным способом; как мы увидим позже, иконку можно просто нарисовать на компоненте, если это более эффективно. 

Интерфейс **_Icon_** определяет свойства `iconHeight` и `iconWidth`.  Эти свойства указываю размер **_Icon_** в пикселях.

### Method

**public abstract void paintIcon(Component c, Graphics g, int x, int y)** - рисует **_Icon_** в указанном месте на заданном [Graphics](Graphics). [Component](Component) предоставляется для того, чтобы разрешить использовать его свойства (такие, как цвет переднего плана или фона) при рисовании или для того, чтобы разрешить использовать компонент в качестве наблюдателя изображения.

### Реализация ваших собственных значков

**Пример 1.** Вот класс, который реализует **_Icon_** интерфейс и использует овалы в качестве простых значков:
```java
// OvalIcon.java
//
import javax.swing.*;
import java.awt.*;

// A simple Icon implementation that draws ovals
public class OvalIcon implements Icon {

  public OvalIcon(int w, int h) {
    width = w;
    height = h;
  }

  public void paintIcon(Component c, Graphics g, int x, int y) {
    g.drawOval(x, y, width-1, height-1);
  }

  public int getIconWidth() { return width; }
  public int getIconHeight() { return height; }

  private int width, height;
}
```
И простой класс, который создает несколько меток, чтобы показать, как это работает:
```java
// TestOval.java  
//  
import javax.swing.*;  
import java.awt.*;  
import java.awt.event.*;  
  
import static com.sun.java.accessibility.util.AWTEventMonitor.addWindowListener;  
  
public class TestOval {  
    public static void main(String[] args) {  
        JFrame f = new JFrame();  
        //f.addWindowListener(new BasicWindowMonitor());  
  
        WindowListener wl = new WindowAdapter() {  
            public void windowClosing(WindowEvent e) {  
                System.exit(0);  
            }  
        };  
        addWindowListener(wl);  
  
        JLabel label1 = new JLabel(new OvalIcon(20,50));  
        JLabel label2 = new JLabel(new OvalIcon(50,20));  
        JLabel label3 = new JLabel  
                ("Round!", new OvalIcon(60,60), SwingConstants.CENTER);  
        label3.setHorizontalTextPosition(SwingConstants.CENTER);  
  
        Container c = f.getContentPane();  
        c.setLayout(new FlowLayout());  
        c.add(label1);  
        c.add(label2);  
        c.add(label3);  
        f.pack();  
        f.setVisible(true);  
    }  
}
```
При запуске этой тестовой программы отображается изображение, показанное на рисунке:
![[Ex1-Icon.png]]

### Динамические значки

Значки не обязаны отображаться одинаково каждый раз, когда они отображаются. Совершенно разумно (и часто весьма полезно) иметь значок, использующий некоторую информацию о состоянии, чтобы определить, как он должна отображаться. В следующем примере мы создаем два ползунка JSlider, которые можно использовать для изменения ширины и высоты динамического значка.
```java
// DynamicIconExample  
//  
import javax.swing.*;  
import javax.swing.event.*;  
import java.awt.*;  
import java.awt.event.WindowAdapter;  
import java.awt.event.WindowEvent;  
import java.awt.event.WindowListener;   
  
// Example of an icon that changes form.  
public class DynamicIconExample {  
    public static void main(String[] args) {  
  
        // Create a couple sliders to control the icon size  
        final JSlider width = new JSlider(JSlider.HORIZONTAL, 1, 150, 75);  
        final JSlider height = new JSlider(JSlider.VERTICAL, 1, 150, 75);  
  
        // A little Icon class that uses the current slider values.  
        class DynamicIcon implements Icon {  
            public int getIconWidth() { return width.getValue(); }  
            public int getIconHeight() { return height.getValue(); }  
  
            public void paintIcon(Component c, Graphics g, int x, int y) {  
                g.fill3DRect(x, y, getIconWidth(), getIconHeight(), true);  
            }  
        };  
        Icon icon = new DynamicIcon();  
        final JLabel dynamicLabel = new JLabel(icon);  
  
        // A listener to repaint the icon when sliders are adjusted.  
        class Updater implements ChangeListener {  
            public void stateChanged(ChangeEvent ev) {  
                dynamicLabel.repaint();  
            }  
        };  
        Updater updater = new Updater();  
  
        width.addChangeListener(updater);  
        height.addChangeListener(updater);  
  
        // Lay it all out  
        JFrame f = new JFrame();  
        WindowListener wl = new WindowAdapter() {  
            public void windowClosing(WindowEvent e) {  
                System.exit(0);  
            }  
        };  
  
        Container c = f.getContentPane();  
        c.setLayout(new BorderLayout());  
        c.add(width, BorderLayout.NORTH);  
        c.add(height, BorderLayout.WEST);  
        c.add(dynamicLabel, BorderLayout.CENTER);  
        f.setSize(210,210);  
        f.setVisible(true);  
    }  
}
```
**Вывод:**
![[Ex2-Icon.png]]
Важно отметить, что **_Icon_** класс фактически не хранит никакой информации. В этом случае мы сделали **_Icon_** класс внутренним классом, предоставив ему прямой доступ к ползункам. Всякий раз, когда значку предлагается нарисовать саму себя, он получает свою ширину и высоту из значений ползунков. Вы также можете сделать свой **_Icon_** класс прослушивателем событий и заставить его обновлять себя в соответствии с изменениями в определенных событиях. Варианты здесь широко открыты.

Независимо от того, как ваш значок получает свои данные, вам нужно убедиться, что каждый раз, когда вы захотите изменить внешний вид значка, вы запускаете перерисовку значка. В этом примере мы сделали это, прослушивая события изменения от ползунков и вызывая `repaint()` метку, на которой находится значок, каждый раз, когда меняется один из ползунков.

### Класс ImageIcon

[Swing](Swing) предоставляет конкретную реализацию интерфейса **_Icon_**, который значительно полезнее нашего `OvalIcon` класса. **_ImageIcon_** использует `java.awt.Image` объект для хранения и отображения любой графики и обеспечивает синхронную загрузку изображений (т. е. `Image` Загружается полностью перед возвратом), что делает **_ImageIcon_** его очень мощным и простым в использовании. Вы даже можете использовать **_ImageIcon_** для отображения анимированного GIF.89a, что делает вездесущий “анимационный апплет” таким простым, как этот:
```java
// AnimationApplet.java
//
import javax.swing.*;

// A simple animation applet
public class AnimationApplet extends JApplet {
  public void init() {
    ImageIcon icon = new ImageIcon("images/rolling.gif");    // animated gif
    getContentPane().add(new JLabel(icon));
  }
}
```
Класс **_ImageIcon_** определяет свойства: `description` позволяет задать произвольное описание изображения (одним из возможных применений этого свойства может быть предоставление слепому пользователю звукового описания изображения), iconHeight, iconWidth, image, imageLoadStatus, imageObserver.

Свойства `iconHeight` и `iconWidth` имеют значение по умолчанию -1, если конструктор не загружает изображение, в то время как `image` свойство просто содержит `Image` объект, отображаемый значком. `ImageLoadStatus` указывает на успех или неудачу процесса загрузки изображения, используя константы, определенные в `java.awt.MediaTracker` (`ABORTED`, `ERRORED` или `COMPLETE`). По умолчанию для этого свойства равно нулю, которое не сопоставляется ни с одной из этих констант.

Свойство `imageObserver` содержит `ImageObserver`, указанное для получения уведомлений об изменениях в изображении. Если это свойство имеет значение `null` (как оно есть по умолчанию), компонент, содержащий иконку, будет рассматриваться как наблюдатель за изображением при раскрашивании изображения.

Диаграмма классов для **_ImageIcon_** и связанных с ней классов:
![[ImageIcon.png]]

### Сериализация

Как и большинство классов [Swing](Swing), **_ImageIcon_** реализует [Serializable](Serializable). Внимательный наблюдатель может увидеть в этом проблему: `java.awt.Image` класс, используемый `ImageIcon`, _не_ сериализуем. По умолчанию это препятствовало бы `ImageIcon` правильной сериализации объектов. Хорошей новостью является то, что в нем `ImageIcon` реализованы методы `readObject()` и `writeObject()`, так что пиксельное представление изображения сохраняется и извлекается правильно.

### Конструкторы

**ImageIcon()**
Создает неинициализированный **_ImageIcon_**.

**ImageIcon(Image image), ImageIcon(Image image, String description)**
Создает **_ImageIcon_** объекты из существующих изображений. Может быть предоставлено текстовое описание изображения. Если описание не предоставлено, предпринимается попытка извлечь свойство “комментарий” из входных данных `Image`. Если это ненулевая строка, она будет использоваться в качестве описания.

**ImageIcon(String filename), ImageIcon(String filename, String description)**
Создает **_ImageIcon_** объекты из содержимого указанного файла GIF или JPEG. Изображение гарантированно будет полностью загружено (если не возникнет ошибка) при возврате конструктора.

ImageIcon(URL location), ImageIcon(URL location, String description)
Создает **_ImageIcon_** объекты из содержимого указанного URL. Изображение гарантированно будет полностью загружено (если не возникнет ошибка) при возврате конструктора.

public ImageIcon(byte imageData[]), public ImageIcon(byte imageData[], String description)
Создает **_ImageIcon_** объекты из массива байтов, содержащего изображение в поддерживаемом формате, таком как GIF или JPEG. Изображение гарантированно будет полностью загружено (если не возникнет ошибка) при возврате конструктора.

### Метод пользовательского интерфейса

public synchronized void paintIcon(Component c, Graphics g, int x, int y)
Рисует `Image` в указанном месте на входе `Graphics`. Данное значение `Component` передается методу `Graphic`’s `drawImage()` как `ImageObserver` (напомним, что [java.awt.Component](Component) реализует `ImageObserver`), если наблюдатель изображений не был явно задан.

### Защищенный метод

protected void loadImage(Image image)
Вызывается конструкторами и `setImage()`. Он использует `java.awt.MediaTracker` объект для синхронной загрузки изображения. По завершении изображение гарантированно будет полностью загружено, если только не произошла ошибка, и в этом случае свойство `imageLoadStatus` отразит ошибку.