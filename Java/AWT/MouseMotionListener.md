#Java #awt #MouseMotionListener

## Интерфейс MouseMotionListener

2024-05-28 15:57

Интерфейс **MouseMotionListener** используется для получения событий движения мыши в компоненте. Класс, который обрабатывает события движения мыши, должен реализовывать этот интерфейс.

## Объявление класса

Ниже приводится объявление для **java.awt.event.MouseMotionListener** интерфейс −
```java
public inteface MouseMotionListener extends EventListener;
```

## Методы интерфейса

| Sr.No. | Метод и описание                                                                                                         |
| ------ | ------------------------------------------------------------------------------------------------------------------------ |
| 1      | **void mouseDragged(MouseEvent e)**<br>Вызывается при нажатии кнопки мыши на компоненте и последующем перетаскивании.    |
| 2      | **void mouseMoved(MouseEvent e)**<br>Вызывается, когда курсор мыши был перемещен на компонент, но кнопки не были нажаты. |

#### Пример 1

```java
import java.awt.*;  
import java.awt.event.*;  
import javax.swing.*;  
  
public class Main {  
    private JFrame mainFrame;  
    private JLabel headerLabel;  
    private JLabel statusLabel;  
    private JPanel controlPanel;  
  
    public Main(){  
        prepareGUI();  
    }  
    public static void main(String[] args){  
        Main  swingListenerDemo = new Main();  
        swingListenerDemo.showMouseMotionListenerDemo();  
    }  
    private void prepareGUI(){  
        mainFrame = new JFrame("Java SWING Examples");  
        mainFrame.setSize(400,400);  
        mainFrame.setLayout(new GridLayout(3, 1));  
  
        headerLabel = new JLabel("",JLabel.CENTER );  
        statusLabel = new JLabel("",JLabel.CENTER);  
        statusLabel.setSize(350,100);  
  
        mainFrame.addWindowListener(new WindowAdapter() {  
            public void windowClosing(WindowEvent windowEvent){  
                System.exit(0);  
            }  
        });  
        controlPanel = new JPanel();  
        controlPanel.setLayout(new FlowLayout());  
  
        mainFrame.add(headerLabel);  
        mainFrame.add(controlPanel);  
        mainFrame.add(statusLabel);  
        mainFrame.setVisible(true);  
    }  
    private void showMouseMotionListenerDemo(){  
        headerLabel.setText("Listener in action: MouseMotionListener");  
  
        JPanel panel = new JPanel();  
        panel.setBackground(Color.magenta);  
        panel.setLayout(new FlowLayout());  
        panel.addMouseMotionListener(new CustomMouseMotionListener());  
  
        JLabel msglabel  
                = new JLabel("Welcome to TutorialsPoint SWING Tutorial.",JLabel.CENTER);  
  
        panel.add(msglabel);  
        controlPanel.add(panel);  
        mainFrame.setVisible(true);  
    }  
    class CustomMouseMotionListener implements MouseMotionListener {  
        public void mouseDragged(MouseEvent e) {  
            statusLabel.setText("Mouse Dragged: ("+e.getX()+", "+e.getY() +")");  
        }  
        public void mouseMoved(MouseEvent e) {  
            statusLabel.setText("Mouse Moved: ("+e.getX()+", "+e.getY() +")");  
        }  
    }  
}
```
**Вывод:**
![[Ex1-MouseMotionListener.png]]