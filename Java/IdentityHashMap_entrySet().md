#Java #Map #IdentityHashMap 

## Метод IdentityHashMap entrySet() в Java

2024-04-16 12:47

Метод _java.util.IdentityHashMap.entrySet()_ класса [_IdentityHashMap_](IdentityHashMap) в Java используется для создания набора из тех же элементов, что содержатся в карте. В основном он возвращает заданное представление хэш-карты идентификатора, или мы можем создать новый набор и сохранить в них элементы карты.

**Синтаксис:**
Identity_HashMap.entrySet()

**Параметры:** Метод не принимает никаких параметров.

**Возвращаемое значение:** Метод возвращает набор [_Set_](Set), содержащий те же элементы, что и карта.

Приведенные ниже программы иллюстрируют метод _java.util.IdentityHashMap.entrySet()_:

**Программа 1:** Преобразование строковых значений в целочисленные ключи.
```java
// Java code to illustrate the entrySet() method 
import java.util.*; 
  
public class Identity_Hash_Map_Demo { 
    public static void main(String[] args) { 
        // Creating an empty IdentityHashMap 
        IdentityHashMap<Integer, String> identity_hash =  
                      new IdentityHashMap<Integer, String>(); 
  
        // Mapping string values to int keys 
        identity_hash.put(10, "Geeks"); 
        identity_hash.put(15, "4"); 
        identity_hash.put(20, "Geeks"); 
        identity_hash.put(25, "Welcomes"); 
        identity_hash.put(30, "You"); 
  
        // Displaying the IdentityHashMap 
        System.out.println("Initial Mappings are: " + identity_hash); 
  
        // Using entrySet() to get the set view 
        System.out.println("The set is: " + identity_hash.entrySet()); 
    } 
} 
```
**Вывод:**
<p style="background-color: navy; color: yellow">
Initial Mappings are: {10=Geeks, 30=You, 20=Geeks, 25=Welcomes, 15=4}<br>
The set is: [10=Geeks, 30=You, 20=Geeks, 25=Welcomes, 15=4]</p>

**Программа 2:** Сопоставление целочисленных значений со строковыми ключами.
```java
// Java code to illustrate the entrySet() method 
import java.util.*; 
  
public class Identity_Hash_Map_Demo { 
    public static void main(String[] args) { 
        // Creating an empty IdentityHashMap 
        IdentityHashMap<String, Integer> identity_hash =  
                       new IdentityHashMap<String, Integer>(); 
  
        // Mapping int values to string keys 
        identity_hash.put("Geeks", 10); 
        identity_hash.put("4", 15); 
        identity_hash.put("Geeks", 20); 
        identity_hash.put("Welcomes", 25); 
        identity_hash.put("You", 30); 
  
        // Displaying the IdentityHashMap 
        System.out.println("Initial Mappings are: " + identity_hash); 
  
        // Using entrySet() to get the set view 
        System.out.println("The set is: " + identity_hash.entrySet()); 
    } 
} 
```
**Вывод:**
<p style="background-color: navy; color: yellow">
Initial Mappings are: {Geeks=20, Welcomes=25, You=30, 4=15}<br>
The set is: [Geeks=20, Welcomes=25, You=30, 4=15]</p>

**Примечание:** Одна и та же операция может быть выполнена с любым типом сопоставлений с изменением и комбинацией различных типов данных.

