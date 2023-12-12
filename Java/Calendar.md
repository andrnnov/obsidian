#Java #Calendar #GregorianCalendar

### Java Calendar ###

2023-12-12 10:46

В версии Java 1.1 появился новый класс — **`Calendar`**. Он сделал работу с датами в Java несколько проще, чем она выглядела раньше. Единственной реализацией класса Calendar, с которой мы и будем работать, является класс GregorianCalendar (он реализует Григорианский календарь, по которому живет большинство стран мира). Его основное удобство заключается в том, что он умеет работать с датами в более удобном формате. Например, он может:
- Прибавить к текущей дате месяц или день
- Проверить, является ли год високосным;
- Получить отдельные компоненты даты (например, получить из целой даты номер месяца)
- А также — внутри него разработана очень удобная система констант.

Еще одним важным отличием класса Calendar является то, что в нем реализована константа Calendar.Era: можно установить для даты эру BC (_“Before Christ” - до рождества Христова, т.е. “до нашей эры”_) или AC (_“After Christ” - “наша эра”_).

Существует несколько конструкторов для объектов GregorianCalendar:

|   |   |
|---|---|
|№|Конструктор и его описание|
|1|**GregorianCalendar()**  <br>Создает значение GregorianCalendar, используя по умолчанию текущей датой и временем, локализацией и часовым поясом.|
|2|**GregorianCalendar(int year, int month, int date)**  <br>Создает GregorianCalendar в соответствии с заданной датой в часовом поясе и локализацией по умолчанию.|
|3|**GregorianCalendar(int year, int month, int date, int hour, int minute)**  <br>Создает GregorianCalendar в соответствии с заданной датой и временем в часовом поясе и локализацией по умолчанию.|
|4|**GregorianCalendar(int year, int month, int date, int hour, int minute, int second)**  <br>Создает GregorianCalendar в соответствии с заданной датой и временем в часовом поясе и локализацией по умолчанию.|
|5|**GregorianCalendar(Locale aLocale)**  <br>Создает GregorianCalendar в соответствии с текущим временем в часовом поясе по умолчанию в рамках заданной локализации.|
|6|**GregorianCalendar(TimeZone zone)**  <br>Конструирует GregorianCalendar, основанный на текущем времени в данной зоне времени с локализацией по умолчанию.|
|7|**GregorianCalendar(TimeZone zone, Locale aLocale)**  <br>Конструирует GregorianCalendar, основанный на текущем времени в заданном часовом поясе и локализации.|

Список нескольких полезных методов, предоставляемых классом GregorianCalendar:

