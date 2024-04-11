#Java #Map #Hashtable

## Java Хэш-таблица

2024-04-11 16:14

Класс Java _Hashtable_ - один из старейших членов Java Collection Framework. Это реализация математической структуры данных _Hashtable_. В Java hashtable внутренне содержит сегменты, в которых хранятся пары ключ / значение. _Hashtable_ очень похож на [_HashMap_](HashMap). Наиболее существенное различие между ними: _Hashtable_ синхронизируется, а [_HashMap_](HashMap) - нет.

### Hashtable как структура данных

 _Hashtable_ - это структура данных, в которой данные хранятся в формате массива. Каждое значение данных имеет уникальное значение ключа. Если ключ известен, доступ к необходимым данным осуществляется очень быстро. Таким образом, операции вставки и поиска выполняются быстро независимо от размера данных.  _Hashtable_ состоит из массива для хранения данных и хэширования для генерации индекса, в котором должен быть расположен элемент. Что такое хэширование? Это правило, которое преобразует объект в набор символов (код). Обычно такого рода функции преобразуют большой фрагмент данных в маленькое целое значение. Хэш-функции могут быть разными, но все они предоставляют определенные свойства:
- Конкретный объект имеет определенный хэш-код.
- Два одинаковых объекта имеют одинаковые хэш-коды. Обратное неверно.
- Если два хэш-кода различаются, объекты определенно не равны.
- Разные объекты могут иметь одинаковый хэш-код. Это очень редкое событие вызывает столкновение. Хорошая хэш-функция минимизирует вероятность столкновений.

Результат применения хэш-функции к объекту вызывает хэш-код.

###  _Hashtable_ в Java

Класс _Hashtable_ - это реализация структуры данных  _Hashtable_. Эта коллекция была создана раньше, чем платформа Java Collection Framework, но позже была включена в нее. Как и все “ранние” коллекции (начиная с Java 1.0),  _Hashtable_ синхронизирована (почти все методы помечены как синхронизированные). Из-за этого фактора  _Hashtable_ имеет значительные проблемы с производительностью. Следовательно, начиная с Java 1.2, в большинстве случаев рекомендуется использовать другие реализации интерфейса [_Map_](Map) из-за отсутствия у них синхронизации. Обычно [_HashMap_](HashMap) является наиболее подходящей заменой. Итак, класс Hashtable<K,V> состоит из ключей и значений. Она хранит ключи по принципу хеширования. Пары ключ-значение хранятся в "корзинах". Корзины вместе образуют "таблицу", своего рода внутренний массив.  _Hashtable_ использует хэш-код ключа, чтобы определить сегмент, которому должна соответствовать пара ключ / значение. Хэш-функция позволяет получить местоположение сегмента по хэш-коду ключа. Эта функция возвращает целое число для объекта. Как мы говорили выше, два равных объекта имеют одинаковый хэш-код, в то время как два неравных объекта не всегда могут иметь разные хэш-коды. Разные объекты, помещенные в  _Hashtable_, могут иметь один и тот же хэш-код. Для решения этой проблемы (коллизии) в hashtable используется массив списков. Пары, сопоставленные одному сегменту, хранятся в списке, а ссылка на этот список хранится в индексе массива.

![[HierarchyofHashtable.png]]

### Конструкторы Java для _Hashtable_

- Hashtable(), конструктор по умолчанию. Он создает пустую  _Hashtable_. (Начальная емкость по умолчанию = 11, коэффициент загрузки = 0,75).
- Hashtable(int size) создает  _Hashtable_ заданного размера.
-  _Hashtable_ (int size, float fillRatio) создает  _Hashtable_ указанного размера и коэффициента заполнения.
-  _Hashtable_ (Map m) создает  _Hashtable_ с теми же отображениями, что и данная карта.

### Объявление _Hashtable_

Класс Java Hashtable реализует интерфейсы [_Map_](Map), [_Cloneable_](Cloneable) и [_Serializable_](Serializable). Она расширяет класс _Dictionary_.
```java
Hashtable.java public class Hashtable<K,V> extends Dictionary<K,V> implements Map<K,V>, Cloneable, java.io.Serializable
```
K - это тип ключей, поддерживаемых картой. V - тип отображаемых значений. Пример:
```java
Hashtable<Student, Integer> myHTable = new Hashtable<>();
```

### Основные операции с _Hashtable_

Основными операциями _Hashtable_ являются получение, вставка в коллекцию и удаление оттуда. Здесь эти три операции:
- Object get(Object key) возвращает значение объекта, у которого указан ключ. Возвращает null, если такой ключ не найден.
- Объект put (Object key, Object value) сопоставляет указанный ключ с указанным значением. Ни ключ, ни значение не могут быть нулевыми.
- Object remove(Object key) удаляет запись (ключ и соответствующее значение) из _Hashtable_.

Другие важные операции:
- int size() возвращает количество записей в _Hashtable_.
- boolean contains(Object value) проверяет, есть ли указанное значение в _Hashtable_. Если это так, метод возвращает true, else возвращает false.
- boolean containsValue(Object value) проверяет, есть ли указанное значение в _Hashtable_. Если это так, метод возвращает true, else возвращает false.
- void clear() удаляет все записи из _Hashtable_.
- boolean containsKey(ключ объекта) возвращает true, если указанный ключ существует в _Hashtable_, в противном случае возвращает false.
- boolean isEmpty() возвращает true, если _Hashtable_ пуста, или false, если она содержит хотя бы один ключ.
- void rehash() увеличивает размер _Hashtable_ и перефразирует все ее ключи.

