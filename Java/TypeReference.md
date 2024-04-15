#Java #Reference

## Типы ссылок в Java

2024-04-15 11:46

В Java существует четыре типа ссылок, различающихся по способу сбора мусора.
1. Strong ссылки
2. Weak ссылки
3. Soft ссылки
4. Phantom ссылки

#### Strong Reference

**Strong References:** это тип/класс ссылочного объекта по умолчанию. Любой объект, имеющий активную strong ссылку, не подлежит сборке мусора. Объект подвергается сборке мусора только в том случае, если переменная, на которую была Strong ссылка, указывает на null.
```java
MyClass obj = new MyClass ();          
```
Здесь объект «obj» является strong ссылкой на вновь созданный экземпляр MyClass, в настоящее время obj является активным объектом, поэтому не может быть собран мусором.
```java
obj = null;
//Объект 'obj' больше не ссылается на экземпляр.
```
Таким образом, объект типа MyClass теперь доступен для сборки мусора.       

**Пример.** Strong reference
```java
// Java program to illustrate Strong reference 
class Gfg 
{ 
    //Code.. 
} 
public class Example 
{ 
    public static void main(String[] args) 
    { 
         //Strong Reference - by default 
        Gfg g = new Gfg();     
          
        //Now, object to which 'g' was pointing earlier is  
        //eligible for garbage collection. 
        g = null;  
    } 
}  
```

#### Weak Reference

**Weak References:** Слабые ссылочные объекты не являются типом/классом ссылочного объекта по умолчанию, и их следует явно указывать при использовании.
- Этот тип ссылки используется в [_WeakHashMap_](WeakHashMap) для ссылки на объекты записи.
- Если JVM обнаруживает объект только со слабыми ссылками (т. е. без Strong или Soft ссылок, связанных с каким-либо объектным объектом), этот объект будет помечен для сборки мусора.
- Для создания таких ссылок используется класс java.lang.ref.WeakReference.
- Эти ссылки используются в приложениях реального времени при установлении соединения DBConnection, которое может быть очищено сборщиком мусора при закрытии приложения, использующего базу данных.

**Пример.** Weak reference
```java
//Java Code to illustrate Weak reference 
import java.lang.ref.WeakReference; 
class Gfg 
{ 
    //code 
    public void x() 
    { 
        System.out.println("GeeksforGeeks"); 
    } 
} 
  
public class Example 
{ 
    public static void main(String[] args) 
    { 
        // Strong Reference 
        Gfg g = new Gfg();      
        g.x(); 
          
        // Creating Weak Reference to Gfg-type object to which 'g'  
        // is also pointing. 
        WeakReference<Gfg> weakref = new WeakReference<Gfg>(g); 
          
        //Now, Gfg-type object to which 'g' was pointing earlier 
        //is available for garbage collection. 
        //But, it will be garbage collected only when JVM needs memory. 
        g = null;  
          
        // You can retrieve back the object which 
        // has been weakly referenced. 
        // It successfully calls the method. 
        g = weakref.get();  
          
        g.x(); 
    } 
} 
```
Выход:
<p style="background-color: navy; color: yellow">
GeeksforGeeks<br>
GeeksforGeeks</p>

#### Soft reference

**Sofr References**: в Soft ссылке, даже если объект свободен для сборки мусора, он также не собирает мусор до тех пор, пока JVM не будет остро нуждаться в памяти. Объекты удаляются из памяти, когда у JVM заканчивается память. Для создания таких ссылок используется класс java.lang.ref.SoftReference.

**Пример.** Soft reference
```java
//Code to illustrate Soft reference 
import java.lang.ref.SoftReference; 
class Gfg 
{ 
    //code.. 
    public void x() 
    { 
        System.out.println("GeeksforGeeks"); 
    } 
} 
  
public class Example 
{ 
    public static void main(String[] args) 
    { 
        // Strong Reference 
        Gfg g = new Gfg();      
        g.x(); 
          
        // Creating Soft Reference to Gfg-type object to which 'g'  
        // is also pointing. 
        SoftReference<Gfg> softref = new SoftReference<Gfg>(g); 
          
        // Now, Gfg-type object to which 'g' was pointing 
        // earlier is available for garbage collection. 
        g = null;  
          
        // You can retrieve back the object which 
        // has been weakly referenced. 
        // It successfully calls the method. 
        g = softref.get();  
          
        g.x(); 
    } 
} 
```
Выход:
<p style="background-color: navy; color: yellow">
GeeksforGeeks<br>
GeeksforGeeks</p>

#### Phantom Reference

**Phantom References**: объекты, на которые ссылаются фантомные ссылки, подлежат сборке мусора. Но прежде чем удалить их из памяти, JVM помещает их в очередь, называемую «очередь ссылок». Они помещаются в очередь ссылок после вызова на них метода Finalize(). Для создания таких ссылок используется класс java.lang.ref.PhantomReference .
```java
//Code to illustrate Phantom reference 
import java.lang.ref.*; 
class Gfg 
{ 
    //code 
    public void x() 
    { 
        System.out.println("GeeksforGeeks"); 
    } 
} 
  
public class Example 
{ 
    public static void main(String[] args) 
    { 
        //Strong Reference 
        Gfg g = new Gfg();      
        g.x(); 
          
        //Creating reference queue 
        ReferenceQueue<Gfg> refQueue = new ReferenceQueue<Gfg>(); 
  
        //Creating Phantom Reference to Gfg-type object to which 'g'  
        //is also pointing. 
        PhantomReference<Gfg> phantomRef = null; 
          
        phantomRef = new PhantomReference<Gfg>(g,refQueue); 
          
        //Now, Gfg-type object to which 'g' was pointing 
        //earlier is available for garbage collection. 
        //But, this object is kept in 'refQueue' before  
        //removing it from the memory. 
        g = null;  
          
        //It always returns null.  
        g = phantomRef.get();  
          
        //It shows NullPointerException. 
        g.x(); 
    } 
} 
```
Выход:
<p style="background-color: navy; color: yellow">
GeeksforGeeks</p>
<p style="background-color: navy; color: red">
Exception in thread "main" java.lang.NullPointerException: Cannot invoke "Gfg.x()" because "g" is null<br>
	at Main.main(Main.java:40)</p>
	



