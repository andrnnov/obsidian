#Java #Map #IdentityHashMap 

## Метод IdentityHashMap putAll() в Java

2024-04-16 11:50

_Java.util.IdentityHashMap.putAll()_ - это встроенный метод класса [_IdentityHashMap_](IdentityHashMap), который используется для операции копирования. Метод копирует все элементы, то есть сопоставления, из одной карты в другую.

**Синтаксис:**
```java
new_Identityhash_map.putAll(_exist_Identityhash_map_)
```
**Параметры:** Метод принимает один параметр _exist_Identityhash_map_, ссылающийся на существующую карту, с которой мы хотим скопировать.

**Возвращаемое значение:** метод не возвращает никаких значений.

**Исключение:** метод выдает _исключение NullPointerException_, если карта, с которой мы хотим скопировать, равна NULL.

Приведенные ниже программы иллюстрируют работу метода _java.util.IdentityHashMap.putAll()_  
**Программа 1:** Преобразование строковых значений в целочисленные ключи.
```java
// Java code to illustrate the putAll() method 
import java.util.*; 
  
public class Identity_Hash_Map_Demo { 
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
  
        // Creating a new Identityhash map and copying 
        Map<Integer, String> new_Identityhash_map = new 
                        IdentityHashMap<Integer, String>(); 
        new_Identityhash_map.putAll(Identity_hash); 
  
        // Displaying the final IdentityHashMap 
        System.out.println("The new map: " + new_Identityhash_map); 
    } 
} 
```
**Вывод:**
<p style="background-color: navy; color: yellow">
Initial Mappings are: {30=You, 15=4, 10=Geeks, 25=Welcomes, 20=Geeks}<br>
The new map: {15=4, 30=You, 10=Geeks, 25=Welcomes, 20=Geeks}</p>

**Программа 2:** Преобразование целочисленных значений в строковые ключи.
```java
// Java code to illustrate the putAll() method 
import java.util.*; 
  
public class IdentityHash_Map_Demo { 
    public static void main(String[] args) { 
  
        // Creating an empty IdentityHashMap 
        Map<String, Integer> Identity_hash = new 
                      IdentityHashMap<String, Integer>(); 
  
        // Mapping int values to string keys 
        Identity_hash.put("Geeks", 10); 
        Identity_hash.put("4", 15); 
        Identity_hash.put("Geeks", 20); 
        Identity_hash.put("Welcomes", 25); 
        Identity_hash.put("You", 30); 
  
        // Displaying the IdentityHashMap 
        System.out.println("Initial Mappings are: " + Identity_hash); 
  
        // Creating a new Identityhash map and copying 
        Map<String, Integer> new_Identityhash_map = new 
                      IdentityHashMap<String, Integer>(); 
        new_Identityhash_map.putAll(Identity_hash); 
  
        // Displaying the final IdentityHashMap 
        System.out.println("The new map: " + new_Identityhash_map); 
    } 
} 
```
**Вывод:**
<p style="background-color: navy; color: yellow">
Initial Mappings are: {Welcomes=25, 4=15, You=30, Geeks=20}<br>
The new map: {Welcomes=25, 4=15, You=30, Geeks=20}</p>


**Примечание:** Одна и та же операция может быть выполнена с любым типом сопоставлений с вариациями и комбинациями различных типов данных.