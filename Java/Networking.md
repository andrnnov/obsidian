#Java #Networking

## Java Networking

2024-08-07 14:28

В палете **_java.net_** языка программирования Java включает в себя различные классы и интерфейсы, которые обеспечивают простой доступ к сетевым ресурсам. Помимо классов и интерфейсов, пакет **_java.net_** также обеспечивается поддержка двух известных сетевых протоколов. Это:

1. **Transmission Control Protocol (TCP)** - TCP или протокол управления передачей обеспечивают безопасную связь между различными приложениями. TCP — это протокол, ориентированный на соединение, который означает, что после соединения  данные могут передаваться в двух направлениях. Этот протокол обычно используется как интернет-протокол. Поэтому TCP также называет TCP/IP. TCP имеет встроенные методы проверки наличия ошибок и обеспечения доставки данных в том порядке, в котором они были отправлены, что делает его полноценным протоколом для передачи информации, таким как изображения, файлы данных и веб-страницы.  
     
2. **User Datagram Protocol (UDP)** - UDP или протокол пользовательских датаграмм - это протокол без подключения, который позволяет передавать данные между различными приложениями. UDP — это более простой интернет-протокол, в котором не требуются службы проверки ошибок и восстановления. В UDP нет дополнительных затрат на открытие соединений, поддержание соединений или завершение соединений. В UDP-данные непрерывно отправляются получателю, независимо от того, получает он их или нет. 
 
Дейтаграмма - это независимое, автономное сообщение, отправляемое по сети, прибытие, время прибытия и содержимое которого не гарантируются.

### Сетевая терминология Java

В сетях Java часто используется множество терминов. Эти широко используемые сетевые термины Java приведены ниже:

1. **IP-адрес.** IP-адрес — это уникальный адрес, который отличает устройство в Интернете или локальной сети. IP означает «Интернет-протокол». Он включает в себя набор правил, регулирующих формат данных, отправляемых через Интернет или локальную сеть. IP-адрес называется логическим адресом, который можно изменить. Он состоит из октетов. Диапазон каждого октета варьируется от 0 до 255.
    - Диапазон IP-адреса – от 0.0.0.0 до 255.255.255.255.
    - Например — 192.168.0.1.  
         
2. **Номер порта.** Номер порта — это метод распознавания конкретного процесса, подключающего Интернет или другую сетевую информацию, когда она достигает сервера. Номер порта используется для уникальной идентификации различных приложений. Номер порта действует как конечная точка связи между приложениями. Номер порта коррелирует с IP-адресом для передачи и связи между двумя приложениями. Всего имеется 65 535 номеров портов, но не все они используются каждый день.  
     
3. **Протокол.** Сетевой протокол представляет собой организованный набор команд, которые определяют, как данные передаются между различными устройствами в одной сети. Сетевые протоколы являются причиной, по которой пользователь может легко общаться с людьми по всему миру и, таким образом, играть решающую роль в современных цифровых коммуникациях. Например – TCP, FTP, POP и т. д.  
     
4. **MAC-адрес –** MAC-адрес означает адрес управления доступом к среде передачи. Это идентификатор, присвоенный NIC (контроллеру/карте сетевого интерфейса). Он содержит 48-битный или 64-битный адрес, который объединяется с сетевым адаптером. MAC-адрес может иметь шестнадцатеричный состав. Проще говоря, MAC-адрес — это уникальный номер, который используется для отслеживания устройства в сети.  
     
5. **Сокет.** Сокет — это одна из конечных точек двустороннего соединения между двумя приложениями, работающими в сети. Механизм сокетов представляет собой метод межпроцессного взаимодействия (IPC) путем установки именованных точек контакта, между которыми происходит связь. Сокет привязан к номеру порта, чтобы уровень TCP мог распознать приложение, которому предназначены данные для отправки.  
     
6. **Протокол с установлением соединения и без него.** В службе, ориентированной на соединение, пользователь должен установить соединение перед началом связи. Когда соединение установлено, пользователь может отправить сообщение или информацию, а после этого он может разорвать соединение. Однако в протоколе без установления соединения данные передаются по одному маршруту от источника к месту назначения без проверки того, находится ли пункт назначения или нет, или готов ли он принять сообщение. Аутентификация не требуется в протоколе без установления соединения.
    - Пример протокола, ориентированного на соединение – протокол управления передачей (TCP)
    - Пример протокола без установления соединения — протокол пользовательских дейтаграмм (UDP)

### Сетевые классы Java

Пакет **java.net** языка программирования Java включает в себя различные классы, которые предоставляют простые в использовании средства доступа к сетевым ресурсам. Классы, включенные в пакет **java.net,** представлены следующим образом:

