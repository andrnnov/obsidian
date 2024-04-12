#Java #Map #EnumMap
## Класс EnumMap в Java

2024-04-12 11:22

EnumMap - это специализированная реализация интерфейса [_Map_](Map) для [типов перечисления](Enum). Он расширяет _AbstractMap_ и реализует интерфейс [_Map_](Map) на Java. Он принадлежит к пакету java.util.

**Синтаксис:** 
```java
public class EnumMap<K extends Enum<K>,?V> extends AbstractMap<K,?V> implements Serializable, Cloneable
```
**Параметры:**
- Тип ключевого объекта
- Тип объекта Value

#### Вот пример того, как вы можете использовать класс EnumMap в Java:

```java
import java.util.EnumMap; 
  
enum Days { 
    MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY 
} 
  
public class EnumMapExample { 
    public static void main(String[] args) { 
        EnumMap<Days, String> schedule = new EnumMap<>(Days.class); 
          
        // Adding elements to the EnumMap 
        schedule.put(Days.MONDAY, "Work"); 
        schedule.put(Days.TUESDAY, "Work"); 
        schedule.put(Days.WEDNESDAY, "Study"); 
        schedule.put(Days.THURSDAY, "Study"); 
        schedule.put(Days.FRIDAY, "Relax"); 
          
        // Getting elements from the EnumMap 
        System.out.println(schedule.get(Days.MONDAY)); // Output: Work 
        System.out.println(schedule.get(Days.FRIDAY)); // Output: Relax 
    } 
} 
```
В этом примере мы определяем тип перечисления Days, который представляет дни недели. Затем мы создаем _EnumMap_ и добавляем в него элементы, используя метод put . Наконец, мы извлекаем элементы из _EnumMap_ с помощью метода get и выводим результаты на консоль.

### Преимущества использования EnumMap:

1. Эффективный: Класс _EnumMap_ обеспечивает быстрый и эффективный доступ к элементам, хранящимся на карте, что делает его хорошим выбором для использования в приложениях, критически важных для производительности.
2. Компактный: Класс _EnumMap_ использует компактное представление карты, что означает, что ему требуется меньше памяти, чем [_HasMap_](HashMap) или [_TreeMap_](TreeMap).
3. Типобезопасный: класс _EnumMap_ допускает ключи только указанного типа [_enum_](Enum), что означает, что он обеспечивает типобезопасное поведение и устраняет необходимость в приведении.
4. Отсортированные ключи: Класс _EnumMap_ предоставляет отсортированные ключи, что означает, что элементы в карте упорядочены в том порядке, в котором объявлены константы [_enum_](Enum).

### Недостатки использования EnumMap:

1. Ограничено ключами enum: Класс _EnumMap_ может использоваться только с ключами типа [_enum_](Enum), что означает, что он не подходит для использования с ключами других типов.
2. Неизменяемые ключи: Класс _EnumMap_ использует ключи [_enum_](Enum), которые являются неизменяемыми и не могут быть изменены после их создания.

### Конструкторы EnumMap

1. **EnumMap(Class keyType):** Конструктор используется для создания пустой _EnumMap_ с указанным _типом ключа_.
2. **EnumMap(EnumMap m):** Конструктор используется для создания карты перечислений с тем же типом ключа, что и указанная карта перечислений, при этом начальные сопоставления совпадают с _EnumMap_.
3. **EnumMap(Map m):** Конструктор используется для создания перечисляемой карты с инициализацией из указанной карты в параметре.

#### Пример

```java
// Java Program to illustrate Working of EnumMap class 
// and its functions 
// Importing EnumMap class 
import java.util.EnumMap; 
  
// Main class 
public class EnumMapExample { 
  
    // Enum 
    public enum GFG { 
        CODE, 
        CONTRIBUTE, 
        QUIZ, 
        MCQ; 
    } 
  
    // Main driver method 
    public static void main(String args[]) { 
        // Java EnumMap 
        // Creating an empty EnumMap with key 
        // as enum type state 
        EnumMap<GFG, String> gfgMap = new EnumMap<GFG, String>(GFG.class); 
        // Putting values inside EnumMap in Java 
        // Inserting Enum keys different from 
        // their natural order 
        gfgMap.put(GFG.CODE, "Start Coding with gfg"); 
        gfgMap.put(GFG.CONTRIBUTE, "Contribute for others"); 
        gfgMap.put(GFG.QUIZ, "Practice Quizes"); 
        gfgMap.put(GFG.MCQ, "Test Speed with Mcqs"); 
  
        // Printing size of EnumMap 
        System.out.println("Size of EnumMap in java: " + gfgMap.size()); 
  
        // Printing Java EnumMap 
        // Print EnumMap in natural order 
        // of enum keys (order on which they are declared) 
        System.out.println("EnumMap: " + gfgMap); 
  
        // Retrieving value from EnumMap 
        System.out.println("Key : " + GFG.CODE + " Value: "
			        + gfgMap.get(GFG.CODE)); 
  
        // Checking if EnumMap contains a particular key 
        System.out.println("Does gfgMap has " + GFG.CONTRIBUTE + ": "
            + gfgMap.containsKey(GFG.CONTRIBUTE)); 
  
        // Checking if EnumMap contains a particular value 
        System.out.println("Does gfgMap has :" + GFG.QUIZ + " : "
            + gfgMap.containsValue("Practice Quizes")); 
        System.out.println("Does gfgMap has :" + GFG.QUIZ 
                           + " : " + gfgMap.containsValue(null)); 
    } 
}
```
**Вывод**
<p style="background-color: navy; color: yellow">
Size of EnumMap in java: 4<br>
EnumMap: {CODE=Start Coding with gfg, CONTRIBUTE=Contribute for others, QUIZ=Practice 
Quizes, MCQ=Test Speed with Mcqs}<br>
Key : CODE Value: Start Coding with gfg<br>
Does gfgMap has CONTRIBUTE: true<br>
Does gfgMap has :QUIZ : true<br>
Does gfgMap has :QUIZ : false</p>

