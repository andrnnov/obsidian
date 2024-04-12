#Java #Collection #Enum #EnumSet

## Java EnumSet

2024-04-12 14:22

_EnumSet_ - это одна из специализированных реализаций интерфейса [_Set_](Set) для использования с [типом перечисления](Еnum). Вот несколько важных особенностей _EnumSet_:

- Он расширяет класс _AbstractSet_ и реализует интерфейс [_Set_](Set) на Java.
- Класс _EnumSet_ является членом Java Collections Framework и не синхронизируется.
- Это высокопроизводительная реализация набора, намного быстрее, чем [_HashSet_](HashSet).
- Все элементы в _EnumSet_ должны относиться к одному [типу перечисления](Enum), который указывается при явном или неявном создании набора.
- Он не допускает **нулевые объекты** и в этом случае выдает _NullPointerException_.
- Он использует **отказоустойчивый** итератор, поэтому не будет вызывать исключение _ConcurrentModificationException_, если коллекция будет изменена во время итерации.

**Синтаксис:**
```java
public abstract class EnumSet<E extends Enum<E>> 
```
Здесь E указывает элементы. E должен расширять [_Enum_](Enum).

### Создание EnumSet

Чтобы создать набор перечислений, мы должны сначала импортировать `java.util.EnumSet` пакет.

В отличие от других реализаций [_Set_](Set), _EnumSet_ не имеет открытых конструкторов. Мы должны использовать предопределенные методы для создания _EnumSet_.

#### 1. Использование allof(Size)

Метод `allof()` создает набор перечислений, который содержит все значения указанного типа перечисления Size. Например,
```java
import java.util.EnumSet;

class Main {
    // an enum named Size
    enum Size {
        SMALL, MEDIUM, LARGE, EXTRALARGE
    }
    
    public static void main(String[] args) {
        // Creating an EnumSet using allOf()
        EnumSet<Size> sizes = EnumSet.allOf(Size.class);

        System.out.println("EnumSet: " + sizes);
    }
}
```
**Вывод**
<p style="background-color: navy; color: yellow">
EnumSet: [SMALL, MEDIUM, LARGE, EXTRALARGE]</p>
Обратите внимание на инструкцию,
```java
EnumSet<Size> sizes = EnumSet.allOf(Size.class);
```
Здесь, Size.class обозначает Size созданного нами перечисления.

#### 2. Использование noneOf(Size)

Метод `noneOf()` создает пустой набор перечислений. Например,
```java
import java.util.EnumSet;

class Main {
     // an enum type Size
    enum Size {
        SMALL, MEDIUM, LARGE, EXTRALARGE
    }

    public static void main(String[] args) {

        // Creating an EnumSet using noneOf()
        EnumSet<Size> sizes = EnumSet.noneOf(Size.class);

        System.out.println("Empty EnumSet: " + sizes);
    }
}
```
**Вывод**
<p style="background-color: navy; color: yellow">
Empty EnumSet : []</p>

Здесь мы создали пустое перечисление с именем sizes.

>**Примечание**: Мы можем вставлять элементы только типа [_enum_](Enum) Size в приведенную выше программу. Это потому, что мы создали наш пустой набор enum с использованием Size enum.

#### 3. Использование метода range(e1, e2)

Метод `range()` создает набор перечислений, содержащий все значения перечисления между e1 и e2, включая оба значения. Например,
```java
import java.util.EnumSet;

class Main {
    enum Size {
        SMALL, MEDIUM, LARGE, EXTRALARGE
    }

    public static void main(String[] args) {
        // Creating an EnumSet using range()
        EnumSet<Size> sizes = EnumSet.range(Size.MEDIUM, Size.EXTRALARGE);

        System.out.println("EnumSet: " + sizes);
    }
}
```
**Вывод**
<p style="background-color: navy; color: yellow">
EnumSet: [MEDIUM, LARGE, EXTRALARGE]</p>

#### 4. Использование метода()

Метод `of()` создает набор перечислений, содержащий указанные элементы. Например,
```java
import java.util.EnumSet;

class Main {
    enum Size {
        SMALL, MEDIUM, LARGE, EXTRALARGE
    }

    public static void main(String[] args) {
        // Using of() with a single parameter
        EnumSet<Size> sizes1 = EnumSet.of(Size.MEDIUM);
        System.out.println("EnumSet1: " + sizes1);

        EnumSet<Size> sizes2 = EnumSet.of(Size.SMALL, Size.LARGE);
        System.out.println("EnumSet2: " + sizes2);
    }
}
```
**Вывод**
<p style="background-color: navy; color: yellow">
EnumSet1: [MEDIUM]<br>
EnumSet2: [SMALL, LARGE]</p>

### Методы EnumSet

Класс _EnumSet_ предоставляет методы, которые позволяют нам выполнять различные элементы в наборе перечислений.

#### Вставка элементов в EnumSet

