#Java #Comparable #Comparator 
## [Comparable и Comparator в Java](https://www.scaler.com/topics/java/comparable-and-comparator-in-java/)

2024-11-12 14:48

Чтобы отсортировать пользовательские объекты, нам нужно предоставить явную логику сортировки.

Для этого в Java предусмотрены интерфейсы [Comparable](Comparable) и [Comparator](Comparator). Интерфейсы Comparable и Comparator в Java позволяют определять собственное поведение сортировки объектов, в том числе сортировку по нескольким элементам данных.

### Разница между Comparable и Comparator в Java

Ключевые различия между [Comparable](Comparable) и [Comparator](Comparator) в Java приведены ниже. 

| [Comparable](Comparable)                                                                         | [Comparator](Comparator)                                                                              |
| ------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------- |
| Comparable - это интерфейс на Java.                                                              | Comparator - это функциональный интерфейс на Java.                                                    |
| Comparable предоставляет метод compareTo() для сортировки объектов.                              | Comparator предоставляет метод compare() для сортировки объектов.                                     |
| Comparable является частью пакета Java.lang.                                                     | Comparator является частью java.util пакета.                                                          |
| Comparable может использоваться для естественного упорядочивания или по умолчанию.               | Comparator можно использовать для пользовательского упорядочивания.                                   |
| Comparable обеспечивает единую последовательность сортировки. Пример: сортировка по id или имени | Компаратор обеспечивает несколько последовательностей сортировки. Например, сортировка по id и имени. |
| Comparable изменяет класс, который его реализует.                                                | Comparator не изменяет ни один класс.                                                                 |

### Использование Comparable интерфейса

Comparable — это интерфейс в Java, который позволяет **сравнивать объект с другими объектами того же типа**. Интерфейс Comparable предоставляется пакетом java.lang. Несколько встроенных классов в Java, таких как [Integer](WrapperInteger), Double, [String](String) и т. д., реализуют интерфейс Comparable.

Comparable используется для сортировки объектов по **естественному или стандартному порядку**, то есть сам объект знает, как его нужно упорядочивать. Пример: объекты SuperHero должны быть упорядочены по id.

Comparable обеспечивает **единую последовательность сортировки**. Это означает, что объекты можно сортировать по одному элементу данных. Пример: объект SuperHero можно сортировать по одному атрибуту, например id, name или age.

**Синтаксис**
```java
class T implements Comparable<T> {
    @Override
    public int compareTo(T t) {
        // comparasion logic
    }
}
```
Класс должен реализовывать интерфейс Comparable и метод compareTo(), чтобы его можно было сравнивать с другими объектами того же типа.

### Методы, используемые в Comparable

### compareTo()

Интерфейс Comparable содержит ровно один метод compareTo(), который принимает в качестве параметра один объект и возвращает целочисленное значение. Java определяет порядок сортировки на основе целочисленного значения, возвращаемого методом compareTo().

**Синтаксис**
```java
int compareTo(T o1);
```

Предположим, что объект x сравнивается с y с помощью оператора x.compareTo(y), тогда значение, возвращаемое методом, должно быть
- 0, если значения x и y равны.
- Отрицательное значение, если значение в x меньше, чем в y.
- Положительное, если значение в x больше, чем в y.

### Пример Comparable в Java

