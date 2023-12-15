#Java #StreamAPI
### Руководство по Java Stream API ###

2023-12-15 12:06

Java Stream API был добавлен в Java 8 вместе с несколькими другими функциями функционального программирования. 

API Java Stream не связан с Java [InputStream](InputStream) и Java [OutputStream](OutputStream) [Java IO](JavaIO). [InputStream](InputStream) и [OutputStream](OutputStream) связаны с потоками байтов. API Java Stream предназначен для обработки потоков объектов, а не байтов.

Java Stream – это компонент, способный выполнять внутреннюю итерацию своих элементов, то есть он может выполнять итерацию своих элементов сам.

#### Потоковая обработка ####

Можно прикрепить слушателей к потоку. Эти слушатели вызываются, когда Stream выполняет внутреннюю итерацию элементов. Слушатели вызываются один раз для каждого элемента в потоке.

Каждый слушатель получает возможность обрабатывать каждый элемент в потоке. Это называется потоковой обработкой.

Слушатели потока формируют цепочку. Первый слушатель в цепочке может обработать элемент в потоке, а затем вернуть новый элемент для обработки следующим слушателем в цепочке. Слушатель может возвращать тот же элемент или новый, в зависимости от назначения.
#### Получение потока ####

Есть много способов получить поток Java. Один из самых распространенных способов получить поток – из Java [Collection](Collections).
```java
List<String> items = new ArrayList<String>();
items.add("one");
items.add("two");
items.add("three");
Stream<String> stream = items.stream();
```
В этом примере сначала создали список Java, а затем добавили три строки. В итоге, в примере вызывается метод stream() для получения экземпляра потока.
#### Терминальные и нетерминальные операции ####

Интерфейс Stream имеет выбор терминальных и нетерминальных операций.

> Нетерминальная потоковая операция – это операция, которая добавляет слушателя в поток, не делая ничего другого.
> 
> Операция терминального потока – это операция, которая запускает внутреннюю итерацию элементов, вызывает всех слушателей и возвращает результат.

```java
import java.util.ArrayList;
import java.util.List;
import java.util.stream.Stream;

public class StreamExamples {
	public static void main(String[] args) {
		List<String> stringList = new ArrayList<String>();
		stringList.add("ONE");
		stringList.add("TWO");
		stringList.add("THREE");
		Stream<String> stream = stringList.stream();
		
		long count = stream
			.map((value) -> { return value.toLowerCase(); })
			.count();
			
		System.out.println("count = " + count);
	}
}
```
Вызов метода map() является нетерминальной операцией. Он просто преобразует каждый элемент в нижний регистр. Вызов метода count() является терминальной операцией. Этот вызов запускает внутреннюю итерацию, в результате чего каждый элемент преобразуется в нижний регистр.

Преобразование элементов в нижний регистр фактически не влияет на количество элементов.
#### Нетерминальные операции ####

Нетерминальные операции потока Java Stream API являются операциями, которые преобразовывают или фильтруют элементы в потоке. Когда добавляется нетерминальная операция в поток, в итоге мы получаем новый поток.
```java
List<String> stringList = new ArrayList<String>();
stringList.add("ONE");
stringList.add("TWO");
stringList.add("THREE");
Stream<String> stream = stringList.stream();

Stream<String> stringStream =
		stream.map((value) -> { return value.toLowerCase(); });
```
Этот вызов возвращает новый экземпляр Stream, представляющий исходный поток строк с применяемой операцией.

Можно добавить только одну операцию в данный экземпляр. Если необходимо объединить несколько операций, следующих друг за другом, потребуется применить вторую операцию к операции потока, полученной в результате первой.
```java
Stream<String> stringStream1 =
		stream.map((value) -> { return value.toLowerCase(); });
Stream<String> stringStream2 =
		stringStream1.map((value) -> { return value.toUpperCase(); });
```
Обратим внимание, как второй вызов map() вызывается в потоке, возвращаемом первым вызовом map().
```java
Stream<String> stream1 = stream
		.map((value) -> { return value.toLowerCase(); })
		.map((value) -> { return value.toUpperCase(); })
		.map((value) -> { return value.substring(0,3); });
```
Многие нетерминальные операции Stream могут принимать Java [Lambda Expression](Lambda) в качестве параметра. Это лямбда-выражение реализует Java functional interface, который подходит для данной нетерминальной операции.

