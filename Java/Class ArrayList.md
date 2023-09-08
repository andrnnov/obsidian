
#ArrayList ArrayList – это реализация динамического использования массива в Java. При использовании массива часто приходится задумываться о требуемом размере, а ArrayList является списком, который увеличивается и уменьшается при необходимости. Этот класс является имплементацией интерфейса (interface) List из Collection Framework, который расположен в пакете `java.utils`. В самом классе есть базовые методы добавления и удаления, а также методы, которые возвращают размер списка; очистка по индексу или же по значению и т. д.
### Создание объекта ###

Существуют несколько конструкторов у ArrayList для создания объекта. Каждый из этих видов имеет свои использования и преимущества. Давайте пройдемся по каждому и рассмотрим, где и как используется каждый из данных видов:

1. **ArrayList()** – простое объявление списка и наиболее часто используемое. Объявляется данный список обычно в конструкторе, который будет использоваться внутри объекта, например, имплементация кэширования и временного хранения в памяти. Является самым простым и удобным объявлением списочного массива в Java.
```java
ArrayList<String> fruits = new ArrayList<>(); // ArrayList() создание списка
```
2. **ArrayList(int initialCapacity)** – объявление списка с указанием размера преимущественно для случаев, когда будет использоваться большое количество данных и в целях оптимизации следует задавать уже большой размер. Например, используется в случаях, когда список увеличивается с каждым вызовом метода в классе. Размер списка растет с нелинейной скоростью и, если заранее известно, что список будет увеличиваться и будет достигать больших размеров (больше 1e3 элементов), оптимально будет задать изначальный размер и резервировать количество мест заранее.
```java
ArrayList<String> employee = new ArrayList<>(100);
```
3. **ArrayList(Collection c)** – объявления списка с уже имеющимся списком, элементы которого были переданы конструктору.
```java
ArrayList<String> cars = new ArrayList<>(Arrays.asList("BMW", "AUDI"));
```

### Добавление элементов ###

Для того чтобы добавить элемент в список, используется простая функция `add`. Для этого метода есть разновидности:
1. **add(E e)** – добавление элемента в конец списка. Это функция является возвращаемой. Если элемент был добавлен в список, то ответ – `true`, иначе – `false`.
```java
ArrayList<String> fruits = new ArrayList<>(); // ArrayList() создание списка
fruits.add("banana"); // добавление элемента
fruits.add("apple"); // добавление элемента

for (var fruit: fruits) {
    System.out.println(fruit); // вывод элементов
}
```
Вывод:
==banana
apple==