- `add()` - вставляет указанные значения [_enum_](Enum) в набор enum
- `addAll()` вставляет все элементы указанной коллекции в [_set_](Set)

Например,
```java
import java.util.EnumSet;

class Main {
    enum Size {
        SMALL, MEDIUM, LARGE, EXTRALARGE
    }

    public static void main(String[] args) {
        // Creating an EnumSet using allOf()
        EnumSet<Size> sizes1 = EnumSet.allOf(Size.class);

        // Creating an EnumSet using noneOf()
        EnumSet<Size> sizes2 = EnumSet.noneOf(Size.class);

        // Using add method
        sizes2.add(Size.MEDIUM);
        System.out.println("EnumSet Using add(): " + sizes2);

        // Using addAll() method
        sizes2.addAll(sizes1);
        System.out.println("EnumSet Using addAll(): " + sizes2);
    }
}
```
**Вывод**
<p style="background-color: navy; color: yellow">
EnumSet using add(): [MEDIUM]<br>
EnumSet using addAll(): [SMALL, MEDIUM, LARGE, EXTRALARGE]</p>

В приведенном выше примере мы использовали `addAll()` метод для вставки всех элементов набора перечислений sizes1 в набор перечислений sizes2.

Также возможно вставлять элементы из других коллекций, таких как [_ArrayList_](Class-ArrayList), [_LinkedList_](Class-LinkedList) и т.д. в набор перечислений с помощью `addAll()`. Однако все коллекции должны иметь один и тот же тип перечисления.

#### Доступ к элементам EnumSet

Для доступа к элементам набора перечислений мы можем использовать [_iterator()_](Iterator) метод. Чтобы использовать этот метод, мы должны импортировать `java.util.Iterator` пакет. Например,
```java
import java.util.EnumSet;
import java.util.Iterator;

class Main {
    enum Size {
        SMALL, MEDIUM, LARGE, EXTRALARGE
    }

    public static void main(String[] args) {
        // Creating an EnumSet using allOf()
        EnumSet<Size> sizes = EnumSet.allOf(Size.class);

        Iterator<Size> iterate = sizes.iterator();

        System.out.print("EnumSet: ");
        while(iterate.hasNext()) {
            System.out.print(iterate.next());
            System.out.print(", ");
        }
    }
}
```
**Вывод**
<p style="background-color: navy; color: yellow">
EnumSet: SMALL, MEDIUM, LARGE, EXTRALARGE,</p>

>**Примечание**:
>- `hasNext()` возвращает `true`, есть ли следующий элемент в наборе перечислений
>- `next()` возвращает следующий элемент в наборе перечислений

#### Удалить элементы EnumSet

- `remove()` - удаляет указанный элемент из набора перечислений
- `removeAll()` - удаляет все элементы из набора перечислений

Например,
```java
import java.util.EnumSet;

class Main {
    enum Size {
        SMALL, MEDIUM, LARGE, EXTRALARGE
    }

    public static void main(String[] args) {
        // Creating EnumSet using allOf()
        EnumSet<Size> sizes = EnumSet.allOf(Size.class);
        System.out.println("EnumSet: " + sizes);

        // Using remove()
        boolean value1 = sizes.remove(Size.MEDIUM);
        System.out.println("Is MEDIUM removed? " + value1);

        // Using removeAll()
        boolean value2 = sizes.removeAll(sizes);
        System.out.println("Are all elements removed? " + value2);
    }
}
```
**Вывод**
<p style="background-color: navy; color: yellow">
EnumSet: [SMALL, MEDIUM, LARGE, EXTRALARGE]<br>
Is MEDIUM removed? true<br>
Are all elements removed? true</p>

#### Другие методы

| Метод        | Описание                                                                          |
| ------------ | --------------------------------------------------------------------------------- |
| `copyOf()`   | Создает копию _EnumSet_                                                           |
| `contains()` | Выполняет поиск в _EnumSet_ указанного элемента и возвращает логический результат |
| `isEmpty()`  | Проверяет, является ли _EnumSet_ пустым                                           |
| `size()`     | Возвращает размер _EnumSet_                                                       |
| `clear()`    | Удаляет все элементы из _EnumSet_                                                 |

### Клонируемые и сериализуемые интерфейсы

В _EnumSet_ классе также реализованы интерфейсы [_Cloneable_](Cloneable) и [_Serializable_](Serializable).

**Клонируемый интерфейс**

Это позволяет _EnumSet_ классу создавать копии экземпляров класса.

**Сериализуемый интерфейс**

Всякий раз, когда объекты Java необходимо передавать по сети, объекты необходимо преобразовывать в биты или байты. Это связано с тем, что объекты Java не могут передаваться по сети.

Интерфейс [_Serializable_](Serializable) позволяет сериализовывать классы. Это означает, что объекты реализующих классов _Serializable_ могут быть преобразованы в биты или байты.

