#Java #awt #KeyEvent

## Класс KeyEvent

2024-05-27 16:13

При вводе с клавиатуры генерируется **_KeyEvent_**. Существует три типа ключевых событий, которые идентифицируются этими целочисленными константами:
- **KEY_PRESSED**,
- **KEY_RELEASED**, 
- **KEY_TYPED**. 
Первые два события генерируются при нажатии или отпускании любой клавиши.  Последнее событие происходит только при генерации символа. Не все нажатия клавиш приводят к появлению символов. Например, нажатие shift не генерирует символ.

### Поле

Ниже приведены поля для класса java.awt.InputEvent:
- static char CHAR_UNDEFINED - События KEY_PRESSED и KEY_RELEASED, которые не сопоставляются с допустимым символом Unicode, используют его для значения keyChar.
- static int KEY_FIRST - Первое число в диапазоне идентификаторов, используемых для ключевых событий.
- static int KEY_LAST - Последнее число в диапазоне идентификаторов, используемых для ключевых событий.
- static int KEY_LOCATION_LEFT - Константа, указывающая, что нажатая или отпущенная клавиша находится в левом месте клавиши (для этой клавиши может быть более одного места).
- static int KEY_LOCATION_NUMPAD - Константа, указывающая, что ключевое событие возникло на цифровой клавиатуре или с виртуальной клавиши, соответствующей цифровой клавиатуре.
- static int KEY_LOCATION_RIGHT - Константа, указывающая, что нажатая или отпущенная клавиша находится в правильном месте клавиши (для этой клавиши может быть несколько возможных мест).
- static int KEY_LOCATION_STANDARD - Константа, указывающая, что нажатая или отпущенная клавиша не распознается как левая или правая версия клавиши и не была создана на цифровой клавиатуре (или возникла не с виртуальной клавиши, соответствующей цифровой клавиатуре).
- static int KEY_LOCATION_UNKNOWN - Константа, указывающая, что keyLocation не определено или не имеет значения.
- static int KEY_PRESSED - Событие «нажата клавиша».
- static int KEY_RELEASED - Событие «ключ отпущен».
- static int KEY_TYPED - Событие "нажата клавиша".
- static int VK_0 - VK_0 - VK_9 такие же, как ASCII от '0' до '9' (0 × 30 - 0 × 39)
- static int VK_1
- static int VK_2
- static int VK_3
- static int VK_4
- static int VK_5
- static int VK_6
- static int VK_7
- static int VK_8
- static int VK_9
- static int VK_A - VK_A - VK_Z такие же, как ASCII от 'A' до 'Z' (0 × 41 - 0 × 5A)
- static int VK_ACCEPT - Константа для функциональной клавиши Accept или Commit.
- static int VK_ADD
- static int VK_AGAIN
- static int VK_ALL_CANDIDATES - Константа для функциональной клавиши «Все кандидаты».
- static int VK_ALPHANUMERIC - Константа для буквенно-цифровой функциональной клавиши.
- static int VK_ALT
- static int VK_ALT_GRAPH - Константа для функциональной клавиши AltGraph.
- static int VK_AMPERSAND
- static int VK_ASTERISK
- static int VK_AT - Константа для клавиши "@".
- static int VK_B
- static int VK_BACK_QUOTE
- static int VK_BACK_SLASH - Константа для обратной косой черты "\"
- static int VK_BACK_SPACE
- static int VK_BEGIN - Константа для ключа Begin.
- static int VK_BRACELEFT
- static int VK_BRACERIGHT
- static int VK_C
- static int VK_CANCEL
- static int VK_CAPS_LOCK
- static int VK_CIRCUMFLEX - Константа для клавиши «^».
- static int VK_CLEAR
- static int VK_CLOSE_BRACKET - Константа для клавиши закрывающей скобки "]"
- static int VK_CODE_INPUT - Константа для функциональной клавиши ввода кода.
- static int VK_COLON - Константа для клавиши ":".
- static int VK_COMMA - Константа для клавиши запятой, ","
- static int VK_COMPOSE - Константа для функциональной клавиши Compose.
- static int VK_CONTEXT_MENU - Константа для клавиши контекстного меню Microsoft Windows.
- static int VK_CONTROL
- static int VK_CONVERT - Константа для функциональной клавиши Convert.
- static int VK_COPY
- static int VK_CUT
- static int VK_D
- static int VK_DEAD_ABOVEDOT
- static int VK_DEAD_ABOVERING
- static int VK_DEAD_ACUTE
- static int VK_DEAD_BREVE
- static int VK_DEAD_CARON
- static int VK_DEAD_CEDILLA
- static int VK_DEAD_CIRCUMFLEX
- static int VK_DEAD_DIAERESIS
- static int VK_DEAD_DOUBLEACUTE
- static int VK_DEAD_GRAVE
- static int VK_DEAD_IOTA
- static int VK_DEAD_MACRON
- static int VK_DEAD_OGONEK
- static int VK_DEAD_SEMIVOICED_SOUND
- static int VK_DEAD_TILDE
- static int VK_DEAD_VOICED_SOUND
- static int VK_DECIMAL
- static int VK_DELETE
- static int VK_DIVIDE
- static int VK_DOLLAR - Константа для клавиши «$».
- static int VK_DOWN - Константа для клавиши со стрелкой вниз без цифровой клавиатуры.
- static int VK_E
- static int VK_END
- static int VK_ENTER
- static int VK_EQUALS - Константа для ключа равенства, "="
- static int VK_ESCAPE
- static int VK_EURO_SIGN - Константа для ключа знака валюты евро.
- static int VK_EXCLAMATION_MARK- Постоянный знак "!" ключ.
- static int VK_F
- static int VK_F1 - Константа для функциональной клавиши F1.
- static int VK_F10 - Константа для функциональной клавиши F10.
- static int VK_F11 - Константа для функциональной клавиши F11.
- static int VK_F12 - Константа для функциональной клавиши F12.
- static int VK_F13 - Константа для функциональной клавиши F13.
- static int VK_F14 - Константа для функциональной клавиши F14.
- static int VK_F15 - Константа для функциональной клавиши F15.
- static int VK_F16 - Константа для функциональной клавиши F16.
- static int VK_F17 - Константа для функциональной клавиши F17.
- static int VK_F18 - Константа для функциональной клавиши F18.
- static int VK_F19 - Константа для функциональной клавиши F19.
- static int VK_F2 - Константа для функциональной клавиши F2.
- static int VK_F20 - Константа для функциональной клавиши F20.
- static int VK_F21 - Константа для функциональной клавиши F21.
- static int VK_F22 - Константа для функциональной клавиши F22.
- static int VK_F23 - Константа для функциональной клавиши F23.
- static int VK_F24 - Константа для функциональной клавиши F24.
- static int VK_F3 - Константа для функциональной клавиши F3.
- static int VK_F4 - Константа для функциональной клавиши F4.
- static int VK_F5 - Константа для функциональной клавиши F5.
- static int VK_F6 - Константа для функциональной клавиши F6.
- static int VK_F7 - Константа для функциональной клавиши F7.
- static int VK_F8 - Константа для функциональной клавиши F8.
- static int VK_F9 - Константа для функциональной клавиши F9.
- static int VK_FINAL
- static int VK_FIND
- static int VK_FULL_WIDTH - Константа для функциональной клавиши полноширинных символов.
- static int VK_G
- static int VK_GREATER
- static int VK_H
- static int VK_HALF_WIDTH - Константа для функциональной клавиши символов половинной ширины.
- static int VK_HELP
- static int VK_HIRAGANA - Константа для функциональной клавиши хирагана.
- static int VK_HOME
- static int VK_I
- static int VK_INPUT_METHOD_ON_OFF - Константа для кнопки включения / выключения метода ввода.
- static int VK_INSERT
- static int VK_INVERTED_EXCLAMATION_MARK - Константа для клавиши с перевернутым восклицательным знаком.
- static int VK_J
- static int VK_JAPANESE_HIRAGANA - Константа для функциональной клавиши японского языка хирагана.
- static int VK_JAPANESE_KATAKANA - Константа для функциональной клавиши японско-катакана.
- static int VK_JAPANESE_ROMAN - Константа для функциональной клавиши японско-римского алфавита.
- static int VK_K
- static int VK_KANA
- static int VK_KANA_LOCK - Константа для блокировки функциональной клавиши Кана.
- static int VK_KANJI
- static int VK_KATAKANA - Константа для функциональной клавиши Катакана.
- static int VK_KP_DOWN - Константа для клавиши со стрелкой вниз на цифровой клавиатуре.
- static int VK_KP_LEFT - Константа для клавиши со стрелкой влево на цифровой клавиатуре.
- static int VK_KP_RIGHT - Константа для клавиши со стрелкой вправо цифровой клавиатуры.
- static int VK_KP_UP - Константа для клавиши со стрелкой вверх на цифровой клавиатуре.
- static int VK_L
- static int VK_LEFT - Константа для клавиши со стрелкой влево без цифровой клавиатуры.
- static int VK_LEFT_PARENTHESIS - Константа для клавиши "(".
- static int VK_LESS
- static int VK_M
- static int VK_META
- static int VK_MINUS - Константа для клавиши «минус», «-»
- static int VK_MODECHANGE
- static int VK_MULTIPLY
- static int VK_N
- static int VK_NONCONVERT - Константа для функциональной клавиши "Не преобразовывать".
- static int VK_NUM_LOCK
- static int VK_NUMBER_SIGN - Константа для клавиши "#".
- static int VK_NUMPAD0
- static int VK_NUMPAD1
- static int VK_NUMPAD2
- static int VK_NUMPAD3
- static int VK_NUMPAD4
- static int VK_NUMPAD5
- static int VK_NUMPAD6
- static int VK_NUMPAD7
- static int VK_NUMPAD8
- static int VK_NUMPAD9
- static int VK_O
- static int VK_OPEN_BRACKET - Константа для ключа открытой скобки "["
- static int VK_P
- static int VK_PAGE_DOWN
- static int VK_PAGE_UP
- static int VK_PASTE
- static int VK_PAUSE
- static int VK_PERIOD - Константа для ключа периода "."
- static int VK_PLUS - Константа для клавиши «+».
- static int VK_PREVIOUS_CANDIDATE - Константа для функциональной клавиши Предыдущий кандидат.
- static int VK_PRINTSCREEN
- static int VK_PROPS
- static int VK_Q
- static int VK_QUOTE
- static int VK_QUOTEDBL
- static int VK_R
- static int VK_RIGHT - Константа для клавиши со стрелкой вправо без цифровой клавиатуры.
- static int VK_RIGHT_PARENTHESIS - Константа для клавиши ")".
- static int VK_ROMAN_CHARACTERS - Константа для функциональной клавиши латинских букв.
- static int VK_S
- static int VK_SCROLL_LOCK
- static int VK_SEMICOLON - Константа для ключа с точкой с запятой ";"
- static int VK_SEPARATER - Эта константа устарела и включена только для обратной совместимости.
- static int VK_SEPARATOR - Константа для клавиши Numpad Separator.
- static int VK_SHIFT
- static int VK_SLASH - Константа для клавиши косой черты "/"
- static int VK_SPACE
- static int VK_STOP
- static int VK_SUBTRACT
- static int VK_T
- static int VK_TAB
- static int VK_U
- static int VK_UNDEFINED - Это значение используется, чтобы указать, что keyCode неизвестен.
- static int VK_UNDERSCORE - Константа для клавиши «_».
- static int VK_UNDO
- static int VK_UP - Константа для клавиши со стрелкой вверх без цифровой клавиатуры.
- static int VK_V
- static int VK_W
- static int VK_WINDOWS - Константа для клавиши Microsoft Windows "Windows".
- static int VK_X
- static int VK_Y
- static int VK_Z

