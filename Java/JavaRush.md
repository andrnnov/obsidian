Обучение на Java‑разработчика включает в себя 5 модулей с лекциями, практикой и итоговыми проектами (от новичка до уровня Junior-разработчика), а также финальный групповой проект.

МОДУЛЬ 1. JAVA SYNTAX.

#### Вводное занятие. Команды и первая программа на Java

- о преимуществах Java и его сферах применения
- о JavaRush и Java‑университете
- структура программы, метод `main`
- `sout`
- знакомство с сайтом и WebIDE

#### Работа с переменными, типы int и String

- охранение текста к переменной, вывод ее в консоли
- объявление и инициализация переменных `String`
- комментарии в коде
- элементарные математические операции с переменными типа `int`
- инкремент, декремент
- конкатенация
- `Integer.parseInt()`, `String.valueOf()`

#### Знакомство с типами и ввод с клавиатуры. Знакомство с IDEA

- хранение примитивных переменных в памяти
- хранения String переменных в памяти
- `byte`, `short`, `char`, `long`, `float`, `double`
- `System.in`, `Scanner`
- методы `Scanner`
- установка IDEA, скачивание проекта, скачивание JDK (версия 11)
- установка плагина, рассказ о его функционале

#### Условный оператор

- `if`, `if-else`, `if-else-if`
- блоки команд
- вложенные блоки команд (вложенные `if`-ы))
- тип boolean
- операторы сравнения, в т.ч. `double`
- логические `AND`, `OR`, `NOT`, `XOR`
- тернарний оператор
- сравнение примитивов и `String`

#### Факультатив

- подтягиваем новичков
- опытным рассказываем про фишки IDEA и т.п.
- компиляция класса в байт-код из консоли, запуск программы

#### Циклы

- проблематика на примере задачи сделать что-то много раз
- `while`
- `break`, `continue`
- `for`
- `do-while`
- сравнение разных циклов, выявление где какой лучше использовать

#### Массивы

- создание и заполнение массивов
- обход массива
- хранение массивов в памяти

#### Двумерные массивы

- двумерные массивы
- зубчатые массивы
- n-мерные массивы

#### Функции

- объявление и вызов методов
- параметры
- возвращаемое значение, `void`
- модификаторы доступа
- локальные переменные метода
- модификаторы методов, метод `main`

#### Работа со строками и продолжение предыдущей темы

- константы
- сокрытие переменных (shadowing)
- экранирование символов
- основные методы класса `String`

#### Факультатив

- литералы
- кодировки
- вспомогательные классы для работы со строками: `StringBuilder`, `String.format`
- утилитный класс `Arrays`

#### Типы данных. Знакомство с ООП

- примитивные типы
- приведение типов данных
- ссылочные типы
- объекты
- `null`
- знакомство с ООП
- наследование

#### Объекты

- создание объектов (`new`)
- конструктор, конструктор по умолчанию
- конструктор с параметрами
- порядок вызова конструкторов при наследовании
- доступ к полям объекта (геттер, сеттер)
- `hashCode`, `equals`

#### Классы и static

- статические переменные
- псравнение статических и нестатических переменных
- статические методы
- порядок инициализации при использовании конструкторов и статических блоков
- внутренние классы

#### Факультатив

- жизненный цикл объекта
- загрузка класса

#### Списки и Generics

- классы обертки
- `ArrayList`
- `Array` VS `ArrayList`
- типизация `ArrayList` (дженерики)

#### Коллекции

- иерархия коллекций
- `Set`, `HashSet`
- `iterator`, `for-each`

#### Коллекции

- `Map`, `HashMap`
- для каких задач лучше использовать какие коллекции
- `Collections`

#### Факультатив

- `LinkedList`
- `ArrayList` VS `LinkedList`
- `Queue`
- `SortedMap`, `TreeMap`

#### Singleton, Enum, switch

- зачем нужны перечисления
- объявления `Enum`
- `Enum` – лучший синглтон
- `switch`