|   |   |
|---|---|
|№|Методы с описанием|
|1|**void add(int field, int amount)**  <br>Добавляет указанное количество времени в данное временное поле в соответствии с правилами календаря.|
|2|**protected void computeFields()**  <br>Преобразует время по Гринвичу в миллисекунды до значения полей времени.|
|3|**protected void computeTime()**  <br>Преобразует значения временного поля Календаря в UTC формате в миллисекундах.|
|4|**boolean equals(Object obj)**  <br>Сравнивает этот GregorianCalendar эталонным объектом.|
|5|**int get(int field)**  <br>Получает значение для поля заданного времени.|
|6|**int getActualMaximum(int field)**  <br>Возвращает максимальное значение, которое это поле может иметь, учитывая текущую дату.|
|7|**int getActualMinimum(int field)**  <br>Возвращает минимальное значение, которое это поле может иметь, учитывая текущую дату.|
|8|**int getGreatestMinimum(int field)**  <br>Возвращает наибольшее минимальное значение для данного поля, если изменяется.|
|9|**Date getGregorianChange()**  <br>Получает изменения даты по григорианскому календарю.|
|10|**int getLeastMaximum(int field)**  <br>Возвращает минимально максимальное значение для данного поля, если изменяется.|
|11|**int getMaximum(int field)**  <br>Возвращает максимальное значение для данного поля.|
|12|**Date getTime()**  <br>Определяет текущее время в соответствии с календарем.|
|13|**long getTimeInMillis()**  <br>Получает текущее время по Календарю как длительное.|
|14|**TimeZone getTimeZone()**  <br>Возвращает часовой пояс.|
|15|**int getMinimum(int field)**  <br>Возвращает минимальное значение для данного поля.|
|16|**int hashCode()**  <br>Переопределите хэш-код.|
|17|**boolean isLeapYear(int year)**  <br>Определяет, является ли год високосным.|
|18|**void roll(int field, boolean up)**  <br>Добавление или вычитание (вверх/вниз) одной единицы времени в данном временном поле без изменений в больших полях.|
|19|**void set(int field, int value)**  <br>Устанавливает временное поле с заданным значением.|
|20|**void set(int year, int month, int date)**  <br>Задает значения для поля год, месяц и дата.|
|21|**void set(int year, int month, int date, int hour, int minute)**  <br>Задает значения для поля год, месяц, дату, час и минуту.|
|22|**void set(int year, int month, int date, int hour, int minute, int second)**  <br>Задает значения для поля год, месяц, дату, час, минуту и секунду.|
|23|**void setGregorianChange(Date date)**  <br>Устанавливает дату изменения грегорианского календаря.|
|24|**void setTime(Date date)**  <br>Устанавливает в соответствии с данным календарем текущее время с заданной датой.|
|25|**void setTimeInMillis(long millis)**  <br>Устанавливает в соответствии с данным календарем текущее время от заданного long значения.|
|26|**void setTimeZone(TimeZone value)**  <br>Задает часовой пояс со значением заданного часового пояса.|
|27|**String toString()**  <br>Возвращает строковое представление календаря.|

Создадим календарь с датой 25 января 2017 года:
```java
public static void main(String[] args) {
  Calendar calendar = new GregorianCalendar(2017, 0 , 25);
}
```
Месяцы в классе `Calendar` (как и в `Date`, кстати) начинаются с нуля, поэтому мы передали число 0 в качестве второго аргумента. Главное при работе с классом `Calendar` — понимать, что это именно календарь, а не отдельная дата.

Дата — это просто несколько чисел, обозначающих конкретный промежуток времени. А календарь - это целое устройство, с помощью которого можно много чего с датами делать:) Это достаточно хорошо видно, если попробовать вывести объект Calendar в консоль. 
Вывод:
<p style="color: yellow">java.util.GregorianCalendar[time=?,areFieldsSet=false,areAllFieldsSet=false,lenient=true,<br>zone=sun.util.calendar.ZoneInfo[id="Europe/Moscow",offset=10800000,dstSavings=0,<br>useDaylight=false,transitions=79,lastRule=null],firstDayOfWeek=2,minimalDaysInFirstWeek=1,<br>ERA=?,YEAR=2017,MONTH=0,WEEK_OF_YEAR=?,WEEK_OF_MONTH=?,DAY_OF_MONTH=25,<br>DAY_OF_YEAR=?,DAY_OF_WEEK=?,DAY_OF_WEEK_IN_MONTH=?,AM_PM=0,HOUR=0,<br>HOUR_OF_DAY=0,MINUTE=0,SECOND=0,MILLISECOND=?,ZONE_OFFSET=?,DST_OFFSET=?]</p>
У календаря есть куча свойств, которыми не обладает обычная дата, и все они выводятся в консоль (так работает метод `toString()` в классе `Calendar`). Если при работе тебе нужно просто получить из календаря простую дату, т.е. объект `Date` — это делается при помощи метода `Calendar.getTime()` (название не самое логичное, но тут уж ничего не поделаешь):
```java
public static void main(String[] args) {

   Calendar calendar = new GregorianCalendar(2017, 0 , 25);
   Date date = calendar.getTime();
   System.out.println(date);
}
```
Вывод:
<p style="background-color: navy; color: yellow">Wed Jan 25 00:00:00 MSK 2017</p>
Помимо цифровых обозначений месяцев, в классе `Calendar` можно использовать константы. Константы — это статические поля класса `Calendar` с уже установленным значением, которое нельзя изменить. Этот вариант на самом деле даже лучше, поскольку такое написание улучшает читаемость кода.
```java
public static void main(String[] args) {
   GregorianCalendar calendar = new GregorianCalendar(2017, Calendar.JANUARY , 25);
}
```
`Calendar.JANUARY` — одна из констант для обозначения месяца. При таком варианте именования никто не забудет, например, что цифра “3” обозначает апрель, а не привычный нам третий по счету месяц - март. Просто пишешь `Calendar.APRIL` - и все:)

