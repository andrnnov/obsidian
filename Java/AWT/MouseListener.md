#Java #awt #MouseListener

## Интерфейс MouseListener

2024-05-28 15:35

Класс, который обрабатывает [MouseEvent](MouseEvent), должен реализовывать этот интерфейс. Объект этого класса должен быть зарегистрирован в компоненте. Объект может быть зарегистрирован с помощью **addMouseListener()** метода.

### Объявление интерфейса

Ниже приводится объявление для **java.awt.event.MouseListener** интерфейс −
```java
public interface MouseListener extends EventListener;
```

## Методы интерфейса

| N   | Метод и описание                                                                                                    |
| --- | ------------------------------------------------------------------------------------------------------------------- |
| 1   | **void mouseClicked(MouseEvent e)**<br>Вызывается, когда кнопка мыши была нажата (нажата и отпущена) на компоненте. |
| 2   | **void mouseEntered(MouseEvent e)**<br>Вызывается при наведении курсора мыши на компонент.                          |
| 3   | **void mouseExited(MouseEvent e)**<br>Вызывается при выходе мыши из компонента.                                     |
| 4   | **void mousePressed(MouseEvent e)**<br>Вызывается при нажатии кнопки мыши на компоненте.                            |
| 5   | **void mouseReleased(MouseEvent e)**<br>Вызывается, когда на компоненте отпущена кнопка мыши.                       |

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
        swingListenerDemo.showMouseListenerDemo();
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
    private void showMouseListenerDemo(){
        headerLabel.setText("Listener in action: MouseListener");

        JPanel panel = new JPanel();
        panel.setBackground(Color.magenta);
        panel.setLayout(new FlowLayout());
        panel.addMouseListener(new CustomMouseListener());

        JLabel msglabel =
                new JLabel("Welcome to TutorialsPoint SWING Tutorial.",JLabel.CENTER);
        panel.add(msglabel);

        msglabel.addMouseListener(new CustomMouseListener());
        panel.add(msglabel);

        controlPanel.add(panel);
        mainFrame.setVisible(true);
    }
    class CustomMouseListener implements MouseListener {
        public void mouseClicked(MouseEvent e) {
            statusLabel.setText("Mouse Clicked: ("+e.getX()+", "+e.getY() +")");
        }
        public void mousePressed(MouseEvent e) {
            statusLabel.setText("Mouse Pressed");
        }
        public void mouseReleased(MouseEvent e) {
            statusLabel.setText("Mouse Released");
        }
        public void mouseEntered(MouseEvent e) {
            statusLabel.setText("Mouse Entered");
        }
        public void mouseExited(MouseEvent e) {
            statusLabel.setText("Mouse Exited");
        }
    }
}
```
**Вывод:**
![[Ex1-MouseListener.png]]