
###  [Java 8 New Date/ Time API](https://vertex-academy.com/tutorials/ru/java-8-new-date-time-api-chast-7) ###

2023-12-12 14:13

Главные проблемы в работе с датой и временем версий [Java 7](https://javadevblog.com/category/java/osobennosti-java-7) и ниже:
1. Классы Java Date Time раскиданы по пакетам. Так, класс [Date](Date) есть как в пакете `java.util`, так и `в` `java.sql` пакете. Классы для форматирования и парсинга определены в `java.text` пакете.
2. Пакет [java.util.Date](Date) содержит как дату, так и время, в то время как `java.sql.Date` содержит только дату. Оба класса не очень хорошо спроектированы.
3. Все классы для работы с датой могут изменяться, поэтому они не [потокобезопасны](https://javadevblog.com/category/java/mnogopotochnost-i-parallelizm). Это одна из самых больших проблем в [Date](Date) и [Calendar](Calendar) классах.
4. Класс [Date](Date) не обеспечивает интернационализацию, не поддерживает часовые пояса. Поэтому были введены классы [java.util.Calendar](Calendar) и `java.util.TimeZone`, но опять-таки, они имеют все перечисленные выше проблемы.

Java 8 Date Time API предназначена заменить старые классы для работы со временем и датой. Давайте рассмотрим основные пакеты нового API.

1. Пакет `java.time` — Это базовый пакет нового Date Time API. Все основные базовые классы являются частью этого пакета: `LocalDate`, `LocalTime`, `LocalDateTime`, `Instant`, `Period`, `Duration` и другие. Все эти классы являются неизменными и потокобезопасными. В большинстве случаев, этих классов будет достаточно для большинства задач.
2. Пакет `java.time.chrono` — пакет с общими интерфейсами для не календарных систем ISO. Мы можем наследовать класс `AbstractChronology` для создания собственной календарной системы.
3. Пакет `java.time.format` — пакет с классами форматирования и парсинга времени и даты. В большинстве случаев, мы не будем использовать их напрямую, потому что классы в пакете `java.time` предоставляют удобные методы для форматирования и парсинга.
4. Пакет `java.time.temporal` используется для работы с временными объектами, например, с помощью него мы можем узнать первый или последний день месяца. Методы таких классов сразу заметны на фоне других, потому что всегда имеют формат ‘`withXXX`‘.
5. Пакет `java.time.zone` — классы для поддержки различных часовых поясов и правила их изменения.

Список новых классов в java.time:
- **LocalDate –** дата без времени и временных зон;
- **LocalTime** **–** время без даты и временных зон;
- **LocalDateTime** **–** дата и время без временных зон;
- **ZonedDateTime** **–** дата и время с временной зоной;
- **DateTimeFormatter** **–** форматирует даты в строки и наоборот, только для классов **java.time;**
- **Instant** **–** количество секунд с **Unix** **epoch time** (полночь 1 января 1970 UTC);
- **Duration** **–** продолжительность в секундах и наносекундах;
- **Period** **–** период времени в годах, месяцах и днях;
- **TemporalAdjuster** **–** корректировщик дат (к примеру, может получить дату следующего понедельника).
#### Как получить текущую дату и/или время? ####

В **_Java 8_** - легко. У классов **LocalDate**, **LocalTime** и **LocalDateTime** есть статический метод **_now(),_** который и возвращает текущую дату, время

LocalDate.now(); // 2018-01-20 LocalTime.now(); // 08:07:35.113028 LocalDateTime.now();// 2018-01-20T08:07:35.113120
```java
LocalDate.now(); // 2018-01-20
LocalTime.now(); // 08:07:35.113028
LocalDateTime.now();// 2018-01-20T08:07:35.113120|
```
Стоит отметить, что отображается именно локальное время, не привязанное к какой-либо временной зоне.
#### Как задать нужную дату? ####

Используя следующие методы:
```java
LocalDate.of(2020, Month.SEPTEMBER, 23); // 2020-09-23
LocalDate.of(2021, 1, 1); // 2021-01-01
LocalDate.ofYearDay(2020, 361); // 2020-12-26
```
Метод _**of()**_ перегружен и принимает год, месяц (либо _**[enum](Enum)**_, либо номер месяца) и день. Метод **_ofYearDay()_** принимает год и день года, начиная с 1 до 365/366. Данные методы, на практике, используются чаще всего, но также есть методы _**ofEpochDate()**_ и _**ofInstant().**_
#### Как задать нужное время? ####

Используя методы **_of(), ofSecondsOfDay(), ofNanoOfDay()_**
```java
LocalTime.of(12, 10); // 12:10
LocalTime.of(18, 15, 10); // 18:15:10
LocalTime.of(23, 59, 59, 700); // 23:59:59.000000700
LocalTime.ofSecondOfDay(9_124); // 02:32:04
LocalTime.ofNanoOfDay(100_000_000_000L); // 00:01:40
```
Метод _**of()**_ перегружен и принимает часы, минуты + секунды + наносекунды. Метод _**ofSecondsOfDay()**_ принимает количество секунд с начала дня, а метод **_ofNanoOfDay()_**
количество наносекунд. Также есть метод **_ofInstant(),_** но он используется не так часто.
#### Как задать нужную дату и время? ####

Поскольку **LocalDateTime** является объединением **LocalDate** и **LocalTime**, то и методы их схожи
```java
LocalDateTime.of(1992, Month.AUGUST, 24, 12, 0); // 1992-08-24T12:00
LocalDateTime.of(2004, Month.AUGUST, 23, 17, 15, 2); // 2004-08-23T17:15:02
LocalDateTime.of(2008, Month.JANUARY, 6, 20, 45, 2, 2); // 2008-01-06T20:45:02.000000002
LocalDateTime.of(2009, 1, 13, 9, 7); // 2009-01-13T09:07
LocalDateTime.of(2012, 4, 4, 6, 16); // 2012-04-04T06:16
LocalDateTime.of(2018, 10, 14, 4, 20); // 2018-10-14T04:20
LocalDateTime.of(LocalDate.now(), LocalTime.now()); // 2018-01-20T09:19:48.603054
```
Как видим, дата и время разделены буквой 'T'. Метод _**of()**_ также может принимать **LocalDate** и **LocalTime**_**,**_ что упрощает получение даты и времени.
#### Добавление в LocalDate ####

Для добавления нескольких дней или чего-то другого в **LocalDate** существуют методы _**plus(), plusDays(),  plusWeeks(), plusMonths()**_
```java
LocalDate now = LocalDate.now(); // 2018-01-21
LocalDate plus2Days = now.plusDays(2); // 2018-01-23
LocalDate plusWeek = now.plusWeeks(1); // 2018-01-28
LocalDate plus3Months = now.plusMonths(3); // 2018-04-21
LocalDate plusPeriod = now.plus(Period.ofDays(3)); // 2018-01-24
LocalDate plusMillennia = now.plus(1, ChronoUnit.MILLENNIA); // 3018-01-21
```
При добавлении к **LocalDate** всегда создается новый экземпляр класса т.к. все классы в новом **API** являются **неизменяемыми.**

Метод _**plus()**_ перегружен и принимает либо **TemporalAmount** (интерфейс, реализации - **Duration, Period**) либо количество того, что мы хотим добавить и собственно **ChronoUnit** (enum, есть значение от **NANOS** до **FOREVER**). Не все **ChronoUnit** являются валидными для **LocalDate**. К примеру, нельзя добавить время (секунды, минуты часы и тд.) и бесконечность.

#### Отнимание в LocalDate ####

Отнимание схоже с добавлением.
```java
LocalDate now = LocalDate.now(); // 2018-01-21
LocalDate minusDays = now.minusDays(3); // 2018-01-18
LocalDate minusWeeks = now.minusWeeks(2); // 2018-01-07
LocalDate minusMonths = now.minusMonths(4); // 2017-09-21
LocalDate minusPeriod = now.minus(Period.ofDays(1)); // 2018-01-20
LocalDate minusEras = now.minus(1, ChronoUnit.CENTURIES); // 1918-01-21
```
Насчет **ChronoUnit** действуют те же правила, что и для добавления.

Забавно то, что можно отнять отрицательное число (как и добавить отрицательное) и это будет валидно!
```java
LocalDate now = LocalDate.now(); // 2018-01-21
LocalDate plusNegative = now.plusDays(-1); // 2018-01-20
LocalDate minusNegative = now.minusDays(-1); // 2018-01-22
```
#### Добавление в LocalTime ####

Добавить к **LocalTime** можно от наносекунд до полудня
```java
LocalTime now = LocalTime.now(); // 08:49:39.678703
LocalTime plusNanos = now.plusNanos(100_000); // 08:49:39.678803
LocalTime plusSeconds = now.plusSeconds(20); // 08:49:59.678703
LocalTime plusMinutes = now.plusMinutes(20); // 09:09:39.678703
LocalTime plusHours = now.plusHours(6); // 14:51:58.601216
LocalTime plusMillis = now.plus(Duration.ofMillis(100)); // 08:49:39.778703
LocalTime plusHalfDay = now.plus(1, ChronoUnit.HALF_DAYS); // 20:49:39.678703
```
В данном случае валидными **ChronoUnit** считаются только те, которые относятся ко времени, а не датам. К примеру, при использовании **ChronoUnit.DAYS** мы получим **UnsupportedTemporalTypeException.**
#### Отнимание в LocalTime ####

Все так же как и в добавлении
```java
LocalTime now = LocalTime.now(); // 08:57:19.743004
LocalTime minusNanos = now.minusNanos(100_000); // 08:57:19.742904
LocalTime minusSeconds = now.minusSeconds(20); // 08:56:59.743004
LocalTime minusMinutes = now.minusMinutes(20); // 08:37:19.743004
LocalTime minusHours = now.minusHours(6); // 02:57:19.743004
LocalTime minusMillis = now.minus(Duration.ofMillis(100)); // 08:57:19.643004
LocalTime minusHalfDay = now.minus(1, ChronoUnit.HALF_DAYS); // 20:57:19.743004
```
Не баг а фича с отрицательным добавлением/отниманием также работает.
#### Добавление и отнимание в LocalDateTime ####

Поскольку **LocalDateTime** это и дата и время, то методы по добавлению/отниманию просто делегируют исполнение методам из **LocalDate** и **LocalTime.**

Добавление
```java
LocalDateTime now = LocalDateTime.now(); // 2018-01-21T09:11:48.486298
LocalDateTime minusNanos = now.plusNanos(780_000_000); // 2018-01-21T09:11:49.266298
LocalDateTime minusSeconds = now.plusSeconds(59); // 2018-01-21T09:12:47.486298
LocalDateTime minusMinutes = now.plusMinutes(5); // 2018-01-21T09:16:48.486298
LocalDateTime minusHours = now.plusHours(3); // 2018-01-21T12:11:48.486298
LocalDateTime minusDays = now.plusDays(7); // 2018-01-28T09:11:48.486298
LocalDateTime minusWeeks = now.plusWeeks(3); // 2018-02-11T09:11:48.486298
LocalDateTime minusMonths = now.plusMonths(5); // 2018-06-21T09:11:48.486298
LocalDateTime minusYears = now.plusYears(2); // 2020-01-21T09:11:48.486298
LocalDateTime minusPeriod = now.plus(Period.ofWeeks(2)); // 2018-02-04T09:11:48.486298
LocalDateTime minusDecades = now.plus(1, ChronoUnit.DECADES); // 2028-01-21T09:11:48.48629
```
Отнимание
```java
LocalDateTime now = LocalDateTime.now(); // 2018-01-21T09:09:33.650251
LocalDateTime minusNanos = now.minusNanos(780_000_000); // 2018-01-21T09:09:32.870251
LocalDateTime minusSeconds = now.minusSeconds(59); // 2018-01-21T09:08:34.650251
LocalDateTime minusMinutes = now.minusMinutes(5); // 2018-01-21T09:04:33.650251
LocalDateTime minusHours = now.minusHours(3); // 2018-01-21T06:09:33.650251
LocalDateTime minusDays = now.minusDays(7); // 2018-01-14T09:09:33.650251
LocalDateTime minusWeeks = now.minusWeeks(3); // 2017-12-31T09:09:33.650251
LocalDateTime minusMonths = now.minusMonths(5); // 2017-08-21T09:09:33.650251
LocalDateTime minusYears = now.minusYears(2); // 2016-01-21T09:09:33.650251
LocalDateTime minusPeriod = now.minus(Period.ofWeeks(2)); // 2018-01-07T09:09:33.650251
LocalDateTime minusDecades = now.minus(1, ChronoUnit.DECADES); // 2008-01-21T09:09:33.65025
```
И тут также работает фишка с отрицательным добавление/отниманием (методы ведь делегируют все). **ChronoUnit** в этом случае можно выбирать любой (кроме бесконечности, конечно же).
#### Сравнение дат ####

Для сравнения **LocalDate** существует два метода - _**isAfter()**_ а так же _**isBefore()**_
```java
LocalDate now = LocalDate.now();
LocalDate _2017 = LocalDate.of(2017, 9, 23);
boolean after = now.isAfter(_2017);// true
boolean before = now.isBefore(_2017);// false
```
#### Сравнение времени ####

Сравнение **LocalTime** так же просто, как и в случае с **LocalDate -** те же методы и та же логика
```java
LocalTime now = LocalTime.now();
LocalTime _2HoursAfter = now.plusHours(2);
boolean after = now.isAfter(_2HoursAfter); // false
boolean before = now.isBefore(_2HoursAfter); // true
```
#### Сравнение дат и времени ####

Нечего и добавить, все так же как и в случае с **LocalDate** и **LocalTime**
```java
LocalDateTime now = LocalDateTime.now();
LocalDateTime monthAgo = now.minusMonths(1);
boolean after = now.isAfter(monthAgo); // true
boolean before = now.isBefore(monthAgo); // false
```
Во всех трёх классах при сравнении используется метод _**compareTo()**_, который можно вызвать и самостоятельно
```java
LocalDate localDate = LocalDate.now();
LocalDate tomorrow = LocalDate.now().plusDays(1);
boolean isDateAfter = localDate.compareTo(tomorrow) &gt; 0; // false
 
LocalTime localTime = LocalTime.now();
LocalTime hourLater = localTime.plusHours(1);
boolean isTimeBefore = localTime.compareTo(hourLater) &lt; 0; // true
 
 
LocalDateTime localDateTime = LocalDateTime.now();
LocalDateTime lastYear = localDateTime.minusYears(1);
boolean isDateTimeAfter = localDateTime.compareTo(lastYear) &gt; 0; // true
```
Но зачем, когда есть такие методы как _**isAfter()**_ и _**isBefore()**_
### Форматирование дат и времени ###

Для форматирования в новом **Date/Time API** есть класс **DateTimeFormatter,** который умеет форматировать как **LocalDate** и **LocalTime,** так и **LocalDateTime.**
#### Форматирование LocalDate ####

В **DateTimeFormatter** существует множество предопределенных форматов, к примеру
```java
LocalDate now = LocalDate.now();
String basicIsoDate = now.format(DateTimeFormatter.BASIC_ISO_DATE); // 20180128
String isoDate = now.format(DateTimeFormatter.ISO_DATE); // 2018-01-28
String isoWeekDate = now.format(DateTimeFormatter.ISO_WEEK_DATE); // 2018-W04-7
String isoLocalDate = now.format(DateTimeFormatter.ISO_LOCAL_DATE); // 2018-01-28
String isoOrdinalDate = now.format(DateTimeFormatter.ISO_ORDINAL_DATE); // 2018-028
```
Если же нужного нам формата нет, всегда можно задать свой
```java
LocalDate now = LocalDate.now();
String native = now.format(DateTimeFormatter.ofPattern("dd MMM yyyy")); // 28 Jan 2018
String french = now.format(DateTimeFormatter.ofPattern("dd MMM yyyy", Locale.FRANCE)); // 28 janv. 2018
```
#### Форматирование LocalTime ####

С **LocalTime** примерно та же история, что и с **LocalDate** (что уже не удивительно) - несколько уже созданных форматов
```java
LocalTime now = LocalTime.now();
String isoLocalTime = now.format(DateTimeFormatter.ISO_LOCAL_TIME); // 08:09:31.514569
String isoTime = now.format(DateTimeFormatter.ISO_TIME); // 08:09:31.514569
```
**ISO_TIME** в отличие от **ISO_LOCAL_TIME**  может включать временной сдвиг (offset), если он есть. Подробнее разберем этот случай в следующей статье.

Также есть возможность задать свой формат
```java
LocalTime now = LocalTime.now();
String nativeFormat = now.format(DateTimeFormatter.ofPattern("hh:mm:ss ")); // 08:10:43
String engFormat = now.format(DateTimeFormatter.ofPattern("h:mm a")); // 08:10 AM
```
#### Форматирование LocalDateTime ####

Здесь уже больше возможностей для форматирования, ведь у нас есть и дата и время
```java
LocalDateTime now = LocalDateTime.now();
String rfcFormat = now.format(DateTimeFormatter.ofPattern("E, dd MMM yyyy hh:mm:ss")); // Sun, 28 Jan 2018 08:24:31
String basicIsoDate = now.format(DateTimeFormatter.BASIC_ISO_DATE); // 20180128
String isoDateTime = now.format(DateTimeFormatter.ISO_DATE_TIME); // 2018-01-28T08:24:31.412511
String isoLocalDateTime = now.format(DateTimeFormatter.ISO_LOCAL_DATE_TIME); // 2018-01-28T08:24:31.412511
String isoLocalDate = now.format(DateTimeFormatter.ISO_LOCAL_DATE); // 2018-01-28
```
#### Базовая работа с  ZonedDateTime ####

Создать **ZonedDateTime** можно так же как и **LocalDateTime**.
```java
ZonedDateTime now = ZonedDateTime.now(); // 2018-02-10T08:49:50.886682+01:00[Europe/Warsaw]
 
LocalDate localDate = LocalDate.of(2018, 1, 1);
LocalTime localTime = LocalTime.of(10, 30);
ZoneId zone = ZoneId.of("Europe/Kiev");
ZonedDateTime kievTime = ZonedDateTime.of(localDate, localTime, zone); // 2018-01-01T10:30+02:00[Europe/Kiev]
```
да и вообще **ZonedDateTime** просто-напросто содержит внутри себя **LocalDateTime** и **ZoneId.** Так что вы уже умеете добавлять, отнимать дату и время, а так же форматировать и сравнивать **ZonedDateTime.**
#### Конвертация ZonedDateTime между зонами ####

Конвертация между временными зонами происходит с помощью метода withZoneSameInstant()
```java
LocalDate localDate = LocalDate.of(2018, 1, 1);
LocalTime localTime = LocalTime.of(10, 30);
ZoneId zone = ZoneId.of("Europe/Kiev");
 
ZonedDateTime kievTime = ZonedDateTime.of(localDate, localTime, zone); // 2018-01-01T10:30+02:00[Europe/Kiev]
ZonedDateTime nyTime = kievTime.withZoneSameInstant(ZoneId.of("America/New_York")); // 2018-01-01T03:30-05:00[America/New_York]
ZonedDateTime japanTime = kievTime.withZoneSameInstant(ZoneOffset.of("-09:00")); // 2017-12-31T23:30-09:00
```
Временную зону можно указывать либо с помощью **ZoneId** либо с помощью **ZoneOffset** в случае, если вы не знаете id города/страны.
#### Как получить все временные зоны ####

Вот так
```java
List<String> zones = new ArrayList<>(ZoneId.getAvailableZoneIds());
zones.forEach(System.out::println);
```
Данный код выведет все id временных зон, но без указания смещения (**offset**). Для вывода временных зон со смещением можно использовать следующий код
```java
public class Example {
    private static final LocalDateTime LDT = LocalDateTime.now();
 
    public static void main(String[] args) {
        List<String> zones = new ArrayList<>(ZoneId.getAvailableZoneIds());
 
        Map<String, String> map = zones.stream()
                .collect(Collectors.toMap(zone -> zone, Example::getOffset));
 
        TreeMap<String, String> sortedMap = new TreeMap<>(map);
        sortedMap.forEach((zone, offset) -> System.out.printf("%s (UTC%s) \n", zone, offset));
    }
 
    private static String getOffset(String zone) {
        ZonedDateTime zdt = LDT.atZone(ZoneId.of(zone));
        return zdt.getOffset().getId().replace("Z", "+00:00");
    }
}
```
#### Period ####

**Period** указывает временной промежуток между двумя датами. Допустим, вам понадобилось узнать сколько осталось дней до дня рождения пользователя
```java
LocalDate nextBirthday = LocalDate.of(2018, 9, 23);
LocalDate now = LocalDate.now();
 
Period period = Period.between(now, nextBirthday);
int days = period.getDays();
 
System.out.println(now);
System.out.println(period);
System.out.println(days);
```
Можно предположить, что _**getDays()**_ вернет количество дней до дня рождения. Так и будет, в буквальном смысле, ТОЛЬКО количество дней до дня рождения. Вывод в консоль ->
<p style="background-color: navy; color: yellow">2018-02-11<br>
P7M12D<br>
12</p>
Для того, чтобы вывести кол-во дней нормально, придется смотреть сколько дней в конкретном месяце, считать их самому и т.д.

Проще говоря, для такой задачи **Period** не очень подходит. Плюс ко всему с **Period** можно "переборщить"
```java
Period period = Period.of(1, 15, 40);
System.out.println(period); // P1Y15M40D
 
int days = period.getDays();
System.out.println(days); // 40
```
Почему так??? Дело в том, что **Period** не имеет ограничений по количеству месяцев, дней. Но эту ситуацию можно немного  исправить, для этого существует метод _**normalized()**_
```java
Period period = Period.of(1, 15, 60).normalized();
System.out.println(period); // P2Y3M60D
 
int days = period.getDays();
System.out.println(days); // 60
```
Количество дней никак не станет 30, 31, или 29. Ведь продолжительность не привязана к месяцам. Но если мы добавим **Period** к дате, все встанет на свои места.
```java
Period period = Period.of(1, 15, 60);
LocalDate localDate = LocalDate.of(2018, 1, 1);
LocalDate plus = localDate.plus(period); // 2020-05-31
```
#### Duration ####

**Duration**, по сути, исполняет ту же роль, что и **Period** но измеряет все в часах, минутах, секундах ...
```java
LocalTime _10AM = LocalTime.of(10, 10,15);
LocalTime _9PM = LocalTime.of(21, 30);
 
Duration duration = Duration.between(_10AM, _9PM); // PT11H19M45S
```
Вот с помощью **Duration** можно решить нашу проблему с днём рождения, правда с маленькой хитростью.
```java
LocalDate localDate = LocalDate.of(2018, 2, 11);
LocalDate birthday = LocalDate.of(2018, 9, 23);
 
Duration duration = Duration.between(localDate.atStartOfDay(), birthday.atStartOfDay());
System.out.println(duration.toDays()); // 224
```
**Duration** не работает с **LocalDate,** зато с **LocalDateTime** еще как. Преобразовав одно в другое с помощью метода _**atStartOfDay()**_**,** мы можем получить **Duration,** а уже у него получить количество дней.

Конечно, можно пойти путем еще проще, используя класс **ChronoUnit**
```java
LocalDate localDate = LocalDate.of(2018, 2, 11);
LocalDate birthday = LocalDate.of(2018, 9, 23);
 
long daysToBirthday = ChronoUnit.DAYS.between(localDate, birthday); // 224
```
Это еще раз доказывает, что существует множество вариантов решения одной и той же задачи. Не все из них хороши, не все так изящны. Но чем больше вариантов вы знаете, тем больше возможностей у вас есть.

### TemporalAdjusters ###

С помощью **TemporalAdjusters** можно решать довольно специфические задачи, к примеру, узнать какое число будет в следующее воскресенье или получить последний день месяца (кто знает, зачем он вам понадобился). Такое не каждый день пригодится, но раз в году и ... сами знаете что, поэтому знать будет полезно.

Например, мы хотим узнать дату **4-го воскресенья в месяце** - не проблема:
```java
LocalDate localDate = LocalDate.of(2018, Month.AUGUST, 24);
TemporalAdjuster fourthSunday = TemporalAdjusters.dayOfWeekInMonth(4, DayOfWeek.SUNDAY);
System.out.println(localDate.with(fourthSunday)); // 2018-08-26
```
Возможно, мы хотим узнать дату "страшного дня" - **первый понедельник месяце**
```java
LocalDate localDate = LocalDate.of(2017, Month.MARCH, 19);
TemporalAdjuster firstMonInMonth = TemporalAdjusters.firstInMonth(DayOfWeek.MONDAY);
System.out.println(localDate.with(firstMonInMonth));
```
Или же нам хочется узнать, сколько осталось до "сладостного дня" - **последней пятницы**
```java
LocalDate localDate = LocalDate.of(2017, Month.April, 21);
TemporalAdjuster lastFriInMonthAdjuster = TemporalAdjusters.lastInMonth(DayOfWeek.FRIDAY);
LocalDate lastFri = localDate.with(lastFriInMonthAdjuster); // 2017-04-28
 
Period until = localDate.until(lastFri);
System.out.println(until.getDays()); // 7
```
Хотим всё первое? Да легко
```java
LocalDate localDate = LocalDate.of(2017, Month.MAY, 10);
 
TemporalAdjuster firstDayOfMonth = TemporalAdjusters.firstDayOfMonth();
TemporalAdjuster firstDayOfNextMonth = TemporalAdjusters.firstDayOfNextMonth();
TemporalAdjuster firstDayOfYear = TemporalAdjusters.firstDayOfYear();
TemporalAdjuster firstDayOfNextYear = TemporalAdjusters.firstDayOfNextYear();
 
System.out.println(localDate.with(firstDayOfMonth)); // 2017-04-01
System.out.println(localDate.with(firstDayOfNextMonth)); // 2017-05-01
System.out.println(localDate.with(firstDayOfYear)); // 2017-01-01
System.out.println(localDate.with(firstDayOfNextYear)); // 2018-01-01
```
Нужно узнать **последний день месяца или года**? Все невозможное возможно
```java
LocalDate localDate = LocalDate.of(2017, Month.APRIL, 17);
 
TemporalAdjuster lastDayOfMonth = TemporalAdjusters.lastDayOfMonth();
TemporalAdjuster lastDayOfYear = TemporalAdjusters.lastDayOfYear();
 
System.out.println(localDate.with(lastDayOfMonth)); // 2017-04-30
System.out.println(localDate.with(lastDayOfYear)); // 2017-12-31
```
Срочно спросили **когда будет следующий вторник**, а вы не знаете? TemporalAdjusters всегда поможет
```java
LocalDate localDate = LocalDate.of(2020, Month.OCTOBER, 28);
TemporalAdjuster nextTue = TemporalAdjusters.next(DayOfWeek.TUESDAY);
System.out.println(localDate.with(nextTue)); // 2020-11-03
```
И еще один похожий метод может прийти на помощь
```java
LocalDate localDate = LocalDate.of(2020, Month.OCTOBER, 28);
 
TemporalAdjuster nextOrSameWed = TemporalAdjusters.nextOrSame(DayOfWeek.WEDNESDAY);
System.out.println(localDate.with(nextOrSameWed)); // 2020-10-28
```
Особенность его в том, что если текущий день недели совпадает с желаемым, то он таким и останется. Отсюда и название, _**nextOrSame.**_

И еще два метода на эту же тематику
```java
LocalDate localDate = LocalDate.of(2020, Month.OCTOBER, 28);
 
TemporalAdjuster previousThu = TemporalAdjusters.previous(DayOfWeek.THURSDAY);
TemporalAdjuster previousOrSameSat = TemporalAdjusters.previousOrSame(DayOfWeek.SATURDAY);
 
System.out.println(localDate.with(previousThu)); // 2020-10-22
System.out.println(localDate.with(previousOrSameSat)); // 2020-10-24
```