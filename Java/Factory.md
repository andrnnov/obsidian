#Java #DesignPatterns #Factory

## Паттерн проектирования Factory

2024-07-17 14:48

Паттерн **Factory** — это порождающий паттерн проектирования, который определяет общий интерфейс для создания объектов в суперклассе, позволяя подклассам изменять тип создаваемых объектов.

Представим, что нам нужна "фабрика", которая выпускает разные пончики:
- пончик с вишней
- пончик с белым шоколадом
- пончик с миндалем

Соответственно, под **каждый пончик** должен быть **свой класс.** Однако все эти классы очень похожи. Все пончики будут иметь одинаковый набор параметров:
- вес
- калорийность
- дату изготовления
- начинку
- и т.д.

Поскольку эти классы пончиков очень похожи, создавать каждый экземпляр класса вручную будет достаточно громоздко и к тому же они будут практически одинаковыми. Поэтому мы можем создать специальный объект, который будет уметь делать пончик, **зная его начинку**.

То есть мы сможем просто сказать:
- "Создай пончик **с вишней**"
- "Создай пончик **с белым шоколадом**"
- "Создай пончик **с миндалем**"

Для этого нам необходимо использовать **паттерн Factory.** Создаем нашу первую "фабрику" (Factory). Давайте назовем ее "Фабрика пончиков" (DoughnutFactory):
```java
public class DoughnutFactory {
}
```
Для того чтобы мы могли их производить на одной фабрике, нужно "указать, что все эти пончики имеют **один тип**" - а именно, "пончик". Давайте объединим их, создав общий для всех интерфейс **Doughnut** (Doughnut.java):
```java
public interface Doughnut {
    void eat();
}
```
Теперь давайте создадим три класса пончиков, которые имплементиуют интерфейс **Doughnut**.
```java
public class CherryDoughnut implements Doughnut {
    @Override
    public void eat() {
        System.out.println("You are eating Cherry doughnut!");
    }
}

public class ChocolateDoughnut implements Doughnut {
    @Override
    public void eat() {
        System.out.println("You are eating Chocolate doughnut!");
    }
}

public class AlmondDoughnut implements Doughnut {
    @Override
    public void eat() {
        System.out.println("You are eating Almond doughnut!");
    }
}
```
Итак, суть фабрики сводится к тому, чтобы производить объекты **разного типа**. Но как сделать так, чтоб Фабрика понимала какой именно тип объекта(пончика) мы хотим получить: с вишней, с белым шоколадом или с миндалем?

Для этого давайте создадим [ENUM](Enum), в котором запишем все возможные типы пончиков:
```java
public enum DoughnutTypes {
    CHERRY,
    CHOCOLATE,
    ALMOND
}
```
Конечно, мы могли бы использовать вместо [ENUM](Enum) строку [String](String) с названием, но тогда ошибок гораздо сложнее избежать. Если исключить опечатки, то пришлось бы запоминать, в каком формате вводить строку - "Chocolate", "CHOCOLATE" или "ChocolateDoughnut"? В общем, все эти проблемы нам не нужны, поэтому мы создали [ENUM](Enum).

Таким образом, наша фабрика будет принимать название объекта (в нашем случае ENUM), и возвращать объект нужного типа. Прототип такой функции будет выглядеть следующим образом:
```java
public class DoughnutFactory {
    public Doughnut getDoughnut(DoughnutTypes type) {
    Doughnut toReturn = null;
        switch (type) {
            case CHERRY:
                toReturn = new CherryDoughnut();
                break;
            case CHOCOLATE:
                toReturn = new ChocolateDoughnut();
                break;
            case ALMOND:
                toReturn = new AlmondDoughnut();
                break;
            default:
                throw new IllegalArgumentException("Wrong doughnut type:" + type);
        }
        return toReturn;
    }
}
```
Принимается ENUM **DoughnutTypes**, а возвращается любой объект, имплементирующий интерфейс **Doughnut**.

Мы создаем и возвращаем новый объект нужного типа. Если будет введено не CHERRY, не CHOCOLATE и не ALMOND (а это может быть только **null**), тогда мы показываем ошибку.

Протестируем наш код. Создадим **main()**, в котором создадим все типы поисков по очереди и вызовем на них метод **eat()**:
```java
public class Main {
    public static void main(String[] args) {
        DoughnutFactory factory = new DoughnutFactory();
 
        Doughnut cherry = factory.getDoughnut(DoughnutTypes.CHERRY);
        Doughnut chocolate = factory.getDoughnut(DoughnutTypes.CHOCOLATE);
        Doughnut almond = factory.getDoughnut(DoughnutTypes.ALMOND);
 
        cherry.eat();
        chocolate.eat();
        almond.eat();
    }
}
```

