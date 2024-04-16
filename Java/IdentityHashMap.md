#Java #Map #IdentityHashMap

## Класс IdentityHashMap в Java

2024-04-16 10:23

Класс _IdentityHashMap_ является реализацией абстрактного класса _AbstractMap_. _IdentityHashMap_ является классом в Фреймворке коллекции Java (Java Collection Framework), который реализует интерфейс [_Map_](Map). _IdentityHashMap_ полностью поддерживает все функции, указанные в интерфейсе [_Map_](Map), включая дополнительные функции. В основном _IdentityHashMap_ очень похож на [_HashMap_](HashMap), они используют метод хеширования (hashing technique) для улучшения доступа к данным и производительности хранения. Однако они отличаются тем, как хранятся данные и как сравниваются ключи (key). 

**Особенности IdentityHashMap**
- Он соответствует ссылочному равенству, вместо использования метода equals() используется оператор `==`.
- Он не синхронизирован и должен быть синхронизирован извне.
- Итераторы работают без сбоев, выдают **исключение ConcurrentModificationException** при попытке внести изменения во время итерации.
- Этот класс обеспечивает производительность с постоянным временем для основных операций (получение и размещение), при условии, что хеш-функция системного идентификатора (System.identityHashCode(Object)) правильно распределяет элементы по сегментам. _IdentityHashMap_ не использует метод hashCode(), вместо этого используется метод System.identityHashCode(). Это существенное отличие, поскольку теперь вы можете использовать изменяемые объекты в качестве ключей в [_Map_](Map), чей хэш-код может измениться, когда сопоставление хранится внутри _IdentityHashMap_.

Вот пример того, как вы могли бы использовать IdentityHashMap в Java:
```java
import java.util.IdentityHashMap; 
  
public class Example { 
    public static void main(String[] args) { 
        IdentityHashMap<String, Integer> identityHashMap =
		         new IdentityHashMap<>(); 
        identityHashMap.put("A", 1); 
        identityHashMap.put(new String("A"), 2); 
        System.out.println(identityHashMap.size()); // 2 
        System.out.println(identityHashMap.get("A")); // 1 
    } 
} 
```
вывод;
<p style="background-color: navy; color: yellow">
2 <br>
1</p>

### Преимущества использования IdentityHashMap по сравнению с [_HashMap_](HashMap):

1. Более быстрый поиск: поскольку _IdentityHashMap_ использует равенство ссылок для сравнения, он работает быстрее по сравнению с [_HashMap_](HashMap), который использует равенство объектов.
2. Полезно для сравнения экземпляров объектов: _IdentityHashMap_ полезен в ситуациях, когда вы хотите сравнивать экземпляры объектов, а не значения объектов.

### Недостатки использования IdentityHashMap:

1. Использует больше памяти: _IdentityHashMap_ использует больше памяти по сравнению с [_HashMap_](HashMap), поскольку ему необходимо хранить ссылку на объект.
2. Подходит не для всех случаев использования: _IdentityHashMap_ подходит не для всех случаев использования, и его следует использовать с осторожностью, поскольку в определенных ситуациях это может привести к неожиданному поведению.

**Иерархия IdentityHashMap**
![[IdentityHashMap.png]]

### Конструкторы IdentityHashMap

|                                                   |                                                                                                                                                                                                                                                               |
| ------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `IdentityHashMap()`                               | Создает пустой объект _IdentityHashMap_ с максимальным ожидаемым размером по умолчанию (21).                                                                                                                                                                  |
| `IdentityHashMap(int expectedMaxSize)`            | Создает пустой объект _IdentityHashMap_ с заданным максимальным ожидаемым размером. Добавление большего, чем ожидалось, сопоставления **expectedMaxSize** в _IdentityHashMap_ приведет к росту внутренней структуры данных, что может занять немного времени. |
| `IdentityHashMap(Map<? extends K,? extends V> m)` | Создает объект _IdentityHashMap_ с отображениями, скопированными с указанной [_Map_](Map).                                                                                                                                                                    |