### **Основные операции с EnumMap**

#### Операция 1: Добавление элементов

Чтобы добавить элементы в EnumMap, мы можем использовать метод put() или putAll(), как показано ниже:
- `put()` - вставляет указанное сопоставление ключа / значения (запись) в enum map
- `putAll()` - вставляет все записи указанной карты в эту карту
```java
// Java Program to Add Elements to the EnumMap 
// Importing EnumMap class 
import java.util.EnumMap; 
  
// Main class 
// AddingElementsToEnumMap 
class GFG { 
    enum Color { RED, GREEN, BLUE, WHITE } 
    public static void main(String[] args) { 
  
        // Creating an EnumMap of the Color enum 
        EnumMap<Color, Integer> colors1 = new EnumMap<>(Color.class); 
  
        // Insert elements in Map 
        // using put() method 
        colors1.put(Color.RED, 1); 
        colors1.put(Color.GREEN, 2); 
  
        // Printing mappings to the console 
        System.out.println("EnumMap colors1: " + colors1); 
  
        // Creating an EnumMap of the Color Enum 
        EnumMap<Color, Integer> colors2 = new EnumMap<>(Color.class); 
  
        // Adding elements using the putAll() method 
        colors2.putAll(colors1); 
        colors2.put(Color.BLUE, 3); 
  
        // Printing mappings to the console 
        System.out.println("EnumMap colors2: " + colors2); 
    } 
}
```
**Вывод:**
<p style="background-color: navy; color: yellow">
EnumMap colors1: {RED=1, GREEN=2}<br>
EnumMap colors2: {RED=1, GREEN=2, BLUE=3}</p>

#### Операция 2: Доступ к элементам

Мы можем получить доступ к элементам _EnumMap_ с помощью entrySet(), keySet(), values(), get(). Приведенный ниже пример объясняет эти методы.
- `entrySet()` - возвращает набор всех ключей / значений, отображаемых (запись) перечисляемой карты
- `keySet()` - возвращает набор всех ключей перечисляемой карты
- `values()` - возвращает набор всех значений перечисляемой карты
```java
// Java Program to Access the Elements of EnumMap
// Importing required classes 
import java.util.EnumMap; 
// Main class 
// AccessElementsOfEnumMap 
class GFG { 
    // Enum 
    enum Color { RED, GREEN, BLUE, WHITE } 
  
    // Main driver method 
    public static void main(String[] args) { 
  
        // Creating an EnumMap of the Color enum 
        EnumMap<Color, Integer> colors 
            = new EnumMap<>(Color.class); 
  
        // Inserting elements using put() method 
        colors.put(Color.RED, 1); 
        colors.put(Color.GREEN, 2); 
        colors.put(Color.BLUE, 3); 
        colors.put(Color.WHITE, 4); 
  
        System.out.println("EnumMap colors : " + colors); 
  
        // Using the entrySet() method 
        System.out.println("Key/Value mappings: " + colors.entrySet()); 
  
        // Using the keySet() method 
        System.out.println("Keys: " + colors.keySet()); 
  
        // Using the values() method 
        System.out.println("Values: " + colors.values()); 
  
        // Using the get() method 
        System.out.println("Value of RED : " + colors.get(Color.RED)); 
    } 
}
```
**Вывод**
<p style="background-color: navy; color: yellow">
EnumMap colors : {RED=1, GREEN=2, BLUE=3, WHITE=4}<br>
Key/Value mappings: [RED=1, GREEN=2, BLUE=3, WHITE=4]<br>
Keys: [RED, GREEN, BLUE, WHITE]<br>
Values: [1, 2, 3, 4]<br>
Value of RED : 1</p>

#### Операция 3: Удаление элементов