### Конструкторы классов

| N   | Конструктор и описание                                                                                                      |
| --- | --------------------------------------------------------------------------------------------------------------------------- |
| 1   | **KeyEvent(Component source, int id, long when, int modifiers, int keyCode)**<br><br>Устарело. с JDK1.1                     |
| 2   | **KeyEvent(Component source, int id, long when, int modifiers, int keyCode, char keyChar)**<br><br>Создает объект KeyEvent. |
| 3   | **KeyEvent(Component source, int id, long when, int modifiers, int keyCode, char keyChar, int keyLocation)**                |

Здесь _source_ является ссылкой на [Component](Component), сгенерировавший событие. Тип события определяется с помощью _id_. Системное время, в которое была нажата клавиша, передается в _when._ Аргумент _modifiers_ указывает, какие модификаторы были нажаты, когда произошло это ключевое событие. Код виртуального ключа _keyCode_, такой, как **VK_UP**, **VK_A** и так далее, передается в _коде._ Эквивалент символа (если он существует) передается в _keyChar_. 

Если не существует допустимого символа, то _keyChar_ содержит **CHAR_UNDEFINED**. Для событий с типом **KEY_TYPED** будет содержать **VK_UNDEFINED**.

### Методы класса

| Sr. No. | Метод и описание                                                                                                                                     |
| ------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1       | **char getKeyChar()**<br><br>Возвращает символ, связанный с ключом в этом событии.                                                                   |
| 2       | **int getKeyCode()**<br><br>Возвращает целочисленный keyCode, связанный с ключом в этом событии.                                                     |
| 3       | **int getKeyLocation()**<br><br>Возвращает расположение ключа, который вызвал это событие ключа.                                                     |
| 4       | **static String getKeyModifiersText(int modifiers)**<br><br>Возвращает строку с описанием клавиш-модификаторов, например «Shift» или «Ctrl + Shift». |
| 5       | **static String getKeyText(int keyCode)**<br><br>Возвращает строку, описывающую keyCode, например «HOME», «F1» или «A».                              |
| 6       | **boolean isActionKey()**<br><br>Возвращает, является ли ключ в этом событии ключом «действия».                                                      |
| 7       | **String paramString()**<br><br>Возвращает строку параметра, идентифицирующую это событие.                                                           |
| 8       | **void setKeyChar(char keyChar)**<br><br>Установите значение keyChar, чтобы указать логический символ.                                               |
| 9       | **void setKeyCode(int keyCode)**<br><br>Установите значение keyCode, чтобы указать физический ключ.                                                  |
| 10      | **void setModifiers(int modifiers)**<br><br>Не рекомендуется. с JDK1.1.4                                                                             |

