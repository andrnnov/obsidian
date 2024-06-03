#Java #Swing #Menu

## Меню на java

**Создание JMenu в java с использованием Netbeans-** приложения редко обходятся без строк меню или контекстных меню (меню, которое открывается правой кнопкой мыши). По мере усложнения программы потребность в меню обычно возрастает. Они, так сказать, являются указателями приложения, которые направляют пользователя по программе. В следующей таблице приведен краткий обзор классов, с которыми мы будем иметь дело в этой статье, и краткое описание соответствующего назначения.

### Классы меню Java:

|**Класс**|**краткое описание**|
|---|---|
|JMenuItem|_JMenuItem_ представляет собой пункт меню (запись в меню), например “Открыть файл” или “Выйти”.|
|JMenu|_JMenu_ - это контейнер для _JMenuItems_, в который можно добавить любое количество _JMenuItems_. “Файл” в строке меню вашего браузера или текстового процессора может быть примером _JMenu_.|
|JMenuBar|_Строка JMenuBar_ - это вся строка меню окна. Она может содержать любое количество _JMenu_.|
|JCheckBoxMenuItem|_JCheckBoxMenuItem_ похож на _JMenuItem_, но с добавлением флажка. При нажатии галочка устанавливается или снимается. _Например, JCheckBoxMenuItems_ часто используются для активации или деактивации содержимого окна.|
|JRadioButtonMenuItem|Здесь используются переключатели, аналогичные _JCheckBoxMenuItem_. Обычно существует по крайней мере два _JRadioButtonMenuItem_, представляющих варианты для выбора.|
|JPopupMenu|J_PopupMenu_ - это так называемое контекстное меню, которое появляется при нажатии правой кнопки мыши.|
|JSeperator|Разделитель используется для разделения пунктов меню.|

### Класс JMenuBar

В Java строки меню реализованы с использованием класса JMenuBar. Объекты _JMenuBar_ служат контейнерами для каждого элемента строки меню.

#### Пример 1. Как создать простую строку меню с помощью JMenuBar в java

```java
import java.awt.Color ; 
import javax.swing.JDialog ; 
import javax.swing.JMenuBar ; 
import javax.swing.border.LineBorder ; 
import javax.swing.border.Border ;
 
 
/**
 *
 * @author Fawadkhan
 */
public class JmenuExamples {
    public static void main ( String [ ] args ) {
        // Creation of a new 
        JDialog myJDialog =  new  JDialog ( ) ; 
        myJDialog.setTitle ( "menu creating Example" ) ; 
        myJDialog.setSize ( 450 , 300 ) ; 
        // To illustrate, we'll create a red border
         Border border=  new  LineBorder ( Color .red) ; 
        // create a menu bar 
        JMenuBar bar =  new JMenuBar ( ) ; 
        // We set the created border for our menu 
        bar. setBorder ( border ) ; 
        // menu bar is set for the dialog
         myJDialog. setJMenuBar ( bar ) ; 
        // We display our dialog 
        myJDialog. setVisible ( true ) ; 
    }    
}
```
**Вывод:**
![[Ex1-Menu.png]]

Сначала мы создаем объект нашего класса [JDialog](JDialog). Мы могли бы также использовать a [JFrame](JFrame), для строки меню это не имеет значения. Затем мы даем нашему диалоговому окну заголовок ”menu creating Example”. Чтобы строка меню оставалась видимой, мы обведем ее простой красной рамкой. Для этого мы создаем объект класса LineBorder и передаем конструктору красный цвет. Затем мы создаем объект класса JMenuBar для нашей строки меню. С помощью метода setBorder. Давайте свяжем границу со строкой меню. Затем мы добавим строку меню в наше диалоговое окно и затем отобразим ее.

На скриншоте вы можете видеть красную полосу вверху. Поскольку наша строка меню не содержит никаких элементов, ее можно узнать только по нашему объекту _LineBorder_.

Класс _JMenuBar_ имеет ряд методов. Наиболее важным является метод add. Этот метод получает объект из класса _JMenu_ в качестве параметра передачи, который, в свою очередь, содержит структуру меню из отдельных пунктов меню (_JMenuItem_).

### Класс JMenu

Класс Java _javax.swing.JMenu_ служит контейнером для самих пунктов меню. Объекты класса _JMenu_ могут быть добавлены в a _JMenuBar_ или a _JPopupMenu_. Меню также могут быть вложенными. 