#### Исключения

- нормальное выполнение кода и ошибки в рантайме
- `try-catch`
- иерархия исключений
- `multicatch`
- `throw`
- `checked` и `unchecked` исключения
- `throws`

#### Исключения

- `finally`
- создание своих исключений
- `Throwable`
- stack trace
- `try-with-resources`
- `AutoCloseable`

#### Факультатив

- Оборачивание исключения
- `Error`

#### Потоки ввода-вывода

- `InputStream`
- `Reader`
- `BufferedReader`
- `OutputStream`
- `Writer`
- `BufferedWriter`

#### Потоки ввода-вывода. Pattern Decorator

- `ByteArrayInputStream`
- `ByteArrayOutputStream`
- комбинирование потоков

#### Потоки ввода-вывода. java.nio

- io VS nio
- `FileChannel`
- `Selector`
- `Path`
- `Paths`
- `Files`

#### Работа со временем и датой

- `Date`
- `DateFormat`
- `Calendar`
- `LocalDate`, `LocalTime`, `LocalDateTime`
- `Instant`
- `ZonedDateTime`
- `DateTimeFormatter`

#### Git. Итоговый проект. (Крипто-анализатор)

МОДУЛЬ 2. JAVA CORE.

#### ООП: инкапсуляция, полиморфизм. Интерфейсы

- инкапсуляция
- полиморфизм
- приведение типов
- `this`, `super`
- интерфейсы

#### ООП: Перегрузка, переопределение, абстрактные классы

- абстрактный класс
- реализация абстрактных методов предка
- перегрузка (overload) методов - одинаковые названия
- переопределение (override) методов

#### Stream API

- анонимный внутренний класс
- реализация абстрактных методов предка
- лямбда выражения
- функциональные интерфейсы
- method reference
- `Stream`
- промежуточные и терминальные методы `Stream`-а
- `map-reduce`

#### ООП: композиция, агрегация, наследование

- ассоциация: композиция и агрегация
- наследование

#### Интерфейсы: сравнение с абстрактным классом, множественное наследование

- объявление поведения
- дефолтные методы
- реализация нескольких интерфейсов
- проблема “ромба”
- сравнение абстрактных классов и интерфейсов

#### Приведение типов, instanceof switch-expression

- `instanceof`
- приведение типов (расширение и сужение)
- `switch` expression, `Enum`

#### Особенности вызова конструкторов. Блок static

- процесс создание объекта
- порядок вызова конструкторов
- порядок инициализации переменных

#### Устройство Object: equals, hashCode, clone, toString(). Immutable objects

- класс `Object`
- методы класса `Object`
- mutable та immutable objects

#### Рекурсия

#### Знакомство с нитями: Thread, Runnable, start, sleep

- `Thread`
- `Runnable`
- `start`
- `sleep`
- `interrupt`

#### Знакомство с нитями: synchronized, volatile, wait, notify.DeadLock

- `synchronized`
- `volatile`
- `join`
- `wait`, `notify`
- проблема `DeadLock`

#### Executors

- `ExecutorService`
- патерн (шаблон) “фабричний метод”
- добавление задач в сервис
- `Callable`
- получение результата: `Future`
- остановка `ExecutorService`
- `FixedThreadPool`
- `CachedThreadPool`
- `ScheduledExecutorService`

#### ThreadLocal, Callable, Future

- `ThreadLocal` контекст
- `ThreadLocalRandom`

#### Внутренние/вложенные классы, примеры: Map.Entry

- вложенные классы
- внутренние классы
- внутренние статические классы
- внутренние анонимные классы
- примеры разных типов классов из JDK

#### Сериализация JSON/XML/YAML

- java сериализация
- форматы данных xml, json, yaml
- jackson `ObjectMapper`

#### Reflection API

- зачем нужен Reflection API
- получение данных: класса, метода, конструктора, поля
- создание объекта
- изменение внутреннего состояния объекта
- прокси
- RMI

#### Аннотации в Java