### Основные операции с IdentityHashMap

#### 1. Добавление элементов

Чтобы вставить или добавить сопоставление в _IdentityHashMap_, у нас есть методы put() и putAll(). put() может вставить определенный ключ и значение, которое он отображает, в определенную карту. Если передается существующий ключ, предыдущее значение заменяется новым значением. putAll() копирует все элементы, т.е. сопоставления, из одной карты в другую.
```java
// Java code to illustrate 
// adding elements to IdentityHashMap 
import java.util.*; 
  
public class AddingElementsToIdentityHashMap { 
    public static void main(String[] args) { 
        // Creating an empty IdentityHashMap 
        Map<Integer, String> identity_hash 
            = new IdentityHashMap<Integer, String>(); 
  
        // Mapping string values to int keys 
        // using put() method 
        identity_hash.put(10, "Geeks"); 
        identity_hash.put(15, "4"); 
        identity_hash.put(20, "Geeks"); 
        identity_hash.put(25, "Welcomes"); 
        identity_hash.put(30, "You"); 
  
        // Displaying the IdentityHashMap 
        System.out.println("Initial Mappings are: " + identity_hash); 
  
        // Inserting existing key along with new value 
          // previous value gets returned and stored in 
          // returned_value 
        String returned_value = (String)identity_hash.put(20, "All"); 
  
        // Verifying the returned value 
        System.out.println("Returned value is: " + returned_value); 
        // Displaying the new map 
        System.out.println("New map is: " + identity_hash); 
  
        // Creating a new Identityhash map and copying 
        Map<Integer, String> new_Identityhash_map 
            = new IdentityHashMap<Integer, String>(); 
        new_Identityhash_map.putAll(identity_hash); 
  
        // Displaying the final IdentityHashMap 
        System.out.println("The new map: " + new_Identityhash_map); 
    } 
}
```
**Выход**
<p style="background-color: navy; color: yellow">
Initial Mappings are: {30=You, 10=Geeks, 15=4, 25=Welcomes, 20=Geeks}<br>
Returned value is: Geeks<br>
New map is: {30=You, 10=Geeks, 15=4, 25=Welcomes, 20=All}<br>
The new map: {30=You, 10=Geeks, 15=4, 25=Welcomes, 20=All}</p>

#### 2. Удаление элементов.

Чтобы удалить сопоставления, мы используем метод remove() , встроенный метод класса _IdentityHashMap_, который используется для удаления сопоставления любого конкретного ключа с карты.
```java
// Java code to illustrate removing 
// elements from IdentityHashMap 
import java.util.*;  
  
public class RemovingMappingsFromIdentityHashMap {  
    public static void main(String[] args) {  
  
        // Creating an empty IdentityHashMap  
        Map<Integer, String> Identity_hash = new
                    IdentityHashMap<Integer, String>();  
      
        // Mapping string values to int keys  
        Identity_hash.put(10, "Geeks");  
        Identity_hash.put(15, "4");  
        Identity_hash.put(20, "Geeks");  
        Identity_hash.put(25, "Welcomes");  
        Identity_hash.put(30, "You");  
  
        // Displaying the IdentityHashMap  
        System.out.println("Initial Mappings are: " + Identity_hash);  
        // Removing the existing key mapping  
        String returned_value = (String)Identity_hash.remove(20);  
        // Verifying the returned value  
        System.out.println("Returned value is: " + returned_value);  
        // Displaying the new map  
        System.out.println("New map is: " + Identity_hash);  
    }  
}  
```
**Выход**
<p style="background-color: navy; color: yellow">
Initial Mappings are: {30=You, 10=Geeks, 15=4, 25=Welcomes, 20=Geeks}<br>
Returned value is: Geeks<br>
New map is: {30=You, 10=Geeks, 15=4, 25=Welcomes}</p>

