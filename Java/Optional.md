#Java #Optional
### Java 8 Optional ###

2023-12-18 11:55

**Optional** - новый класс в пакете **java.util**, является контейнером (оберткой) для значений которая также может безопасно содержать **null**.

Благодаря опциональным типам можно забыть про проверки на **null** и **NullPointerException**.
#### Optional basics ####

Для создания **Optional** используются методы:
- **Optional.of**
```java
public static void main(String[] args) {
    Optional<String> name = Optional.of("John");
    System.out.println(name); //output Optional[John]
}
```
В метод **Optional.of** нельзя передавать **null**, если конечно мы не хотим получить **NullPointerException**
```java
public static void main(String[] args) {
    Optional<String> name = Optional.of(null); // java.lang.NullPointerException
    System.out.println(name);
}
```
- **Optional.ofNullable**
```java
public static void main(String[] args) {
    Optional<String> name = Optional.ofNullable("John");
    System.out.println(name); //output Optional[John]
}
```
А вот в метод **Optional.ofNullable** передавать **null** можно безопасно
```java
public static void main(String[] args) {
    String john = null;
    Optional<String> name = Optional.ofNullable(john);
    System.out.println(name); //output Optional.empty
}
```
- **Optional.empty** для создания пустого **Optional**
```java
public static void main(String[] args) {
    Optional<String> emptyOptional = Optional.empty();
    System.out.println(emptyOptional); //output Optional.empty
}
```
Для получения значения из **Optional** используется метод **Optional.get**, но он является небезопасным и может бросить **NoSuchElementException**
```java
public static void main(String[] args) {
    Optional<String> name = Optional.of("John");
    System.out.println(name.get()); //output John
    Optional<Object> nullOptional = Optional.ofNullable(null);
    System.out.println(nullOptional.get()); // java.util.NoSuchElementException: No value present
}
```
#### Optional isPresent, ifPresent ####

##### Optional isPresent #####

Метод **Optional.isPresent** возвращает **true**, если значение в нем присутствует, иначе возвращает **false**
```java
public static void main(String[] args) {
    Optional<String> name = Optional.of("John");
    if (name.isPresent()) {             //условие выполнится и мы увидим имя
        System.out.println(name.get()); //output John
    }

    Optional<Object> empty = Optional.empty();
    if (empty.isPresent()) {            //условие не выполнится, значит исключения не будет
        System.out.println(empty.get());
    }
}
```
Метод **Optional.get** лучше использовать в паре с **Optional.isPresent, чтобы предотвратить исключения
##### Optional ifPresent #####

Метод **Optional.ifPresent** выполняет переданное действие, если значение в **Optional** присутствует, иначе игнорирует его. Метод принимает [лямбда-выражение](Lambda) известное как **потребитель** (**[[Functional-Interface#Consumer|Consumer]]**).
```java
public static void main(String[] args) {
    Optional<String> name = Optional.of("John");
    name.ifPresent(val -> System.out.println(val)); //условие выполнится и мы увидим John
    Optional<Object> empty = Optional.empty();
    empty.ifPresent(val -> System.out.println(val)); //условие не выполнится, действие игнорируется
}
```
#### Optional orElse ####

Метод **Optional.orElse** возвращает переданное значение, если **Optional** пустой
```java
public static void main(String[] args) {
    Optional<String> name = Optional.of("John");
    System.out.println(name.orElse("blank")); //output John
    Optional<Object> empty = Optional.empty();
    System.out.println(empty.orElse("blank")); //output blank
}
```
##### Optional orElseGet #####

Метод **Optional.orElseGet** возвращает переданное значение из [_лямда-выражение_](Lambda) , если **Optional** пустой
```java
public static void main(String[] args) {
    Optional<String> name = Optional.of("John");
    System.out.println(name.orElseGet(() -> "blank")); //output John
    Optional<Object> empty = Optional.empty();
    System.out.println(empty.orElseGet(() -> "blank")); //output blank
}
```
#### Optional map, flatMap ####
##### Optional map #####

Метод **Optional.map** служит для преобразования значения внутри **Optional**. Если **Optional** пустой, преобразование не будет происходить
```java
public static void main(String[] args) {
    Optional<String> name = Optional.of("JOHN");
    System.out.println(name.map(String::toLowerCase));  //output Optional[john]
    Optional<String> empty = Optional.empty();
    System.out.println(empty.map(String::toLowerCase)); //output Optional.empty
}
```
##### Optional flatMap #####

Метод **Optional.flatMap** преобразовывает значение внутри **Optional,** но при этом не оборачивает их
```java
public static void main(String[] args) {
    Optional<Optional<String>> name = Optional.of(Optional.of("JOHN"));
    Optional<String> lowerCaseName = name.flatMap(o -> o.map(String::toLowerCase));
    System.out.println(lowerCaseName);  //output Optional[john]
    Optional<Optional<String>> empty = Optional.of(Optional.empty());
    System.out.println(empty.flatMap(o -> o.map(String::toLowerCase))); //output Optional.empty
}
```
