#Java #InetAddress

## Класс InetAddress

2024-07-15 14:41

Класс **InetAddress** используется для работы с числовым IP-адресом или доменным именем. Поддерживаются адреса IPv4 и IPv6.
1. **Unicast (Одноадресная рассылка)** — идентификатор для одного интерфейса. Пакет, отправленный на одноадресный адрес, доставляется на интерфейс, идентифицированный этим адресом.
2. **Multicast (Многоадресная рассылка)** — идентификатор для набора интерфейсов (обычно принадлежащих разным узлам). Пакет, отправленный на адрес многоадресной рассылки, доставляется на все интерфейсы, идентифицированные этим адресом.
```java
public class InetAddress extends Object implements Serializable;
```

Чтобы создать объекта класса **InetAddress**, следует использовать один из многих доступных методов-фабрик, например.
- static InetAddress getLocalHost() throws UnknownHostException - возвращает объект класса **InetAddress**, представляющий локальный хост
- static InetAddress getByName(String host) throws UnknownHostException - возвращает объект класса **InetAddress** хоста по указанному имени
- static InetAddress[] getAllByName(String host) throws UnknownHostException - возвращает массив объект класса **InetAddress**, представляющий все адреса, в которое преобразуется конкретное имя
- public static InetAddress getByAddress(byte IPAddress[]) throws UnknownHostException - этот метод возвращает объект InetAddress, созданный на основе необработанного IP-адреса
- public static InetAddress getByAddress(String hostName, byte IPAddress[]) throws UnknownHostException - этот метод создает и возвращает InetAddress на основе предоставленного имени хоста и IP-адреса.

Java-реализация класса InetAddress, демонстрирующая использование фабричных методов:
```java
import java.io.*;
import java.net.*;
import java.util.*;
 
class Main {
    public static void main(String[] args)
        throws UnknownHostException
    {
        // To get and print InetAddress of Local Host
        InetAddress address1 = InetAddress.getLocalHost();
        System.out.println("InetAddress of Local Host : " + address1);
 
        // To get and print InetAddress of Named Host
        InetAddress address2 = InetAddress.getByName("45.22.30.39");
        System.out.println("InetAddress of Named Host : " + address2);
 
        // To get and print ALL InetAddresses of Named Host
        InetAddress address3[]
            = InetAddress.getAllByName("172.19.25.29");
        for (int i = 0; i < address3.length; i++) {
            System.out.println(
                "ALL InetAddresses of Named Host : " + address3[i]);
        }
 
        // To get and print InetAddresses of
        // Host with specified IP Address
        byte IPAddress[] = { 125, 0, 0, 1 };
        InetAddress address4 = InetAddress.getByAddress(IPAddress);
        System.out.println("InetAddresses of Host with specified IP Address : "
            + address4);
 
        // To get and print InetAddresses of Host
        // with specified IP Address and hostname
        byte[] IPAddress2 = { 105, 22, (byte)223, (byte)186 };
        InetAddress address5 = InetAddress.getByAddress("gfg.com", IPAddress2);
        System.out.println(
	        "InetAddresses of Host with specified IP Address and hostname : "
            + address5);
    }
}
```
**Вывод:**
<p style="background-color: navy; color: yellow">
InetAddress of Local Host : localhost/127.0.0.1<br>
InetAddress of Named Host : /45.22.30.39<br>
ALL InetAddresses of Named Host : /172.19.25.29<br>
InetAddresses of Host with specified IP Address : /125.0.0.1<br>
InetAddresses of Host with specified IP Address and hostname : gfg.com/105.22.223.186</p>

### Методы InetAddress

Класс InetAddress имеет множество методов экземпляра, которые можно вызывать с помощью объекта. Методы экземпляра:

