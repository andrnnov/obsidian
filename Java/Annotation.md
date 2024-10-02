#Java #Annotation
### [Руководство по аннотациям в Java и механизму их работы](https://topjava.ru/blog/rukovodstvo-po-annotatsiyam-v-java-i-mekhanizmu-ikh-raboty?ysclid=lroyg3ktmr717807333)

2024-01-23 12:21

#### Введение  

Аннотации появились в Java 5 в 2004 году.  

Это специальная форма синтаксических метаданных, которая может быть добавлена в исходный код. Аннотации используются для анализа кода, при компиляции или во время выполнения программы. Их можно применять к пакетам, классам, методам, переменным и параметрам.  

Самая простая аннотация, применимая к классу, выглядит так:  
```java
@MyAnnotation 
public class Foo {}
```

#### Маркерный интерфейс  

С момента появления языка Java возникла необходимость помечать, для выполнения тех или иных действий, определенным образом класс или иерархию классов. До Java 5 это делалось через _интерфейсы без методов_.  

Этот вид интерфейса не похож ни на один другой. Он не определяет никаких контрактов между собой и реализующими его классами, т. к. всегда пуст. Поэтому он называется _маркерным интерфейсом_. Такие интерфейсы нужны для маркировки чего-либо для JVM, компилятора или какой-либо библиотеки.  

[Serializable](Serializable) и [Cloneable](Cloneable) — два примера маркерных интерфейсов, которые достались нам в наследство. Например, [Serializable](Serializable) позволяет пометить класс, сообщая о том, что его экземпляры можно сериализовать. При этом перед сериализацией делается проверка на наличие имплементации этого интерфейса.
![[marker-interfaces.svg]]
Пример маркерных интерфейсов из JDK

С появлением аннотаций необходимость в использовании маркерных интерфейсов хоть и отпала, но до сих пор повсеместно используется.  

Пример интерфейса и аналогичной ему аннотации:  
```java
public class Foo implements MarkerInterface {} (1)

@MyAnnotation
public class Foo {} (2)
```
(1) Маркерный интерфейс  
(2) Аннотация — эквивалент маркерного интерфейса

#### Интерфейсы определяют тип  

По факту, маркерный интерфейс отмечает объект, реализующий какой-либо тип, что исключает ошибки на этапе компиляции.  

Например, создадим интерфейс без методов _MyMark и_ ряд классов: _MarkedClass_ (реализует MyMark); _NonMarkedClass_; _Main,_ в котором разместим метод _test,_ принимающий на вход объект типа _MyMark_.
```java
public interface MyMark {}

class MarkedClass implements MyMark {}

class NonMarkedClass {}

class Main {
    public static void main(String[] args) {
    	  MarkedClass marked = new MarkedClass();
    	  NonMarkedClass nonMarked = new NonMarkedClass();
   	 
    	  test(marked);
        //test(nonMarked); 
    }

    static void test(MyMark markedObject) {
        System.out.println("Метод 'Test' успешно завершен!");
    }
}
```
Вывод:
<p style="background-color: navy; color: yellow">
Метод 'Test' успешно завершен!</p>
Код _test (marked)_ успешно выполнится, поскольку класс объекта _marked_ реализует интерфейс _MyMark_, что требуется для работы метода _test (MyMark markedObject)_.  

Если раскомментировать строку _test (nonMarked),_ мы получим ошибку компиляции:
<font color="red">java: incompatible types: NonMarkedClass cannot be converted to MyMark</font>

Ошибка вызвана тем, что требуемым типом для метода _test()_ является _MyMark_, а мы передаем тип _NonMarkedClass_.

#### Интерфейс определяет тип для наследников класса  

Если класс реализует интерфейс, то и все его наследники будут реализовывать этот интерфейс. Нельзя «отвязать» интерфейс от наследников.  

В этом месте аннотации имеют преимущество, поскольку позволяют реализовать такой механизм «отвязывания». Но в этом есть и минус — проверка наличия маркера (аннотации) теперь проводится во время исполнения, а не во время компиляции, что чревато ошибками.  
Рассмотрим следующий код:
```java ------ MyAnnotation.java
import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

@Target(value = ElementType.TYPE)
@Retention(value = RetentionPolicy.RUNTIME)
public @interface MyAnnotation {}
```

```java ------ MyMark.java
public interface MyMark {}
```

```java ------ Main.java
@MyAnnotation
class Parent implements MyMark {}
//@MyAnnotation
class Child extends Parent {}

class Main {

    public static void main(String[] args) {
        Parent parent = new Parent();
        Child child = new Child();

        testInterface(parent);
        testInterface(child);

        testAnnotation(parent);
        testAnnotation(child);
    }

    public static void testInterface(MyMark markedObject) {
        System.out.println("Метод 'TestInterface' успешно завершен!");
    }

    public static void testAnnotation(Object object) {
        if (!object.getClass().isAnnotationPresent(MyAnnotation.class)) {
            throw new RuntimeException("Объект не аннотирован аннотацией 'MyAnnotation'");
        }
        System.out.println("Метод 'testAnnotation' успешно завершен!");
    }
}
```
Вывод:
<p style="background-color: navy; color: yellow">
Метод 'TestInterface' успешно завершен!<br>
Метод 'TestInterface' успешно завершен!<br>
Метод 'testAnnotation' успешно завершен!</p>
<font color="red">Exception in thread "main" java.lang.RuntimeException: Объект не аннотирован аннотацией 'MyAnnotation'<br>
	at Main.testAnnotation(Main.java:27)<br>
	at Main.main(Main.java:18)</font>

