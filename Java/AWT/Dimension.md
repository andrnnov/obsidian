#Java #awt #Dimension

## Класс Dimension

2024-05-22 16:26

Класс **_Dimension_** является частью Java [AWT](AWT). Он содержит высоту и ширину компонента в целочисленном формате, а также двойной точности. Использование класса **_Dimension_** заключается в том, что многие функции Java [AWT](AWT) и [Swing](Swing) возвращают объект **_Dimension_**.

### Конструкторы класса Dimension

1. **Dimension()** : создаст новый объект с нулевой высотой и шириной.
2. **Dimension (Dimension d)** : создаст новый объект с той же высотой и шириной, что и указанный объект.
3. **Dimension(int w, int h)** : создаст новый объект с указанной высотой и шириной.

### Методы класса

| Метод                                | Объяснение                                                        |
| ------------------------------------ | ----------------------------------------------------------------- |
| equals(Object o)                     | проверяет, равны ли двухмерные объекты.                           |
| getHeight()                          | возвращает высоту объекта измерения                               |
| getWidth()                           | возвращает ширину объекта измерения                               |
| getSize()                            | возвращает размер объекта измерения.                              |
| hashCode()                           | возвращает хэш-код для измерения.                                 |
| setSize(Dimension d)                 | установить размер объекта по указанному размеру                   |
| setSize(double width, double height) | установите высоту и ширину на указанное двойное значение          |
| setSize(int width, int height)       | установите высоту и ширину для указанного целочисленного значения |

#### Программа 1. Программа для отображения функций класса Dimension (целочисленная точность)

```java
// Java Program to show the functions
// of dimension class(Integer precision)
import java.awt.*;
class dimen {
 
    // Main Method
    public static void main(String args[])
    {
 
        // create dimension
        Dimension d = new Dimension();
        Dimension d1 = new Dimension(20, 30);
        Dimension d2 = new Dimension(d1);
 
        // set height and width of dimension d
        d.setSize(30, 30);
 
        // equating dimensions
        System.out.println("Dimension d and d1 " + 
                    "are equal = " + d.equals(d1));
                     
        System.out.println("Dimension d and d1 " + 
                "are equal = " + d1.equals(d2));
 
        // print hashcode
        System.out.println("Hashcode of Dimension " + 
                            "d = " + d.hashCode());
 
        // display dimension
        display(d, "Dimension d");
        display(d1, "Dimension d1");
        display(d2, "Dimension d2");
    }
 
    // display dimension
    public static void display(Dimension d, String s)
    {
        System.out.println(s +" Height = " + d.getHeight() + 
                                " Width= " + d.getWidth());
    }
}
```
**Вывод:**
<p style="background-color: navy; color: yellow">
Dimension d and d1 are equal = false<br>
Dimension d and d1 are equal = true<br>
Hashcode of Dimension d = 1860<br>
Dimension d Height = 30.0 Width= 30.0<br>
Dimension d1 Height = 30.0 Width= 20.0<br>
Dimension d2 Height = 30.0 Width= 20.0</p>