### Унаследованные методы

Этот класс наследует методы от следующих классов:
- java.awt.event.InputEvent
- java.awt.event.ComponentEvent
- java.awt.AWTEvent
- java.util.EventObject
- [java.lang.Object](Object)

#### Пример 1

```java
import javax.swing.*;  
import java.awt.*;  
import java.awt.event.KeyEvent;  
import java.awt.event.KeyListener;  
  
public class Main  implements KeyListener {  
    @Override  
    public void keyTyped(KeyEvent e) {  
        System.out.println("Key Type Event ");  
    }  
  
    @Override  
    public void keyPressed(KeyEvent e) {  
        System.out.println("Key Press Event ");  
    }  
  
    @Override  
    public void keyReleased(KeyEvent e) {  
        System.out.println("Key Release Event ");  
    }  
  
    public static void main(String[] args) {  
        JFrame jf = new JFrame("MyListener");  
        jf.addKeyListener(new Main());  
        jf.setBounds(300,300,200,200);  
        jf.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);  
        jf.setVisible(true);  
    }  
}
```
**Вывод в консоле:**
Когда я набираю «1», консоль печатает:
```java
Key Type Event
```

Затем введите «A», и консоль напечатает:
```java
Key Type Event 
Key Press Event 
Key Type Event 
Key Release Event 
```

