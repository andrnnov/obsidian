#Java #DesignPatterns #Visitor

## [Паттерн проектирования: Builder](https://vertex-academy.com/tutorials/ru/pattern-builder-java/)

2024-07-10 12:08

### Что такое паттерн Builder и зачем он нужен

Представим, что нам нужно создать класс с большим количеством параметров - например, класс **Person**. Какие поля у нас будут? Давайте добавим:
- имя (name)
- фамилия (surname)
- возраст (age)
- рост (height)
- вес (weight)
- родители (parents)

Можно еще много параметров дописывать - но и этого пока хватит. В "реальных" классах полей может быть и намного больше.

Таким образом, получаем такой класс:
```java
public class Person {
    private String name;
    private String surname;
    private int age;
    private int height;
    private int weight;
    private Set<Person> parents;
}
```
А теперь представим, что мы хотим для данного класса задать все возможные варианты конструкторов, которые нам могут понадобиться. Зачем? Чтобы в разных частях кодах использовать разные конструкторы и создавать экземпляры класса Person с разным количеством заполненных полей ( например, у нас в классе 6 полей. А мы хотим заполнить только 3 поля).

Например, это будет выглядеть так:
```java
public class Person {
    private String name;
    private String surname;
    private int age;
    private int height;
    private int weight;
    private Set<Person> parents; 
 
    Person (String name, String surname){
        this.name = name;
        this.surname = surname;
    }
 
    Person (String name, String surname, int age){
        this.name = name;
        this.surname = surname;
        this.age = age;
    }
 
    Person (String name, String surname, int age, int height){
        this.name = name;
        this.surname = surname;
        this.age = age;
        this.height = height;
    }
    //... more constructors here
}
```
Как видите, мы прописали 3 конструктора и предполагается, что их может быть намного больше.

И так нам придется писать разные сочетания параметров? Более того, очень легко будет случайно перепутать параметры местами. Например, если мы напишем **Person("Doe", "Jane")** вместо **Person("Jane", "Doe")** - перепутаем местами имя и фамилию? Или, например, возраст и рост? Оба параметра имеют одинаковый тип, и мы можем долго не замечать ошибку.

Все эти проблемы нам помогает решить паттерн проектирования Builder. Давайте создадим его!

Для этого **вернемся к первоначальной версии** нашего класса:
```java
public class Person {
    private String name;
    private String surname;
    private int age;
    private int height;
    private int weight;
    private Set<Person> parents; 
}
```
Создаем внутри нашего класса еще один класс - **Builder**:
```java
public class Person {
    private String name;
    private String surname;
    private int age;
    private int height;
    private int weight;
    private Set<Person> parents; 
 
   /* ---=== getters are supposed to be here. We skipped this part of code to make it simple ===--- */
 
    public static class Builder {
        private Person newPerson;
 
        public Builder() {
            newPerson = new Person();
        }
 
        public Builder withName(String name){
            newPerson.name = name;
            return this;
        }
 
        public Builder withSurname(String surname){
            newPerson.surname = surname;
            return this;
        }
 
        public Builder withAge(int age){
            newPerson.age = age;
            return this;
        }
 
        public Builder withHeight(int height){
            newPerson.height = height;
            return this;
        }
 
        public Builder withWeight(int weight){
            newPerson.weight = weight;
            return this;
        }
 
        public Builder withParents(Set<Person> parents){
            newPerson.parents = parents;
            return this;
        }
 
        public Person build(){
            return newPerson;
        }
    }
}
```
Если бы у нас был такой же **Builder**, только на один параметр (например, **имя**), он выглядел бы так:
```java
public static class Builder {
        private Person newPerson;
 
        public Builder() {
            newPerson = new Person();
        }
 
        public Builder withName(String name){
            newPerson.name = name;
            return this;
        }
 
        public Person build(){
            return newPerson;
        }
    }
```
Если разделить на части будет так:
![[Builder.png]]
Далее вызываем **Builder** - пишем main():
```java
public static void main(String[] args) {
    Person myPerson = new Person.Builder()
            .withName("Jane")
            .withSurname("Doe")
            .withAge(32)
            .withHeight(165)
            .withWeight(70)
            .build();
}
```
Мы построили наш первый объект с помощью паттерна **Builder**.

