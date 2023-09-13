### Двусвязный список LinkedList ###

#LinkedList #ArrayList 

2023-09-11 17:27

В  LinkedList элементы фактически представляют собой звенья одной цепи. У каждого элемента помимо тех данных, которые он хранит, имеется ссылка на предыдущий и следующий элемент. По этим ссылкам можно переходить от одного элемента к другому.
```java
public class Main {

   public static void main(String[] args) {

       String str1 = new String("Hello World!");
       String str2 = new String("My name is Earl");
       String str3 = new String("I love Java");
       String str4 = new String("I live in Moscow");

       LinkedList<String> earlBio = new LinkedList<>();
       earlBio.add(str1);
       earlBio.add(str2);
       earlBio.add(str3);
       earlBio.add(str4);

       System.out.println(earlBio);

   }
}
```
Вывод:

==Hello World! My name is Earl, I love Java, I live in Moscow==

Элементы **`LinkedList`** являются единым списком именно благодаря вот этой цепочке ссылок. Внутри **`LinkedList`** нет массива, как в [**`ArrayList`**](Class ArrayList), или чего-то похожего.
Вся работа с ArrayList (по большому счету) сводится к работе с внутренним массивом. Вся работа с `LinkedList` сводится к изменению ссылок.
Добавление элемента в список:
```java
public class Main {

   public static void main(String[] args) {

       String str1 = new String("Hello World!");
       String str2 = new String("My name is Earl");
       String str3 = new String("I love Java");
       String str4 = new String("I live in Moscow");

       LinkedList<String> earlBio = new LinkedList<>();
       earlBio.add(str1);
       earlBio.add(str3);
       earlBio.add(1, str2);

       System.out.println(earlBio);

   }
}
```
Удаление элемента из списка:
```java
public class Main {

   public static void main(String[] args) {

       String str1 = new String("Hello World!");
       String str2 = new String("My name is Earl");
       String str3 = new String("I love Java");
       String str4 = new String("I live in Moscow");

       LinkedList<String> earlBio = new LinkedList<>();
       earlBio.add(str1);
       earlBio.add(str3);
       earlBio.add(1, str2);

       earlBio.remove(1);
       System.out.println(earlBio);
   }
}
```
В отличие от удаления в `ArrayList` здесь нет никаких сдвигов элементов массива и тому подобного. Мы просто переопределяем ссылки у элементов `str1` и `str3`. Теперь они указывают друг на друга, а объект `str2` “выпал” из этой цепочки ссылок, и больше не является частью списка.

### Обзор методов ###

У **`LinkedList`** есть много общих с **`ArrayList`** методов. Например, такие методы как **`add()`, `remove()`, `indexOf()`, `clear()`, `contains()`** (содержится ли элемент в списке), **`set()`** (вставка элемента с заменой) и **`size()`** есть в обоих классах. Хотя (как мы выяснили на примере **`add()`** и **`remove()`**) внутри многие из них работают по другому, но в конечном итоге они делают то же самое. Однако, у **`LinkedList`** есть отдельные методы для работы с началом и концом списка, которых нет в **`ArrayList`**:

**`addFirst()`, `addLast()`**: методы для добавления элемента в начало/конец списка
```java
public class Car {

   String model;

   public Car(String model) {
       this.model = model;
   }

   public static void main(String[] args) {
       LinkedList<Car> cars = new LinkedList<>();
       Car ferrari = new Car("Ferrari 360 Spider");
       Car bugatti = new Car("Bugatti Veyron");
       Car lambo = new Car("Lamborghini Diablo");
       Car ford = new Car("Ford Mondeo");
       Car fiat = new Car("Fiat Ducato");

       cars.add(ferrari);
       cars.add(bugatti);
       cars.add(lambo);
       System.out.println(cars);

       cars.addFirst(ford);
       cars.addLast(fiat);
       System.out.println(cars);
   }

   @Override
   public String toString() {
       return "Car{" +
               "model='" + model + '\'' +
               '}';
   }
}
```
Вывод:

==Car{model='Ferrari 360 Spider'}, Car{model='Bugatti Veyron'}, Car{model='Lamborghini Diablo'}
Car{model='Ford Mondeo'}, Car{model='Ferrari 360 Spider'}, Car{model='Bugatti Veyron'}, Car{model='Lamborghini Diablo'}, Car{model='Fiat Ducato'}==