Все поля календаря (число, месяц, минуты, секунды и т.д.) можно устанавливать по отдельности с помощью метода `set()`. Он очень удобен, поскольку в классе `Calendar` для каждого поля выделена своя константа, и итоговый код будет выглядеть максимально просто. Например, в прошлом примере мы создали дату, но не установили для нее текущее время. Давай установим время 19:42:12
```java
public static void main(String[] args) {
   Calendar calendar = new GregorianCalendar();
   calendar.set(Calendar.YEAR, 2017);
   calendar.set(Calendar.MONTH, 0);
   calendar.set(Calendar.DAY_OF_MONTH, 25);
   calendar.set(Calendar.HOUR_OF_DAY, 19);
   calendar.set(Calendar.MINUTE, 42);
   calendar.set(Calendar.SECOND, 12);

   System.out.println(calendar.getTime());
}
```
Вывод:
<p style="background-color: navy; color: yellow">Wed Jan 25 19:42:12 MSK 2017</p>
Мы вызываем метод `set()`, передаем в него константу (в зависимости от того поля, которое хотим изменить) и новое значение для этого поля. Получается, что метод `set()` — эдакий “супер-сеттер”, который умеет устанавливать значение не для одного поля, а для множества полей. 

Прибавление и вычитание значений в классе `Calendar` осуществляется с помощью метода `add()`. В него необходимо передать то поле, которое ты хочешь изменить, и число - сколько именно ты хочешь прибавить/убавить от текущего значения. Например, вернем дату, которую мы создали, на 2 месяца назад:
```java
public static void main(String[] args) {
   Calendar calendar = new GregorianCalendar(2017, Calendar.JANUARY , 25);
   calendar.set(Calendar.HOUR, 19);
   calendar.set(Calendar.MINUTE, 42);
   calendar.set(Calendar.SECOND, 12);

   calendar.add(Calendar.MONTH, -2);//чтобы отнять значение - в метод нужно передать отрицательное число
   System.out.println(calendar.getTime());
}
```
Вывод:
<p style="background-color: navy; color: yellow">Fri Nov 25 19:42:12 MSK 2016</p>
Мы вернули дату на 2 месяца назад. В результате изменился не только месяц, но и год, с 2017 на 2016. Подсчет текущего года при переносе дат, конечно, выполняется автоматически и его не надо контролировать вручную. 

Но если для каких-то целей тебе нужно отключить это поведение — можно и так. Специальный метод `roll()` может прибавлять и убавлять значения, не затрагивая при этом остальные значения. К примеру, вот так:
```java
public static void main(String[] args) {
   Calendar calendar = new GregorianCalendar(2017, Calendar.JANUARY , 25);
   calendar.set(Calendar.HOUR, 10);
   calendar.set(Calendar.MINUTE, 42);
   calendar.set(Calendar.SECOND, 12);

   calendar.roll(Calendar.MONTH, -2);
   System.out.println(calendar.getTime());
}
```
Мы сделали ровно то же самое, что и в предыдущем примере — отняли 2 месяца от текущей даты. Но теперь код сработал по-другому: месяц поменялся с января на ноябрь, но год как был 2017-ым, так и остался! 
Вывод:
<p style="background-color: navy; color: yellow">Sat Nov 25 10:42:12 MSK 2017</p>
Все поля объекта `Calendar` можно получить по отдельности. За это отвечает метод `get()`:
```java
public static void main(String[] args) {
   GregorianCalendar calendar = new GregorianCalendar(2017, Calendar.JANUARY , 25);
   calendar.set(Calendar.HOUR, 10);
   calendar.set(Calendar.MINUTE, 42);
   calendar.set(Calendar.SECOND, 12);

   System.out.println("Год: " + calendar.get(Calendar.YEAR));
   System.out.println("Месяц: " + calendar.get(Calendar.MONTH));
   System.out.println("Порядковый номер недели в месяце: " + calendar.get(Calendar.WEEK_OF_MONTH));//порядковый номер недели в месяце

   System.out.println("Число: " + calendar.get(Calendar.DAY_OF_MONTH));

   System.out.println("Часы: " + calendar.get(Calendar.HOUR));
   System.out.println("Минуты: " + calendar.get(Calendar.MINUTE));
   System.out.println("Секунды: " + calendar.get(Calendar.SECOND));
   System.out.println("Миллисекунды: " + calendar.get(Calendar.MILLISECOND));
}
```
Вывод:
<p style="background-color: navy; color: yellow">Год: 2017 <br>
Месяц: 0 <br>
Порядковый номер недели в месяце: 4 <br>
Число: 25 <br>
Часы: 10 <br>
Минуты: 42 <br>
Секунды: 12 <br>
Миллисекунды: 0</p>
То есть помимо “супер-сеттера” в классе `Calendar` есть еще и “супер-геттер”.