- декларативный и императивный подход написания кода
- популярные аннотации: `@Deprecated`, `@Override`, `@Nullable`, …
- создание аннотаций
- обработка аннотаций в рантайме

#### Факультатив

- работа с Swing

#### Sockets

- `Socket`
- `ServerSocket`
- live coding: написание примитивного чата для группы

#### Итоговый проект

МОДУЛЬ 3. JAVA PROFESSIONAL.

#### Сборка мусора и типы ссылок в Java

- память JVM: stack и heap
- CG: Serial, Parallel, CMS, G1, Shenandoah, ZGC
- кеш
- `WeakReference`, `SoftReference`, `PhantomReference`

#### Паттерны проектирования

- поведенческие: цепочка ответственности, команда, итератор, интерпретатор, посредник, хранитель, наблюдатель, состояние, стратегия, посетитель, шаблонный метод
- порождающие: прототип, строитель, синглтон, абстрактная фабрика, фабричный метод
- структурные: декоратор, компоновщик, фасад, приспособленец, прокси

#### Методологии разработки

- waterfall
- v-model
- incremental
- RAD model
- agile
- iterative
- spiral

#### Основы Maven. Установка Maven, управление зависимостями, виды Maven-репозиториев, сборка Java-проекта

- скачивание, прописывание переменных окружения
- создание maven-проекта
- зависимости
- плагины
- фазы (lifecycle)
- профили
- билд артефактов

#### Опыт работы с Guava, Apache Commons Collections

- `Multimap`, `BiMap`
- `Multiset`
- неизменяемые коллекции
- Objects: `hashCode`, `equals`
- `Throwables`
- `CollectionUtils`
- `StringUtils`

#### JUnit

- зачем нужно тестирование
- типы тестирования
- `@Test`
- `@Before`, `@After`
- `@BeforeClass`, `@AfterClass`
- параметризованные тесты

#### Mockito

- моки
- `mock` и `spy`
- `when` и `thenReturn`
- `verify`
- `any`, `once`, `times`

#### Логирование

- зачем нужны логи
- уровни логирования
- slf4j
- реализации: log4j, JUL, logback, common-loggins
- аппендеры

#### Устройство сети. Сетевая модель

- топология сети
- модель OSI
- DNS

#### Архитектура ПО. Клиент-серверная архитектура и ее составляющие, трехуровневая архитектура, архитектурные шаблоны

- клиент-серверная архитектура
- трехуровневая архитектура (клиент-сервер-БД)
- критерии хорошей архитектуры: эффективность, гибкость, расширяемость, масштабируемость, удобство тестирования, читаемый и понятный код
- модульная архитектура. декомпозиция

#### Протоколы HTTP/HTTPS. Протокол передачи данных, HTTP-запросы и ответы, отличия HTTP и HTTPS. Cookies, Session

- протоколы передачи данных в сети
- http методы (`GET`, `POST`, `PUT`, …)
- параметры запросов
- тело запроса
- хедеры
- коды ответов
- http VS https
- http сессии
- куки
- http/2

#### HttpClient

- AJAX
- java http client
- синхронные и асинхронные запросы
- задача на получение данных с нета, например погода

#### Сервлеты, Java servlet API. Пишем простое веб-приложение

- что такое сервлет
- жизненный цикл
- сервлет-контейнер Tomcat
- `doGet`, `doPost`
- `redirect` VS `forward`
- фильтры

#### Контейнеры сервлетов: Tomcat, развертывание приложения, настройка сервера

- практика по предыдущей лекции

#### Знакомство с MVC (Model-View-Controller). JSP

- набор архитектурных принципов и идей MVC
- схемы MVC
- MVC в вебе
- типичная ошибка: бизнес-логика в контроллере
- MVC на примере задачи
- JSP

#### Веб-сервисы

- что такое веб-сервис
- протоколы http, jms, ftp, …
- синхронные и асинхронные запросы
- облачные сервисы: IaaS, PaaS, SaaS (что угодно as a service))