В итоге “Форд” оказался в начале списка, а “Фиат” — в конце.

**`peekFirst()`, `peekLast()`**: возвращают первый/последний элемент списка. Возвращают `null`, если список пуст.
```java
public static void main(String[] args) {
   LinkedList<Car> cars = new LinkedList<>();
   Car ferrari = new Car("Ferrari 360 Spider");
   Car bugatti = new Car("Bugatti Veyron");
   Car lambo = new Car("Lamborghini Diablo");

   cars.add(ferrari);
   cars.add(bugatti);
   cars.add(lambo);
   System.out.println(cars.peekFirst());
   System.out.println(cars.peekLast());
}
```
Вывод:

==Car{model='Ferrari 360 Spider'}
Car{model='Lamborghini Diablo'}==

**`pollFirst()`, `pollLast()`**: возвращают первый/последний элемент списка и удаляют его из списка. Возвращают `null`, если список пуст
```java
public static void main(String[] args) {
   LinkedList<Car> cars = new LinkedList<>();
   Car ferrari = new Car("Ferrari 360 Spider");
   Car bugatti = new Car("Bugatti Veyron");
   Car lambo = new Car("Lamborghini Diablo");

   cars.add(ferrari);
   cars.add(bugatti);
   cars.add(lambo);
   System.out.println(cars.pollFirst());
   System.out.println(cars.pollLast());

   System.out.println("Что осталось в списке?");
   System.out.println(cars);
}
```
Вывод:

==Car{model='Ferrari 360 Spider'}
Car{model='Lamborghini Diablo'}==
Что осталось в списке?
==Car{model='Bugatti Veyron'}==

**`toArray()`**: возвращает массив из элементов списка
```java
public static void main(String[] args) {
   LinkedList<Car> cars = new LinkedList<>();
   Car ferrari = new Car("Ferrari 360 Spider");
   Car bugatti = new Car("Bugatti Veyron");
   Car lambo = new Car("Lamborghini Diablo");

   cars.add(ferrari);
   cars.add(bugatti);
   cars.add(lambo);
   Car[] carsArray = cars.toArray(new Car[3]);
   System.out.println(Arrays.toString(carsArray));
}
```

Вывод:

==Car{model='Ferrari 360 Spider'}, Car{model='Bugatti Veyron'}, Car{model='Lamborghini Diablo'}==

Теперь мы знаем, как устроен **`LinkedList`** и чем он отличается от `ArrayList`. В чем же заключаются выгоды от использования **`LinkedList`**? Прежде всего, в работе с серединой списка. Вставка и удаление в середину **`LinkedList`** устроены гораздо проще, чем в **`ArrayList`**. Мы просто переопределяем ссылки соседних элементов, а ненужный элемент “выпадает” из цепочки ссылок. В то время как в **`ArrayList`** мы:

- проверяем, хватает ли места (при вставке)
- если не хватает — создаем новый массив и копируем туда данные (при вставке)
- удаляем/вставляем элемент, и сдвигаем все остальные элементы вправо/влево (в зависимости от типа операции). Причем сложность этого процесса сильно зависит от размера списка. Одно дело — скопировать/сдвинуть 10 элементов, и совсем другое — сделать то же самое с миллионом элементов.

То есть, если в твоей программе чаще происходят операции вставки/удаления с серединой списка, **`LinkedList`** должен быть быстрее, чем **`ArrayList`**.

## Теоретически
```java
public class Main {

   public static void main(String[] args) {
       List<Integer> list = new LinkedList<>();

       for (int i = 0; i < 5000000; i++) {
           list.add(new Integer(i));
       }

       long start=System.currentTimeMillis();

       for(int i=0;i<100;i++){
           list.add(2000000, new Integer(Integer.MAX_VALUE));
       }
       System.out.println("Время работы для LinkedList (в милисекундах) = " + (System.currentTimeMillis()-start));
   }
}
```

Вывод:

==Время работы для LinkedList (в милисекундах) = 1873==