Для создания даты “до нашей эры” нужно использовать поле `Calendar.Era` Например, создадим дату, обозначающую битву при Каннах, в которой Ганнибал победил войско Рима. Это произошло 2 августа 216 г. до н. э.:
```java
public static void main(String[] args) {
   GregorianCalendar cannes = new GregorianCalendar(216, Calendar.AUGUST, 2);
   cannes.set(Calendar.ERA, GregorianCalendar.BC);

   DateFormat df = new SimpleDateFormat("dd MMM yyy GG");
   System.out.println(df.format(cannes.getTime()));
}
```
Здесь мы использовали класс `SimpleDateFormat`, чтобы вывести дату в более понятном нам формате (буквы “GG” отвечают как раз за вывод эры). Вывод:
<p style="background-color: navy; color: yellow">02 авг 216 до н.э.</p>
#### SimpleDateFormat и Calendar ####

SimpleDateFormat позволит тебе форматировать все создаваемые объекты [Date](Date) и Calendar для последующего использования. Рассмотрим такой интересный момент как работа с эрами. Для создания даты “до нашей эры” нужно использовать поле Calendar.Era. Например, создадим дату, обозначающую битву при Каннах, в которой Ганнибал победил войско Рима. Это произошло 2 августа 216 г. до н. э.:

```java
public static void main(String[] args) {
   GregorianCalendar cannes = new GregorianCalendar(216, Calendar.AUGUST, 2);
   cannes.set(Calendar.ERA, GregorianCalendar.BC);

   DateFormat df = new SimpleDateFormat("dd MMM yyy GG");
   System.out.println(df.format(cannes.getTime()));
}
```
Здесь мы использовали класс SimpleDateFormat, чтобы вывести дату в более понятном нам формате (как указано выше, буквы “GG” отвечают как раз за вывод эры). Вывод:
<p style="background-color: navy; color: yellow">02 авг 216 до н.э.</p>
#### Java Date Format ###

А вот еще один случай. Предположим, что данный формат даты нас не устраивает:
<p style="color: yellow">Sat Nov 25 10:42:12 MSK 2017</p>
Так вот. С помощью наших возможностей в java date format его можно поменять его на свой собственный, без особых сложностей:
```java
public static void main(String[] args) {
   SimpleDateFormat dateFormat = new SimpleDateFormat("EEEE, d MMMM yyyy");
   Calendar calendar = new GregorianCalendar(2017, Calendar.JANUARY , 25);
   calendar.set(Calendar.HOUR, 10);
   calendar.set(Calendar.MINUTE, 42);
   calendar.set(Calendar.SECOND, 12);

   calendar.roll(Calendar.MONTH, -2);
   System.out.println(dateFormat.format(calendar.getTime()));
}
```
Вывод:
<p style="background-color: navy; color: yellow">суббота, 25 Ноябрь 2017</p>