Листинг программы main.java:
```java
public class Main {
public enum DoughnutTypes {
    CHERRY,
    CHOCOLATE,
    ALMOND
}

public static class DoughnutFactory {

    public Doughnut getDoughnut(DoughnutTypes type) {
        Doughnut toReturn = null;
        switch (type) {
            case CHERRY:
                toReturn = new CherryDoughnut();
                break;
            case CHOCOLATE:
                toReturn = new ChocolateDoughnut();
                break;
            case ALMOND:
                toReturn = new AlmondDoughnut();
                break;
            default:
                throw new IllegalArgumentException("Wrong doughnut type:" + type);
        }
        return toReturn;
    }
}
public static class CherryDoughnut implements Doughnut {
    @Override
    public void eat() {
        System.out.println("You are eating Cherry doughnut!");
    }
}

public static class ChocolateDoughnut implements Doughnut {
    @Override
    public void eat() {
        System.out.println("You are eating Chocolate doughnut!");
    }
}

public static class AlmondDoughnut implements Doughnut {
    @Override
    public void eat() {
        System.out.println("You are eating Almond doughnut!");
    }
}
    public static void main(String[] args) {
        DoughnutFactory factory = new DoughnutFactory();

        Doughnut cherry = factory.getDoughnut(DoughnutTypes.CHERRY);
        Doughnut chocolate = factory.getDoughnut(DoughnutTypes.CHOCOLATE);
        Doughnut almond = factory.getDoughnut(DoughnutTypes.ALMOND);

        cherry.eat();
        chocolate.eat();
        almond.eat();
    }
}
```
В консоли получим:
<p style="background-color: navy; color: yellow">
You are eating Cherry doughnut!<br>
You are eating Chocolate doughnut!<br>
You are eating Almond doughnut!</p>

### Применимость 

#### Когда заранее неизвестны типы и зависимости объектов, с которыми должен работать ваш код.

 Фабричный метод отделяет код производства продуктов от остального кода, который эти продукты использует.

Благодаря этому, код производства можно расширять, не трогая основной. Так, чтобы добавить поддержку нового продукта, вам нужно создать новый подкласс и определить в нём фабричный метод, возвращая оттуда экземпляр нового продукта.

#### Когда вы хотите дать возможность пользователям расширять части вашего фреймворка или библиотеки.

 Пользователи могут расширять классы вашего фреймворка через наследование. Но как сделать так, чтобы фреймворк создавал объекты из этих новых классов, а не из стандартных?

Решением будет дать пользователям возможность расширять не только желаемые компоненты, но и классы, которые создают эти компоненты. А для этого создающие классы должны иметь конкретные создающие методы, которые можно определить.

Например, вы используете готовый UI-фреймворк для своего приложения. Но вот беда — требуется иметь круглые кнопки, вместо стандартных прямоугольных. Вы создаёте класс `RoundButton`. Но как сказать главному классу фреймворка `UIFramework`, чтобы он теперь создавал круглые кнопки, вместо стандартных?

Для этого вы создаёте подкласс `UIWithRoundButtons` из базового класса фреймворка, переопределяете в нём метод создания кнопки (а-ля `createButton`) и вписываете туда создание своего класса кнопок. Затем используете `UIWithRoundButtons` вместо стандартного `UIFramework`.

#### Когда вы хотите экономить системные ресурсы, повторно используя уже созданные объекты, вместо порождения новых.

 Такая проблема обычно возникает при работе с тяжёлыми ресурсоёмкими объектами, такими, как подключение к базе данных, файловой системе и т. д.

Представьте, сколько действий вам нужно совершить, чтобы повторно использовать существующие объекты:

1. Сначала вам следует создать общее хранилище, чтобы хранить в нём все создаваемые объекты.
2. При запросе нового объекта нужно будет заглянуть в хранилище и проверить, есть ли там неиспользуемый объект.
3. А затем вернуть его клиентскому коду.
4. Но если свободных объектов нет — создать новый, не забыв добавить его в хранилище.

Весь этот код нужно куда-то поместить, чтобы не засорять клиентский код.

Самым удобным местом был бы конструктор объекта, ведь все эти проверки нужны только при создании объектов. Но, увы, конструктор всегда создаёт **новые** объекты, он не может вернуть существующий экземпляр.

Значит, нужен другой метод, который бы отдавал как существующие, так и новые объекты. Им и станет фабричный метод.

### Шаги реализации

1. Приведите все создаваемые продукты к общему интерфейсу. 

2. В классе, который производит продукты, создайте пустой фабричный метод. В качестве возвращаемого типа укажите общий интерфейс продукта.