```java
public class Main {

   public static void main(String[] args) {
       List<Integer> list = new ArrayList<>();

       for (int i = 0; i < 5000000; i++) {
           list.add(new Integer(i));
       }

       long start=System.currentTimeMillis();

       for (int i=0;i<100;i++){
           list.add(2000000, new Integer(Integer.MAX_VALUE));
       }
       System.out.println("Время работы для ArrayList (в миллисекундах) = " + (System.currentTimeMillis()-start));
   }
}
```

Вывод:

==Время работы для ArrayList (в миллисекундах) = 181==

Неожиданно! Казалось бы, мы проводили операцию, где `LinkedList` должен быть намного эффективнее — вставку 100 элементов в середину списка. Да и список у нас огромный — 5000000 элементов: `ArrayList`’у приходилось сдвигать по паре миллионов элементов каждый раз при вставке! В чем же причина его победы? Во-первых, доступ к элементу осуществляется в `ArrayList` за фиксированное время. Когда ты указываешь:

```java
list.add(2_000_000, new Integer(Integer.MAX_VALUE));
```

то в случае с `ArrayList` [2_000_000] это конкретный адрес в памяти, ведь у него внутри массив. В то время как у `LinkedList` массива нет. Он будет искать элемент номер 2_000_000 по цепочке ссылок. Для него это не адрес в памяти, а ссылка, до которой еще надо дойти:

==fistElement.next.next.next.next.next.next.next.next.next.next.next.next.next.next.next.next.next.next.next.next.next.next.next.next.next.next.next.next.next.next………==

В итоге при каждой вставке (удалении) в середине списка **`ArrayList`** уже знает точный адрес в памяти, к которому он должен обратиться, а вот **`LinkedList`**’у еще надо до нужного места “дотопать”. Во-вторых, дело в структуре самого **`ArrayList`**’a. Расширение внутреннего массива, копирование всех элементов и сдвиг элементов осуществляет специальная внутренняя функция — **`System.arrayCopy()`**. Она работает очень быстро, потому что специально оптимизирована для этой работы. А вот в ситуациях, когда “топать” до нужного индекса не нужно, **`LinkedList`** действительно показывает себя лучше. Например, если вставка происходит в начало списка. Попробуем вставить туда миллион элементов:

```java
public class Main {

   public static void main(String[] args) {
       getTimeMsOfInsert(new ArrayList());
       getTimeMsOfInsert(new LinkedList());
   }

   public static long getTimeMsOfInsert(List list) {
       //напишите тут ваш код
       Date currentTime = new Date();
       insert1000000(list);
       Date newTime = new Date();
       long msDelay = newTime.getTime() - currentTime.getTime(); //вычисляем разницу
       System.out.println("Результат в миллисекундах: " + msDelay);
       return msDelay;
   }
	public static void insert1000000(List list) {
       for (int i = 0; i < 1000000; i++) {
           list.add(0, new Object());
       }
	}
}
```
Вывод:
==Результат в миллисекундах: 43448
Результат в миллисекундах: 107==

Совсем другой результат! На вставку миллиона элементов в начало списка `ArrayList` затратил больше 43 секунд, в то время как `LinkedList` справился за 0,1 секунды! Сказался именно тот факт, что в этой ситуации `LinkedList`’у не пришлось “пробегать” каждый раз по цепочке ссылок до середины списка. Он сразу находил нужный индекс в начале списка, а там уже разница в принципах работы была на его стороне:) На самом деле, дискуссия “**`ArrayList`** против **`LinkedList`**” имеет очень широкое распространение, и сильно в нее углубляться на текущем уровне мы не будем. Главное, что тебе нужно запомнить:

- Не все преимущества той или иной коллекции “на бумаге” будут действовать в реальности (мы разобрали это на примере с серединой списка)
- Не стоит бросаться в крайности при выборе коллекции (“**`ArrayList`** всегда быстрее, используй его и не ошибешься. **`LinkedList`** давно никто не пользуется”).

Хотя даже создатель **`LinkedList`** Джошуа Блох так говорит:) Тем не менее, эта точка зрения верна далеко не на 100%, и мы в этом убедились. В нашем предыдущем примере **`LinkedList`** отработал в 400 (!) раз быстрее. Другое дело, что ситуаций, когда **`LinkedList`** будет лучшим выбором, действительно немного. Но они есть, и в нужный момент **`LinkedList`** может тебя серьезно выручить. 

