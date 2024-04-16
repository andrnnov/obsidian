#Java #Collection #Vector

## Класс Vector

2024-04-16 14:50

Одним из их основных недостатков массивов в Java является постоянство размера. Создав массив определенного размера, вы не сможете изменить его позже. В языке Java существует несколько классов Java Collection framework, которые решают эту проблему. Одним из них является класс Java _Vector_. 

_Vector_ из Java Collection Framework устраняет проблему статического размера массивов. Java _Vector_ - это своего рода динамический массив, который может увеличиваться или уменьшаться в размерах. Используя класс коллекции _Vector_, мы можем хранить группу элементов в виде простых объектов и манипулировать ими с помощью различных методов. Класс _Vector_ доступен из пакета java.util. 

Класс _Vector_ уже довольно старый, и позже появились коллекции, которые могут заменить его в подавляющем большинстве случаев. Популярным “аналогом” Java _Vector_ является класс [_ArrayList_](Class-ArrayList). Наиболее важным отличием этих классов друг от друга является то, что _Vector_ синхронизирован, а [_ArrayList_](Class-ArrayList) - нет. 

### Конструкторы

**1. Vector():** создает вектор по умолчанию с начальной емкостью 10.
```java
Vector<E> v = new Vector<E>();
```
**2. Vector(int size):** создает вектор, начальная емкость которого определяется размером.
```java
Vector<E> v = new Vector<E>(int size);
```
**3. Vector(int size, int incr):** Создает вектор, начальная емкость которого определяется размером size, а приращение задается параметром incr. Он определяет количество элементов, которые необходимо выделить каждый раз, когда размер вектора увеличивается.
```java
Vector<E> v = new Vector<E>(int size, int incr);
```
**4. Vector(Collection c):** Создает вектор, содержащий элементы коллекции c.
```java
Vector<E> v = new Vector<E>(Collection c);
```

### Методы класса _Vector_

Методы класса _Vector_:
- void add(int index, Object element) вставляет указанный элемент в указанную позицию вектора.
- boolean add(Object o) добавляет указанный элемент в конец вектора.
- boolean addAll(Collection c) добавляет все элементы в указанной коллекции в конец вектора в том порядке, в котором они возвращаются указанным итератором коллекции.
- boolean addAll(int index, Collection c) вставляет все элементы из указанной коллекции в вектор в указанной позиции.
- void addElement(Object obj) добавляет указанный компонент в конец этого вектора, увеличивая его размер на единицу.
- int capacity() возвращает текущую емкость этого вектора.
- void clear() удаляет все элементы из этого вектора.
- Object clone() возвращает клон этого вектора.
- boolean contains(Object elem) проверяет, является ли указанный объект компонентом в этом векторе.
- boolean containsAll(Collection c) возвращает true, если вектор содержит все элементы указанной коллекции.
- void copyInto(Object[] anArray) копирует компоненты этого вектора в указанный массив.
- Object elementAt(int index) возвращает компонент с указанным индексом.
- Enumeration elements() возвращает перечисление компонентов этого вектора.
- void ensureCapacity(int minCapacity) увеличивает емкость этого вектора, при необходимости, чтобы гарантировать, что он может содержать по крайней мере количество компонентов, указанное в аргументе минимальной емкости.
- boolean equals(Object o) сравнивает указанный объект с этим вектором.
- Object FirstElement() возвращает первый компонент (элемент с индексом 0) этого вектора.
- Object get(int index) возвращает элемент в указанной позиции в этом векторе.
- int hashCode() возвращает значение хэш-кода для этого вектора.
- int indexOf(Object elem) выполняет поиск первого вхождения данного аргумента, проверяя равенство с помощью метода equals.
- int indexOf(Object elem, int index) выполняет поиск первого вхождения данного аргумента, начиная с индекса, и проверяет равенство с помощью метода equals.
- void insertElementAt(Object obj, int index) вставляет указанный объект в качестве компонента в этот вектор с указанным индексом.
- boolean isEmpty() проверяет этот вектор на наличие отсутствующих компонентов.
- Object lastElement() возвращает последний компонент вектора.
- int lastIndexOf(Object elem) возвращает индекс последнего появления указанного объекта в этом векторе.
- int lastIndexOf(Object elem, int index) выполняет обратный поиск указанного объекта, начиная с указанного индекса, и возвращает ему индекс.
- Object remove(int index) удаляет элемент в указанной позиции в этом векторе.
- boolean remove(Object o) удаляет первое вхождение указанного элемента в этом векторе. Если вектор не содержит элемента, он не изменяется.
- boolean removeAll(Collection c) удаляет все элементы из вектора, которые содержатся в указанной коллекции.
- void removeAllElements() удаляет все компоненты из вектора и устанавливает его размер равным нулю.
- boolean removeElement(Object obj) удаляет первое (с наименьшим индексом) вхождение аргумента из этого вектора.
- void removeElementAt(int index) удаляет элемент по индексу.
- protected void RemoveRange(int fromIndex, int toIndex) удаляет из этого списка все элементы, индекс которых находится между fromIndex включительно и toIndex исключительно.
- boolean retainAll(Collection c) сохраняет только элементы в векторе, которые содержатся в указанной коллекции.
- Object set(int index, Object element) заменяет элемент в указанной позиции в этом векторе на указанный элемент.
- void setElementAt(Object obj, int index) устанавливает компонент с указанным индексом этого вектора в качестве данного объекта.
- void setSize(int NewSize) задает размер этого вектора.
- int size() возвращает количество компонентов в этом векторе.
- List subList(int fromIndex, int toIndex) возвращает представление (view) части этого списка [_List_](List) между fromIndex включительно и toIndex исключительно.
- Object[] toArray() возвращает массив, содержащий все элементы этого вектора в правильном порядке.
- Object[] toArray(Object[] a) возвращает массив, содержащий все элементы этого вектора в правильном порядке; типом выполнения возвращаемого массива является тип указанного массива.
- String toString() возвращает строковое представление этого вектора, содержащее строковое представление каждого элемента.
- void trimToSize() ограничивает емкость этого вектора до текущего размера вектора.