#### 3. Доступ к элементам

Мы можем получить доступ к элементам _IdentityHashMap_ с помощью метода get() , пример этого приведен ниже.
```java
// Java code to illustrate the accessing 
// elements from IdentityHashMap 
  
import java.util.*; 
  
public class AccessingElementsFromIdentityHashMap { 
    public static void main(String[] args) { 
  
        // Creating an empty IdentityHashMap 
        Map<Integer, String> identity_hash 
            = new IdentityHashMap<Integer, String>(); 
  
        // Mapping string values to int keys 
        identity_hash.put(10, "Geeks"); 
        identity_hash.put(15, "4"); 
        identity_hash.put(20, "Geeks"); 
        identity_hash.put(25, "Welcomes"); 
        identity_hash.put(30, "You"); 
  
        // Displaying the IdentityHashMap 
        System.out.println("Initial Mappings are: " + identity_hash); 
        // Getting the value of 25 
        System.out.println("The Value is: " + identity_hash.get(25)); 
        // Getting the value of 10 
        System.out.println("The Value is: " + identity_hash.get(10)); 
          // Using keySet() to get the set view of keys  
        System.out.println("The set is: " + identity_hash.keySet()); 
          // Using entrySet() to get the set view  
        System.out.println("The set is: " + identity_hash.entrySet());  
    } 
}
```
**Выход**
<p style="background-color: navy; color: yellow">
Initial Mappings are: {30=You, 10=Geeks, 15=4, 25=Welcomes, 20=Geeks}<br>
The Value is: Welcomes<br>
The Value is: Geeks<br>
The set is: [30, 10, 15, 25, 20]<br>
The set is: [30=You, 10=Geeks, 15=4, 25=Welcomes, 20=Geeks]</p>

#### 4. Обход

Мы можем использовать интерфейс [_Iterator_](Iterator) для обхода любой структуры Collection Framework. Поскольку итераторы работают с одним типом данных, мы используем `Entry<? , ? >` чтобы преобразовать два отдельных типа в совместимый формат. Затем, используя метод next(), мы печатаем элементы _IdentityHashMap_.
```java
// Java code to illustrate the  
// iterating over IdentityHashmap 
import java.util.*; 
  
public class IteratingIdentityHashMap { 
    public static void main(String[] args) { 
  
        // Creating an empty IdentityHashMap 
        IdentityHashMap<Integer, String> identity_hash 
            = new IdentityHashMap<Integer, String>(); 
  
        // Mapping string values to int keys 
        identity_hash.put(10, "Geeks"); 
        identity_hash.put(15, "4"); 
        identity_hash.put(20, "Geeks"); 
        identity_hash.put(25, "Welcomes"); 
        identity_hash.put(30, "You"); 
  
        // Displaying the IdentityHashMap 
        System.out.println("Initial Mappings are: " + identity_hash); 
  
        // Create an Iterator over the 
        // IdentityHashMap 
        Iterator<IdentityHashMap.Entry<Integer, String> > 
            itr = identity_hash.entrySet().iterator(); 
  
        // The hasNext() method is used to check if there is 
        // a next element The next() method is used to 
        // retrieve the next element 
        while (itr.hasNext()) { 
            IdentityHashMap.Entry<Integer, String> entry = itr.next(); 
            System.out.println("Key = " + entry.getKey() 
                               + ", Value = "
                               + entry.getValue()); 
        } 
    } 
}
```
**Выход**
<p style="background-color: navy; color: yellow">
Initial Mappings are: {30=You, 10=Geeks, 15=4, 25=Welcomes, 20=Geeks}<br>
Key = 30, Value = You<br>
Key = 10, Value = Geeks<br>
Key = 15, Value = 4<br>
Key = 25, Value = Welcomes<br>
Key = 20, Value = Geeks</p>

### Синхронизированная IdentityHashMap

