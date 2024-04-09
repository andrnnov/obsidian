#Java 
## Оглавление


Глава. Классы. Объектно-ориентированное программирование
- Классы и объекты
- Пакеты
- Модификаторы доступа и инкапсуляция
- Статические члены и модификатор [static](Static)
- Объекты как параметры методов
- Внутренние и вложенные классы
- Наследование
- [[AbstractInterface#Абстрактные классы|Абстрактные классы]]
- Иерархия наследования и преобразование типов
- [Интерфейсы](Interface)
- Интерфейсы в механизме обратного вызова
- Перечисления [enum](Enum)
- Класс [Object](Object) и его методы
- Обобщения ([Generics](Generics))
- Ограничения обобщений
- Наследование и обобщения
- Ссылочные типы и клонирование объектов
- Records

Глава. Обработка исключений
- Оператор throws
- Классы исключений
- Создание своих классов исключений

Глава. [Коллекции](Collections)
- [Типы коллекций](Collections). Интерфейс [[Collections#Интерфейс Java Collection|Collection]]
- Класс [ArrayList](Class-ArrayList) и интерфейс [List](List)
- Очереди [Queue](Queue), [PriorityQueue](PriorityQueue), [Deque](Deque) и класс [ArrayDeque](ArrayDeque)
- Класс [LinkedList](Class-LinkedList)
- Интерфейс [Set](Set) и классы [HashSet](HashSet), [LinkedHashSet](LinkedHashSet)
- [SortedSet](SortedSet), [NavigableSet](NavigableSet), [TreeSet](TreeSet)
- Интерфейсы [Comparable](Comparable) и [Comparator](Comparator). Сортировка
- Интерфейс [Map](Map) и класс HashMap
- Интерфейсы SortedMap и NavigableMap. Класс TreeMap
- Итераторы ([Iterator](Iterator), [[Iterator#ListIterator|ListIterator]])

Глава. Потоки ввода-вывода. Работа с файлами
- [Потоки ввода-вывода](JavaIO)
- Чтение и запись файлов. [FileInputStream](FileInputStream) и [FileOutputStream](FileOutputStream)
- [Закрытие потоков](closeStream)
- Классы [ByteArrayInputStream](ByteArrayInputStream) и [ByteArrayOutputStream](ByteArrayOutputStream)
- Буферизованные потоки [BufferedInputStream](BufferedInputStream) и [BufferedOutputStream](BufferedOutputStream)
- Форматируемый вывод. [PrintStream](PrintStream) и PrintWriter
- Классы [DataOutputStream](DataOutputStream) и [DataInputStream](DataInputStream)
- Чтение и запись текстовых файлов. [FileWriter](FileWriter), [FileReader](FileReader)
- Буферизация символьных потоков. [BufferedReader](BufferedReader) и [BufferedWriter](BufferedWriter)
-  Сериализация объектов. Интерфейс [Serializable](Serializable)
- Класс [File](File). Работа с файлами и каталогами. [File](File), [[Files, Path#Files|Files]] и [[Files, Path#Path|Path]]
- Работа с ZIP-архивами.  [ZipInputStream](ZipInputStream) и [ZipOutputStream](ZipOutputStream)
- Класс Console

Глава. Работа со строками
- Класс [String](String)
- StringBuffer и [StringBuilder](StringBuilder)
- [Регулярные выражения](Regex)

Глава. [Лямбда-выражения](Lambda)
- [[Lambda#Понятие о лямбда-выражении. Преимущества применения лямбда-выражений|Введение в лямбда-выражения]]
- [Лямбды как параметры и результаты методов](LambdaMethod)
- Встроенные [функциональные интерфейсы](Functional-Interface)
- [Лямбда-выражения для обобщенных функциональных интерфейсов](LambdaGeneric)
- [Генерирование исключений в лямбда-выражениях](LambdaException)

Глава. [Многопоточное программирование](Multithreading)
- Класс [Thread](Thread)
- Создание и выполнение потоков
- Завершение и прерывание потока
- Синхронизация потоков. Оператор synchronized
- Взаимодействие потоков. Методы [wait и notify](wait-notify)
- [Семафоры](Semaphore)
- Обмен между потоками. Класс [Exchanger](Exchanger)
- Класс [Phaser](Phaser)
- [Блокировки.](Locks) [[Locks#Класс ReentrantLock|ReentrantLock]]
- Условия в блокировках. [[Locks#Интерфейс Condition|Condition]]

Глава. Stream API
- Введение в [Stream API](StreamAPI)
- [Создание потока данных](CreateStream)
- Фильтрация (Метод [[StreamAPI#filter()|filter]]), перебор элементов (Метод [[StreamAPI#forEach()|forEach]]) и отображение (Методы [[StreamAPI#map()|map]] и [[StreamAPI#flatMap()|flatMap]])
- Сортировка (Метод [sorted](sorted()))
- Получение подпотока и объединение потоков (Методы [[StreamAPI#takeWhile()|takeWhile]], [[StreamAPI#dropWhile()|dropWhile]], [[StreamAPI#concat()|concat]] и [[StreamAPI#distinct()|distinct]])
- Методы [[StreamAPI#skip(long n)|skip]] и [[StreamAPI#limit()|limit]]
- Операции сведения (Методы [[StreamAPI#count()|count()]], [[StreamAPI#findFirst()|findFirst()]], [[StreamAPI#findAny()|findAny()]], [[StreamAPI#allMatch()|allMatch()]], [[StreamAPI#anyMatch()|anyMatch()]], [[StreamAPI#noneMatch()|noneMatch()]], [[StreamAPI#min()|min()]] и [[StreamAPI#max()|max())]]
- Метод [[StreamAPI#reduce()|reduce]]
- Тип [Optional](Optional)
- Метод [collect](collect())
- [Группировка](GroupingStream)
- [Параллельные потоки](parallel())
- [Параллельные операции над массивами](parallelArray)