#### Пример 2. Как создать меню в строке меню с помощью JMenu в Java

```java
import java.awt.Color ; 
import javax.swing.JDialog ; 
import javax.swing.JMenuBar ; 
import javax.swing.border.LineBorder ; 
import javax.swing.border.Border ;
import javax.swing.JMenu;

public class JmenuExamples {
    public static void main ( String [ ] args ) {
          // Creation of a new 
         JDialog myJDialog =  new  JDialog ( ) ; 
        myJDialog.setTitle ( "menu creating Example" ) ; 
        myJDialog.setSize ( 450 , 300 ) ; 
        // To illustrate, we'll create a red border
         Border border=  new  LineBorder ( Color .red) ; 
        // create a menu bar 
        JMenuBar bar =  new JMenuBar ( ) ; 
        // We set the created border for our menu 
        bar. setBorder ( border ) ; 
        JMenu newfile =  new  JMenu ( "New File" ) ;
        bar. add ( newfile ) ; 
        JMenu Edit =  new  JMenu ( "Edit" ) ;
        bar. add ( Edit ) ; 
         JMenu View =  new  JMenu ( "View" ) ;
        bar. add ( View ) ; 
        // menu bar is set for the dialog
         myJDialog. setJMenuBar ( bar ) ; 
        // We display our dialog 
        myJDialog. setVisible ( true ) ; 
    }    
}
```
Теперь, когда мы установили нашу границу, мы создаем объект класса JMenu, конструктору которого мы можем передать заголовок напрямую. Затем мы добавляем объект JMenu в строку JMenuBar. Если мы запустим приведенный выше исходный код Java, то получим следующее диалоговое окно:
![[Ex2-Menu.png]]

### Методы класса _JMenu_ 

