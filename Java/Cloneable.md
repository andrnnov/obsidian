#Java #Cloneable 
### Ссылочные типы и копирование объектов ###

2023-11-27 16:20

При работе с объектами классов надо учитывать, что они все представляют ссылочные типы, то есть указывают на какой-то объект, расположенный в памяти. Чтобы понять возможные трудности, с которыми мы можем столкнуться, рассмотрим пример:
```java
public class Program{
    public static void main(String[] args) {
		Person tom = new Person("Tom", 23);
        tom.display();      // Person Tom
        Person bob = tom;
        bob.setName("Bob");
        tom.display();      // Person Bob
    }
}
class Person{
    private String name;
    private int age;
     
    Person(String name, int age){
        this.name=name;
        this.age=age;
    }
    void setName(String name){
        this.name = name;
    }
    void setAge(int age){
        this.age = age;
    }
    void display(){
        System.out.printf("Person Name: %s \n", name);
    }
}
```
Здесь создаем два объекта Person и один присваиваем другому. Но, несмотря на то, что мы изменяем только объект bob, вместе с ним изменяется и объект tom. Потому что после присвоения они указывают на одну и ту же область в памяти, где собственно данные об объекте Person и его полях и хранятся.

Чтобы избежать этой проблемы, необходимо создать отдельный объект для переменной bob, например, с помощью метода `clone`:
```java
class Person implements Cloneable{
    private String name;
    private int age;
     
    Person(String name, int age){
        this.name=name;
        this.age=age;
    }
    void setName(String name){
        this.name = name;
    }
    void setAge(int age){
        this.age = age;
    }
    void display(){
        System.out.printf("Person %s \n", name);
    }
     
    public Person clone() throws CloneNotSupportedException{
      
        return (Person) super.clone();
    }
}
```
Для реализации клонирования класса Person должен применить интерфейс Cloneable, который определяет метод `clone` класса [Object](Object). Реализация этого метода просто возвращает вызов метода `clone` для родительского класса - то есть класса [Object](Object) с преобразованием к типу Person.

Интерфейс Cloneable не реализует ни одного метода. Он является всего лишь маркером, говорящим, что данный класс реализует клонирование объекта. Само клонирование осуществляется вызовом родительского метода clone().

Кроме того, на случай если класс не поддерживает клонирование, метод должен выбрасывать исключение CloneNotSupportedException, что определяется с помощью оператора throws.

Затем с помощью вызова этого метода мы можем осуществить копирование:
```java
try{
    Person tom = new Person("Tom", 23);
    Person bob = tom.clone();
    bob.setName("Bob");
    tom.display();      // Person Tom
}
catch(CloneNotSupportedException ex){
    System.out.println("Clonable not implemented");
}
```
Однако данный способ осуществляет неполное копирование и подойдет, если клонируемый объект не содержит сложных объектов. Например, пусть класс Book имеет следующее определение:
```java
class Book implements Cloneable{
 
    private String name;
    private Author author;
     
    public void setName(String n){ name=n;}
    public String getName(){ return name;}
     
    public void setAuthor(String n){ author.setName(n);}
    public String getAuthor(){ return author.getName();}
 
    Book(String name, String author){
         
        this.name = name;
        this.author = new Author(author);
    }
     
    public String toString(){
         
        return "Книга '" + name + "' (автор " +  author + ")";
    }
     
    public Book clone() throws CloneNotSupportedException{
     
        return (Book) super.clone();
    }
}
 
class Author{
 
    private String name;
     
    public void setName(String n){ name=n;}
    public String getName(){ return name;}
     
    public Author(String name){
     
        this.name=name;
    }
}
```
Если мы попробуем изменить автора книги, нас постигнет неудача:
```java
try{
    Book book = new Book("War and Peace", "Leo Tolstoy");
    Book book2 = book.clone();
    book2.setAuthor("Ivan Turgenev");
    System.out.println(book.getAuthor());
}
catch(CloneNotSupportedException ex){
    System.out.println("Cloneable not implemented");
}
```
В этом случае, хотя переменные book и book2 будут указывать на разные объекты в памяти, но эти объекты при этом будут указывать на один объект Author.

И в этом случае нам необходимо выполнить полное копирование. Для этого надо определить метод клонирования у класса Author:
```java
class Author implements Cloneable{
 
    // остальной код класса
     
    public Author clone() throws CloneNotSupportedException{
     
        return (Author) super.clone();
    }
}
```
И затем исправим метод clone в классе Book следующим образом:
```java
public Book clone() throws CloneNotSupportedException{
    Book newBook = (Book) super.clone();
    newBook.author=(Author) author.clone();
    return newBook;
}
```
