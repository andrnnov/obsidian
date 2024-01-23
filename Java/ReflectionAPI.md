#Java #ReflectionAPI

### Java Reflection API ###

2024-01-16 12:04

<font color="lightgreen">Рефлексия в Java</font> — это механизм, с помощью которого можно вносить изменения и получать информацию о классах, интерфейсах, полях и методах во время выполнения, при этом не зная имен этих классов, методов и полей. Кроме того, Reflection API дает возможность создавать новые экземпляры классов, вызывать методы, а также получать или устанавливать значения полей.

>Начинающие Java-программисты часто путают рефлексию с интроспекцией. Интроспекция — проверка кода и возможность видеть типы объектов во время выполнения. Рефлексия дает возможность вносить изменения во время выполнения программы путем использования интроспекции. Здесь важно понимать различие, поскольку некоторые языки поддерживают интроспекцию, но не поддерживают рефлексию, например, C++.

Рефлексия — мощная концепцией, которая лежит в основе большинства современных Java/Java EE [фреймворков](http://javadevblog.com/kak-sozdat-frejmvork-na-java-za-5-minut.html) и [библиотек](http://javadevblog.com/v-chem-raznitsa-mezhdu-frejmvorkom-i-bibliotekoj.html). Например, для Java классическими примерами являются:

- **JUnit** – фреймворк для модульного тестирования. Он использует рефлексию для парсинга аннотаций (например, `@Test`) для получения описанных программистом тестовых методов и дальнейшего их выполнения.
- **Spring** – фреймворк для разработки приложений на Java платформе, в основе которого лежит внедрение зависимостей (инверсия управления).

#### Ограничения при работе с рефлексией в Java ####

Почему мы не должны использовать рефлексию в обычном программировании, когда уже есть доступ к интерфейсам и классам. Причин несколько:
1. **Низкая производительность** — поскольку рефлексия в Java определяет типы динамически, то она сканирует classpath, чтобы найти класс для загрузки, в результате чего снижается программы.
2. **Ограничения системы безопасности** — рефлексия требует разрешения времени выполнения, которые не могут быть доступны для систем, работающих под управлением менеджера безопасности (Java Security Manager).
3. **Нарушения безопасности** **приложения** — с помощью рефлексии мы можем получить доступ к части кода, к которой мы не должны получать доступ. Например, мы можем получить доступ к закрытым полям класса и менять их значения. Это может быть серьезной угрозой безопасности.
4. **Сложность в поддержке** — код, написанный с помощью рефлексии трудно читать и отлаживать, что делает его менее гибким и трудно поддерживаемым.

#### Java Reflection: Работа с классами ####

Объект [`java.lang.Class`](Class) является точкой входа для всех операций рефлексии. Для каждого типа объекта, [JVM](http://javadevblog.com/chto-takoe-jdk-jre-i-jvm-v-java.html) создает неизменяемый экземпляр `java.lang.Class` который предоставляет методы для получения свойств объекта, создания новых объектов, вызова методов.

Все типы в Java, включая примитивные типы и массивы имеют связанный с ними `java.lang.Class` объект. Если мы знаем название класса во время компиляции, то сможем получить объект следующим образом:
```java
Class mClassObject = SomeObject.class
```
Если мы не знаем имя **во время компиляции**, но знаем имя класса **во время выполнения**, то можно сделать так:
```java
Class mClassObject = Class.forName("здесь имя класса")
```
При использовании метода `Class.forName()` мы должны указать полное имя класса. То есть имя класса, включая все имена пакетов. Например, если `SomeObject` находится в пакете `com.javadevblog.app`, то полным именем вашего класса является строка: `com.javadevblog.app.SomeObject`.

Метод `Class.forName()` может бросить исключение `ClassNotFoundException` если класс не будет найден в `classpath` во время выполнения.

#### Получаем название класса

С помощью объекта `Class` мы можем получить имя класса двумя способами.
- Методом `getName()`, который вернет полное имя класса с пакетом
```java
String fullClassName = mClassObject.getName();
```
- И с помощью метода `getSimpleName()`, который вернет только название класса без имени пакета:
```java
String justClassName = mClassObject.getSimpleName();
```

#### Работа с модификаторами доступа ####

Мы можем получить доступ к модификаторам доступа с помощью [Class](Class) объекта. Модификаторы представляют собой ключевые слова public, static, private и т.д. Мы можем получить модификаторы с помощью метода getModifiers():
```java
Class mClassObject = SomeObject.class
int classModifiers = mClassObject.getModifiers();
```
Результат выполнения находится в переменной int, где каждый модификатор — это битовый флаг, который может быть установлен или сброшен. Мы можем проверить модификаторы, используя следующие методы в классе java.lang.reflect.Modifier:
- Modifier.isAbstract(int modifiers)
- Modifier.isFinal(int modifiers)
- Modifier.isInterface(int modifiers)
- Modifier.isNative(int modifiers)
- Modifier.isPrivate(int modifiers)
- Modifier.isProtected(int modifiers)
- Modifier.isPublic(int modifiers)
- Modifier.isStatic(int modifiers)
- Modifier.isStrict(int modifiers)
- Modifier.isSynchronized(int modifiers)
- Modifier.isTransient(int modifiers)
- Modifier.isVolatile(int modifiers)
В параметры метода просто передадим modifiers и каждый из этих методов вернет true или false.

##### Получение информации о пакете #####

Зная только класс мы можем получить информацию о пакете:
```java
Class mClassObject = SomeObject.class
Package package = mClassObject.getPackage();
```
Мы также можем получить доступ к информации, указанной для данного пакета в Manifest файле внутри JAR файла. 

##### Реализованные интерфейсы #####

Список интерфейсов, реализуемых данным классом можно получить так:
```java
Class mClassObject = SomeObject.class
Class[] interfaces = mClassObject.getInterfaces();
```
Класс может реализовать много интерфейсов. Поэтому возвращается массив объектов Class. В Java Reflection API интерфейсы также представлены объектами Class.

>**Обратите внимание:** Метод вернул только интерфейсы, которые реализует указанный класс, а не его суперкласс. Для того чтобы получить полный список интерфейсов, реализованных в этом классе, вы должны обратиться как к текущему классу, так и к его суперклассу.

#### Рефлексия в Java: Конструкторы ####

С помощью Java Reflection API можно получать информацию про конструкторы классов и создавать объекты во время выполнения. Это делается с помощью класса Java java.lang.reflect.Constructor.

##### Получаем конструкторы класса #####

```java
Class mClassObject = SomeObject.class
Constructor[] constructors = mClassObject.getConstructors();
```
В коде выше мы получили массив конструкторов класса и теперь можем работать с ними. 

Если известны параметры конкретного конструктора, то массив можно не получать, а работать уже с известным. Например, следующий конструктор класса принимает String в качестве параметра:
```java
Class mClassObject = SomeObject.class
Constructor constructor = mClassObject.getConstructor(new Class[]{String.class});
```
Если мы ошиблись с аргументом конструктора, то будет выброшено исключение NoSuchMethodException.

##### Получаем параметры конструктора #####

На примерах выше мы получили массив конструкторов. Теперь мы можем узнать параметры для каждого из них. Например, получить типы параметров какого-то конструктора можно так:
```java
Class[] parameterTypes = constructor.getParameterTypes();
```

##### Создание объектов с помощью конструкторов #####

Теперь получив конструкторы класса и зная их переметры, мы можем создать новый экземпляр указанного класса:
```java
// получаем конструктор, который принимает String в качестве параметра
Constructor constructor = SomeObject.class.getConstructor(String.class);

SomeObject myObject = (SomeObject)
        constructor.newInstance("здесь какой-то строковый аргумент");
```
Создание нового экземпляра класса произошло после вызова метода newInstance()на конструкторе класса.

#### Рефлексия в Java: Поля ####

Используя рефлексию мы можем работать с полями — переменными-членами класса. В этом нам помогает Java класс java.lang.reflect.Field. С помощью него в рантайме мы можем устанавливать значения и получать данные с полей.

##### Получаем поля класса #####

Получить поля класса с помощью рефлексии можно с помощью следующей строчки кода:
```java
Class mClassObject = SomeObject.class
Field[] fields = mClassObject.getFields();
```
Каждый элемент массива содержит экземпляр public поля, объявленного в классе.
Если вы знаете имя поля, к которому вы хотите получить доступ, достаточно вызвать следующую строчку:
```java
Class mClassObject = SomeObject.class
Field field = mClassObject.getField("fieldName");

```
Строчка выше вернет значение поля под именем fieldName с типом Field нашего класса SomeObject:
```java
public class SomeObject {
	public String fieldName = null;
}
```
Если мы укажем неверное имя поля, то получим NoSuchFieldException.

##### Получаем название поля #####

```java
Field field = mClassObject.getField("fieldName");
String fieldName = field.getName();
```

##### Получаем тип поля #####

```java
Field field = mClassObject.getField("fieldName");
Object fieldType = field.getType();
```

##### Получаем и устанавливаем значения полей #####

```java
Class mClassObject = SomeObject.class
Field field = mClassObject.getField("fieldName");
SomeObject instance = new SomeObject();

Object value = field.get(instance);

field.set(instance, value);
```
Параметр instance, который передается в методы для получения и установки значения поля, должен быть экземпляром класса, которому принадлежит само поле. В приведенном выше примере используется экземпляр класса SomeObject, потому что поле fieldName является членом экземпляра этого класса.

#### Java Reflection API: Методы ####

Используя ревфлексию в Java мы можем получать информацию о методах и вызывать их в рантайме. Для этого используется класс java.lang.reflect.Method:
```java
Class mClassObject = SomeObject.class
Method[] methods = mClassObject.getMethods();
```
В коде выше мы получили все методы класса.
Нам не нужно получать массив со всеми методами, если нам известны точные типы параметров метода, который мы хотим использовать. Например, у нас есть метод под названием «sayHello«, который принимает String в качестве параметра. Получить объект Method для него можно так:
```java
Class mClassObject = SomeObject.class
Method method = mClassObject.getMethod("sayHello", new Class[]{String.class});
```
Если такого метода нет, то будет выброшен NoSuchMethodException.

Если метод sayHello() без параметров, то нужно передать null в методе getMethod():
```java
Method method = mClassObject.getMethod("sayHello", null);
```

#### Параметры метода и типы возвращаемых значений ####

Получить параметры метода можно так:
```java
Class[] parameterTypes = method.getParameterTypes();
```
В строчке ниже мы можем получить тип возвращаемого значения:
```java
Class returnType = method.getReturnType();
```

##### Вызов метода с помощью Java рефлексии #####

```java
Class mClassObject = SomeObject.class
Method method = mClassObject.getDeclaredMethod("sayHello", parameterTypes);
method.invoke(objectToInvokeOn, params);
```
В коде выше мы получили метод указанного класса и вызвали для него метод invoke().
objectToInvokeOn имеет тип [Object](Object) и является объектом, для которого мы хотим вызвать метод sayHello(). Где parameterTypes — имеет тип Class[] и представляет собой параметры, которые метод принимает на вход, params имеет тип Object[] и представляет собой параметры переданные методу.

Следует отметить: если мы знаем, что метод sayHello — статический, то вызов метода с помощью рефлексии можно переписать так:
```java
method.invoke(null, params);
```
То есть вместо объекта вызова objectToInvokeOn указать null.

#### Java Reflection API: Методы установки и получения значения ####

Кроме обычных методов класса мы также можем работать с методам get и set с помощью рефлексии. Получить эти методы можно несколькими способами: явно указать геттер или сеттер при работе или обойти все доступные в классе методы и проверить их на то являются ли они методами get или set:
Чтобы определить геттер или сеттер нам нужно определить некоторые правила:
-  Геттер — метод, имя которого начинается на ‘get’. Он не принимает аргументы и обязательно возвращает какое-то значение.
- Сеттер — метод, имя которого начинается на ‘set’. Он принимает 1 параметр.

Обычно сеттеры не возвращают значение, однако при опеределении метода к сеттеру возвращаемый параметр не учитывается.
Смотрим на примере определения метода как сеттера или геттера с помощью рефлексии в Java:
```java
public static void printGettersOrSetters(Class aClass){
  Method[] methods = aClass.getMethods();

  for(Method method : methods){
    if(isGetter(method)) System.out.println("getter: " + method);
    if(isSetter(method)) System.out.println("setter: " + method);
  }
}

public static boolean isGetter(Method method){
  if (!method.getName().startsWith("get")) {
       return false;
  }
  if (method.getParameterTypes().length != 0) {
       return false;  
  }
  if (void.class.equals(method.getReturnType()) {
       return false;
  }
  return true;
}

public static boolean isSetter(Method method){
  if (!method.getName().startsWith("set")) {
       return false;
  }
  if (method.getParameterTypes().length != 1) {
       return false;
  }
  return true;
}
```

#### Java Reflection API: Приватные поля и методы ####

С помощью рефлексии в Java можно получить доступ к private полям других классов. Это очень удобно, например, для модульного тестирования.

Обратите внимание, что получение приватных полей корректно работает только в standalone Java приложениях. Если вы попытаетесь обратиться к приватным полям внутри Java-апплета, то нужно будет возиться с Java SecurityManager.

##### Доступ к private полям с помощью рефлексии #####

Чтобы получить доступ к закрытому полю нужно будет использовать метод Class.getDeclaredField(String name) или Class.getDeclaredFields() метод. Методы Class.getField(String name) и Class.getFields() возвращают только public поля, поэтому в нашем случае они работать не будут.

Давайте на примере посмотрим работу с private полям с помощью Java Reflection:
```java
public class PrivateClass {
  private String mPrivateString = null;

  public PrivateClass(String privateString) {
    this.mPrivateString = privateString;
  }
}
```
 У нас есть класс PrivateClass с закрытым полем mPrivateString. Теперь напишем код, с помощью которого мы будем получить к нему доступ:
```java
PrivateClass privateObject = new PrivateClass("Значение приватного поля");

Field privateStringField = PrivateClass.class.getDeclaredField("mPrivateString");
privateStringField.setAccessible(true);
String fieldValue = (String) privateStringField.get(privateObject);
System.out.println("значение приватного поля = " + fieldValue);
```
 В коде выше мы использовали метод getDeclaredField, который имеет доступ лишь к полям, объявленным в конкретном классе и не имеет доступ к полям суперкласса.
 
Обратите внимание, что в коде выше мы использовали Field.setAcessible(true), который отключает проверку доступа для указанного поля. Теперь мы можем работать с ним с помощью рефлексии, даже если у него был private, protected или default доступ. Без использования рефлексии этот метод все также приватный и компилятор не позволит нам обратиться к нему.

##### Доступ к приватным методам с помощью рефлексии #####

Уже известные нам методы работы с методами Class.getMethod(String name, Class[] parameterTypes) и Class.getMethods() здесь не помогут, так как они имеют доступ лишь к public методам.

Доступ к закрытым методам осуществляется с помощью методов Class.getDeclaredMethod(String name, Class[] parameterTypes) или Class.getDeclaredMethods().

Теперь давайте рассмотрим способ получения private метода в Java с помощью рефлексии. Давайте добавим закрытый метод getPrivateString() в созданный выше класс PrivateClass:
```java
private String getPrivateString() {
    return this.mPrivateString;
}
```
Теперь напишем код, который используя рефлексию получит доступ к этому private методу:
```java
PrivateClass privateObject = new PrivateClass("Какое-то значение");

Method privateStringMethod = PrivateClass.class.
						getDeclaredMethod("getPrivateString", null);

privateStringMethod.setAccessible(true);

String returnValue = (String)privateStringMethod.invoke(privateObject, null);
System.out.println("значение, которое возвращает private метод = " + returnValue);
```
 Также как и приватными полями, мы можем получить доступ к приватным методам только текущего класса (без доступа к private методам суперкласса).
 
С помощью Method.setAcessible(true) снимаем проверку доступа только для рефлексии.

#### Java Reflection: Аннотации ####

С помощью Java рефлексии мы можем обрабатывать аннотации в рантайме.
Аннотации также могут быть обработаны с помощью рефлексии. Для полноты руководства по Java Reflection давайте создадим простую аннотацию и затем научимся обрабатывать ее с помощью рефлексии:
```java
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.TYPE)
public @interface Reflectable {
    public String name();
    public String value();
}
```
С помощью @ мы указываем, что описываем аннотацию.
Также мы использовали две аннотации, которые применяются только к аннотациям при создании:
- @Retention(RetentionPolicy.RUNTIME) и @Target(ElementType.TYPE)указывают как будет использоваться пользовательская аннотация.
- @Retention(RetentionPolicy.RUNTIME) указала на то, что аннотация будет использована в рантайме, следовательно, мы сможем получить к ней доступ с помощью рефлексии.
- @Target(ElementType.TYPE) указывает на то, что мы можем использовать аннотацию на интерфейсах и классах.

 Теперь давайте «повесим» нашу аннотацию на какой-то класс:
```java
@Reflectable(name="reflectable",  value = "какие-то метаданные")
public class SimpleClass {
}
```
 С помощью рефлексии мы можем работать с аннотациями класса, метода или поля в рантайме. Давайте теперь получим все аннотации класса SimpleClass (в нашем случае у нас только 1 наша аннотация):
```java
Class aClass = SimpleClass.class;
Annotation[] annotations = aClass.getAnnotations();

for (Annotation annotation : annotations) {
    if(annotation instanceof Reflectable) {
        Reflectable mAnnotation = (Reflectable) annotation;
        System.out.println("name: " + mAnnotation.name());
        System.out.println("value: " + mAnnotation.value());
    }
}
```
 В коде выше мы использовали метод getAnnotations() для получения всех аннотаций класса в виде массива объектов Annotation. В цикле по всем аннотациям мы ищем пользовательскую аннотацию — Reflectable и получаем информацию о ней.
Если же нам интересна конкретная аннотация, то получить к ней доступ можно следующим образом:
```java
Class aClass = SimpleClass.class;
Annotation annotation = aClass.getAnnotation(Reflectable.class);
```

##### [Работа с аннотациями на методах](Annotation) #####

Аннотации на методах работают точно также, как и на примере выше, единственная разница в получении списка аннотаций. Если выше мы использовали метод getAnnotations(), то для аннотаций на методах можно вызывать метод getDeclaredAnnotations() — получение всех аннотаций с указанного метода.
Наш класс с аннотацией на методе:
```java
public class SimpleClass {
  @Reflectable(name="reflectable",  value = "какие-то метаданные")
  public void sayHello(){}
}
```
Используем рефлексию:
```java
Class mClassObject = SimpleClass.class
Method method = mClassObject.getMethod("sayHello", null);

Annotation[] annotations = method.getDeclaredAnnotations();

for(Annotation annotation : annotations) {
    if(annotation instanceof Reflectable) {
        Reflectable mAnnotation = (Reflectable) annotation;
        System.out.println("name: " + mAnnotation.name());
        System.out.println("value: " + mAnnotation.value());
    }
}
```
Или же явно получаем с указанного метода (если знаем наверняка, что она есть на этом методе):
```java
Annotation annotation = method.getAnnotation(Reflectable.class);
```

##### Аннотации на параметрах метода #####

Давайте добавим в наш класс еще один метод sayBye() с одним параметром, помеченным аннотацией:
```java
public class SimpleClass {
  //...
  public static void sayBye(
        @Reflectable(name="reflectable", value="какие-то метаданные") String param){
  }
}
```
Теперь напишем код для получения аннотаций на параметрах метода:
```java
Class mClassObject = SimpleClass.class
Method method = mClassObject.getMethod("sayBye", new Class[]{String.class});

Annotation[][] paramAnnotations = method.getParameterAnnotations();
Class[] paramTypes = method.getParameterTypes();

int i = 0;
for (Annotation[] annotations : paramAnnotations){
  Class parameterType = paramTypes[i++];

  for (Annotation annotation : annotations) {
    if (annotation instanceof Reflectable) {
        Reflectable mAnnotation = (Reflectable) annotation;
        System.out.println("param: " + paramType.getName());
        System.out.println("name: " + mAnnotation.name());
        System.out.println("value: " + mAnnotation.value());
    }
  }
}
```
В коде выше мы получили двумерный массив аннотаций на методе: внутренний массив каждого элемента является набором аннотаций для каждого параметра (аргумента метода).

##### Аннотации на полях #####

В наш класс добавим поле: пусть это будет строка со значением null:
```java
public class SimpleClass {
  @Reflectable(name="reflectable",  value = "какие-то метаданные")
  public String mField = null;
}
```
Теперь используя рефлексию получим аннотации к полю:
```java
Class mClassObject = SimpleClass.class
Field field = mClassObject.getField("mField");
Annotation annotation = field.getAnnotation(Reflectable.class);
```

#### Java Reflection API: Дженерики (Generics — родовые типы) ####

В различных статьях и на форумах часто пишут, что вся информация про дженерики в Java стирается во время компиляции и мы не можем получить ее во время выполнения (так называемое стирание типов). Это утверждение не совсем верно. Возможность получить информацию о дженериках во время выполнения есть в нескольких случаях. Давайте ниже рассмотрим их.

Как правило, дженерики в Java используются в следующих ситуациях:
- При объявлении параметризованного класса или интерфейса.
- Использование параметризованного класса.

Примером может послужить java.util.List интерфейс. Вместо того, чтобы создать список объектов, можно параметризовать его, скажем с помощью String.

Во время выполнения программы посмотреть тип параметризированного java.util.List возможности нет, но мы можем найти его в полях и методах, где он используется и параметризируется с помощью Java рефлексии. 

##### Информация о дженериках в рантайме #####

Информацию о типе мы можем получить с помощью класса java.lang.reflect.Method.
Ниже представлен класс, который мы будем обрабатывать:
```java
public class SimpleClass {

  protected List<String> simpleList = ...;

  public List<String> getList(){
    return this.simpleList;
  }
}
```
Получить информацию о дженериках параметризированного списка можно, если работать не с самим списком, а с геттером-методом getList():
```java
Method method = SimpleClass.class.getMethod("getList", null);

Type returnType = method.getGenericReturnType();

if (returnType instanceof ParameterizedType) {
    ParameterizedType type = (ParameterizedType) returnType;
    Type[] typeArguments = type.getActualTypeArguments();
    for (Type typeArgument : typeArguments) {
        Class typeClass = (Class) typeArgument;
        System.out.println("тип: " + typeClass);
    }
}
```
Будет напечатано в консоль: 
<p style="background-color: navy; color: yellow">тип: java.lang.String</p>

В коде выше мы определили, что это не просто List, а именно `List<String>`.
Если же у нас есть поле, то получить информацию о типе в рантайме можно следующим образом:
```java
Field field = SimpleClass.class.getField("simpleList");

Type genericFieldType = field.getGenericType();

if (genericFieldType instanceof ParameterizedType) {
    ParameterizedType pType = (ParameterizedType) genericFieldType;
    
    Type[] fieldArgTypes = pType.getActualTypeArguments();
    
    for (Type fieldArgType : fieldArgTypes){
        Class fielClass = (Class) fieldArgType;
        System.out.println("тип: " + fieldClass);
    }
}
```
Будет напечатано в консоль: 
<p style="background-color: navy; color: yellow">тип: java.lang.String</p>
В коде выше мы определили, что тип поля — параметризированный (с помощью instanceof) и по нему уже получили массив типов Type[], который содержит 1 элемент типа Class (он реализует интерфейс Type). Поэтому мы просто кастовали его к Class и распечатали в консоль.

#### Java Reflection API: Массивы ####

Работать с массивами сложнее всего, особенно если мы хотим получить объект Class для массива каких-то int[], например. Получать информацию о массивах можно с помощью класса java.lang.reflect.Array (не путать с java.util.Arrays в пакете Java коллекций)
Создание массива int с 2 элементами выглядит так:
```java
int[] simpleIntArray = (int[]) Array.newInstance(int.class, 2);
```
В первом параметре метода newInstance() указываем тип элементов массива, во втором — количество элементов этого массива.

Теперь рассмотрим работу геттеров и сеттеров при работе с массивами с помощью Java рефлексии:
```java
int[] simpleIntArray = (int[]) Array.newInstance(int.class, 2);

Array.set(simpleIntArray, 0, 443);
Array.set(simpleIntArray, 1, 554);

System.out.println("первый элемент массива = " + Array.get(simpleIntArray, 0));
System.out.println("второй элемент массива = " + Array.get(simpleIntArray, 1));
```

##### Получаем объект типа Class для массива #####

С использованием рефлексии это выглядит довольно трудно:
```java
Class intArrayObject = Class.forName("[I");
```
Обратите внимание на параметр: "[I":
- JVM представляет тип int с помощью символа "I".
- Символ «`[`» слева представляет собой класс массива int.

 Это работает для всех примитивов. А вот для объектов дело обстоит иначе. Смотрим на примере String:
```java
Class stringArrayClassObject = Class.forName("[Ljava.lang.String;");
```
Комбинация "`[L`" вначале и ";" представляет собой массив объектов определенного типа (тип описан между ними).

Такие сложности порождают другие сложности — уже с удобством работы. Для обхода этого обычно пишут такие хелпер-методы:
```java
public Class getClass(String className){
  if ("long".equals(className)) {
     return long.class;
  }
  // вместо long подставляйте любой другой примитив
  return Class.forName(className);
}
```
 А теперь создаем экземпляр Class:
```java
Class arrayClass = getClass(theClassName);
Class stringArrayClass = Array.newInstance(arrayClass, 0).getClass();
// и делаем проверку на всякий случай :)
System.out.println("массив ли это? - " + stringArrayClass.isArray());
```

##### Получаем тип массива #####

Получить тип массива так же просто:
```java
String[] stringArray = new String[2];
Class arrayClass = strings.getClass();
Class arrayComponentType = arrayClass.getComponentType();
System.out.println(arrayComponentType);
```
И получим в консоли:
<p style="background-color: navy; color: yellow">java.lang.String</p>