Вызов метода testAnnotation (child) на этапе исполнения генерирует исключение, сообщая, что объект не аннотирован аннотацией _MyAnnotation_, которой был аннотирован его родительский класс _Parent_. Для успешной компиляции классу _Child_ также необходимо использовать _MyAnnotation_.

#### Ключевые моменты:  

- Если требуется знать, могут ли методы принимать объекты каких-то классов, то такие классы удобнее пометить (реализовать) интерфейсами, так как ошибка выявится на этапе компиляции  
    
- Если необходимо провести анализ метаданных класса, то использование аннотаций даёт больше возможностей, в том числе принимая во внимание возможность аннотаций иметь параметры. Однако в этом случае анализ аннотаций происходит во время исполнения кода

### Анатомия аннотации

Итак, реализация базового определения аннотации имеет следующий вид:  
```java
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.TYPE)
@Inherited
@Documented
public @interface MyAnnotation {
    String name() default "";
    int value();
}
```
Начальный символ @ сообщает о наличии аннотации.  

Кратко расшифруем каждую строку с аннотациями и что они определяют:  
- **@Retention**: в каком жизненном цикле кода аннотация (тут и до конца абзаца речь про @MyAnnotation) будет доступна (в исходнике, в class-файле или во время выполнения)
- **@Target**: для какого элемента ее можно использовать (поле, класс, пакет и тд)
- **@Inherited**: позволяет реализовать наследование аннотаций родительского класса классом-наследником
- **@Documented**: аннотация будет помещена в сгенерированную документацию [javadoc](javadoc)
- **@interface**: сообщает о том, что это аннотация
- Как значения параметров аннотации, так и значения по умолчанию, являются опциональными (в данном примере присутствует два параметра: _name_ типа _String_ со значением по умолчанию и _value_ типа _int_).

Возможно, сейчас вам ничего не понятно, это нормально. Более детально эти аннотации будут рассмотрены далее.  

Стоит заметить, что в аннотации можно перечислить несколько значений, если значения по умолчанию отсутствуют. При этом переменная, именуемая _value_, относится к специальным переменным. Значение _value_ может использоваться без имени переменной, если другие значения отсутствуют. Например:
```java
// Оба значения приведены, их именование обязательно
@MyAnnotation(name = "какое-то имя", value = 42)
public class MyType { ... }
```
```java
// Присутствует только "value()", в качестве "name()" будет его значение по умолчанию
@MyAnnotation(value = 42)
public class MyType2 { ... }
```
```java
/ Если требуется только "value()", мы можем опустить имя
@MyAnnotation(42)
public class MyType3 { ... }
```
Закрепим полученные знания на примере. Создадим аннотацию _JavaFileInfo_, которая будет аннотировать классы и методы информацией об их авторах и версиях класса/метода:  
```java
import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

@Target({ElementType.TYPE, ElementType.METHOD})
@Retention(RetentionPolicy.RUNTIME)
public @interface JavaFileInfo {
    String name() default "Igor M.";
    String value() default "0.0";
}
```

Добавим аннотируемый класс _DemoClass_:  
```java
@JavaFileInfo("2.0")
public class DemoClass {
    @JavaFileInfo(name = "Chi Max", value = "1.0")
    public void printString() {}
}
```

Создадим класс _Main_, который при помощи рефлексии извлечет параметры нашей аннотации из _DemoClass_:  
```java
import java.lang.annotation.Annotation;
import java.lang.reflect.AnnotatedElement;
import java.lang.reflect.Method;

public class Main {
    public static void main(String[] args) throws NoSuchMethodException, SecurityException {
        Class<DemoClass> demoClassObj = DemoClass.class;
        readAnnotationOn(demoClassObj);
        Method method = demoClassObj.getMethod("printString");
        readAnnotationOn(method);
    }

    static void readAnnotationOn(AnnotatedElement element) {
        try {
            System.out.println("\nПоиск аннотаций в " + element.getClass().getName());
            Annotation[] annotations = element.getAnnotations();
            for (Annotation annotation : annotations) {
                if (annotation instanceof JavaFileInfo fileInfo) {
                    System.out.println("Автор: " + fileInfo.name());
                    System.out.println("Версия: " + fileInfo.value());
                }
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```
Результат выполнения программы:
<p style="background-color: navy; color: yellow">
Поиск аннотаций в java.lang.Class<br>
Автор: Igor M.<br>
Версия: 2.0<br>
<br>
Поиск аннотаций в java.lang.reflect.Method<br>
Автор: Chi Max<br>
Версия: 1.0</p>

#### Классификация аннотаций  

Аннотации можно классифицировать по следующим признакам:  

- аннотации для аннотаций:  
1. @Target  
   
- аннотации типов:  
1. @Retention
2. @Documented
3. @Inherited
4. @Repeatable

- аннотации для кода:  
1. @Override
2. @Deprecated  
3. @SuppressWarnings  
4. @SafeVarargs   
5. @FunctionalInterface  

- нативные аннотации
- аннотации, написанные программистом

#### Аннотации для аннотаций  

Аннотации для аннотаций еще называют _мета-аннотациями_.  
Их пять:  
- **@Target:** указывает контекст, для которого применима аннотация
- **@Retention**: указывает, до какого шага во время компиляции аннотация будет доступна
- **@Documented**: указывает, что аннотация должна быть задокументирована с помощью _javadoc_
- **@Inherited**: позволяет реализовать наследование аннотаций родительского класса классом-наследником
- **@Repeatable:** указывает, что аннотация может быть использована повторно в том же месте

#### Аннотация [@Target](https://docs.oracle.com/en/java/javase/15/docs/api/java.base/java/lang/annotation/Target.html)  

```java
@Documented
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.ANNOTATION_TYPE)
public @interface Target
```
Обратите внимание, для определения мета-аннотации _@Target_ используется мета-аннотация _@Target_. 