#### Пример 1. 

Пример, демонстрирующий, как использовать вектор в Java
```java
import java.util.Vector;

public class VectorExample {

   public static void main(String[] args) {
       Vector vector = new Vector();
       System.out.println("the size of the empty vector = " +  vector.size());
       //adding some vector elements
       vector.add("Johnny");
       vector.add("Ivy");
       vector.add("Ricky");
       System.out.println(vector);

       //adding more vector elements
       vector.add("Johnny");
       vector.add("Paul");
       System.out.println(vector);
       System.out.println("the size of the vector = " +  vector.size());
       System.out.println("the first element of the vector = " + vector.firstElement());

       //here the program will print out the first appearance of "Johnny" element
       System.out.println(vector.indexOf("Johnny"));
       //program will print out the first appearance of "Johnny" element starting from the element 1
       System.out.println(vector.indexOf("Johnny", 1));
       vector.clear(); //deleting all vector elements
       System.out.println("the size of the vector after clear method = " +  vector.size());
   }
}
```
**Вывод:**
<p style="background-color: navy; color: yellow">
the size of the empty vector = 0<br>
[Johnny, Ivy, Ricky]<br> [Johnny, Ivy, Ricky, Johnny, Paul]<br> 
the size of the vector = 5<br> 
the first element of the vector = Johnny<br> 
0<br> 
3<br> 
the size of the vector after clear method = 0</p>
### Выполнение различных операций над классом Vector в Java

#### Операция 1: Добавление элементов

Чтобы добавить элементы в вектор, мы используем метод add(). Этот метод перегружен для выполнения нескольких операций на основе разных параметров. Они перечислены ниже следующим образом:
`add(Object)`: этот метод используется для добавления элемента в конец вектора.
`add(int index, Object)`: этот метод используется для добавления элемента по определенному индексу в векторе.

**Пример:**
```java
// Java Program to Add Elements in Vector Class
// Importing required classes
import java.io.*;
import java.util.*;

// Main class
// AddElementsToVector
class GFG {
    // Main driver method
    public static void main(String[] arg) {

        // Case 1
        // Creating a default vector
        Vector v1 = new Vector();

        // Adding custom elements
        // using add() method
        v1.add(1);
        v1.add(2);
        v1.add("geeks");
        v1.add("forGeeks");
        v1.add(3);

        // Printing the vector elements to the console
        System.out.println("Vector v1 is " + v1);

        // Case 2
        // Creating generic vector
        Vector<Integer> v2 = new Vector<Integer>();

        // Adding custom elements
        // using add() method
        v2.add(1);
        v2.add(2);
        v2.add(3);

        // Printing the vector elements to the console
        System.out.println("Vector v2 is " + v2);
    }
}
```
 **Выход:**
 <p style="background-color: navy; color: yellow">
 Vector v1 is [1, 2, geeks, forGeeks, 3]  <br>
Vector v2 is [1, 2, 3]</p>

#### Операция 2: Обновление элементов

Если после добавления элементов мы хотим изменить элемент, это можно сделать с помощью метода set(). Поскольку вектор индексируется, на элемент, который мы хотим изменить, ссылается индекс элемента. Таким образом, этот метод принимает индекс и обновленный элемент, который нужно вставить по этому индексу.