1. [**CacheRequest**](https://www.geeksforgeeks.org/java-net-cacherequest-class-in-java/) **—** класс CacheRequest используется в Java всякий раз, когда возникает необходимость хранить ресурсы в ResponseCache. Объекты этого класса предоставляют объекту OutputStream возможность хранить данные ресурсов в кэше.  
     
2. [**CookieHandler**](https://www.geeksforgeeks.org/java-net-cookiehandler-class-in-java/) **—** класс CookieHandler используется в Java для реализации механизма обратного вызова для обеспечения реализации политики управления состоянием HTTP внутри обработчика протокола HTTP. Механизм управления состоянием HTTP определяет механизм выполнения HTTP-запросов и ответов.  
     
3. [**CookieManager**](https://www.geeksforgeeks.org/java-net-cookiemanager-class-in-java/) **—** класс CookieManager используется для точной реализации CookieHandler. Этот класс отделяет хранение файлов cookie от политики принятия и отклонения файлов cookie. CookieManager состоит из CookieStore и CookiePolicy.  
     
4. [**DatagramPacket**](https://www.geeksforgeeks.org/java-net-datagrampacket-class-java/) **—** класс DatagramPacket используется для обеспечения возможности передачи сообщений без установления соединения из одной системы в другую. Этот класс предоставляет инструменты для создания пакетов дейтаграмм для передачи без установления соединения с помощью класса сокетов дейтаграмм.  
     
5. [**InetAddress**](InetAddress) **—** класс InetAddress используется для предоставления методов для получения IP-адреса любого имени хоста. IP-адрес выражается 32-битным или 128-битным беззнаковым числом. InetAddress может обрабатывать адреса как IPv4, так и IPv6.  
     
6. [**Server Socket**](https://www.geeksforgeeks.org/java-net-serversocket-class-in-java/) **—** класс ServerSocket используется для реализации независимой от системы реализации серверной части соединения Socket Connection клиент/сервер. Конструктор класса ServerSocket выдает исключение, если он не может прослушивать указанный порт. Например – он выдаст исключение, если порт уже используется.  
     
7. [**Socket**](https://www.geeksforgeeks.org/java-net-socket-class-in-java/) **—** класс Socket используется для создания объектов сокетов, которые помогают пользователям реализовывать все основные операции с сокетами. Пользователи могут выполнять различные сетевые действия, такие как отправка, чтение данных и закрытие соединений. Каждый объект Socket, созданный с использованием **класса java.net.Socket** , был подключен ровно к одному удаленному хосту; для подключения к другому хосту пользователь должен создать новый объект сокета.  
     
8. [**DatagramSocket**](https://www.geeksforgeeks.org/java-net-datagramsocket-class-java/) **—** класс DatagramSocket представляет собой сетевой сокет, который обеспечивает точку без установления соединения для отправки и получения пакетов. Каждый пакет, отправленный из дейтаграммного сокета, маршрутизируется и доставляется индивидуально. Кроме того, его можно использовать для передачи и приема широковещательной информации. Дейтаграммные сокеты — это механизм Java для обеспечения сетевой связи через UDP вместо TCP.  
     
9. [**Proxy**](https://www.geeksforgeeks.org/java-net-proxy-class-in-java/) **—** это неизменный объект и своего рода инструмент, метод, программа или система, которая служит для сохранения данных своих пользователей и компьютеров. Он ведет себя как стена между компьютерами и пользователями Интернета. Прокси-объект представляет настройки прокси-сервера, которые будут применяться к соединению.  
     
10. [**URL**](URL) **—** класс URL в Java является точкой входа в любые доступные источники в Интернете. URL-адрес класса описывает унифицированный указатель ресурса, который является сигналом к ​​«ресурсу» во Всемирной паутине. Источник может обозначать простой файл или каталог, а может указывать на более сложный объект, например запрос к базе данных или поисковой системе.  
     
11. [**URLConnection**](URLConnection) **—** класс URLConnection в Java представляет собой абстрактный класс, описывающий соединение ресурса, определенного аналогичным URL-адресом. Класс URLConnection используется для достижения двух различных, но взаимосвязанных целей. Во-первых, он обеспечивает контроль над взаимодействием с сервером (особенно с HTTP-сервером), а не с классом URL. Более того, с помощью URLConnection пользователь может проверить заголовок, переданный сервером, и соответствующим образом отреагировать. Пользователь также может настроить поля заголовков, используемые в клиентских запросах, с помощью URLConnection.

### Сетевые интерфейсы Java

Пакет **java.net** языка программирования Java также включает в себя различные интерфейсы, которые предоставляют простые в использовании средства доступа к сетевым ресурсам. В пакет **java.net** включены следующие интерфейсы :

1. **CookiePolicy –** ​​интерфейс CookiePolicy в пакете **java.net** предоставляет классы для реализации различных сетевых приложений. Он решает, какие файлы cookie следует принять, а какие отклонить. В CookiePolicy есть три предопределенные реализации политики, а именно ACCEPT_ALL, ACCEPT_NONE и ACCEPT_ORIGINAL_SERVER.  
     
2. **CookieStore** — это интерфейс, описывающий место хранения файлов cookie. CookieManager объединяет файлы cookie в CookieStore для каждого ответа HTTP и восстанавливает файлы cookie из CookieStore для каждого HTTP-запроса.  
     
3. **FileNameMap –** интерфейс FileNameMap представляет собой несложный интерфейс, реализующий инструмент для определения имени файла и строки типа MIME. FileNameMap загружает карту имен файлов (известную как mimetable) из файла данных.  
     
4. **SocketOption –** интерфейс SocketOption помогает пользователям контролировать поведение сокетов. Часто бывает необходимо разработать необходимые функции в Sockets. SocketOptions позволяет пользователю устанавливать различные стандартные параметры.  
     
5. **SocketImplFactory —** интерфейс SocketImplFactory определяет фабрику для экземпляров SocketImpl. Он пользуется классом сокета для создания реализаций сокетов, реализующих различные политики.  
     
6. **ProtocolFamily –** этот интерфейс представляет семейство протоколов связи. Интерфейс ProtocolFamily содержит метод name(), который возвращает имя семейства протоколов.