Рассмотрите возможность создания [REST API](https://www.scaler.com/topics/what-is-rest-api/), который будет получать список супергероев с сервера.

- **GET /superheroes**: возвращает супергероев, отсортированных по возрастанию id.
- **GET /superheroes?sort=name**: возвращает супергероев, отсортированных по возрастанию имени.
- **GET /superheroes?sort=age**: возвращает супергероев, отсортированных по возрастанию возраста.

Прежде чем продолжить, давайте определим класс SuperHero со свойствами id, name и age.
```java
class SuperHero {
    private final String id;
    private final String name;
    private final int age;
    
    /* class constructor */
    public SuperHero(String id, String name, int age) {
        this.id = id;
        this.name = name;
        this.age = age;
    }
    
    public String getId() { return this.id; } // getId function
    
    public String getName() { return this.name; } // getName function
    
    public int getAge() { return this.age; } // getAge function
    
    @Override
    public String toString() {
        return String.format("ID: %s | name: %s | Age: %d", id, name, age);
    }
}
```

Возьмём наш первый вариант использования, **GET /superheroes**. Эта конечная точка должна возвращать список супергероев, упорядоченный по id в порядке возрастания.

Нам нужно отсортировать класс SuperHero по id в порядке возрастания. Это можно сделать в два этапа.

### Реализация

1. Сделайте класс SuperHero реализующим интерфейс Comparable.
2. Переопределите метод compareTo().

```java
// 1. Implement Comparable interface
class SuperHero implements Comparable<SuperHero> {
    private final String id;
    private final String name;
    private final int age;
    
    public SuperHero(String id, String name, int age) {
        this.id = id;
        this.name = name;
        this.age = age;
    }
    
    // 2. override compareTo method.
    @Override
    public int compareTo(final SuperHero superHero) {
        return this.id.compareTo(superHero.id);
    }
    
    public String getId() { return this.id; }
    
    public String getName() { return this.name; }
    
    public int getAge() { return this.age; }
    
    @Override
    public String toString() {
        return String.format("ID: %s | Name: %s | Age: %d", id, name, age);
    }
}

public class Main {
    public static void main(String[] args) {
        List<SuperHero> superHeroes = new ArrayList<>();

        superHeroes.add(new SuperHero("2", "Iron Man", 35));
        superHeroes.add(new SuperHero("1", "Captain America", 25));
        superHeroes.add(new SuperHero("3", "Hulk", 20));
        
        Collections.sort(superHeroes);
/* printing result */
        superHeroes.forEach(superHero -> 
                            System.out.println(superHero.toString()));
    }
}
```

**Вывод**

```plaintext
ID: 1 | Name: Captain America | Age: 25
ID: 2 | Name: Iron Man | Age: 35
ID: 3 | Name: Hulk | Age: 20
```

**Объяснение:** Мы реализовали интерфейс Comparable и переопределили метод compareTo() для сортировки объектов SuperHero по id. Collections.sort() внутренне вызывает метод compareTo() объектов SuperHero для их сортировки по id.

### Использование Comparator

[Comparator](Comparator) — это функциональный интерфейс в Java, который можно использовать для сортировки объектов. Он предоставляется пакетом java.util.

[Функциональный интерфейс](Functional-Interface) — это интерфейс, содержащий ровно один абстрактный метод. Он также называется интерфейсом с одним абстрактным методом (SAM).

Но постойте, именно это и делает интерфейс Comparable. Тогда зачем нам нужен интерфейс Comparator? Если класс реализует интерфейс Comparable, то он знает, как сортировать себя, потому что сам класс реализовал метод compareTo().

Это называется **упорядочиванием по умолчанию**. Comparator используется для **пользовательского упорядочивания**, когда класс не знает о логике упорядочивания.

Компаратор обеспечивает **несколько последовательностей сортировки** (т. е. сортировку объектов по нескольким элементам данных). Пример: объекты SuperHero можно сортировать по нескольким атрибутам, таким как id, имя и возраст.

**Синтаксис:**

```java
Comparator<T> comparator = (T t1, T t2) -> { //comparison logic }
```

Компаратор можно создать с помощью лямбда-выражения, которое принимает два объекта заданного типа и должно возвращать целочисленное значение.

### Методы, используемые в Comparator

Конечно! Вот обновленная таблица с описаниями методов и синтаксиса:

| Имя метода      | Описание                                                                    | Синтаксис                                                                        |
| --------------- | --------------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| compare()       | Сравнивает два объекта и возвращает целое значение, указывающее их порядок. | int compare(T o1, T o2);                                                         |
| equals()        | Проверяет, равны ли два компаратора в их порядке.                           | comparator1.equals(comparator2);                                                 |
| comparing()     | Создает компаратор на основе указанной функции keyExtractor.                | Сравнение Comparator(функция keyExtractor);                                      |
| thenComparing() | Связывает компараторы для применения серии последовательностей сортировки.  | Сравнение параметров Comparator(функция keyExtractor, Comparator keyComparator); |

Краткие описания посвящены основной цели каждого метода, а также приводится синтаксис для каждого метода.

### Пример Comparator в Java

Рассмотрим наш второй и третий варианты использования: **GET /superheroes?sort=name** и **GET /superheroes?sort=age**, которые возвращают супергероев, упорядоченных по имени и возрасту в порядке возраста, соответственно. Мы уже переопределили метод compareTo() для сортировки объектов SuperHero по id. Поэтому его нельзя использовать для сортировки по имени или возрасту. Здесь на помощь приходит Comparator, который позволяет создавать пользовательские компараторы. Пример: nameComparator, ageComparator.

```java
public class Main {
    public static void sortByName(List<SuperHero> superHeroes) {
        // Comparator to sort by name ascending
        Comparator<SuperHero> nameComparator = (SuperHero s1, SuperHero s2) ->
        {
            return s1.getName().compareTo(s2.getName());
        };
        
        superHeroes.sort(nameComparator);
    }
    
    public static void sortByAge(List<SuperHero> superHeroes) {
        // Comparator to sort by age ascending
        Comparator<SuperHero> ageComparator = (SuperHero s1, SuperHero s2) -> 
        {
            return s1.getAge() - s2.getAge();
        };
        
        superHeroes.sort(ageComparator);
    }
    
    public static void main(String[] args) {
        List<SuperHero> superHeroes = new ArrayList<>();

        superHeroes.add(new SuperHero("2", "Iron Man", 35));
        superHeroes.add(new SuperHero("1", "Captain America", 25));
        superHeroes.add(new SuperHero("3", "Hulk", 20));

        System.out.println("Sorting By Name Ascending...");
        sortByName(superHeroes);
        superHeroes.forEach(superHero -> 
                            System.out.println(superHero.toString()));
        
        System.out.println("");
        
        System.out.println("Sorting By Age Ascending...");
        sortByAge(superHeroes);
        superHeroes.forEach(superHero -> 
                            System.out.println(superHero.toString()));
    }
}
```

**Вывод**

```plaintext
Sorting By Name Ascending...
ID: 1 | Name: Captain America | Age: 25
ID: 3 | Name: Hulk | Age: 20
ID: 2 | Name: Iron Man | Age: 35

Sorting By Age Ascending...
ID: 3 | Name: Hulk | Age: 20
ID: 1 | Name: Captain America | Age: 25
ID: 2 | Name: Iron Man | Age: 35

```

**Объяснение** Мы создали nameComparator и comparator, которые сортируют объекты SuperHero по имени и возрасту соответственно. Компараторы создаются с помощью **лямбда-выражений**, поскольку Comparator — это функциональный интерфейс.

[Функциональный интерфейс](Functional-Interface) — это интерфейс, содержащий **ровно один абстрактный метод**. Он также называется **интерфейсом с одним абстрактным методом (SAM)**. Он может содержать любое количество методов по умолчанию. 

## Заключение

- Comparable — это интерфейс в Java, который позволяет сравнивать объект с другими объектами того же типа.
- Comparable используется для упорядочивания объектов по умолчанию.
- Классы реализуют интерфейс Comparable и переопределяют метод compareTo(), чтобы обеспечить упорядочивание по умолчанию.
- Comparator — это функциональный интерфейс в Java, который может сортировать объекты. Он используется для пользовательской сортировки объектов.
- Компаратор предоставляет метод compare(), который можно переопределить для реализации пользовательской логики сравнения.