Теперь благодаря паттерну Builder:
- код выглядит **гораздо читабельнее**. Ведь все, относящееся к созданию объекта, вынесено в отдельный класс  - Builder;
- при заполнении полей объекта теперь **параметры трудно перепутать**;
- мы можем заполнять **не все параметры** класса. Как Вы могли заметить, мы указали все параметры кроме родителей (parents).

### Пример 2

```java
// Java code to demonstrate method chainin
final class Student 
    // instance fields
    private int id;
    private String name;
    private String address;

    // Setter Methods
    // Note that all setters method
    // return this reference
    public Student setId(int id) {
        this.id = id;
        return this;
    }

    public Student setName(String name) {
        this.name = name;
        return this;
    }

    public Student setAddress(String address) {
        this.address = address;
        return this;
    }

    @Override public String toString() {
        return "id = " + this.id +
                " name = " + this.name +
                " address = " + this.address;
    }
}

// Driver class
public class Main {
    public static void main(String args[])
    {
        Student student1 = new Student();
        Student student2 = new Student();

        student1.setId(1)
                .setName("Anna")
                .setAddress("NNov");
        student2.setId(2)
                .setName("Liza")
                .setAddress("Moscow");

        System.out.println(student1);
        System.out.println(student2);
    }
}
```
**Вывод:**
<p style="background-color: navy; color: yellow">
id = 1 name = Anna address = NNov<br>
id = 2 name = Liza address = Moscow</p>

А теперь обеспечим потокобезопасность (thread-safe):
```java
// Java code to demonstrate Builder Pattern
// Server Side Code
final class Student {
    // final instance fields
    private final int id;
    private final String name;
    private final String address;

    public Student(Builder builder) {
        this.id = builder.id;
        this.name = builder.name;
        this.address = builder.address;
    }

    // Static class Builder
    public static class Builder {

        // instance fields
        private int id;
        private String name;
        private String address;

        public static Builder newInstance() {
            return new Builder();
        }

        private Builder() {}

        // Setter methods
        public Builder setId(int id) {
            this.id = id;
            return this;
        }
        public Builder setName(String name) {
            this.name = name;
            return this;
        }
        public Builder setAddress(String address) {
            this.address = address;
            return this;
        }

        // build method to deal with outer class
        // to return outer instance
        public Student build()
        {
            return new Student(this);
        }
    }

    @Override
    public String toString()
    {
        return "id = " + this.id + ", name = " + this.name +
                ", address = " + this.address;
    }
}

// Client Side Code
class StudentReceiver {
    // volatile student instance to ensure visibility
    // of shared reference to immutable objects
    private volatile Student student;

    public StudentReceiver() {
        Thread t1 = new Thread(new Runnable() {
            @Override
            public void run() {
                student = Student.Builder.newInstance()
                        .setId(1)
                        .setName("Anna")
                        .setAddress("NNov")
                        .build();
            }
        });

        Thread t2 = new Thread(new Runnable() {
            @Override
            public void run() {
                student = Student.Builder.newInstance()
                        .setId(2)
                        .setName("Liza")
                        .setAddress("Moscow")
                        .build();
            }
        });

        t1.start();
        t2.start();

        try {
            t1.join();
            t2.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }

    public Student getStudent() {
        return student;
    }
}

// Driver class
public class Main {
    public static void main(String args[]) {
        StudentReceiver sr = new StudentReceiver();
        System.out.println(sr.getStudent());
    }
}
```
**Вывод:**
<p style="background-color: navy; color: yellow">
id = 1 name = Anna address = NNov</p>
или
<p style="background-color: navy; color: yellow">
id = 2 name = Liza address = Moscow</p>
Метод Builder.newInstance() также можно вызвать с любыми необходимыми аргументами, чтобы получить экземпляр _Builder_ путем его перегрузки. Объект класса _Student_ создается с помощью вызова метода __build()__ . Приведенная выше реализация шаблона Builder делает класс _Student_ **неизменяемым (immutable)** и, следовательно, **потокобезопасным (thread-safe)**. Также обратите внимание, что поле _Student_ в клиентском коде не может быть объявлено окончательным (final), поскольку ему присвоен новый неизменяемый (immutable) объект. Но его следует объявить [изменчивым (volatile),](volatile) чтобы обеспечить видимость общих ссылок на неизменяемые объекты. Также частные члены класса _Builder_ поддерживают инкапсуляцию. 