Для удаления элементов _EnumMap_ предоставляет два варианта метода remove():
- `remove(key)` - возвращает и удаляет запись, связанную с указанным ключом, с карты
- `remove(key, value)` - удаляет запись с карты, только если указанный ключ сопоставлен с указанным значением и возвращает логическое значение
```java
// Java program to Remove Elements of EnumMap 
// Importing EnumMap class 
import java.util.EnumMap; 
  
// Main class 
class GFG { 
    // Enum 
    enum Color { 
        // Custom elements 
        RED, 
        GREEN, 
        BLUE, 
        WHITE 
    } 
  
    // Main driver method 
    public static void main(String[] args) { 
        // Creating an EnumMap of the Color enum 
        EnumMap<Color, Integer> colors = new EnumMap<>(Color.class); 
  
        // Inserting elements in the Map 
        // using put() method 
        colors.put(Color.RED, 1); 
        colors.put(Color.GREEN, 2); 
        colors.put(Color.BLUE, 3); 
        colors.put(Color.WHITE, 4); 
  
        // Printing colors in the EnumMap 
        System.out.println("EnumMap colors : " + colors); 
  
        // Removing a mapping 
        // using remove() Method 
        int value = colors.remove(Color.WHITE); 
  
        // Displaying the removed value 
        System.out.println("Removed Value: " + value); 
  
        // Removing specific color and storing boolean 
        // if removed or not 
        boolean result = colors.remove(Color.RED, 1); 
  
        // Printing the boolean result whether removed or 
        // not 
        System.out.println("Is the entry {RED=1} removed? " + result); 
  
        // Printing the updated Map to the console 
        System.out.println("Updated EnumMap: " + colors); 
    } 
}
```
**Вывод**
<p style="background-color: navy; color: yellow">
EnumMap colors : {RED=1, GREEN=2, BLUE=3, WHITE=4}<br>
Removed Value: 4<br>
Is the entry {RED=1} removed? true<br>
Updated EnumMap: {GREEN=2, BLUE=3}</p>

#### Операция 4: Замена элементов

Интерфейс [_Map_](Map) предоставляет три варианта метода replace() для изменения отображений _EnumMap_:
- `replace(key, value)` - заменяет значение, связанное с указанным key, на новое value
- `replace(key, old, new)` - заменяет old значение на new значение только в том случае, если old значение уже связано с указанным key
- `replaceAll(function)` - заменяет каждое значение карты результатом указанного функции

```java
import java.util.EnumMap;

class Main {
    enum Size {
        SMALL, MEDIUM, LARGE, EXTRALARGE
    }
    public static void main(String[] args) {
        // Creating an EnumMap of the Size enum
        EnumMap<Size, Integer> sizes = new EnumMap<>(Size.class);
        sizes.put(Size.SMALL, 28);
        sizes.put(Size.MEDIUM, 32);
        sizes.put(Size.LARGE, 36);
        sizes.put(Size.EXTRALARGE, 40);
        System.out.println("EnumMap: " + sizes);

        // Using the replace() Method
        sizes.replace(Size.MEDIUM, 30);
        sizes.replace(Size.LARGE, 36, 34);
        System.out.println("EnumMap using replace(): " + sizes);

        // Using the replaceAll() Method
        sizes.replaceAll((key, oldValue) -> oldValue + 3);
        System.out.println("EnumMap using replaceAll(): " + sizes);
    }
}
```
**Вывод**
<p style="background-color: navy; color: yellow">
EnumMap: {SMALL=28, MEDIUM=32, LARGE=36, EXTRALARGE=40}<br>
EnumMap using replace(): {SMALL=28, MEDIUM=30, LARGE=34, EXTRALARGE=40}<br>
EnumMap using replaceAll(): {SMALL=31, MEDIUM=33, LARGE=37, EXTRALARGE=43}</p>

В приведенной выше программе обратите внимание на инструкцию
```java
sizes.replaceAll((key, oldValue) -> oldValue + 3);
```
Здесь метод обращается ко всем элементам карты. Затем он заменяет все значения новыми значениями, предоставленными [лямбда-выражениями](Lambda).

### Другие методы

| Метод             | Описание                                                                          |
| ----------------- | --------------------------------------------------------------------------------- |
| `clone()`         | Создает копию _EnumMap_                                                           |
| `containsKey()`   | Выполняет поиск в _EnumMap_ указанного ключа и возвращает логический результат    |
| `containsValue()` | Выполняет поиск в _EnumMap_ указанного значения и возвращает логический результат |
| `size()`          | Возвращает размер _EnumMap_                                                       |
| `clear()`         | Удаляет все записи из _EnumMap_                                                   |

### Синхронизированная EnumMap

Реализация _EnumMap_ не синхронизирована. Если несколько потоков обращаются к _EnumMap_ одновременно, и хотя бы один из потоков изменяет набор, он должен быть синхронизирован извне. Обычно это достигается с помощью метода synchronizedMap(). Лучше всего это делать во время создания, чтобы предотвратить случайный несинхронизированный доступ.
```java
 Map<EnumKey, V> m = Collections.synchronizedMap(new EnumMap<EnumKey, V>(...));
```