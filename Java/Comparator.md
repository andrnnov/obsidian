#Java #Comparator
### [Java Comparator](https://www.jenkov.com/tutorials/java-collections/comparator.html) ###

2023-11-01 17:05

Интерфейс Java Comparator, java.util.Comparator представляет собой компонент, который может сравнивать два объекта, чтобы их можно было отсортировать с помощью функции сортировки в Java. При сортировке, например, списка Java вы можете передать Java-компаратор методу сортировки. Затем компаратор используется для сравнения объектов в списке во время сортировки.

Интерфейс Java Comparator отличается от интерфейса Java Comparable. Компаратор является внешним компонентом сравниваемых объектов, тогда как Comparable - это интерфейс, реализуемый самими сравниваемыми объектами. Говорят, что порядок сортировки сопоставимого является естественным порядком сортировки объектов, в то время как порядок сортировки компаратора - нет.
#### Определение интерфейса Java Comparator ####

Интерфейс Java Comparator расположен в пакете java.util.  Интерфейса Java Comparator выглядит следующим образом:
```java
public interface Comparator<T> {
    
    public int compare(T o1, T o2);
}
```
Обратите внимание, что интерфейс Java Comparator имеет только один метод. Этот метод, метод compare(), принимает два объекта, для сравнения которых предназначена реализация Comparator. Метод compare() возвращает значение int, которое сигнализирует о том, какой из двух объектов был больше. Семантика возвращаемых значений такова:
- Отрицательное значение означает, что первый объект был меньше второго объекта. 
- Значение 0 означает, что два объекта равны. 
- Положительное значение означает, что первый объект был больше второго объекта.
##### Переходное сравнение #####

Обратите внимание, что при реализации интерфейса Java Comparator требуется, чтобы реализация учитывала следующие характеристики транзитивного сравнения: Если A больше, чем B, а B больше, чем C, то A также должно быть больше, чем C.
#### Реализация интерфейса Java Comparator ####

Представьте, что у вас есть следующий класс Spaceship, экземпляры которого вы хотели бы иметь возможность сравнивать:
```java
public class Spaceship implements Comparable<Spaceship> {

    private String spaceshipClass = null;
    private String registrationNo = null;

    public Spaceship(String spaceshipClass, String registrationNo) {
        this.spaceshipClass = spaceshipClass;
        this.registrationNo = registrationNo;
    }

    public String getSpaceshipClass() {
        return spaceshipClass;
    }

    public String getRegistrationNo() {
        return registrationNo;
    }

    @Override
    public int compareTo(Spaceship other) {
        int spaceshipClassComparison =
                this.spaceshipClass.compareTo(other.spaceshipClass);

        if(spaceshipClassComparison != 0) {
            return spaceshipClassComparison;
        }

        return this.registrationNo.compareTo(other.registrationNo);
    }
}
```
Обратите внимание, что класс Spaceship уже реализует сопоставимый интерфейс, который сначала сравнивает объекты Spaceship в spaceshipClass, а затем registrationNo. Кстати, в этом нет необходимости, если вы хотите сравнить объекты с помощью компаратора. Реализует ли objects сопоставимый интерфейс или нет, не имеет значения при сравнении объектов с помощью компаратора.

Теперь представьте, что вы хотите отсортировать объекты космического корабля только по их регистрационному номеру и игнорировать класс spaceshipClass. Вот реализация Java Comparator, которая сделает это:
```java
import java.util.Comparator;

public class SpaceshipComparator implements Comparator<Spaceship> {

    @Override
    public int compare(Spaceship o1, Spaceship o2) {
        return o1.getRegistrationNo().compareTo(o2.getRegistrationNo());
    }
}
```
Во-первых, обратите внимание, как класс SpaceshipComparator реализует интерфейс Comparator с типом Spaceship, указанным внутри символов < > ( реализует Comparator`<Spaceship>` ). Это задает тип объектов, которые эта реализация компаратора может сравнивать с объектами космического корабля.

Установка универсального типа реализации Comparator на Spaceship означает, что типам параметров метода compare() может быть присвоено значение Spaceship, а не Object, как это было бы - если бы не был указан универсальный тип (реализует Comparator ). 

Реализация Java Comparator в значительной степени всегда специализирована для того, чтобы иметь возможность сравнивать объекты определенного типа (класса), поэтому указание универсального типа в вашей реализации Comparator почти всегда имеет смысл. 

Во-вторых, обратите внимание, как метод compare() возвращает значение registrationNo первого параметра Spaceship по сравнению с значением registrationNo второго параметра Spaceship. Это абсолютно правильный способ реализации компаратора.
##### Сравнение чисел #####

Если вашей реализации компаратора необходимо сравнить числа из сравниваемых объектов, простой способ - просто вычесть два числа друг из друга и вернуть это значение.

Представьте, если бы переменная registrationNo класса Spaceship была вместо этого int, поэтому функция getRegistrationNo() возвращала бы int. Затем можно было бы сравнить регистрационные данные двух объектов космического корабля следующим образом:
```java
import java.util.Comparator;

public class SpaceshipComparator implements Comparator<Spaceship> {

    @Override
    public int compare(Spaceship o1, Spaceship o2) {
        return o1.getRegistrationNo() - o2.getRegistrationNo();
    }
}
```

