#Java #Map #IdentityHashMap 

## Метод IdentityHashMap clone() в Java

2024-04-16 12:31

Метод _Java.util.IdentityHashMap.clone()_ класса [_IdentityHashMap_](IdentityHashMap) используется для возврата копии хэш-карты. Он просто создает макеты карт.

**Синтаксис:**
```java
Identity_HashMap.clone()
```
**Параметры:** Метод не принимайте никаких параметров.

**Возвращаемое значение:** метод просто возвращает копию хэш-карты.

Приведенные ниже программы использованы для иллюстрации работы метода _java.util.IdentityHashMap.clone()_:

**Программа 1:**
```java
// Java code to illustrate the clone() method 
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
  
        // Displaying the cloned Map using clone() 
        System.out.println("The cloned map: " + identity_hash.clone()); 
    } 
} 
```
**Выход:**
<p style="background-color: navy; color: yellow">
Initial Mappings are: {10=Geeks, 30=You, 20=Geeks, 25=Welcomes, 15=4}<br>
The cloned map: {10=Geeks, 30=You, 20=Geeks, 25=Welcomes, 15=4}</p>


**Программа 2:**
```java
// Java code to illustrate the clone() method 
import java.util.*; 
  
public class Identity_Hash_Map_Demo { 
    public static void main(String[] args) 
    { 
  
        // Creating an empty hash map 
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
  
        // Displaying the cloned map using clone() 
        System.out.println("The cloned map: " + identity_hash.clone()); 
    } 
} 
```
**Выход:**
<p style="background-color: navy; color: yellow">
Initial Mappings are: {Geeks=20, Welcomes=25, You=30, 4=15}<br>
The cloned map: {Geeks=20, Welcomes=25, You=30, 4=15}</p>

**Примечание.** Эту же операцию можно выполнить с любым типом сопоставлений с вариацией и комбинацией разных типов данных.