#Java #awt #BorderLayout

## Класс [AWT](AWT) BorderLayout

2024-05-24 10:52

Класс **BorderLayout** упорядочивает компоненты таким образом, чтобы они соответствовали пяти регионам: востоку, западу, северу, югу и центру. Каждый регион может содержать только один компонент, и каждый компонент в каждом регионе идентифицируется соответствующими постоянными NORTH, SOUTH, EAST, WEST, и CENTER.

### Объявление класса

Ниже приводится объявление для класса **java.awt.FlowLayout**:
```java
public class BorderLayout extends Object implements LayoutManager2, Serializable
```

**Поля класса java.awt.BorderLayout:**
- **static String AFTER_LAST_LINE** - синоним PAGE_END.
- **static String AFTER_LINE_ENDS** - синоним LINE_END.
- **static String BEFORE_FIRST_LINE** - синоним PAGE_START.
- **static String BEFORE_LINE_BEGINS** - синоним LINE_START.
- **static String CENTER** - середина контейнера.
- **static String EAST** - правая сторона контейнера.
- **static String LINE_END** - компонент находится в конце направления строки для макета.
- **static String LINE_START** - компонент находится в начале направления линии для макета.
- **static String NORTH** - верхняя часть контейнера.
- **static String PAGE_END** - компонент находится после последней строки содержимого макета.
- **static String PAGE_START** - компонент находится перед первой строкой содержимого макета.
- **static String SOUTH** - нижняя часть контейнера.
- **static String WEST** - левая сторона контейнера.

### Конструкторы классов

| S.N. | Конструктор и описание                                                                                     |
| ---- | ---------------------------------------------------------------------------------------------------------- |
| 1    | **BorderLayout()**<br>Создает новый макет границы без пробелов между компонентами.                         |
| 2    | **BorderLayout(int hgap, int vgap)**<br>Создает макет границы с заданными промежутками между компонентами. |

### Методы класса

| N   | Метод и описание                                                                                                                                                                                              |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | **void addLayoutComponent(Component comp, Object constraints)**<br>Добавляет указанный компонент в макет, используя указанный объект ограничения.                                                             |
| 2   | **void addLayoutComponent(String name, Component comp)**<br>Если менеджер компоновки использует строку для каждого компонента, добавляет компонент comp в макет, связывая его со строкой, указанной по имени. |
| 3   | **int getHgap()**<br>Возвращает горизонтальный промежуток между компонентами.                                                                                                                                 |
| 4   | **float getLayoutAlignmentX(Container parent)**<br>Возвращает выравнивание по оси x.                                                                                                                          |
| 5   | **float getLayoutAlignmentY(Container parent)**<br>Возвращает выравнивание по оси y.                                                                                                                          |
| 6   | **int getVgap()**<br>Возвращает вертикальный промежуток между компонентами.                                                                                                                                   |
| 7   | **void invalidateLayout(Container target)**<br>Делает макет недействительным, указывая, что если диспетчер макетов имеет кэшированную информацию, ее следует удалить.                                         |
| 8   | **void layoutContainer(Container target)**<br>Определяет аргумент контейнера, используя этот макет границы.                                                                                                   |
| 9   | **Dimension maximumLayoutSize(Container target)**<br>Возвращает максимальные размеры для этого макета с учетом компонентов в указанном целевом контейнере.                                                    |
| 10  | **Dimension minimumLayoutSize(Container target)**<br>Определяет минимальный размер целевого контейнера с помощью этого менеджера компоновки.                                                                  |
| 11  | **Dimension preferredLayoutSize(Container target)**<br>Определяет предпочтительный размер целевого контейнера с помощью этого менеджера компоновки на основе компонентов в контейнере.                        |
| 12  | **void removeLayoutComponent(Component comp)**<br>Удаляет указанный компонент из этого макета.                                                                                                                |
| 13  | **void setHgap(int hgap)**<br>Устанавливает горизонтальный зазор между компонентами.                                                                                                                          |
| 14  | **void setVgap(int vgap)**<br>Устанавливает вертикальный зазор между компонентами.                                                                                                                            |
| 15  | **String toString()**<br>Возвращает строковое представление состояния этого макета.                                                                                                                           |

#### Пример 1