| **метод**                               | **Описание**                                                                                                                                        |
| --------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| JMenuItem add(JMenuItem menuItem)       | Этот метод добавляет объект класса _JMenuItem в JMenu_, добавляя в меню пункт menu.                                                                 |
| JMenuItem add(String s)                 | Этот метод создает объект класса _JMenuItem_ с именем предоставленной строки и добавляет его в качестве пункта меню к вызывающему объекту _JMenu_ . |
| void addSeparator()                     | Этот метод добавляет объект класса _JSeperator_ в качестве разделителя к a _JMenu_.                                                                 |
| JMenuItem insert(JMenuItem mi, int pos) | Этот метод добавляет объект класса _JMenuItem_ в позиции _позиция_ в качестве пункта меню к a _JMenu_.                                              |
| void insert(String s, int pos)          | Этот метод создает объект класса _JMenuItem_ с именем предоставленной строки и добавляет его в качестве пункта меню в _JMenu_ в позиции _позиция._  |
| void insertSeparator(int index)         | Этот метод добавляет объект класса _JSeperator_ в качестве разделителя в позиции _позиция_ для a _JMenu_.                                           |
| boolean isTopLevelMenu(                 | Этот метод проверяет, является ли _JMenu_ прямым “дочерним элементом” строки меню. Это невозможно, если это _JMenu_ было добавлено в _JPopupMenu_.  |
| void remove(int pos)                    | Этот метод удаляет компонент в переданной позиции _позиция_.                                                                                        |
| void remove(JMenuItem item)             | Этот метод удаляет переданный объект класса _JMenuItem_ из _JMenu._                                                                                 |
| void removeAll()                        | Этот метод удаляет все объекты из _JMenu_.                                                                                                          |
| void setMenuLocation(int x, int y)      | _Этот метод устанавливает позицию всплывающего компонента в x_ и _y_ координаты.                                                                    |

### Класс JMenuItem

Отдельные пункты меню a _JMenus_ реализованы с использованием объектов класса _javax.swing.JMenuItem_. 

Отличие от a _JMenu_ заключается в том, что при нажатии a _JMenuItem_ обычно что-то происходит, например, открытие диалогового окна, закрытие программы или изменение представления. Это зависит от действия, назначенного этому пункту меню.

_JMenuItem_ может быть добавлен в _JMenu_ или  _JPopupMenu_ .

### Конструкторы класса _JMenuItem_

| Функция                              | **Описание**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| ------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| JMenuItem(String text)               | Текст, который будет отображаться, передается здесь.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| JMenuItem(String text, Icon icon)    | Текст и _значок_ для пункта меню передаются в конструктор. Здесь следует отметить, что _значок_ это не просто путь к значку, но объект _Значок_ класс, содержащий данные изображения.                                                                                                                                                                                                                                                                                                                                                                                       |
| JMenuItem(String text, int mnemonic) | Здесь передается текст, который будет отображаться, и устанавливается так называемая мнемоника. Мнемоника - это комбинация клавиш, которую вы также можете использовать для выбора пункта меню. Например, во многих программах ”D" является мнемоническим символом для меню “File". Таким образом, вы можете открыть меню “файл", используя комбинацию клавиш "Alt + D".  <br>Поскольку мнемоника - это _Целое число_ значение здесь - это код конкретного символа на клавиатуре, который вы хотите использовать. Все это можно найти в разделе констант класса _KeyEvent_. |

#### Пример 3. Как создать JMenuItem и добавить его в JMenu

```java
import java.awt.Color ; 
import javax.swing.JDialog ; 
import javax.swing.JMenuBar ; 
import javax.swing.border.LineBorder ; 
import javax.swing.border.Border ;
import javax.swing.JMenu;
import javax.swing.JMenuItem;
 
public class JmenuExamples {
    public static void main ( String [ ] args ) {
          // Creation of a new 
         JDialog myJDialog =  new  JDialog ( ) ; 
        myJDialog.setTitle ( "menu creating Example" ) ; 
        myJDialog.setSize ( 450 , 300 ) ; 
        // To illustrate, we'll create a red border
         Border border=  new  LineBorder ( Color .red) ; 
        // create a menu bar 
        JMenuBar bar =  new JMenuBar ( ) ; 
        // We set the created border for our menu 
        bar. setBorder ( border ) ; 
        JMenu file =  new  JMenu ( "File" ) ;
        bar. add ( file ) ; 
        JMenu Edit =  new  JMenu ( "Edit" ) ;
        bar. add ( Edit ) ; 
         JMenu View =  new  JMenu ( "View" ) ;
        bar. add ( View ) ; 
        
        JMenuItem NewFile =  new  JMenuItem ( "New File" ) ;
        JMenuItem Save =  new  JMenuItem ( "Save" ) ;
        JMenuItem OpenFile =  new  JMenuItem ( "Open File" ) ;
        
        file.add(NewFile);
        file.add(Save);
        file.add(OpenFile);
        // menu bar is set for the dialog
         myJDialog. setJMenuBar ( bar ) ; 
        // We display our dialog 
        myJDialog. setVisible ( true ) ; 
    } 
}
```
В приведенном выше примере создан объект класса JMenuItem. Для этого используется конструктор JMenuItem(String Text).

**Вывод:**
![[Ex3-Menu.png]]

Краткий обзор некоторых важных методов класса _JMenuItem_ . Перечислять и объяснять все методы здесь не имеет особого смысла, поскольку многие методы используются редко.

| **метод**                                       | **Описание**                                                                                                                                                                                                                                                                                                                                                                                                               |
| ----------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| public void addActionListener(ActionListener l) | Этот метод был унаследован от класса _AbstractButton ._ Этот метод есть у большинства элементов управления. С помощью _ActionListener_ определенные события, такие как активация пункта меню, могут быть распознаны, чтобы программа могла реагировать соответствующим образом (например, открытие диалогового окна). Существует более подробное описание _Мероприятия_ и _ActionListeners_ в статье об обработке событий. |
| public void setText(String text)                | С помощью этого метода задается текст, который будет отображаться. Он также наследуется от класса _AbstractButton ._ Этот метод также доступен для многих элементов управления. Этот _установщик_ метод также имеет соответствующий метод _getter_ .                                                                                                                                                                       |
| protected void init(String text, Icon icon)     | Этот метод можно использовать для инициализации объекта класса _JMenuItem_ новым текстом и значком.                                                                                                                                                                                                                                                                                                                        |
| void setEnabled(boolean b)                      | Многие элементы управления также имеют метод _setEnabled_ . С помощью этого метода вы можете разрешить нажатие кнопки, передав _true_ или заблокировать ее от любого использования, передав _false_.                                                                                                                                                                                                                       |

### Класс JCheckBoxMenuItem

Класс _JCheckBoxMenuItem_ является дочерним классом класса JMenuItem, рассмотренного в предыдущем разделе. Он отличается от обычного пункта меню тем, что перед этим пунктом стоит флажок.
#### Пример 4. Как добавить флажок в меню в Java с помощью JCheckBoxMenuItem

```java
import java.awt.Color ;
import javax.swing.JCheckBoxMenuItem;
import javax.swing.JDialog ;
import javax.swing.JMenuBar ;
import javax.swing.border.LineBorder ;
import javax.swing.border.Border ;
import javax.swing.JMenu;
import javax.swing.JMenuItem;

public class Main {
    public static void main ( String [ ] args ) {
        // Creation of a new
        JDialog myJDialog =  new  JDialog ( ) ;
        myJDialog.setTitle ( "menu creating Example" ) ;
        myJDialog.setSize ( 300 , 200 ) ;
        // To illustrate, we'll create a red border
        Border border=  new  LineBorder ( Color .red) ;
        // create a menu bar
        JMenuBar bar =  new JMenuBar ( ) ;
        // We set the created border for our menu
        bar. setBorder ( border ) ;
        JMenu file =  new  JMenu ( "File" ) ;
        bar. add ( file ) ;
        JMenu Edit =  new  JMenu ( "Edit" ) ;
        bar. add ( Edit ) ;
        JMenu View =  new  JMenu ( "View" ) ;
        bar. add ( View ) ;

        JMenuItem NewFile =  new  JMenuItem ( "New File" ) ;
        JMenuItem Save =  new  JMenuItem ( "Save" ) ;
        JMenuItem OpenFile =  new  JMenuItem ( "Open File" ) ;

        file.add(NewFile);
        file.add(Save);
        file.add(OpenFile);

        JCheckBoxMenuItem checkBoxItem1 =  new  JCheckBoxMenuItem( "checkBoxItem1" ) ;
        JCheckBoxMenuItem checkBoxItem2 =  new  JCheckBoxMenuItem( "checkBoxItem2" ) ;
        JCheckBoxMenuItem checkBoxItem3 =  new  JCheckBoxMenuItem( "checkBoxItem3" ) ;
        JCheckBoxMenuItem checkBoxItem4 =  new  JCheckBoxMenuItem( "checkBoxItem4" ) ;

        Edit.add(checkBoxItem1);
        Edit.add(checkBoxItem2);
        Edit.add(checkBoxItem3);
        Edit.add(checkBoxItem4);

        // menu bar is set for the dialog
        myJDialog. setJMenuBar ( bar ) ;
        // We display our dialog
        myJDialog. setVisible ( true ) ;
    }
}
```
**Вывод:**
![[Ex4-Menu.png]]

Все конструкторы были переняты из суперкласса JMenuItem. Однако есть два дополнительных конструктора, которые можно использовать для прямой установки статуса флажка при создании JCheckBoxMenuItem:
```java
JCheckBoxMenuItem(String text, boolean b);
JCheckBoxMenuItem(String text, Icon icon, boolean b);
```
Используя логический параметр b, для флажка можно установить значение _true_ в значение selected (галочка присутствует) или значение _false_ в значение deselected (галочка отсутствует).

Также добавлены соответствующие методы получения и установки флажка. Соответствующий статус устанавливается с помощью метода void setState(логическое значение b) и состояние флажка запрашивается с помощью метода логическое значение getState(). В противном случае, a _JCheckBoxMenuItem_ может использоваться так же, как a JMenuItem.

### Класс JRadioButtonMenuItem

Класс JRadioButtonMenuItem является производным от _JMenuItem_. _JRadioButtonMenuItem_ состоит из переключателя и пункта меню. 

#### Пример 5. Как добавить RadioButton в меню в Java с помощью JRadioButtonMenuItem

```java
import java.awt.Color ; 
import javax.swing.JCheckBoxMenuItem;
import javax.swing.JDialog ; 
import javax.swing.JMenuBar ; 
import javax.swing.border.LineBorder ; 
import javax.swing.border.Border ;
import javax.swing.JMenu;
import javax.swing.JMenuItem;
import javax.swing.JRadioButtonMenuItem;
 
public class JmenuExamples {
    public static void main ( String [ ] args ) {
          // Creation of a new 
        JDialog myJDialog =  new  JDialog ( ) ; 
        myJDialog.setTitle ( "menu creating Example" ) ; 
        myJDialog.setSize ( 450 , 300 ) ; 
        // To illustrate, we'll create a red border
        Border border=  new  LineBorder ( Color .red) ; 
        // create a menu bar 
        JMenuBar bar =  new JMenuBar ( ) ; 
        // We set the created border for our menu 
        bar. setBorder ( border ) ; 
        JMenu file =  new  JMenu ( "File" ) ;
        bar. add ( file ) ; 
        JMenu Edit =  new  JMenu ( "Edit" ) ;
        bar. add ( Edit ) ; 
        JMenu View =  new  JMenu ( "View" ) ;
        bar. add ( View ) ; 
        
        JMenuItem NewFile =  new  JMenuItem ( "New File" ) ;
        JMenuItem Save =  new  JMenuItem ( "Save" ) ;
        JMenuItem OpenFile =  new  JMenuItem ( "Open File" ) ;
        
        file.add(NewFile);
        file.add(Save);
        file.add(OpenFile);
        
        JCheckBoxMenuItem checkBoxItem1 =  new  JCheckBoxMenuItem( "checkBoxItem1" ) ; 
        JCheckBoxMenuItem checkBoxItem2 =  new  JCheckBoxMenuItem( "checkBoxItem2" ) ; 
        JCheckBoxMenuItem checkBoxItem3 =  new  JCheckBoxMenuItem( "checkBoxItem3" ) ; 
        JCheckBoxMenuItem checkBoxItem4 =  new  JCheckBoxMenuItem( "checkBoxItem4" ) ; 
        
        Edit.add(checkBoxItem1);
        Edit.add(checkBoxItem2);
        Edit.add(checkBoxItem3);
        Edit.add(checkBoxItem4);
        
        JRadioButtonMenuItem radioButtonItem1 =  new  JRadioButtonMenuItem ( "JRadionButtonMenuItem1" ) ;
        JRadioButtonMenuItem radioButtonItem2 =  new  JRadioButtonMenuItem ( "JRadionButtonMenuItem2" ) ;
        JRadioButtonMenuItem radioButtonItem3 =  new  JRadioButtonMenuItem ( "JRadionButtonMenuItem3" ) ;
        JRadioButtonMenuItem radioButtonItem4 =  new  JRadioButtonMenuItem ( "JRadionButtonMenuItem4" ) ;
        
        View.add(radioButtonItem1);
        View.add(radioButtonItem2);
        View.add(radioButtonItem3);
        View.add(radioButtonItem4);
        // menu bar is set for the dialog       
        myJDialog. setJMenuBar ( bar ) ; 
        // We display our dialog 
        myJDialog. setVisible ( true ) ; 
    } 
}
```
**Вывод:**
![[Ex5-Menu.png]]

Все конструкторы были переняты из суперкласса _JMenuItem_. Однако, существуют два дополнительных конструктора , которые можно использовать для прямой установки состояния соответствующего переключателя:
```java
JRadioButtonMenuItem(String text, boolean  selected);
JRadioButtonMenuItem(String text, Icon icon, boolean selected);
```
Используя параметр Boolean, переключателю можно присвоить значение true с выбранным значением (круг с точкой) или с false значение отменено (круг без точки).

Класс _JRadioButtonMenuItem_ также предоставляет соответствующие методы setter и getter: соответствующий статус устанавливается с помощью параметра _void setSelected(boolean b)_ метод и состояние переключателя запрашиваются с помощью _boolean IsSelected()._ В противном случае a _JRadioButtonMenuItem_ может использоваться точно так же, как a _JMenuItem_.

### Класс JSeparator

Класс Java _javax.swing.JSeparator_ используется для разделения отдельных пунктов меню или групп меню разделительной линией. Объекты этого класса, таким образом, не имеют функционального значения, а лишь помогают сделать пользовательский интерфейс более понятным и, следовательно, более удобным для пользователя.

В дополнение к стандартному конструктору без параметров, JSeparator имеет другой конструктор, который можно использовать для указания выравнивания разделяющей линии:
```java
public JSeparator(int  orientation);
```
Константы из интерфейса класса _SwingConstants_ для выравнивания по горизонтали или вертикали могут быть переданы в качестве параметров:
```java
SwingConstants.HORIZONTAL;
SwingConstants.VERTICAL;
```
Если используется конструктор по умолчанию, выравнивание автоматически устанавливается на горизонтальное.

#### Пример 6. Как использовать JSeparator в java JMenu

```java
import java.awt.Color ;
import javax.swing.JCheckBoxMenuItem;
import javax.swing.JDialog ;
import javax.swing.JMenuBar ;
import javax.swing.border.LineBorder ;
import javax.swing.border.Border ;
import javax.swing.JMenu;
import javax.swing.JMenuItem;
import javax.swing.JRadioButtonMenuItem;
import javax.swing.JSeparator;

public class Main {
    public static void main (String [ ] args) {
        // Creation of a new
        JDialog myJDialog =  new  JDialog ( ) ;
        myJDialog.setTitle ( "menu creating Example" ) ;
        myJDialog.setSize ( 300 , 200 ) ;
        // To illustrate, we'll create a red border
        Border border=  new  LineBorder ( Color .red) ;
        // create a menu bar
        JMenuBar bar =  new JMenuBar ( ) ;
        // We set the created border for our menu
        bar. setBorder ( border ) ;
        JMenu file =  new  JMenu ( "File" ) ;
        bar. add ( file ) ;
        JMenu Edit =  new  JMenu ( "Edit" ) ;
        bar. add ( Edit ) ;
        JMenu View =  new  JMenu ( "View" ) ;
        bar. add ( View ) ;

        JSeparator sp=new JSeparator();
        JSeparator sp2=new JSeparator();

        JMenuItem NewFile =  new  JMenuItem ( "New File" ) ;
        JMenuItem Save =  new  JMenuItem ( "Save" ) ;
        JMenuItem OpenFile =  new  JMenuItem ( "Open File" ) ;

        file.add(NewFile);
        file.add(sp);
        file.add(Save);
        file.add(sp2);
        file.add(OpenFile);

        JCheckBoxMenuItem checkBoxItem1 =  new  JCheckBoxMenuItem( "checkBoxItem1" ) ;
        JCheckBoxMenuItem checkBoxItem2 =  new  JCheckBoxMenuItem( "checkBoxItem2" ) ;
        JCheckBoxMenuItem checkBoxItem3 =  new  JCheckBoxMenuItem( "checkBoxItem3" ) ;
        JCheckBoxMenuItem checkBoxItem4 =  new  JCheckBoxMenuItem( "checkBoxItem4" ) ;

        Edit.add(checkBoxItem1);
        Edit.add(checkBoxItem2);
        Edit.add(checkBoxItem3);
        Edit.add(checkBoxItem4);

        JRadioButtonMenuItem radioButtonItem1 =  new  JRadioButtonMenuItem ( "JRadionButtonMenuItem1" ) ;
        JRadioButtonMenuItem radioButtonItem2 =  new  JRadioButtonMenuItem ( "JRadionButtonMenuItem2" ) ;
        JRadioButtonMenuItem radioButtonItem3 =  new  JRadioButtonMenuItem ( "JRadionButtonMenuItem3" ) ;
        JRadioButtonMenuItem radioButtonItem4 =  new  JRadioButtonMenuItem ( "JRadionButtonMenuItem4" ) ;

        View.add(radioButtonItem1);
        View.add(radioButtonItem2);
        View.add(radioButtonItem3);
        View.add(radioButtonItem4);

        // Creation of an object of the class JSeparator
        // menu bar is set for the dialog
        myJDialog. setJMenuBar ( bar ) ;
        // We display our dialog
        myJDialog. setVisible ( true ) ;
    }
}
```
**Вывод:**
![[Ex6-Menu.png]]
_Метод **setOrientation**_ может использоваться для установки ориентации разделителя на горизонтальную или вертикальную, как в конструкторе, описанном выше. Соответствующий метод получения вызывается _getOrientation_ и возвращает ориентацию в виде _Целое число_ значение.

### Класс JPopupMenu

Контекстное меню, также известное как всплывающее меню, - это меню, которое открывается после щелчка правой кнопкой мыши. Это меню реализовано в Java с использованием класса _javax.swing.JPopupMenu_ . _Как и JMenuBar, JPopupMenu_ является контейнером для пунктов меню и также может содержать те же объекты.

_В дополнение к стандартному конструктору, в классе JPopupMenu_ есть еще один, который принимает заголовок контекстного меню в качестве параметра.

#### Пример 7

```java
import java.awt.Color ;
import javax.swing.JCheckBoxMenuItem;
import javax.swing.JDialog ;
import javax.swing.JMenuBar ;
import javax.swing.border.LineBorder ;
import javax.swing.border.Border ;
import javax.swing.JMenu;
import javax.swing.JMenuItem;
import javax.swing.JPopupMenu;
import javax.swing.JRadioButtonMenuItem;
import javax.swing.JSeparator;

public class Main {
    public static void main ( String [ ] args ) {
        // Creation of a new
        JDialog myJDialog =  new  JDialog ( ) ;
        myJDialog.setTitle ( "menu creating Example" ) ;
        myJDialog.setSize ( 300 , 200 ) ;
        // To illustrate, we'll create a red border
        Border border=  new  LineBorder ( Color .red) ;
        // create a menu bar
        JMenuBar bar =  new JMenuBar ( ) ;
        // We set the created border for our menu
        bar. setBorder ( border ) ;
        JMenu file =  new  JMenu ( "File" ) ;
        bar. add ( file );
        JMenu Edit =  new  JMenu ( "Edit" ) ;
        bar. add ( Edit );
        JMenu View =  new  JMenu ( "View" ) ;
        bar. add ( View );

        // Creation of an object of the class JSeparator
        JSeparator sp=new JSeparator();
        JSeparator sp2=new JSeparator();
        JSeparator sp3=new JSeparator();

        JMenuItem NewFile =  new  JMenuItem ( "New File" ) ;
        JMenuItem Save =  new  JMenuItem ( "Save" ) ;
        JMenuItem OpenFile =  new  JMenuItem ( "Open File" ) ;

        file.add(NewFile);
        file.add(sp);
        file.add(Save);
        file.add(sp2);
        file.add(OpenFile);

        JCheckBoxMenuItem checkBoxItem1 =  new  JCheckBoxMenuItem( "checkBoxItem1" ) ;
        JCheckBoxMenuItem checkBoxItem2 =  new  JCheckBoxMenuItem( "checkBoxItem2" ) ;
        JCheckBoxMenuItem checkBoxItem3 =  new  JCheckBoxMenuItem( "checkBoxItem3" ) ;
        JCheckBoxMenuItem checkBoxItem4 =  new  JCheckBoxMenuItem( "checkBoxItem4" ) ;

        Edit.add(checkBoxItem1);
        Edit.add(checkBoxItem2);
        Edit.add(checkBoxItem3);
        Edit.add(checkBoxItem4);

        JRadioButtonMenuItem radioButtonItem1 =  new  JRadioButtonMenuItem ( "JRadionButtonMenuItem1" ) ;
        JRadioButtonMenuItem radioButtonItem2 =  new  JRadioButtonMenuItem ( "JRadionButtonMenuItem2" ) ;
        JRadioButtonMenuItem radioButtonItem3 =  new  JRadioButtonMenuItem ( "JRadionButtonMenuItem3" ) ;
        JRadioButtonMenuItem radioButtonItem4 =  new  JRadioButtonMenuItem ( "JRadionButtonMenuItem4" ) ;

        View.add(radioButtonItem1);
        View.add(radioButtonItem2);
        View.add(radioButtonItem3);
        View.add(radioButtonItem4);

        JMenuItem popItem =  new  JMenuItem ( "Open File");
        JRadioButtonMenuItem popRadio=  new  JRadioButtonMenuItem ( "popRadio",true ) ;
        JCheckBoxMenuItem PopcheckBox =  new  JCheckBoxMenuItem( "PopcheckBox",true ) ;

        // Creation of a JPopupMenu object
        JPopupMenu pop =  new     JPopupMenu();

        pop. setLocation ( 100 , 100 ) ;
        // We add our menu items to our context menu
        pop. add(popItem);
        pop. add(sp3);
        pop. add(PopcheckBox);
        pop. add(popRadio);
        // menu bar is set for the dialog
        myJDialog. setJMenuBar ( bar ) ;
        // We display our dialog
        myJDialog. setVisible ( true ) ;
        pop. setVisible ( true ) ;
    }
}
```
**Вывод:**
![[Ex7-Menu.png]]