| Метод                                                     | **Описание**                                                                                         |
| --------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| equals(Object obj)                                        | Эта функция сравнивает этот объект с указанным объектом.                                             |
| getAddress()                                              | Этот метод возвращает необработанный IP-адрес этого объекта InetAddress в байтах.                    |
| getCanonicalHostName()                                    | Этот метод возвращает полное доменное имя для этого IP-адреса.                                       |
| getHostAddress()                                          | Этот метод получает IP-адрес в строковой форме.                                                      |
| getHostName()                                             | Этот метод возвращает имя хоста для этого IP-адреса.                                                 |
| hashCode()                                                | Этот метод получает хэш-код для этого IP-адреса.                                                     |
| isAnyLocalAddress()                                       | Этот метод позволяет проверить, является ли InetAddress непредсказуемым адресом.                     |
| isLinkLocalAddress()                                      | Этот метод позволяет проверить, не связан ли адрес с локальным одноадресным адресом.                 |
| isLoopbackAddress()                                       | Этот метод используется для проверки того, представляет ли InetAddress адрес обратной связи.         |
| isMCGlobal()                                              | Утилита этого метода проверяет, имеет ли этот адрес многоадресный адрес глобальной области действия. |
| isMCLinkLocal()                                           | Утилита этого метода проверяет, имеет ли этот адрес многоадресный адрес локальной области действия.  |
| isMCNodeLocal()                                           | Утилита этого метода проверяет, имеет ли многоадресный адрес область действия узла.                  |
| isMCOrgLocal()                                            | Утилита этого метода проверяет, имеет ли многоадресный адрес область действия организации.           |
| isMCSiteLocal()                                           | Утилита этого метода проверяет, имеет ли адрес многоадресной рассылки область действия сайта.        |
| isMulticastAddress()                                      | Этот метод проверяет, имеет ли сайт несколько серверов.                                              |
| isReachable(int timeout)                                  | Этот метод проверяет, доступен ли этот адрес.                                                        |
| isReachable(NetworkInterface netif, int ttl, int timeout) | Этот метод проверяет, доступен ли этот адрес.                                                        |
| isSiteLocalAddress()                                      | Программа утилиты этого метода проверяет, является ли InetAddress локальным адресом сайта.           |
| toString()                                                | Этот метод преобразует и возвращает IP-адрес в строковой форме.                                      |

Пример Java-реализации класса InetAddress, демонстрирующий использование методов экземпляра.
```java
import java.io.*;
import java.net.*;
import java.util.*;
 
class GFG {
    public static void main(String[] args)
        throws UnknownHostException
    {
 
        InetAddress address1 = InetAddress.getByName("45.22.30.39");
        InetAddress address2 = InetAddress.getByName("45.22.30.39");
        InetAddress address3 = InetAddress.getByName("172.19.25.29");
 
        // true, as clearly seen above
        System.out.println("Is Address-1 equals to Address-2? : "
			            + address1.equals(address2));
        // false
        System.out.println("Is Address-1 equals to Address-3? : "
			            + address1.equals(address3));
 
        // returns IP address
        System.out.println("IP Address : " + address1.getHostAddress());
        // returns host name,
        // which is same as IP
        // address in this case
        System.out.println("Host Name for this IP Address : "
				        + address1.getHostName());
 
        // returns address in bytes
        System.out.println("IP Address in bytes : " + address1.getAddress());
 
        // false, as the given site
        //  has only one server
        System.out.println("Is this Address Multicast? : "
                        + address1.isMulticastAddress());
 
        System.out.println("Address in string form : " + address1.toString());
 
        // returns fully qualified
        // domain name for this IP address.
        System.out.println(
            "Fully qualified domain name for this IP address : "
				        + address1.getCanonicalHostName());
 
        // hashcode for this IP address.
        System.out.println("Hashcode for this IP address : "
                        + address1.hashCode());
 
        // to check if the InetAddress is
        // an unpredictable address..
        System.out.println("Is the InetAddress an unpredictable address? : "
			            + address1.isAnyLocalAddress());
    }
}
```
**Вывод:**
<p style="background-color: navy; color: yellow">
Is Address-1 equals to Address-2? : true<br>
Is Address-1 equals to Address-3? : false<br>
IP Address : 45.22.30.39<br>
Host Name for this IP Address : 45.22.30.39<br>
IP Address in bytes : [B@579bb367<br>
Is this Address Multicast? : false<br>
Address in string form : 45.22.30.39/45.22.30.39<br>
Fully qualified domain name for this IP address : 45.22.30.39<br>
Hashcode for this IP address : 756424231<br>
Is the InetAddress an unpredictable address? : false</p>