Если несколько потоков одновременно обращаются к хеш-карте идентификаторов и хотя бы один из потоков изменяет структуру карты, ее необходимо синхронизировать извне. (Структурная модификация — это любая операция, которая добавляет или удаляет одно или несколько сопоставлений; простое изменение значения, связанного с ключом, который уже содержит экземпляр, не является структурной модификацией.) Обычно это достигается путем синхронизации некоторого объекта, который естественным образом инкапсулирует отображение. . Если такого объекта не существует, карту следует «обернуть» с помощью метода **_Collections.synchronizedMap_**. Лучше всего это делать во время создания, чтобы предотвратить случайный несинхронизированный доступ к карте.
```java
Map m = Collections.synchronizedMap(new IdentityHashMap(…));
```

### Методы IdentityHashMap

- **K** – тип ключей на карте.
- **V** – тип значений, отображаемых на карте.

| МЕТОД                                                                                                      | ОПИСАНИЕ                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| [clear()](https://www.geeksforgeeks.org/identityhashmap-clear-method-in-java/)                             | Удаляет все сопоставления с этой карты.                                                                                                   |
| [clone()](IdentityHashMap_clone())                                                                         | Возвращает неполную копию этой хэш-карты идентификаторов: сами ключи и значения не клонируются.                                           |
| [containsKey(Object key)](https://www.geeksforgeeks.org/identityhashmap-containskey-method-in-java/)       | Проверяет, является ли указанная ссылка на объект ключом в этой хэш-карте идентификаторов.                                                |
| [containsValue(Object value)](https://www.geeksforgeeks.org/identityhashmap-containsvalue-method-in-java/) | Проверяет, является ли указанная ссылка на объект значением в этой хеш-карте идентификаторов.                                             |
| [entrySet()](IdentityHashMap_entrySet())                                                                   | Возвращает представление [_Set_](Set) сопоставлений, содержащихся на этой карте.                                                          |
| [equals(Object o)](https://www.geeksforgeeks.org/identityhashmap-equals-method-in-java/)                   | Сравнивает указанный объект с этой картой на предмет равенства.                                                                           |
| [get(Object key)](https://www.geeksforgeeks.org/identityhashmap-get-method-in-java/)                       | Возвращает значение, с которым сопоставлен указанный ключ, или значение null, если это сопоставление не содержит сопоставления для ключа. |
| [hashCode()](https://www.geeksforgeeks.org/identityhashmap-hashcode-method-in-java/)                       | Возвращает значение хеш-кода для этой карты.                                                                                              |
| [isEmpty()](https://www.geeksforgeeks.org/identityhashmap-isempty-method-in-java/)                         | Возвращает true, если эта хеш-карта идентификаторов не содержит сопоставлений «ключ-значение».                                            |
| [keySet()](https://www.geeksforgeeks.org/identityhashmap-keyset-method-in-java/)                           | Возвращает представление набора ключей, содержащихся в этой карте, на основе идентификаторов.                                             |
| [put(K key, V value)](https://www.geeksforgeeks.org/identityhashmap-put-method-in-java/)                   | Связывает указанное значение с указанным ключом в этой хеш-карте идентификаторов.                                                         |
| [putAll(<`? extends K,? extends V>` m)](IdentityHashMap_putAll())                                          | Копирует все сопоставления с указанной карты на эту карту.                                                                                |
| [remove(Object key)](https://www.geeksforgeeks.org/identityhashmap-remove-method-in-java/)                 | Удаляет сопоставление этого ключа с этой карты, если оно присутствует.                                                                    |
| [size()](https://www.geeksforgeeks.org/identityhashmap-size-method-in-java/)                               | Возвращает количество сопоставлений ключ-значение в этой карте хэша идентификаторов.                                                      |
| [values()](https://www.geeksforgeeks.org/identityhashmap-values-method-in-java/)                           | Возвращает представление коллекции значений, содержащихся на этой карте.                                                                  |