```java
import java.awt.*;
import java.awt.event.*;

public class AwtLayoutDemo {
   private Frame mainFrame;
   private Label headerLabel;
   private Label statusLabel;
   private Panel controlPanel;
   private Label msglabel;

   public AwtLayoutDemo(){
      prepareGUI();
   }

   public static void main(String[] args){
      AwtLayoutDemo  awtLayoutDemo = new AwtLayoutDemo();  
      awtLayoutDemo.showBorderLayoutDemo();       
   }
      
   private void prepareGUI(){
      mainFrame = new Frame("Java AWT Examples");
      mainFrame.setSize(250,350);
      mainFrame.setLayout(new GridLayout(3, 1));
      mainFrame.addWindowListener(new WindowAdapter() {
         public void windowClosing(WindowEvent windowEvent){
            System.exit(0);
         }        
      });    
      headerLabel = new Label();
      headerLabel.setAlignment(Label.CENTER);
      statusLabel = new Label();        
      statusLabel.setAlignment(Label.CENTER);
      statusLabel.setSize(350,100);

      msglabel = new Label();
      msglabel.setAlignment(Label.CENTER);
      msglabel.setText("Welcome to TutorialsPoint AWT Tutorial.");

      controlPanel = new Panel();
      controlPanel.setLayout(new FlowLayout());

      mainFrame.add(headerLabel);
      mainFrame.add(controlPanel);
      mainFrame.add(statusLabel);
      mainFrame.setVisible(true);  
   }

   private void showBorderLayoutDemo(){
      headerLabel.setText("Layout in action: BorderLayout");      

      Panel panel = new Panel();
      panel.setBackground(Color.darkGray);
      panel.setSize(300,300);
      BorderLayout layout = new BorderLayout();
      layout.setHgap(10);
      layout.setVgap(10);
      panel.setLayout(layout);        
	  
      panel.add(new Button("Center"),BorderLayout.CENTER);
      panel.add(new Button("Line Start"),BorderLayout.LINE_START); 
      panel.add(new Button("Line End"),BorderLayout.LINE_END);
      panel.add(new Button("East"),BorderLayout.EAST);   
      panel.add(new Button("West"),BorderLayout.WEST); 
      panel.add(new Button("North"),BorderLayout.NORTH); 
      panel.add(new Button("South"),BorderLayout.SOUTH); 

      controlPanel.add(panel);

      mainFrame.setVisible(true);  
   }
}
```
**Вывод:**
![[Ex1-BorderLayout.png]]

#### Пример 2. С использованием [Swing](Swing)

```java
import java.awt.BorderLayout;  
import javax.swing.*;  
  
public class Main {  
    public static void main(String[] args) {  
        // создаем фрейм и устанавливаем его размер.  
        JFrame  jf = new JFrame();  
        jf.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);  
        jf.setSize(400, 300);  
        // создаем панель.  
        JPanel  p = new JPanel();  
        jf.add(p);  
        // к панели добавляем менеджер BorderLayout.  
        p.setLayout(new BorderLayout());  
        // к панели добавляем кнопку и устанавливаем для нее менеджер в верхнее расположение.  
        p.add(new JButton("Свере (верх)"), BorderLayout.NORTH);  
        // к панели добавляем кнопку и устанавливаем для нее менеджер в нижнее расположение.  
        p.add(new JButton("Юг (низ)"), BorderLayout.SOUTH);  
        // к панели добавляем метку и устанавливаем для нее правое расположение.  
        p.add(new JLabel("Восток (справа)"), BorderLayout.EAST);  
        // к панели добавляем флажок и устанавливаем для него левое расположение.  
        p.add(new JCheckBox("Запад (слева)"), BorderLayout.WEST);  
        // к панели добавляем кнопку и устанавливаем для нее центральное расположение.  
        p.add(new JButton("Кнопка в центре"), BorderLayout.CENTER);  
        jf.setVisible(true);  
    }  
}
```
**Вывод:**
![[Ex2-BorderLayout.png]]

Что характерно, если мы добавим к какой-нибудь панели, например, к левой, новый элемент:
```java
	// к панели добавляем флажок и устанавливаем для него левое расположение.
    p.add(new JCheckBox("Запад (слева)"), BorderLayout.WEST);          
    // к панели добавляем флажок и устанавливаем для него левое расположение.
    p.add(new JCheckBox("Еще одна метка"), BorderLayout.WEST);  
```
То она перекроек старый.