Например, интерфейс [[Functional-Interface#Function|Function]] или [[Functional-Interface#Predicate|Predicate]]. Параметр метода нетерминальной операции обычно является функциональным интерфейсом, поэтому его также можно реализовать с помощью Java lambda expression.
#### filter() ####

filter() можно использовать для фильтрации элементов. Метод фильтра принимает  [[Functional-Interface#Predicate|Predicate]], который вызывается для каждого элемента в потоке.

Если элемент должен быть включен в результирующий поток, [[Functional-Interface#Predicate|Predicate]] должен вернуть значение “true”. Если элемент не должен быть включен, [[Functional-Interface#Predicate|Predicate]]  должны возвращать значение “false”.
```java
Stream<String> longStringsStream = stream.filter((value) -> {
	return value.length() >= 3;
});
```
#### map() ####

Метод map() преобразует (отображает) элемент в другой объект. Например, если у нас был список строк, он мог бы преобразовать каждую строку в нижний регистр, верхний регистр или в подстроку исходной строки.
```java
List<String> list = new ArrayList<String>();
Stream<String> stream = list.stream();
Stream<String> streamMapped = stream.map((value) -> value.toUpperCase());
```
#### flatMap() ####

Методы Java Stream flatMap() отображают один элемент на несколько элементов. Идея состоит в том, что мы «сплющиваем» каждый элемент из сложной структуры, состоящей из нескольких внутренних элементов, в «плоский» поток, состоящий только из этих внутренних элементов.

Например, представим, что у нас есть объект с вложенными объектами (дочерние объекты). Затем можно отобразить этот объект в «плоский» поток, состоящий из себя плюс его вложенные объекты – или только вложенные объекты.

Можно также отобразить поток списков элементов на сами элементы. Или сопоставить поток строк с потоком слов в этих строках – или с отдельными экземплярами символов в этих строках.
```java
List<String> stringList = new ArrayList<String>();
stringList.add("One flew over the cuckoo's nest");
stringList.add("To kill a muckingbird");
stringList.add("Gone with the wind");
Stream<String> stream = stringList.stream();

stream.flatMap((value) -> {
		String[] split = value.split(" ");
		return (Stream<String>) Arrays.asList(split).stream();
	})
.forEach((value) -> System.out.println(value));
```
Этот пример flatMap() сначала создает список из 3 строк, содержащих названия книг. Затем получается поток для списка и вызывается flatMap().

flatMap(), вызываемый в потоке, должен возвращать другой поток, представляющий элементы плоского отображения. В приведенном выше примере каждая исходная строка разбивается на слова, превращается в список, а поток получается и возвращается из этого списка.

Этот пример заканчивается вызовом forEach(). Предназначен только для запуска внутренней итерации и, следовательно, операции flat map. Если в цепочке Stream не было вызвано ни одной операции терминала, ничего бы не произошло. Никакого плоского картирования на самом деле не было бы.
#### distinct() ####

Метод distinct() это нетерминальная операция, возвращающая новый поток, который будет содержать только отдельные элементы из исходного потока. Любые дубликаты будут удалены.
```java
List<String> stringList = new ArrayList<String>();
stringList.add("one");
stringList.add("two");
stringList.add("three");
stringList.add("one");
Stream<String> stream = stringList.stream();

List<String> distinctStrings = stream
			.distinct()
			.collect(Collectors.toList());
System.out.println(distinctStrings);
```
В этом примере элемент 1 появляется 2 раза в исходном потоке. Только первое вхождение этого элемента будет включено в поток, возвращаемый Different(). Таким образом, результирующий список (от вызова collect()) будет содержать только один, два и три. 
Вывод будет:
<p style="background-color: navy; color: yellow">one two three</p>
#### limit() ####

Метод limit()может ограничивать количество элементов в потоке числом, данным методу limit() в качестве параметра. Метод limit() возвращает новый поток, который будет максимально содержать заданное количество элементов.
```java
List<String> stringList = new ArrayList<String>();
stringList.add("one");
stringList.add("two");
stringList.add("three");
stringList.add("one");
Stream<String> stream = stringList.stream();

stream.limit(2).forEach( element -> { System.out.println(element); });
```
В этом примере сначала создается Stream, затем вызывается limit(), а затем вызывается forEach() с лямбда-выражением, которое выводит элементы в потоке. Только два первых элемента будут напечатаны из-за вызова limit(2).
#### peek() ####

Метод peek() – это нетерминальная операция, которая принимает [[Functional-Interface#Consumer|Consumer(java.mutilfunction.Consumer)]] в качестве параметра. [[Functional-Interface#Consumer|Consumer]] будет вызван для каждого элемента в потоке. Метод peek() возвращает новый поток, который содержит все элементы в исходном потоке.

Цель состоит в том, чтобы посмотреть на элементы в потоке, а не преобразовать их. Он не запускает внутреннюю итерацию элементов. Для этого нужно вызвать терминальную операцию.
```java
List<String> stringList = new ArrayList<String>();
stringList.add("abc");
stringList.add("def");
Stream<String> stream = stringList.stream();
Stream<String> streamPeeked = stream.peek((value) -> {System.out.println("value"); });
```
#### Терминальные операции ####

Терминальные операции Java Stream обычно возвращают одно значение. Как только операция терминала вызывается в потоке, начинается итерация потока и любого из связанных потоков. По завершении итерации возвращается результат операции терминала.

Операция терминала обычно не возвращает новый экземпляр. Таким образом, как только вызывается терминальная операция в потоке, цепочка экземпляров Stream из нетерминальной операции заканчивается.
```java
long count = stream
			.map((value) -> { return value.toLowerCase(); })
			.map((value) -> { return value.toUpperCase(); })
			.map((value) -> { return value.substring(0,3); })
			.count();
```
Поскольку count() возвращает long, цепочка нетерминальных операций заканчивается.
#### anyMatch() ####

Метод anyMatch() – это терминальная операция, которая принимает один Predicate в качестве параметра, запускает внутреннюю итерацию потока и применяет параметр Predicate к каждому элементу.

Если Predicate возвращает true для любого из элементов, метод anyMatch() возвращает true. Если ни один элемент не соответствует Predicate, anyMatch() вернет false.
```java
List<String> stringList = new ArrayList<String>();
stringList.add("One flew over the cuckoo's nest");
stringList.add("To kill a muckingbird");
stringList.add("Gone with the wind");
Stream<String> stream = stringList.stream();
boolean anyMatch = stream.anyMatch((value) -> { return value.startsWith("One"); });
System.out.println(anyMatch);
```
В приведенном выше примере вызов вернет true, поскольку первый строковый элемент в потоке начинается с «one».
#### allMatch() ####

Метод Java Stream allMatch() является терминальной операцией, которая принимает один Predicate в качестве параметра, запускает внутреннюю итерацию элементов в потоке и применяет параметр Predicate к каждому элементу.

Если Predicate возвращает true для всех элементов в потоке, allMatch() вернет true. Если не все элементы соответствуют Predicate, метод allMatch() возвращает false.
```java
List<String> stringList = new ArrayList<String>();
stringList.add("One flew over the cuckoo's nest");
stringList.add("To kill a muckingbird");
stringList.add("Gone with the wind");
Stream<String> stream = stringList.stream();
boolean allMatch = stream.allMatch((value) -> { return value.startsWith("One"); });
System.out.println(allMatch);
```
В приведенном выше примере метод allMatch() вернет false, поскольку только одна из строк в Stream начинается с «one».
#### noneMatch() ####

noneMatch() является терминальной операцией, которая будет выполнять итерацию элементов в потоке и возвращать true или false в зависимости от того, соответствуют ли элементы в потоке Predicate, переданному noneMatch() в качестве параметра.

Метод noneMatch() вернет значение true, если ни один элемент не соответствует элементу Predicate, и значение false, если один или несколько элементов соответствуют.

Вот пример использования:
```java
List<String> stringList = new ArrayList<String>();
stringList.add("abc");
stringList.add("def");
Stream<String> stream = stringList.stream();
boolean noneMatch = stream.noneMatch((element) -> { return "xyz".equals(element);});
System.out.println("noneMatch = " + noneMatch);
```
#### collect() ####

Метод collect() является терминальной операцией, которая запускает внутреннюю итерацию элементов и собирает элементы в потоке в коллекции или объекты какого-либо вида.
```java
List<String> stringList = new ArrayList<String>();
stringList.add("One flew over the cuckoo's nest");
stringList.add("To kill a muckingbird");
stringList.add("Gone with the wind");
Stream<String> stream = stringList.stream();
List<String> stringsAsUppercaseList = stream
			.map(value -> value.toUpperCase())
			.collect(Collectors.toList());
System.out.println(stringsAsUppercaseList);
```
Метод collect() принимает в качестве параметра Collector (java.util.stream.Collector). Реализация Collector требует некоторого изучения интерфейса Collector.

К счастью, класс Java java.util.stream.Collectors содержит набор предварительно реализованных действий Collector, которые можно использовать для наиболее распространенных операций.

В приведенном выше примере использовалась реализация Collector, возвращаемая Collectors.toList(). Этот Collector просто собирает все элементы в потоке в стандартный [список Java](https://hr-vector.com/java/spiski-metody-interfejsa-list).
#### count() ####

Метод подсчета является терминальной операцией, которая подсчитывает элементы. Вот пример подсчета:
```java
List<String> stringList = new ArrayList<String>();
stringList.add("One flew over the cuckoo's nest");
stringList.add("To kill a muckingbird");
stringList.add("Gone with the wind");
Stream<String> stream = stringList.stream();
long count = stream.flatMap((value) -> {
			String[] split = value.split(" ");
			return (Stream<String>) Arrays.asList(split).stream();})
		.count();
System.out.println("count = " + count);
```
Сначала создается список строк, затем получается поток для этого списка, для него добавляется операция flatMap(), а затем заканчивается вызов метода count().

Метод count() запускает итерацию элементов в потоке, в результате чего строковые элементы разбиваются на слова в операции flatMap(), а затем подсчитываются. Окончательный результат, который будет выведен – 14.
#### findAny() ####

findAny() может найти отдельный элемент. Здесь все просто и понятно.
```java
List<String> stringList = new ArrayList<String>();
stringList.add("one");
stringList.add("two");
stringList.add("three");
stringList.add("one");
Stream<String> stream = stringList.stream();
Optional<String> anyElement = stream.findAny();
System.out.println(anyElement.get());
```
Обратим внимание, как метод findAny() возвращает Optional. Поток может быть пустым, поэтому элемент не может быть возвращен. Можно проверить, был ли элемент найден с помощью дополнительного метода isPresent().
#### FindFirst() ####

findFirst() находит первый элемент в потоке, если в потоке присутствуют какие-либо элементы. Метод findFirst() возвращает необязательный параметр, из которого можно получить элемент, если он есть.
```java
List<String> stringList = new ArrayList<String>();
stringList.add("one");
stringList.add("two");
stringList.add("three");
stringList.add("one");
Stream<String> stream = stringList.stream();
Optional<String> result = stream.findFirst();
System.out.println(result.get());
```
Можно проверить, содержит ли возвращаемый Optional элемент через его метод isPresent().
#### forEach() ####

forEach() является терминальной операцией, которая запускает внутреннюю итерацию элементов и применяет Consumer (java.util.function.Consumer) к каждому элементу в стриме.
```java
List<String> stringList = new ArrayList<String>();
stringList.add("one");
stringList.add("two");
stringList.add("three");
stringList.add("one");
Stream<String> stream = stringList.stream();
stream.forEach( element -> { System.out.println(element); });
```
#### min() ####

min() является терминальной операцией, которая возвращает наименьший элемент в потоке. Наименьший элемент, определяется реализацией Comparator, которую мы передаем методу min().
```java
List<String> stringList = new ArrayList<String>();
stringList.add("abc");
stringList.add("def");
Stream<String> stream = stringList.stream();
Optional<String> min = stream.min((val1, val2) -> { return val1.compareTo(val2);});
String minString = min.get();
System.out.println(minString);
```
Обратим внимание, как метод min() возвращает необязательный параметр, который может содержать или не содержать результат. Если поток пустой, дополнительный метод get() генерирует исключение NoSuchElementException.
#### max() ####

max() возвращает самый большой элемент в потоке. Наибольший элемент определяется реализацией Comparator, которую мы передаем методу max().
```java
List<String> stringList = new ArrayList<String>();
stringList.add("abc");
stringList.add("def");
Stream<String> stream = stringList.stream();
Optional<String> max = stream.max((val1, val2) -> { return val1.compareTo(val2);});
String maxString = max.get();
System.out.println(maxString);
```
Возвращает необязательный параметр, который может содержать или не содержать результат. Если поток пустой, дополнительный метод get() будет генерировать исключение NoSuchElementException.
#### reduce() ####

reduce() может свести все элементы в потоке к одному элементу. Посмотрите на реализацию:
```java
List<String> stringList = new ArrayList<String>();
stringList.add("One flew over the cuckoo's nest");
stringList.add("To kill a muckingbird");
stringList.add("Gone with the wind");
Stream<String> stream = stringList.stream();
Optional<String> reduced = stream.reduce((value, combinedValue) -> {
			return combinedValue + " + " + value;});
			System.out.println(reduced.get());
```
Обратим внимание на необязательный параметр, возвращаемый методом reduce(). Этот необязательный параметр содержит значение (если оно есть), возвращаемое лямбда-выражением, переданным методу reduce(). Мы получаем значение, вызывая метод Optionalget().
#### toArray() ####

Метод Java Stream toArray() является терминальной операцией, которая запускает внутреннюю итерацию элементов в потоке и возвращает массив Object, содержащий все элементы.
```java
List<String> stringList = new ArrayList<String>();
stringList.add("One flew over the cuckoo's nest");
stringList.add("To kill a muckingbird");
stringList.add("Gone with the wind");
Stream<String> stream = stringList.stream();
Object[] objects = stream.toArray();
```
### Конкатенация потоков в Java ###

Статический метод concat() может объединять два потока в один. Результатом является новый поток, содержащий все элементы из первого, за которыми следуют все элементы из второго.
```java
List<String> stringList = new ArrayList<String>();
stringList.add("One flew over the cuckoo's nest");
stringList.add("To kill a muckingbird");
stringList.add("Gone with the wind");
Stream<String> stream1 = stringList.stream();

List<String> stringList2 = new ArrayList<>();
stringList2.add("Lord of the Rings");
stringList2.add("Planet of the Rats");
stringList2.add("Phantom Menace");
Stream<String> stream2 = stringList2.stream();

Stream<String> concatStream = Stream.concat(stream1, stream2);
List<String> stringsAsUppercaseList = concatStream
			.collect(Collectors.toList());

System.out.println(stringsAsUppercaseList);
```
### Недостатки Java Stream API ###

По сравнению с другими  API потоковой передачи данных, такими как Apache Kafka Streams API, у Java Stream API есть небольшие недостатки. Они не являются очень важными, но их полезно иметь в виду.
#### Пакетный, но не потоковый ####

Несмотря на свое название, Java Stream API не является в действительности API потоковой обработки. Терминальные операции возвращают конечный результат итерации по всем элементам в потоке и предоставляют нетерминальные и терминальные операции элементам. Результат операции терминала возвращается после обработки последнего элемента в потоке.

Возврат окончательного результата после обработки последнего элемента потока возможен, только если знать, какой элемент является последним.

Мы никогда не знаем, является ли данный элемент последним или нет. Поэтому невозможно выполнить терминальную операцию. Лучшее, что можно сделать, это собрать временные результаты после обработки данного элемента, но это будет выборка, а не окончательный результат.
#### Цепь, а не график ####

Можно добавить только одну нетерминальную операцию в Stream, что приведет к созданию нового объекта. Можно добавить еще одну нетерминальную операцию к результирующему объекту Stream, но не к первому. Результирующая структура нетерминальных экземпляров стрима образует цепочку.

В настоящем API потоковой обработки, корневой поток и слушатели событий обычно могут образовывать график, а не просто цепочку. Несколько слушателей могут прослушивать корневой поток, и каждый слушатель может обрабатывать элементы в потоке по-своему, и в результате могут пересылать преобразованный элемент.

> Таким образом, каждый слушатель (нетерминальная операция) обычно может действовать как сам поток, который другие слушатели могут прослушивать результаты. Так устроен Apache Kafka Streams.

Чтобы легко поддерживать операции терминала, должна быть одна, последняя операция, из которой возвращается конечный результат. API обработки потоков на основе графика может вместо этого поддерживать «примерную» операцию, в которой у каждого узла в графике обработки потоков запрашивается любое значение, которое он может содержать внутри (например, сумма), если таковые имеются (чисто преобразовывающие узлы слушателя не будут иметь никакого внутреннего состояния ).
#### Внутренняя, а не внешняя итерация ####

Стримы специально разработаны для внутренней итерации элементов в потоке. Итерация начинается, когда терминальная операция вызывается в потоке. Фактически, чтобы терминальные операции могли возвращать результат, терминальная операция должна инициировать итерацию элементов в потоке.

Некоторые API обработки потоков на основе графиков также предназначены для того, чтобы скрыть итерацию элементов от пользователя API (например, Apache Kafka Streams и RxJava).

Однако более предпочтителен проект, в котором каждый узел потока (корневой поток и слушатели) могут иметь элементы, передаваемые им через вызов метода, и этот элемент передается через полный график для обработки.

Такой способ облегчил бы тестирование каждого слушателя на графике, так как вы можно настроить график и пропустить через него элементы, и, наконец, проверить результат.