3. Затем пройдитесь по коду класса и найдите все участки, создающие продукты. Поочерёдно замените эти участки вызовами фабричного метода, перенося в него код создания различных продуктов.
    
    В фабричный метод, возможно, придётся добавить несколько параметров, контролирующих, какой из продуктов нужно создать.
    
    На этом этапе фабричный метод, скорее всего, будет выглядеть удручающе. В нём будет жить большой условный оператор, выбирающий класс создаваемого продукта. Но не волнуйтесь, мы вот-вот исправим это.
    
4. Для каждого типа продуктов заведите подкласс и переопределите в нём фабричный метод. Переместите туда код создания соответствующего продукта из суперкласса.
    
5. Если создаваемых продуктов слишком много для существующих подклассов создателя, вы можете подумать о введении параметров в фабричный метод, которые позволят возвращать различные продукты в пределах одного подкласса.
    
    Например, у вас есть класс `Почта` с подклассами `АвиаПочта` и `НаземнаяПочта`, а также классы продуктов `Самолёт`, `Грузовик` и `Поезд`. `Авиа` соответствует `Самолётам`, но для `НаземнойПочты` есть сразу два продукта. Вы могли бы создать новый подкласс почты для поездов, но проблему можно решить и по-другому. Клиентский код может передавать в фабричный метод `НаземнойПочты` аргумент, контролирующий тип создаваемого продукта.
    
6. Если после всех перемещений фабричный метод стал пустым, можете сделать его абстрактным. Если в нём что-то осталось — не беда, это будет его реализацией по умолчанию. 

###  Преимущества

-  Избавляет класс от привязки к конкретным классам продуктов.
-  Выделяет код производства продуктов в одно место, упрощая поддержку кода.
-  Упрощает добавление новых продуктов в программу.
-  Реализует _принцип открытости/закрытости_.

### Недостатки

Может привести к созданию больших параллельных иерархий классов, так как для каждого класса продукта надо создать свой подкласс создателя.

#### Пример использования фабрики

Мы можем создавать объекты разных типов с помощью **одного и того же метода**. Это очень удобно, когда возникает ситуация, в которой мы не знаем, какой тип нам понадобится.

Например, создадим метод "скушать случайный пончик" - **eatRandomDoughnut**:
```java
import java.util.Random;
 
    public static void eatRandomDoughnut(DoughnutFactory factory){ 
        Doughnut randomDougnut = getRandomDougnut(factory); 
        System.out.printf("What a surprise! "); 
        randomDougnut.eat();
   }
   
    public static Doughnut getRandomDougnut(DoughnutFactory factory){
        Random random = new Random();
        DoughnutTypes type = DoughnutTypes.values()[random.nextInt(DoughnutTypes.values().length)];
 
        return(factory.getDoughnut(type));
    }
```
Обратите внимание - nextInt() будет генерировать целые числа в диапазоне от 0 до 3. То есть возможны такие опции: 0, 1 и 2. А это и есть 3 вида начинок пончиков.

Давайте запустим:
```java
import java.util.Random;
 
public class Main {
 
    public static void main(String[] args) { 
        DoughnutFactory factory = new DoughnutFactory(); 
        eatRandomDoughnut(factory);
   }
    
    public static void eatRandomDoughnut(DoughnutFactory factory){ 
        Doughnut randomDougnut = getRandomDougnut(factory);
        System.out.printf("What a surprise! "); 
        randomDougnut.eat(); 
    }
 
    public static Doughnut getRandomDougnut(DoughnutFactory factory){
        Random random = new Random();
        DoughnutTypes type = DoughnutTypes.values()[random.nextInt(DoughnutTypes.values().length)];
 
        return(factory.getDoughnut(type));
    }
}
```
Для убедительности, можно запустить метод **eatRandomDoughnut()** сто раз:
```java
import java.util.Random;
 
public class Main {
 
    public static void main(String[] args) {
        DoughnutFactory factory = new DoughnutFactory(); 
        for(int i = 0; i < 100; i++) { 
            eatRandomDoughnut(factory);
        } 
    }
 
    public static void eatRandomDoughnut(DoughnutFactory factory) {
        Doughnut randomDougnut = getRandomDougnut(factory); 
        System.out.printf("What a surprise! "); 
        randomDougnut.eat(); 
    }
 
    public static Doughnut getRandomDougnut(DoughnutFactory factory){
        Random random = new Random();
        DoughnutTypes type = DoughnutTypes.values()[random.nextInt(DoughnutTypes.values().length)];
 
        return(factory.getDoughnut(type));
    }
 
}
```
**Вывод:**
<p style="background-color: navy; color: yellow">
What a surprise! You are eating Cherry doughnut!<br>
What a surprise! You are eating Chocolate doughnut!<br>
What a surprise! You are eating Almond doughnut!<br>
What a surprise! You are eating Cherry doughnut!<br>
What a surprise! You are eating Chocolate doughnut!<br>
What a surprise! You are eating Chocolate doughnut!<br>
What a surprise! You are eating Chocolate doughnut!<br>
What a surprise! You are eating Chocolate doughnut!<br>
What a surprise! You are eating Cherry doughnut!<br>
What a surprise! You are eating Chocolate doughnut!</p>