### Реализация хэш-таблицы, Java-код:

Давайте создадим класс Student:
```java
import java.util.Date;
public class Student {
   String surname;
   String name;
   String secondName;
   Long birthday; // Long instead of long is used by Gson/Jackson json parsers and various orm databases

   public Student(String surname, String name, String secondName, Date birthday ){
       this.surname = surname;
       this.name = name;
       this.secondName = secondName;
       this.birthday = birthday == null ? 0 : birthday.getTime();
   }

   @Override
   public int hashCode(){
       //TODO: check for nulls
       return (surname + name + secondName + birthday).hashCode();
   }
   @Override
   public boolean equals(Object other_) {
       Student other = (Student)other_;
       return (surname == null || surname.equals(other.surname) )
               && (name == null || name.equals(other.name))
               && (secondName == null || secondName.equals(other.secondName))
               && (birthday == null || birthday.equals(other.birthday));
   }
}
```

Вот пример _Hashtable_ Java. Давайте поместим два объекта класса Student в _Hashtable_, затем удалим некоторые и проверим некоторые параметры.
```java
public class HashTableExample {
   public static void main(String[] args) {

       Hashtable<Student, Integer> myHTable = new Hashtable<>();
       Student sarah1 = new Student("Sarah","Connor", "Jane", null);
       Student john = new Student("John","Connor", "Kyle", new Date(1985, 02-1, 28)); // date not exists
       myHTable.put(john,1);
       myHTable.put(sarah1,0);
       System.out.println(myHTable.get(john));
       System.out.println(myHTable.isEmpty());
       System.out.println(myHTable.size());
       System.out.println(myHTable.contains(1));
       myHTable.remove(john);
       System.out.println(myHTable.contains(0));
       System.out.println(myHTable.contains(1));
       System.out.println(myHTable.containsKey(sarah1));
   }
}
```
Результатом запуска программы является:
<p style="background-color: navy; color: yellow">
1<br> 
false<br>
2<br>
true<br> 
true<br> 
false<br>
true</p>

### [HashMap](HashMap) против Hashtable

- _Hashtable_ похожа на [_HashMap_](HashMap) в Java. Наиболее существенное отличие заключается в том, что _Hashtable_ синхронизируется, а [_HashMap_](HashMap) - нет. Следовательно, _Hashtable_ работает медленнее, чем [_HashMap_](HashMap), из-за синхронизации.
- За исключением проблемы синхронизации, _Hashtable_ не позволяет использовать null в качестве значения или ключа. [_HashMap_](HashMap) допускает один нулевой ключ и несколько нулевых значений.
- _Hashtable_ наследует класс _Dictionary_, в то время как [_HashMap_](HashMap) наследует класс _AbstractMap_.
- [_HashMap_](HashMap) обрабатывается итератором. _Hashtable_ может обрабатываться не только [итератором](Iterator), но и [перечислителем](Enumeration).

#### Пример Java Hashtable (Hashtable против нулевого ключа HashMap)

Вот фрагмент кода, демонстрирующий значение null, используемое в качестве ключа и значения в [_HashMap_](HashMap) и _Hashtable_
```java
// Null key Java hashtable example and hashmap example

try{
      System.out.println("Hashtable");
      Hashtable hashTable = new Hashtable();
      hashTable.put(null, new Object());
    }catch(Exception ex){
      ex.printStackTrace();
    }
    System.out.println("HashMap");
    HashMap hashMap = new HashMap();
    hashMap.put(null, new Object());
    System.out.println("as you see no exceptions with null key in HashMap");
  }
```
Результат запуска программы, содержащей этот фрагмент:
<p style="background-color: navy; color: yellow">
java.lang.NullPointerException<br>
	at java.base/java.util.Hashtable.put(Hashtable.java:480)<br>
	at Character.main(Character.java:58)<br>
HashMap<br>
as you see no exceptions with null key in HashMap</p>

#### Преимущества Hashtable:

1. Потокобезопасность: класс _Hashtable_ является поточно-ориентированным, что означает, что несколько потоков могут обращаться к нему одновременно, не вызывая повреждения данных или других проблем с синхронизацией.
2. Простота в использовании. Класс _Hashtable_ прост в использовании и предоставляет базовые функции структуры данных «ключ-значение», которые могут быть полезны в простых случаях.

#### Недостатки Hashtable:

1. Устарело: класс _Hashtable_ считается устаревшим, и его использование обычно не рекомендуется. Это связано с тем, что он был разработан до появления платформы коллекций и не реализует интерфейс [_Map_](Map), что затрудняет его использование совместно с другими частями платформы.
2. Ограниченная функциональность. Класс _Hashtable_ обеспечивает базовую функциональность структуры данных «ключ-значение», но не предоставляет полный спектр функций, доступных в интерфейсе [_Map_](Map) и его реализациях.
3. Низкая производительность: класс Hashtable синхронизирован, что может привести к снижению производительности по сравнению с другими реализациями интерфейса [_Map_](Map), такими как [_HashMap_](HashMap) или _ConcurrentHashMap_.
