#Java #try-with-resources
### [try-with-resources в Java](https://rukovodstvo.net/posts/id_1114/)

2024-01-22 12:44

_try-with-resources_ - это один из нескольких `try` в Java, призванный освободить разработчиков от обязанности освобождать ресурсы, используемые в блоке `try`.

Первоначально он был представлен в Java 7, и вся идея заключалась в том, что разработчику не нужно беспокоиться об управлении ресурсами для ресурсов, которые они используют только в одном блоке _try-catch-finally._ Это достигается за счет устранения необходимости в `finally`, которые на практике разработчики использовали только для закрытия ресурсов.

Кроме того, код, использующий _try-with-resources_, часто чище и читабельнее, что упрощает управление кодом, особенно когда мы имеем дело со многими блоками `try`.

Синтаксис _try-with-resources_ почти идентичен обычному синтаксису _try-catch-finally._ Единственное отличие - это скобки после `try` в которых мы объявляем, какие ресурсы мы будем использовать.
```java
BufferedWriter writer = null; 
 try { 
	 writer = new BufferedWriter(new FileWriter(fileName)); 
	 writer.write(str); // do something with the file we've opened 
 } catch (IOException e) { 
	 // handle the exception 
	 } finally { 
		 try { 
			 if (writer != null) 
			 writer.close(); 
		 } catch (IOException e) { 
	 // handle the exception 
	 } 
 } 
```
Тот же код, написанный с использованием _try-with-resources,_ будет выглядеть так:
```java
try(BufferedWriter writer = new BufferedWriter(new FileWriter(fileName))){ 
	 writer.write(str); // do something with the file we've opened 
 } 
 catch(IOException e){ 
	 // handle the exception 
 } 
```
То, как Java понимает этот код:

> Ресурсы, открытые в круглых скобках после _оператора try,_ понадобятся только здесь и сейчас. Я вызову их `.close()` как только закончу работу с блоком _try._ Если в _блоке try_ возникает исключение, я все равно закрою эти ресурсы.

До того как этот подход был введен, закрытие ресурсов выполнялось вручную, как было показано в коде ранее. По сути, это был шаблонный код, и кодовые базы были завалены им, снижая удобочитаемость и усложняя поддержку.

`catch` и, `finally` часть _try-with-resources_ работают должным образом, при этом `catch` обрабатывают соответствующие исключения, а `finally` выполняется независимо от того, было исключение или нет. Единственное отличие - это подавленные исключения, которые описаны в конце этой статьи.

**Примечание**. Начиная с Java 9, объявлять ресурсы в операторе _try-with-resources необязательно._ Вместо этого мы можем сделать что-то вроде этого:
```java
BufferedWriter writer = new BufferedWriter(new FileWriter(fileName)); 
try (writer) { 
	writer.write(str); // do something with the file we've opened 
} 
catch(IOException e) { 
// handle the exception 
} 
```
#### Множественные ресурсы

Еще один хороший аспект _try-with-resources_ - это простота добавления / удаления ресурсов, которые мы используем, с уверенностью, что они будут закрыты после того, как мы закончим.

Если бы мы хотели работать с несколькими файлами, мы открывали файлы в `try()` и разделяли их точкой с запятой:

```java
try (BufferedWriter writer = new BufferedWriter(new FileWriter(fileName)); 
		Scanner scanner = new Scanner(System.in)) { 
	if (scanner.hasNextLine()) 
		writer.write(scanner.nextLine()); 
} 
catch(IOException e) { 
// handle the exception 
} 
```
Затем Java заботится о том, чтобы вызвать `.close()` для всех ресурсов, которые мы открыли в `try()`.

**Примечание: они закрываются в обратном порядке объявления, что означает, что в нашем примере `scanner` будет закрыт раньше `writer`.

#### Поддерживаемые классы

Все ресурсы, объявленные в `try()` должны реализовывать интерфейс `AutoCloseable` Обычно это различные типы писателей, читателей, сокетов, выходных или входных потоков и т. Д. Все, что вам нужно для написания `resource.close()` после того, как вы закончите с ним работать.

Это, конечно, включает определяемые пользователем объекты, реализующие интерфейс `AutoClosable` Тем не менее, вы редко встретите ситуацию, когда вы захотите написать свои собственные ресурсы.