Мы можем "запаковать" дополнительный функционал в нашу Фабрику. Например, посчитаем, сколько пончиков каждого типа было создано конкретной фабрикой.

Сначала создаем новые переменные, которые будут хранить результат:
```java
public class DoughnutFactory {
    private Integer cherryDoughnutCount = 0;
    private Integer chocolateDoughnutCount = 0;
    private Integer almondDoughnutCount = 0;
 
    //...
}
```
Теперь, как мы будем изменять эти значения? Очень просто -дополним наш метод getDoughnut():
```java
public Doughnut getDoughnut(DoughnutTypes type) {
    Doughnut toReturn = null;
    switch (type) {
        case CHERRY:
            cherryDoughnutCount++;
            toReturn = new CherryDoughnut();
            break;
        case CHOCOLATE:
            chocolateDoughnutCount++;
            toReturn = new ChocolateDoughnut();
            break;
        case ALMOND:
            almondDoughnutCount++;
            toReturn = new AlmondDoughnut();
            break;
        default:
            throw new IllegalArgumentException("Wrong doughnut type:" + type);
    }
    return toReturn;
}
```
Для вывода результатов в консоль напишем следующий метод:
```java
public void printCount() {
    System.out.println("Number of doughnuts produced (by type):");
    System.out.println("Cherry doughnuts: " + cherryDoughnutCount);
    System.out.println("Chocolate doughnuts: " + chocolateDoughnutCount);
    System.out.println("Almond doughnuts: " + almondDoughnutCount);
    System.out.println("Total: " + (cherryDoughnutCount + chocolateDoughnutCount + almondDoughnutCount));
}
```

Итого, наш класс DoughnutFactory целиком, со всеми дополнениями, будет выглядеть так:
```java
public class DoughnutFactory {
    private Integer cherryDoughnutCount = 0;
    private Integer chocolateDoughnutCount = 0;
    private Integer almondDoughnutCount = 0;
 
    public Doughnut getDoughnut(DoughnutTypes type) {
        Doughnut toReturn = null;
        switch (type) {
            case CHERRY:
                cherryDoughnutCount++;
                toReturn = new CherryDoughnut();
                break;
            case CHOCOLATE:
                chocolateDoughnutCount++;
                toReturn = new ChocolateDoughnut();
                break;
            case ALMOND:
                almondDoughnutCount++;
                toReturn = new AlmondDoughnut();
                break;
            default:
                throw new IllegalArgumentException("Wrong doughnut type:" + type);
        }
        return toReturn;
    }
 
    public void printCount() {
        System.out.println("Number of doughnuts produced (by type):");
        System.out.println("Cherry doughnuts: " + cherryDoughnutCount);
        System.out.println("Chocolate doughnuts: " + chocolateDoughnutCount);
        System.out.println("Almond doughnuts: " + almondDoughnutCount);
        System.out.println("Total: " + (cherryDoughnutCount + chocolateDoughnutCount + almondDoughnutCount));
    }
}
```
Теперь запустим с помощью такого кода:
```java
import java.util.Random;
 
public class Main {
 
    public static void main(String[] args) {
        DoughnutFactory factory = new DoughnutFactory(); 
        for(int i = 0; i < 100; i++) { 
            eatRandomDoughnut(factory);
        }
        factory.printCount(); 
    }
 
    public static void eatRandomDoughnut(DoughnutFactory factory) {
        Doughnut randomDougnut = getRandomDougnut(factory); 
        System.out.printf("What a surprise! "); 
        randomDougnut.eat(); 
    }
 
    public static Doughnut getRandomDougnut(DoughnutFactory factory){
        Random random = new Random();
        DoughnutTypes type = DoughnutTypes.values()[random.nextInt(DoughnutTypes.values().length)];
 
        return(factory.getDoughnut(type));
    }
 
}
```
В консоли получим что-то похожее на это:
<p style="background-color: navy; color: yellow">
What a surprise! You are eating Cherry doughnut!<br>
What a surprise! You are eating Chocolate doughnut!<br>
What a surprise! You are eating Cherry doughnut!<br>
What a surprise! You are eating Chocolate doughnut!<br>
What a surprise! You are eating Almond doughnut!<br>
Number of doughnuts produced (by type):<br>
Cherry doughnuts: 37<br>
Chocolate doughnuts: 31<br>
Almond doughnuts: 32<br>
Total: 100</p>