Затем снова введите «Shift», и консоль напечатает:
```java
Key Type Event 
Key Press Event 
Key Type Event 
Key Release Event 
Key Press Event 
Key Release Event 
Key Press Event 
Key Release Event 
```

#### Пример 2

```java
import javax.swing.*;
import java.awt.*;
import java.awt.event.KeyEvent;
import java.awt.event.KeyListener;

public class MyListener  implements KeyListener {
	@Override
	public void keyTyped(KeyEvent e) {
		System.out.println("Key Type Event ");
		System.out.println("Key Code： " + e.getKeyCode());
		System.out.println("Key Char： " + e.getKeyChar());
	}

	@Override
	public void keyPressed(KeyEvent e) {
		System.out.println("Key Press Event ");
	}

	@Override
	public void keyReleased(KeyEvent e) {

	}

	public static void main(String[] args) {
		JFrame jf = new JFrame("MyListener");
		jf.addKeyListener(new MyListener());
		jf.setBounds(300,300,800,600);
		jf.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		jf.setVisible(true);
	}
}
```
**Вывод в консоле:**
После ввода "а"  
```java
Key Press Event 
Key Type Event 
Key Code： 0
Key Char： a
```

#### Пример 3. Перемещение изображения в окне с помощью клавиш

```java
import javax.swing.*;
import java.awt.event.KeyEvent;
import java.awt.event.KeyListener;

public class Main implements KeyListener {
    static JLabel jl = new JLabel();

    @Override
    public void keyTyped(KeyEvent e) {
    }

    @Override
    public void keyPressed(KeyEvent e) {
        if (e.getKeyCode() == KeyEvent.VK_LEFT) {
            jl.setLocation(jl.getX()-10,jl.getY());
        }

        if (e.getKeyCode() == KeyEvent.VK_RIGHT) {
            jl.setLocation(jl.getX()+10,jl.getY());
        }

        if (e.getKeyCode() == KeyEvent.VK_UP) {
            jl.setLocation(jl.getX(),jl.getY()-10);
        }

        if (e.getKeyCode() == KeyEvent.VK_DOWN) {
            jl.setLocation(jl.getX(),jl.getY()+10);
        }
    }

    @Override
    public void keyReleased(KeyEvent e) {
    }

    public static void main(String[] args) {
        JFrame jf = new JFrame("Moving Ball");
        jf.addKeyListener(new Main());
        jf.setBounds(300,300,500,500);
        jf.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        ImageIcon pic = new ImageIcon("C:\\book\\Icon.jpg");

        jl.setIcon(pic);
        jf.add(jl);
        jf.setVisible(true);
    }
}
```
**Вывод:**
![[Ex1-KeyEvent.png]]