#### HTML-факультатив

- что такое HTML
- структура HTML документа
- теги и их атрибуты
- CSS, его синтаксис
- классы и идентификаторы
- селекторы

#### Итоговый проект. Servlet-quest конкурс

- Написать на сервлетах текстовую пошаговую игру-квест

МОДУЛЬ 4. РАБОТА С БАЗАМИ ДАННЫХ. HIBERNATE.

#### Введение в базы данных. Установка СУБД (MySQL). ddl, dml

- зачем нужны БД
- реляционные и нереляционные БД
- реляционная модель
- CAP теорема
- установка MySQL developer
- группы SQL (ddl, dml, dcl, tcl)

#### Типы данных. Создание таблицы. Написание insert, select, update, delete

- создание схемы
- создание таблиц
- изменение структуры таблиц
- insert
- select
- update
- delete

#### Выбор данных

- select с условием
- перечень выбираемых данных
- subselect
- join: left, right, inner, cross
- group by и агрегатные функции
- index

#### Транзакции БД

- концепции ACID (Atomicity, Consistency, Isolation, Durability)
- управление транзакциями
- уровни изоляции данных

#### Проектирование баз данных

- первая нормальная форма
- вторая нормальная форма
- третья нормальная форма
- ключи (foreign key)
- отношения: one to …, many to …

#### JDBC 1

- зачем нужен
- основные интерфейсы
- получение данных в приложении из БД
- обновление и удаление данных в приложении из БД

#### JDBC 2

- транзакции
- уровни изоляции
- обработка checker исключений

#### ORM. Hibernate

- нестыковки объектной и реляционной моделей данных
- ORM (Hibernate), JPA
- архитектура Hibernate
- конфигурация, основные аннотации
- получение данных в приложении из БД
- обновление и удаление данных в приложении из БД
- Hibernate VS JDBC

#### Hibernate. OneTo…, ManyTo…

- отношения (работа с коллекциями)

#### Наследование Entity for ORM

- одна таблица для каждого класса
- одна таблица для каждого класса с предками
- единая таблица для всей иерархии классов
- одна таблица для каждого класса с использованием соединений (join)

#### Итоговый проект

- hash for passwords

МОДУЛЬ 5. SPRING + SPRING BOOT.

#### IoC, DI. Spring. Components. Beans

- почему Spring стал де-факто стандартом отрасли (преимущества)
- принципы IoC и DI
- бин
- контекст (ApplicationContext)
- AOP

#### Spring modules general. Spring Web MVC

- core (beans, core, context, SpEL)
- data access
- testing
- web
- integration
- web mvc

#### Проектирование REST API

- оперирование ресурсами, а не методами
- http методы
- http коды ответов
- ошибки
- запрос коллекции
- запрос количества объектов в коллекции
- запрос объекта коллекции
- добавление данных в коллекцию
- редактирование
- удаление
- домашнее задание: спроектировать 2-ранговый REST API

#### App controller-service-dao

- иерархия контекстов
- servlet config
- контроллер - прием запроса
- сервис - бизнес логика
- dao – хранение состояния

#### Spring ORM. @Transaction

- абстракция “транзакция”
- декларативные транзакции
- transaction propagation
- преимущества ORM + Spring
- настройка hibernate `SessionFactory`
- live coding example

#### Spring Test. AOP (logging)

- unit testing
- integration testing
- основные аннотации
- `TestContext`
- live coding example (ттестирование API-метода или пары методов)
- spring commons logging bridge

#### Spring Security (memory, DB)

- ключевые объекты контекста spring security: `SecurityContextHolder`, `Authentication`, `UserDetails`, `GrantedAuthority`
- авторизация и аутентификация
- OAuth2
- сессии в памяти
- сессии в БД

#### Spring Boot. Spring JPA

- стартеры
- автоконфигурация
- встроенные tomcat
- аннотации конфигурации
- демонстрация spring data jpa (генерация запроса по названию метода в рантайме)