**Пример**
```java
// Java code to change the
// elements in vector class
import java.util.*; 

// Driver Class
public class UpdatingVector { 
      // Main Function
    public static void main(String args[]) { 
        // Creating an empty Vector 
        Vector<Integer> vec_tor = new Vector<Integer>(); 

        // Use add() method to add elements in the vector 
        vec_tor.add(12); 
        vec_tor.add(23); 
        vec_tor.add(22); 
        vec_tor.add(10); 
        vec_tor.add(20); 

        // Displaying the Vector 
        System.out.println("Vector: " + vec_tor); 

        // Using set() method to replace 12 with 21 
        System.out.println("The Object that is replaced is: "
                        + vec_tor.set(0, 21)); 

        // Using set() method to replace 20 with 50 
        System.out.println("The Object that is replaced is: "
                        + vec_tor.set(4, 50)); 

        // Displaying the modified vector 
        System.out.println("The new Vector is:" + vec_tor); 
    } 
} 
```
**Выход**
<p style="background-color: navy; color: yellow">
Vector: [12, 23, 22, 10, 20]<br>
The Object that is replaced is: 12<br>
The Object that is replaced is: 20<br>
The new Vector is:[21, 23, 22, 10, 50]</p>

#### Операция 3: Удаление элементов

Чтобы удалить элемент из вектора, мы можем использовать метод remove(). Этот метод перегружен для выполнения нескольких операций на основе разных параметров. Они есть:
- remove(Object): этот метод используется для удаления объекта из вектора. Если таких объектов несколько, то первое вхождение объекта удаляется.
- remove(int index): поскольку вектор индексируется, этот метод принимает целочисленное значение, которое просто удаляет элемент, присутствующий в этом конкретном индексе в векторе. После удаления элемента все элементы перемещаются влево, чтобы заполнить пространство, а индексы объектов обновляются.
- 
**Пример**
```java
// Java code illustrating the removal
// of elements from vector
import java.util.*;
import java.io.*;

class RemovingElementsFromVector {
    public static void main(String[] arg) {
        // Create default vector of capacity 10
        Vector v = new Vector();

        // Add elements using add() method
        v.add(1);
        v.add(2);
        v.add("Geeks");
        v.add("forGeeks");
        v.add(4);

        // Removing first occurrence element at 1
        v.remove(1);

        // Checking vector
        System.out.println("after removal: " + v);
    }
}
```
 **Выход:**
 <p style="background-color: navy; color: yellow">
 after removal: [1, Geeks, forGeeks, 4]</p>

#### Операция 4: Итерация вектора

Существует несколько способов перебора вектора. Наиболее известные способы — использование базового цикла for в сочетании с методом get() для получения элемента по определенному индексу и расширенного цикла for.

**Пример**
```java
// Java program to iterate the elements
// in a Vector

import java.util.*;

public class IteratingVector {
    public static void main(String args[]) {
          // create an instance of vector
        Vector<String> v = new Vector<>();

          // Add elements using add() method
        v.add("Geeks");
        v.add("Geeks");
        v.add(1, "For");

        // Using the Get method and the
        // for loop
        for (int i = 0; i < v.size(); i++) {
            System.out.print(v.get(i) + " ");
        }

        System.out.println();

        // Using the for each loop
        for (String str : v)
            System.out.print(str + " ");
    }
}
```
**Выход**
<p style="background-color: navy; color: yellow">
1<br>
0<br>
3</p>

Обратите внимание, что класс _Vector_ синхронизирован, а это означает, что несколько потоков могут получить доступ к одному и тому же вектору, не вызывая проблем. Однако эта синхронизация происходит за счет производительности, поэтому, если вам не нужно совместно использовать вектор между несколькими потоками, обычно лучше использовать альтернативный класс, такой как [_ArrayList_](Class-ArrayList), который не синхронизируется.

### Преимущества использования Vector в Java:

1. Синхронизация. Как упоминалось ранее, _Vector_ синхронизируется, что делает его безопасным для использования в многопоточной среде.
2. Динамический размер. Размер вектора может динамически увеличиваться или уменьшаться по мере добавления или удаления элементов, поэтому вам не нужно беспокоиться об установке начального размера, который будет вмещать все элементы.
3. Поддержка устаревших версий: _Vector_ является частью Java с момента его создания и до сих пор поддерживается, поэтому это хороший вариант, если вам нужно работать со старым кодом Java, использующим _Vector_.

### Недостатки использования Vector в Java:

1. Производительность. Синхронизация в _Vector_ может привести к снижению производительности по сравнению с другими классами коллекций, такими как [_ArrayList_](Class-ArrayList).
2. Устаревший код: хотя _Vector_ все еще поддерживается, новый код Java часто пишется с использованием более современных классов коллекций, поэтому может быть сложнее найти примеры и поддержку _Vector_.
3. Ненужные накладные расходы. Если вам не нужны функции синхронизации _Vector_, их использование добавит ненужные накладные расходы в ваш код.