2. **add(int index, E element)** – в данном методе добавление элемента происходит в определенную позицию (index), а все последующие элементы двигаются слева направо. Метод эффективен для небольших размеров списка (когда размер списка не более ~100 элементов). В ином случае – если в программе происходит много сдвигов, то лучше использовать [LinkedList](https://www.geeksforgeeks.org/data-structures/linked-list/).
```java
ArrayList<String> fruits = new ArrayList<String>();
        fruits.add("apple");
        fruits.add("banana");

        fruits.add(1, "watermelon"); // добавляем элемент на 2-ую позицию.

        for (var fruit : fruits) {
            System.out.println(fruit);
        }
```

Вывод:
==apple
watermelon
banana==
3. **addAll(Collection )** – добавление списка элементов в конец добавляемого списка. То есть, при вызове данного метода в конец списка добавляются все элементы в таком же порядке.
```java
 //список фруктов
        ArrayList<String> fruits = new ArrayList<String>();
        fruits.add("apple");
        fruits.add("banana");
        fruits.add(1, "watermelon"); 

        //список овощей
        ArrayList<String> vegetables = new ArrayList<>();
        vegetables.add("cucumber");
        vegetables.add("carrot");

        //список покупок
        ArrayList<String> groceries = new ArrayList<>();

        //добавляем в список покупок овощи и фрукты
        groceries.addAll(vegetables); 
        groceries.addAll(fruits);

        for (var item : groceries) {
            System.out.println(item);
        }
```
Вывод:
==cucumber
carrot
apple
watermelon
banana==
4. **addAll(int index, Collection )** – это смесь добавления списка и также добавления элемента в определенную позицию. В этом методе в позицию `index` производится добавление всех элементов из списка, а все последующие элементы смещаются направо.
```java	
        //список фруктов         
        ArrayList<String> fruits = new ArrayList<String>();         
        fruits.add("apple");         
        fruits.add("banana");         
        fruits.add(1, "watermelon");         
        //список овощей         
		ArrayList<String> vegetables = new ArrayList<>();    
		vegetables.add("cucumber");         
        vegetables.add("carrot");          
        //список покупок         
        ArrayList<String> groceries = new ArrayList<>();          
        //добавляем в список покупок овощи и фрукты         
        groceries.addAll(vegetables);         
        groceries.addAll(1, fruits); 
        //добавляем список фруктов на 1-ую позицию списка продуктов 			     
        //индекс  0,       1,      2,      3,          4 			
        //было - cucumber, carror 		  
        //стало - cucumber, apple, banana, watermelon, carrot          
        for (var item : groceries) { 
	        System.out.println(item);         
	    }
```
Вывод:
==cucumber             
apple             
watermelon             
banana             
carrot==

### Удаление элементов ###

В ArrayList, существуют методы для удаления элементов. Всего существуют 3 метода для удаления элемента:
1. **remove(int index)** – удаление осуществляется, используя индекс определенного элемента. То есть, передается порядковый номер элемента и этот элемента удаляется из списка. Не забываем, что индекс начинается с 0.
```java
//список фруктов
        ArrayList<String> fruits = new ArrayList<String>();
        fruits.add("apple");
        fruits.add("banana");
        fruits.add("watermelon");

        fruits.remove(0); // удаляем первый фрукт

        for (var fruit : fruits) {
            System.out.println(fruit);
        }
```
Вывод:
==watermelon
banana==

2. **remove(object o)** – метод удаляет первый встретившийся элемент, который равняется переданному объекту в параметрах. Если проще, то метод проходится по всему списку и ищет элемент, который равняется удаляемому объекту и при нахождении удаляет только первый встретившийся.
```java
//список фруктов
        ArrayList<String> fruits = new ArrayList<String>();
        fruits.add("apple");
        fruits.add("banana");
        fruits.add("watermelon");

        fruits.remove("banana"); // удаляем фрукт банан
        for (var fruit : fruits) {
            System.out.println(fruit);
        }
        /* output
```
Вывод:
==apple
watermelon==
3. **removaAll(Collection c)** – данный метод удаляет все элементы, находящиеся в передаваемом списке.
```java
//список фруктов
        ArrayList<String> fruits = new ArrayList<String>();
        fruits.add("apple");
        fruits.add("banana");
        fruits.add(1, "watermelon");

        ArrayList<String> fruitsToDelete = new ArrayList<>();
        fruitsToDelete.add("apple");
        fruitsToDelete.add("watermelon");

        fruits.removeAll(fruitsToDelete);
        for (var fruit : fruits) {
            System.out.println(fruit);
        }
```
Вывод:
==banana==

### Вспомогательные методы ###

В Arraylist встречаются различные методы, которые являются вспомогательными при различных условиях:
1. **size()** – возвращает размер списка.
```java
//список фруктов
        ArrayList<String> fruits = new ArrayList<String>();
        fruits.add("apple");
        fruits.add("banana");
        fruits.add(1, "watermelon");

        System.out.println(fruits.size());
```
Вывод:
==3==
2. **sort(Comparator c)** – происходит сортировка элементов по заданным параметрам `Comparator`. Есть уже значения по умолчанию у `Comparator`, которыми можно пользоваться, `Comparator.naturalOrder()`, а также `Comparator.reverseOrder()`.
```java
		ArrayList<Integer> numbers = new ArrayList<>();
        numbers.add(1);
        numbers.add(3);
        numbers.add(-1);
        numbers.add(5);

        //сортирует по возрастанию
        numbers.sort(Comparator.naturalOrder());

        for (var number:numbers) {
            System.out.print(number + " ");
        }
        
        //переворачивает список в конца
        numbers.sort(Comparator.reverseOrder());
        System.out.println();
        for (var number:numbers) {
            System.out.print(number + " ");
        }
```
3. **toArray()** – данный метод превращает список в массив. Он возвращает массив объектов (`Object[]`), но можно вернуть желаемый тип данных и для этого потребуется в метод `toArray(Array a)` передать уже созданный массив.
```java
		ArrayList<Integer> numbers = new ArrayList<>();
        numbers.add(1);
        numbers.add(3);
        numbers.add(-1);
        numbers.add(5);

        var numbersArray = numbers.toArray();
        for (var number:numbersArray) {
            System.out.print(number + " ");
        }
        System.out.println();
        //определения типа Integer[], чтобы  в тип данных
        var numbersArrayDefined = new Integer[numbers.size()];
        numbers.toArray(numbersArrayDefined);
        for (var number: numbersArrayDefined){
            System.out.print(number + " ");
        }
```
Вывод:
==1 3 -1 5 
1 3 -1 5==

4. **isEmpty()** – проверка списка на наличие элементов. Если список пустой, то возвращает `true`, в противном случае – `false`.
```java
		ArrayList<Integer> numbers = new ArrayList<>();
        numbers.add(1);
        numbers.add(3);
        numbers.add(-1);
        numbers.add(5);

        System.out.println(numbers.isEmpty());//false

        ArrayList<Integer> numbersEmpty = new ArrayList<>();
        System.out.println(numbersEmpty.isEmpty()); //true
```
5. **indexOf(Object o)** – метод возвращает позицию передаваемого элемента, и, если элемент не был найден, возвращает -1.
```java
		ArrayList<String> fruits = new ArrayList<>();
        fruits.add("apple");
        fruits.add("banana");
        fruits.add("watermelon");

        System.out.println(fruits.indexOf("apple")); // 0
        System.out.println(fruits.indexOf("banana")); // 1
        System.out.println(fruits.indexOf("watermelon")); // 2
```
6. **clear()** – удаляет все элементы из списка.
```java
		ArrayList<String> fruits = new ArrayList<>();
        fruits.add("apple");
        fruits.add("banana");
        fruits.add("watermelon");

        fruits.clear(); // очищаем список
        System.out.println(fruits.isEmpty()); // true
```
7. **clone()** – метод копирует список. После копирования нужно привести к необходимому классу, то есть `type casting`. Когда список клонируется, создается отдельный независимый объект и удаление родительского списка не влияет на элементы нового списка.
```java
ArrayList<String> fruits = new ArrayList<>();
        fruits.add("apple");
        fruits.add("banana");
        fruits.add("watermelon");

        var fruitsNew = (ArrayList<String>)fruits.clone();
        fruits.clear(); // очищаем предыдущий список 
        // для проверки что fruitsNew действительно новый список

        for (var fruit : fruitsNew) {
            System.out.println(fruit);
        }
```
Вывод:
==apple
banana
watermelon==