_@Target_ определяет контекст, для которого она применима (актуально для Java 15):  
1. **ElementType.ANNOTATION_TYPE**: применяется для определения другой аннотации
2. **ElementType.CONSTRUCTOR**: применяется для определения конструктора
3. **ElementType.FIELD**: применяется для определения поля, включая константы Enum
4. **ElementType.LOCAL_VARIABLE**: применяется для определения локальной переменной
5. **ElementType.METHOD**: применяется для определения метода
6. **ElementType.MODULE**: применяется для определения модуля (с Java 9)
7. **ElementType.PACKAGE**: применяется для определения пакета
8. **ElementType.PARAMETER**: применяется для определения параметра
9. **ElementType.TYPE**: применяется для определения класса, интерфейса (включая аннотируемый тип), Enum или record.
10. **ElementType.TYPE_PARAMETER**: применяется для определения типа параметра (с Java 8)
11. **ElementType.TYPE_USE**: применяется для определения используемого типа (с Java 8)
12. **ElementType.RECORD_COMPONENT**: ассоциируется с records как компонент записи (с Java 14)

[_ElementType_](https://docs.oracle.com/en/java/javase/15/docs/api/java.base/java/lang/annotation/ElementType.html) представляет собой _[Enum](Enum)_, обеспечивая простую классификацию возможных мест для размещения аннотаций в коде. В свою очередь, они делятся на контексты объявления, где аннотации применяются к объявлениям, и на контексты типов, где аннотации применяются к типам, используемые в объявлениях и выражениях.  

Константы ANNOTATION_TYPE, CONSTRUCTOR, FIELD, LOCAL_VARIABLE, METHOD, PACKAGE, MODULE, PARAMETER, TYPE и TYPE_PARAMETER соответствуют контекстам объявления. TYPE_USE соответствует контекстам типа, а также двум контекстам объявления: объявлениям типов (включая объявления типов аннотаций) и объявлениям параметров типа.  

Например, аннотация, тип которой аннотирован с помощью _@Target (ElementType.FIELD)_, может быть записан только как модификатор для объявления поля. В тоже время аннотация, тип которой аннотирован с помощью _@Target (ElementType.TYPE_USE)_, может быть записана в типе поля, а также может выступать в качестве модификатора, например, для объявления класса.  

##### Рассмотрим несколько примеров.  

**Пример 1**: В этом примере @Target информирует о том, что определяемый аннотацией MetaAnnotationType тип сам по себе является мета-аннотацией и может быть использован только для аннотаций:  
```java
@Target(ElementType.ANNOTATION_TYPE)
public @interface MetaAnnotationType {
    ...
}
```
Ярким примером такого использования аннотации является определение самой аннотации @Target, показанное ранее.  
**Пример 2**: @Target информирует о том, что объявленный ею тип предназначен исключительно для использования в качестве типа элемента в объявлениях сложных типов аннотаций:  
```java
@Target({})
public @interface MemberType {
    ...
}
```
**Пример 3**: Когда константа ElementType появляется более одного раза в аннотации @Target, возникает ошибка времени компиляции (compile-time error):  
```java
@Target({ElementType.FIELD, ElementType.METHOD, ElementType.FIELD})
public @interface Bogus {
    ...
}
```
В последующем изложении материала вы будете встречать эту аннотацию постоянно, поэтому постарайтесь понять ее смысл как можно раньше.

#### Аннотации типов  

До Java 8 аннотации можно было размещать только перед объявлением метода, класса, конструктора и т. д. В Java 8 добавилось еще одно место для размещения аннотаций — рядом с типом. Такой вид аннотации часто называют аннотацией типа. Теперь мы можем аннотировать возвращаемый методом тип, [дженерики](Generics). Аннотации типов важны, поскольку улучшают систему типов Java и позволяют программным инструментам (например, IDE) автоматически выполнять дополнительные проверки типов во время компиляции.  

Аннотация типа должна включать _ElementType.TYPE_USE_ или/и _ElementType.TYPE_PARAM_ в качестве «target». Пример:  
```java
@Target({ElementType.TYPE_PARAMETER, ElementType.TYPE_USE})
@interface TypeAnnotation { ... }
```
_ElementType.TYPE_PARAMETER_ указывает, что аннотация _TypeAnnotation_ может быть записана в объявлении переменной типа.  

В то же время, _ElementType.TYPE_USE_ указывает, что аннотация может быть использована для любого типа (например, типов, появляющихся в объявлениях, дженериках и при преобразованиях типов).  

Аннотацию _@TypeAnnotation_ необходимо разместить перед аннотируемым типом:  
```java
void method() throws @TypeAnnotation NullPointerException {...}
```
Другие возможные варианты применения аннотации типов:  
```java
@NotNull String str = getValue(args);
@Encrypted String str;
@Format(theFormatterConstant) String str;
@Localized String str;
List<@ReadOnly T> list;
Store<@NotNull Product> product;
Store<@Prod(Type.Grocery) Product> product;
void showResources(@Authenticated User user);
@SwingElementOrientation int orientation;
@Positive int i;
@CreditCard string cardNumber;
Date date = (@Readonly Date) object;
Date date = (@NotNull Date) object;
```
В языке Java отсутствуют встроенные аннотации типов, но мы можем создать их самостоятельно, а также написать свой обработчик аннотаций и подключить его к компилятору для проверки аннотированного кода. При этом генерируя на основе созданных нами правил ошибки или предупреждения, если код им не соответствует.

#### Аннотация [@Retention](https://docs.oracle.com/en/java/javase/15/docs/api/java.base/java/lang/annotation/Retention.html)  

```java
@Documented
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.ANNOTATION_TYPE)
public @interface Retention
```
Аннотация _@Retention_ (с англ. означает удержание, задержка) определяет, до какого шага во время компиляции аннотация будет доступна. Все шаги (они еще называются политиками) находятся в [Enum](Enum):  
1. **RetentionPolicy.SOURCE**: аннотация сохраняется только в исходном файле и удаляется во время компиляции
2. **RetentionPolicy.CLASS**: аннотация сохраняется в файле .class во время компиляции, но недоступна во время выполнения через JVM
3. **RetentionPolicy.RUNTIME**: аннотация сохраняется в файле .class во время компиляции и доступна через JVM во время выполнения

В случае отсутствия аннотации _@Retention_ по умолчанию будет использована политика _RetentionPolicy.CLASS_.  

Рассмотрим пример.  Опишем аннотацию в _RetentionAnnotation.java_:  
```java
import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.TYPE)
public @interface RetentionAnnotation {}
```
Создадим файл AnnotatedClass.java, аннотированный двумя аннотациями:  
```java
@RetentionAnnotation
@Deprecated
public class AnnotatedClass {}
```
Создадим и запустим файл _Main.java_:  
```java
import java.lang.annotation.Annotation;

public class Main {
    public static void main(String[] args) {
        AnnotatedClass anAnnotatedClass = new AnnotatedClass();
    	  Annotation[] annotations = anAnnotatedClass.getClass().getAnnotations();

        System.out.println("Общее кол-во аннотаций времени исполнения (RunTime): " + annotations.length);
    	  System.out.println("1: " + annotations[0]);
    	  System.out.println("2: " + annotations[1]);
    }
}
```
Результат выполнения программы:
<p style="background-color: navy; color: yellow">
Общее кол-во аннотаций времени исполнения (RunTime): 2<br>
1: @RetentionAnnotation()<br>
2: @java.lang.Deprecated(forRemoval=false, since="")</p>
В этом примере мы создали свою собственную аннотацию _RetentionAnnotation_, а также использовали аннотацию _@Deprecated_, которая также имеет политику _RetentionPolicy.RUNTIME_.  

Если мы исправим политику аннотации _RetentionAnnotation_ с _RetentionPolicy.RUNTIME_ на _RetentionPolicy.SOURCE_ (и закомментируем строку в классе _Main_, выводящую второй элемент массива), то программа отобразит только одну аннотацию _deprecated_, поскольку аннотация с _RetentionPolicy.SOURCE_ во время компиляции будет удалена.

#### Аннотация [@Documented](https://docs.oracle.com/en/java/javase/15/docs/api/java.base/java/lang/annotation/Documented.html)  

```java
@Documented
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.ANNOTATION_TYPE)
public @interface Documented
```
По умолчанию аннотации не включаются в _[javadoc](javadoc)_. Аннотация, помеченная _@Documented_ информирует, что такая аннотация должна быть задокументирована с помощью инструмента _[javadoc](javadoc)_.  

Рассмотрим пример использования _@Documented_.  Создадим аннотацию _@TestDocumented,_ используя _@Documented_:  
```java
import java.lang.annotation.Documented;

@Documented
public @interface TestDocumented {
    String doTestDocument();
}
```
Создадим аннотацию _@TestNotDocumented,_ и не пометим её какой-либо аннотацией:  
```java
public @interface TestNotDocumented {
    String doTestNoDocument();
}
```
Теперь создадим класс _Tester_, пометив в нем два метода, созданными ранее аннотациями:  
```java
public class Tester {
    @TestDocumented(doTestDocument = "Hello DOC with annotation")
    public void doSomeTestDocumented() {
        System.out.println("Test for annotation with 'Documented'");
    }

    @TestNotDocumented(doTestNoDocument = "Hello DOC without annotation")
    public void doSomeTestNotDocumented() {
        System.out.println("Test for annotation without 'Documented'");
    }
}
```
Теперь, если вы запустите команду _javadoc_ (или используете _IntellijIdea_: _Tools -> Generate JavaDoc…_) и просмотрите сгенерированный файл _Tester.html_, то увидите следующее (представлена часть видимого экрана):
![[Tester.webp]]
Как видно на скриншоте, для метода _doSomeTestNotDocumented()_ отсутствует информация о типе аннотации, но эта информация предоставляется для метода _doSomeTestDocumented()_. Причина этому _@Documented_, прикрепленная к нашей аннотации _@TestDocumented_. _@TestNotDocumented_ не использует эту аннотацию.

#### Аннотация [@Inherited](https://docs.oracle.com/en/java/javase/15/docs/api/java.base/java/lang/annotation/Inherited.html)  

```java
@Documented
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.ANNOTATION_TYPE)
public @interface Inherited
```
В данном примере _@Inherited_ может использоваться только для аннотирования класса.  

По умолчанию аннотации, примененные к родительскому классу, не будут доступны в наследуемом классе. Если мы хотим, чтобы аннотации также наследовались, родительский класс необходимо пометить аннотацией _@Inherited_: в этом случае все аннотации родительского класса будут применимы к наследникам.  

Рассмотрим пример использования @Inherited.  Создадим наследуемую аннотацию _@InheritantAnnotation_:  
```java
import java.lang.annotation.Inherited;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;

@Retention(RetentionPolicy.RUNTIME)
@Inherited
public @interface InheritantAnnotation {}
```
Создадим не «наследуемую» аннотацию _@NonInheritantAnnotation_:  
```java
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;

@Retention(RetentionPolicy.RUNTIME)
public @interface NonInheritantAnnotation {}
```
Создадим родительский класс _Parent_, применив к нему две аннотации:  
```java
@InheritantAnnotation
@NonInheritantAnnotation
public class Parent {}
```
Создадим наследника Parent, класс _Child_:  
```java
public class Child extends Parent {}
```
Что мы получили сейчас: в классе _Parent_ применены две аннотации (одна из них наследуемая), а в классе _Child_ аннотации явно отсутствуют, но неявно присутствует унаследованная от родительского класса аннотация _@InheritantAnnotation_.  

Используем перечисленные выше классы в _Main_ и запустим его:  
```java
import java.lang.annotation.Annotation;

public class Main {
    public static void main(String[] args) {
        Parent parent = new Parent();
    	Child child = new Child();

    	if(parent.getClass().getAnnotations().length > 0) {
            System.out.println("Для класса 'Parent' применены следующие аннотации: ");
            for(Annotation annotationName: parent.getClass().getAnnotations()) {
                System.out.println(annotationName);
	        }
	    } else {
	        System.out.println("К классу 'Parent' не применены какие-либо аннотации.");
    	}

    	if(child.getClass().getAnnotations().length > 0) {
            System.out.println("\nДля класса 'Child' применены следующие аннотации: ");
        	for(Annotation annotationName: child.getClass().getAnnotations()) {
                System.out.println(annotationName);
	        }
	    } else {
	        System.out.println("\nК классу 'Child' не применены какие-либо аннотации.");
        }
    }
}
```
Результат выполнения программы:
<p style="background-color: navy; color: yellow">
Для класса 'Parent' применены следующие аннотации:<br>
@InheritantAnnotation<br>
@NonInheritantAnnotation<br>
<br>
Для класса 'Child' применены следующие аннотации: <br>
@InheritantAnnotation</p>
Как говорится, что и требовалось доказать. 

В коде класса _Main_ используется [рефлексия (Reflection)](ReflectionAPI), что может усложнить его понимание. Поскольку целью этой статьи является ознакомление вас с аннотациями, то механизм рефлексии в ней не рассматривается.

#### Аннотация [@Repeatable](https://docs.oracle.com/en/java/javase/15/docs/api/java.base/java/lang/annotation/Repeatable.html)  

```java
@Documented
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.ANNOTATION_TYPE)
public @interface Repeatable
```
Иногда возникают ситуации, когда необходимо повторно применить одну и ту же аннотацию к какому-то элементу (объявлению класса, интерфейсу, полю или к используемому типу).  

**До Java 8 применялось группирование аннотаций в единый контейнер аннотаций. Выглядело это следующим образом. ** 

Определим повторяемую аннотацию Game:  
```java
@interface Game {
    String name() default "Что-то под вопросом";
    String day();
}
```
Определим контейнер Games:  
```java
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;

@Retention(RetentionPolicy.RUNTIME)
@interface Games {
    Game[] value();
}
```
Использовалось это так:  
```java
@Games({
    @Game(name = "Крикет",  day = "воскресенье"),
    @Game(day = "четверг"),
    @Game(name = "Хоккей",   day = "понедельник")
})
public class Main {
    public static void main(String[] args) {
        Games games = Main.class.getAnnotation(Games.class);

        for (Game game : games.value()) {
            System.out.println(game.name() + " в " + game.day());
        }
    }
}
```
Обратите внимание, повторяющиеся аннотации разделяются запятой.

Результат выполнения программы:
<p style="background-color: navy; color: yellow">
Крикет d воскресенье<br>
Что-то под вопросом в четверг<br>
Хоккей в понедельник</p>

**С появлением Java 8 и @Repeatable все стало немного проще. **

В поле _value_ такой аннотации необходимо указать контейнер для повторяющейся аннотации. Контейнер также представляет собой аннотацию, в которой поле _value_ является массивом типа повторяющейся аннотации.  

Таким образом, мы должны создать контейнерную аннотацию, а затем указать её тип в качестве аргумента.  

В нашем случае, перед определением аннотации _@Game_ необходимо добавить новую аннотацию _@Repeatable_:  
```java
import java.lang.annotation.Repeatable;

@Repeatable(Games.class)
@interface Game {
    String name() default "Что-то под вопросом";
    String day();
}
```
Теперь перед определением класса _Main_ можно применить несколько раз аннотацию _@Game_:  
```java
@Game(name = "Крикет",  day = "воскресенье")
@Game(day = "четверг")
@Game(name = "Хоккей",   day = "понедельник")
public class Main {
    public static void main(String[] args) {
        Games games = Main.class.getAnnotation(Games.class);

    	  for (Game game : games.value()) {
            System.out.println(game.name() + " в " + game.day());
    	  }
    }
}
```
Результат выполнения программы тот же.

Мы также можем вместо _getAnnotation (Games.class)_ использовать _getAnnotationsByType (Game.class)_ или _getDeclaredAnnotationsByТуре (Game.class)_:  
```java
@Game(name = "Крикет",  day = "воскресенье")
@Game(day = "вторник")
@Game(name = "Хоккей",   day = "пятница")
public class Main {
    public static void main(String[] args) {
        Game[] arrayGames = Main.class.getAnnotationsByType(Game.class);
    	  for(Game game : arrayGames) {
            System.out.println(game.name() + " в " + game.day());
    	  }
    }
}
```
Результат будет тем же.

### Аннотации для кода  

Их пять:  
- **@Override**: указывает, что метод переопределяет, объявленный в суперклассе или интерфейсе метод
- **@Deprecated**: помечает код, как устаревший
- **@SuppressWarnings**: отключает для аннотированного элемента предупреждения компилятора. Обратите внимание, что если необходимо отключить несколько категорий предупреждений, их следует добавить в фигурные скобки, например @SuppressWarnings ({"unchecked", "cast"}).
- **@SafeVarargs**: отключает предупреждения для всех методов или конструкторов, принимающих в качестве параметра varargs
- **@FunctionalInterface**: помечает интерфейсы, имеющие только один абстрактный метод (при этом они могут содержать любое количество методов по умолчанию или статических)

Рассмотрим перечисленные аннотации более детально.

#### Аннотация [@Override](https://docs.oracle.com/en/java/javase/15/docs/api/java.base/java/lang/Override.html)  

```java
@Target(ElementType.METHOD)
@Retention(RetentionPolicy.SOURCE)
public @interface Override
```
Аннотация _@Override_ относится к маркерным аннотациям и указывает, что метод переопределяет/реализует унаследованный метод. Эта информация не является строго необходимой, но помогает уменьшить количество ошибок, поскольку при такой аннотации компилятор должен генерировать сообщение об ошибке, если не выполняется одно из двух следующих условий:
— Метод переопределяет или реализует метод, объявленный в супертипе  
— У метода есть сигнатура (название метода + список параметров), эквивалентная переопределяемой сигнатуре метода, объявленного в родительском классе/интерфейсе.  

Продемонстрируем применение аннотации. Создадим класс _Parent_ с методом _display()_, класс _Child, который_ является его наследником, и класс _Main, который_ создает экземпляр _Child_ и запускает метод _display()_:
```java
public class Parent {
    public void display() {
        System.out.println("Выполнился метод из родительского класса");
    }
}
```
```java
public class Child extends Parent {
    public void display() {
        System.out.println("Выполнился метод из класса-наследника");
    }
}
```
```java
public class Main {
    public static void main(String args[]) {
        Child instance = new Child();
    	  instance.display();
    }
}
```
Результат выполнения программы:
<p style="background-color: navy; color: yellow">
Выполнился метод из класса-наследника</p>
Давайте умышленно добавим ошибку в названии метода в классе _Child_:  
```java
public class Child extends Parent {
    public void dispay() {
        System.out.println("Выполнился метод из класса-наследника");
    }
}
```
Результат выполнения программы:
<p style="background-color: navy; color: yellow">
Выполнился метод из родительского класса</p>
В итоге в классе _Child_ мы имеем два метода: унаследованный метод суперкласса _display()_ и новый метод _dispay()_. В классе _Main_ у нас вызывается именно родительский метод, поскольку другого метода _display()_ в классе _Child_ нет.  

Перед определением метода в класс Child добавим аннотацию _@Override_:  
```java
public class Child extends Parent {    
    @Override
    public void dispay() {
        System.out.println("Выполнился метод из класса-наследника");
    }
}
```
В такой ситуации IDE подчеркнет красным аннотацию, информируя, что «_Method does not override method from its superclass_» (метод не переопределяет метод его суперкласса).

При запуске получим ошибку компиляции:
<font color="red">java: Method does not override or implement a method from its superclass</font>

Теперь уже компилятор сообщает нам, что «_метод не переопределяет или не реализует метод его суперкласса_»  

Исправим «опечатку» в названии метода в классе _Child_ и запустим программу:  
```java
public class Child extends Parent {
    @Override
    public void display() {
        System.out.println("Выполнился метод из класса-наследника");
    }
}
```
Результат выполнения программы:
<p style="background-color: navy; color: yellow">
Выполнился метод из класса-наследника</p>
Таким образом, применяя аннотацию _@Override_, мы даем задание компилятору выполнять проверку соответствия сигнатуры метода класса наследника классу родителя, что устраняет ошибки «по невнимательности» в виде опечаток.

#### Аннотация [@Deprecated](https://docs.oracle.com/en/java/javase/15/docs/api/java.base/java/lang/Deprecated.html)  

```java
@Documented
@Retention(RetentionPolicy.RUNTIME)
@Target(value={CONSTRUCTOR, FIELD, LOCAL_VARIABLE, METHOD, PACKAGE, MODULE, PARAMETER, TYPE})
public @interface Deprecated
```

Определяющие аннотацию аннотации мы рассмотрели ранее, тут для вас не должно быть трудностей. Приведем примеры использования.  

В код предыдущего примера добавим в класс _Child_ аннотацию _@Deprecated_:  
```java
public class Child extends Parent {
    @Override
    @Deprecated(since = "1.2", forRemoval = true)
    public void display() {
        System.out.println("Выполнился метод из класса-наследника");
    }
}
```
Результат выполнения программы:
<p style="background-color: navy; color: yellow">
Выполнился метод из класса-наследника</p>
Результат остался тем же, ошибок нет. Но, обратите внимание на класс Main, используемый метод display() в IntellijIdea перечеркнут (!). Подобные визуальные оповещения есть и в других IDE.  
```java
public class Main {
    public static void main(String args[]) {
        Child instance = new Child();
    	  instance.display();  
    }
}
```

#### Аннотация @[SuppressWarnings](https://docs.oracle.com/en/java/javase/15/docs/api/java.base/java/lang/SuppressWarnings.html)  

```java
@Target({TYPE, FIELD, METHOD, PARAMETER, CONSTRUCTOR, LOCAL_VARIABLE, MODULE})
@Retention(RetentionPolicy.SOURCE)
public @interface SuppressWarnings
```
Предупреждающие сообщения компилятора обычно полезны, но иногда, они могут «зашумлять» полезную информацию. Особенно, когда мы не можем или не хотим их устранять. В таких случаях можно воспользоваться аннотацией _@SuppressWarnings,_ отключив такие предупреждения, чтобы они не отображались.  

Рассматривая код для аннотации _@Override_, мы вызывали в классе _Main_ метод _display()_ из класса _Child_. В тоже время метод _display()_ из класса _Parent_ не использовался. Среда IDE предполагала, что здесь где-то может быть ошибка (создали лишний метод или ошибочно используем не тот метод и т. д.) и соответственно, подсвечивая, выделяла цветом название неиспользуемого метода _display()_ (и при наведении курсора выдавала сообщение: «_Method 'Display()' is never used_»).  

Чтобы этого небыло, такое предупреждение можно отключить аннотацией _@SuppressWarnings («unused»)_, установив её перед методом _display()_:  
```java
public class Parent {
    @SuppressWarnings("unused")
    public void display() {
        System.out.println("Выполнился метод из родительского класса");
    }
}
```
Еще одним предупреждением компилятора является предупреждение о применении устаревшего метода, помеченного в коде аннотацией _@Deprecated_. Чтобы его устранить, необходимо пометить вызов метода _main()_ в классе _Main_ аннотацией _@SuppressWarnings («deprecation»)_:  
```java
public class Main {
    @SuppressWarnings("deprecation")
    public static void main(String[] args) {
        Child instance = new Child();
    	  instance.display();
    }
}
```
Сам код теперь стал проще для чтения, а название метода _display()_ не перечеркивается.  

Чтобы отключить список из нескольких предупреждений, необходимо через запятую перечислить список предупреждений.  

Например, в следующем виде:  
```java
@SuppressWarnings({"unused", "deprecation"})
```

#### Аннотация [@SafeVarargs](https://docs.oracle.com/en/java/javase/15/docs/api/java.base/java/lang/SafeVarargs.html)  

```java
@Documented
@Retention(RetentionPolicy.RUNTIME)
@Target({ElementType.CONSTRUCTOR, ElementType.METHOD})
public @interface SafeVarargs
```
Эта аннотация, представленная в java 7, гарантирует, что тело аннотированного метода или конструктора не выполняет потенциально небезопасные операции с параметром [varargs](Varargs). Аннотация _@SafeVarargs_ похожа на _@SupressWarnings_ тем, что позволяет нам объявить, что конкретное предупреждение компилятора является ложным срабатыванием. Добавлять эту аннотацию мы можем только убедившись в том, что наши действия безопасны.

#### Аннотация [@FunctionalInterface](https://docs.oracle.com/en/java/javase/15/docs/api/java.base/java/lang/FunctionalInterface.html)  

```java
@Documented
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.TYPE)
public @interface FunctionalInterface
```
Как и аннотация _@Override_, аннотация _@FunctionalInterface_ защищает код от возможных ошибок программиста. Несмотря на то, что любой интерфейс может содержать бесконечное множество абстрактных методов, [функциональный интерфейс](Functional-Interface) может содержать исключительно один абстрактный метод, иначе он не сможет использоваться в [лямбда-выражении.](Lambda)  

В тоже время, абстрактные методы, переопределяющие один из публичных методов класса _[Object](Object),_ не учитываются.  

Рассмотрим простейший пример: напишем [функциональный интерфейс](Functional-Interface), реализующий что-то абстрактное и важное.  
```java
@FunctionalInterface
public interface MyFunctionalInterface {
    abstract public void abstractMethod();
    //abstract public void anotherAbstractMethod();
}
```
```java
public class Main implements MyFunctionalInterface {

    public static void main(String[] args) {
        Main main = new Main();
    	main.abstractMethod();
    }

    @Override
    public void abstractMethod() {
        System.out.println("Это сообщение из abstractMethod()");
    }
}
```
Если мы добавим еще один абстрактный метод (_anotherAbstractMethod()_, в коде он закомментирован), компилятор сообщит про ошибку:
<font color="red">java: Unexpected @FunctionalInterface annotation<br>
  MyFunctionalInterface is not a functional interface<br>
    multiple non-overriding abstract methods found in interface MyFunctionalInterface</font>

Создадим еще один функциональный интерфейс и расширим им интерфейс, созданный нами ранее:  
```java
package functional;

@FunctionalInterface
public interface AnotherFunctionalInterface extends MyFunctionalInterface {
    abstract public void anotherAbstractMethod();
}
```
Вроде все хорошо, у нас один абстрактный метод, но IDE снова подсказывает о наличии той же самой ошибки.

Ошибка вызвана тем, что мы, расширяя интерфейс _MyFunctionalInterface,_ наследуем абстрактный метод расширяемого интерфейса, и как результат, имеем два абстрактных метода, что не совместимо с аннотацией _@FunctionalInterface_.  

Таким образом, мы не сможем использовать интерфейс, помеченный аннотацией _@FunctionalInterface_ и включающей в себя явно или неявно два и более абстрактных метода.

#### Аннотация [@Native](https://docs.oracle.com/en/java/javase/15/docs/api/java.base/java/lang/annotation/Native.html)  

```java
@Documented
@Target(ElementType.FIELD)
@Retention(RetentionPolicy.SOURCE)
public @interface Native
```
Начиная с Java 8, в пакете _java.lang.annotation_ появилась новая аннотация под названием _@Native_, применимая только к полям. Она указывает, что аннотированное поле является константой, на которую можно ссылаться с нативного кода. Например, вот как она используется в классе Integer:  
```java
public final class Integer {
    @Native public static final int MIN_VALUE = 0x80000000;
    // последующий код опущен
}
```
Эта аннотация также может служить подсказкой для программных инструментов, генерирующих некоторые вспомогательные файлы.

### Обработка аннотаций

#### Обработка аннотаций во время выполнения: [рефлексия](ReflectionAPI)  

_[Рефлексия](ReflectionAPI)_, как способность получать информацию о коде во время его выполнения, появилась в Java с момента появления языка.  

Например:  
```java
var session = request.getHttpSession();
var object = session.getAttribute("object"); (1)
var clazz = object.getClass();               (2)
var methods = clazz.getMethods();            (3)

for (var method : methods) {
    if (method.getParameterCount() == 0) {   (4)
        method.invoke(foo);                  (5)
    }
}
```
(1) Получаем объект, хранящийся в сеансе  
(2) Получаем класс среды выполнения (runtime class) объекта  
(3) Получаем все общедоступные методы, имеющиеся у объекта  
(4) Если у метода нет параметра, то  
(5) Вызываем этот метод

С появлением аннотаций рефлексия получила соответствующие улучшения:
![[java-reflection-api.svg]]
Фреймворки начали использовать аннотации для различных сценариев использования. Среди них сценарий конфигурирования был одним из наиболее часто используемых: например, вместо (или, точнее, в дополнение к) XML, Spring добавил возможность конфигурирования на основе аннотаций.

#### Обработка аннотаций во время компиляции: обработчики аннотаций  

Долгое время и получатели данных, и поставщики данных были довольны доступом через рефлексию к аннотациям во время выполнения. Поскольку основное внимание уделяется сценариям конфигурирования, рефлексия происходит во время запуска приложения. В ограниченном по производительности окружении это слишком большая нагрузка для приложений: наиболее известным примером такого окружения является платформа Android. Здесь хотелось бы иметь самое быстрое время запуска, но рефлексия замедляет его.  

Альтернативным решением этой проблемы является **обработка аннотаций во время их компиляции**. Для этого компилятор должен быть настроен на использование специальных **обработчиков аннотаций**. У них могут быть разные выходные данные: простые файлы, сгенерированный код и т. д. Компромисс этого подхода заключается в том, что компиляция приложения каждый раз снижает производительность, но при этом не влияет на время запуска.  

Одним из первых фреймворков, в которых использовался этот подход для генерации кода, был Dagger: это DI-фреймворк (Dependency Injection) для Android. Работа фреймворка базируется не на времени выполнения (runtime-based), а на времени компиляции (compile-time). Долгое время генерация кода во время компиляции использовалась только в экосистеме Android.  

Однако, в последнее время такой подход приняли и такие серверные фреймворки, как _Quarkus_ и _Micronaut_. Цель состоит в том, чтобы сократить время запуска приложения за счет генерации кода во время компиляции вместо самоанализа во время выполнения. Кроме того, предварительная компиляция полученного байт-кода в собственный код дополнительно сокращает время запуска, а также потребление памяти.  

Мир обработчиков аннотаций огромен: этот раздел представляет собой очень небольшое введение, поэтому при желании можно продолжить их изучение.  

Обработчик аннотаций — это просто определенный класс, который необходимо зарегистрировать во время компиляции. Зарегистрировать их можно несколькими способами. С Maven это просто вопрос настройки плагина компилятора:  

pom.xml  
```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.8.1</version>
            <configuration>
                <annotationProcessors>
                    <annotationProcessor>ch.frankel.blog.SampleProcessor</annotationProcessor>
                </annotationProcessors>
            </configuration>
        </plugin>
    </plugins>
</build>
```
Сам обработчик должен реализовывать _Processor_, но абстрактный класс _AbstractProcessor_ самостоятельно реализует большую часть своих методов, кроме метода _process()_: на практике достаточно наследоваться от _AbstractProcessor_. Очень упрощенная схема API выглядит так:
![[java-annotation-proc.svg]]
Давайте создадим очень простой обработчик. Он должен перечислять только классы, помеченные конкретными аннотациями. Настоящие процессоры аннотаций, скорее всего, сделают что-нибудь полезное, например сгенерируют код, но эта дополнительная логика выходит далеко за рамки этого поста.  
```java
@SupportedAnnotationTypes("ch.frankel.blog.*")                                          (1)
@SupportedSourceVersion(SourceVersion.RELEASE_8)
public class SampleProcessor extends AbstractProcessor {

    @Override
    public boolean process(Set<? extends TypeElement> annotations,                      (2)
    RoundEnvironment env) {
        annotations.forEach(annotation -> {                                             (3)
            Set<? extends Element> elements = env.getElementsAnnotatedWith(annotation); (4)
            elements.stream()
                    .filter(TypeElement.class::isInstance)                              (5)
                    .map(TypeElement.class::cast)                                       (6)
                    .map(TypeElement::getQualifiedName)                                 (7)
                    .map(name -> "Class " + name + " is annotated with " +         annotation.getQualifiedName())
                    .forEach(System.out::println);
        });
    return true;
    }
}
```
(1) Обработчик будет вызываться для каждой аннотации, принадлежащей пакету ch.frankel.blog  
(2) process(): основной метод, подлежащий переопределению  
(3) Цикл вызывается для каждой аннотации  
(4) Аннотация не так интересна, как аннотированный ею элемент. Это способ получить аннотированный элемент  
(5) В зависимости от того, какой элемент аннотирован, его необходимо привести к правильному дочернему интерфейсу Element. Здесь могут быть аннотированы только классы, поэтому, переменная должна быть протестирована, чтобы проверить, имеет ли назначаемый TypeElement доступ к своим дополнительным атрибутам далее по цепочке операций  
(6) Нам нужно полное имя класса, для которого установлена аннотация, поэтому необходимо привести его к типу, который делает этот конкретный атрибут доступным  
(7) получаем полное имя от TypeElement

### Заключение  

Аннотации очень эффективны и не важно, используются ли они во время выполнения или во время компиляции. С другой стороны, самая большая проблема заключается в том, что они работают как будто по волшебству: нет простого способа узнать, какой класс, использующий рефлексию, или обработчик аннотаций их использует. Каждый в своем контексте должен решать, перевешивают ли плюсы аннотаций их минусы. Использование аннотаций без каких-либо предположений о будущем программы оказывает большую медвежью услугу такому коду… так же, как и отказ от них из-за неуместной идеологии.