В случае, если это произойдет, вам необходимо реализовать `AutoCloseable` или [`Closeable`](Closeable) (только там, чтобы сохранить обратную совместимость, предпочитайте `AutoCloseable`) и переопределите метод `.close()`:
```java
public class MyResource implements AutoCloseable { 
	@Override 
	public void close() throws Exception { 
	// close your resource in the appropriate way 
	} 
} 
```

#### Обработка исключений

Если исключение выбрасывается из _блока Java try-with-resources_, любой ресурс, открытый в круглых скобках `try` все равно будет автоматически закрыт.

Как упоминалось ранее, _try-with-resources_ работает так же, как _try-catch-finally_, за исключением одного небольшого дополнения. Добавление называется _подавленными исключениями_.

Представьте себе ситуацию:
- По какой-то причине в блоке _try-with-resources возникает исключение_;
- Java останавливает выполнение в _блоке try-with-resources_ и вызывает `.close()` для всех ресурсов, объявленных в `try()`;
- Один из `.close()` вызывает исключение;
- Какое исключение ловит блок catch?

Эта ситуация знакомит нас с вышеупомянутыми подавленными исключениями. Подавленное исключение - это исключение, которое в некотором смысле игнорируется, когда оно создается в неявном блоке finally блока _try-with-resources_, в случае, когда исключение также генерируется из блока `try`

Эти исключения являются исключениями, которые возникают в `.close()` и доступ к ним отличается от «обычных» исключений.

Важно понимать, что порядок исполнения такой:
1. блок _try-with-resources_
2. неявный finally
3. блок catch (если исключение было сгенерировано в [1] и / или [2])
4. (явный) finally

Например, вот ресурс, который ничего не делает, кроме исключения:
```java
public static class MyResource implements AutoCloseable { 
	// method throws RuntimeException 
	public void doSomething() { 
		throw new RuntimeException("From the doSomething method"); 
	 } 
 
 // we'll override close so that it throws an exception in the implicit finally block of try-with-resources (when it attempts to close our resource) 
 @Override 
	public void close() throws Exception { 
		throw new ArithmeticException("I can throw whatever I want, you can't stop me."); 
	} 
 } 
 
	public static void main(String[] arguments) throws Exception { 
	 // declare our resource in try 
	try (MyResource resource = new MyResource()) { 
		resource.doSomething(); 
		} 
		catch (Exception e) { 
			System.out.println("Regular exception: " + e.toString()); 
			// getting the array of suppressed exceptions, and its length 
			Throwable[] suppressedExceptions = e.getSuppressed(); 
			int n = suppressedExceptions.length; 
 
			 if (n > 0) { 
				 System.out.println("We've found " + n + " suppressed exceptions:"); 
			 for (Throwable exception : suppressedExceptions) { 
				 System.out.println(exception.toString()); 
			 } 
		 } 
	 } 
 } 
```
Этот код работоспособен. Вы можете использовать его, чтобы поэкспериментировать с использованием нескольких `MyResource` или посмотреть, что происходит, когда _try-with-resources_ не генерирует исключение, а `.close()` делает.

**Подсказка: внезапно стали важны исключения, возникающие при закрытии ресурсов.

Важно отметить, что если ресурс выдает исключение при попытке закрыть его, любые другие ресурсы, открытые в том же _блоке try-with-resources,_ все равно будут закрыты.

Еще один факт, который следует отметить, заключается в том, что в ситуации, когда `try` не генерирует исключение и когда возникает несколько исключений при попытке использовать `.close()` используемые ресурсы, **первое** исключение будет распространяться вверх по стеку вызовов, а остальные будут подавлены.

Как вы можете видеть в коде, вы можете получить список всех подавленных исключений, `Throwable` массиву `Throwable.getSuppressed()`.

Помните, что внутри блока try может быть создано только одно исключение. Как только возникает исключение, код блока try завершается, и Java пытается закрыть ресурсы.

#### Заключение

По возможности следует использовать _try-with-resources_ _вместо обычного try-catch-finally_ . Легко забыть закрыть один из ваших ресурсов после нескольких часов написания кода или забыть закрыть ресурс, который вы только что добавили в свою программу, после случайного всплеска вдохновения.
