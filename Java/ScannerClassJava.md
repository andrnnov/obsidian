### Класс сканера на Java ###

#Java #ScannerClass

2023-09-06 15:22

В Java  Scanner - это класс в пакете java.util, используемый для получения входных данных примитивных типов, таких как int, double и т.д., и строк. Использование класса Scanner в Java - это самый простой способ считывания входных данных в программе Java, хотя и не очень эффективный, если вам нужен метод ввода для сценариев, где время является ограничением, как в конкурентном программировании.
#### Типы ввода Java-сканера ####

Класс сканера помогает использовать стандартный поток ввода в Java. Итак, нам нужны некоторые методы для извлечения данных из потока. Методы, используемые для извлечения данных, упомянуты ниже:

|Метод|Описание|
|---|---|
|**nextBoolean()**|Используется для чтения логического значения|
|**nextByte()**|Используется для считывания байтового значения|
|**nextDouble()**|Используется для считывания двойного значения|
|**nextFloat()**|Используется для считывания значения с плавающей точкой|
|**nextInt()**|Используется для считывания значения Int|
|**nextLine()**|Используется для считывания значения строки|
|**nextLong()**|Используется для считывания длинного значения|
|**nextShort()**|Используется для считывания короткого значения|

Давайте посмотрим на фрагмент кода для чтения данных различных типов.
```java
import java.util.Scanner;
public class ScannerDemo1 {
    public static void main(String[] args)
    {
        // Declare the object and initialize with
        // predefined standard input object
        Scanner sc = new Scanner(System.in);
 
        // String input
        String name = sc.nextLine();
 
        // Character input
        char gender = sc.next().charAt(0);
 
        // Numerical data input
        // byte, short and float can be read
        // using similar-named functions.
        int age = sc.nextInt();
        long mobileNo = sc.nextLong();
        double cgpa = sc.nextDouble();
 
        // Print the values to check if the input was
        // correctly obtained.
        System.out.println("Name: " + name);
        System.out.println("Gender: " + gender);
        System.out.println("Age: " + age);
        System.out.println("Mobile Number: " + mobileNo);
        System.out.println("CGPA: " + cgpa);
    }
}
```
**Ввод**
==Geek
F
40
9876543210
9.9==

**Вывод**
==Name: Geek
Gender: F
Age: 40
Mobile Number: 9876543210
CGPA: 9.9==

Иногда нам приходится проверять, относится ли следующее прочитанное значение к определенному типу или ввод закончился (обнаружен маркер EOF).

Затем мы проверяем, соответствуют ли входные данные сканера нужному нам типу с помощью функций hasNextXYZ(), где XYZ - это интересующий нас тип. Функция возвращает true, если у сканера есть токен этого типа, в противном случае false. Например, в приведенном ниже коде мы использовали hasNextInt(). Для проверки наличия строки мы используем hasNextLine(). Аналогично, для проверки наличия одного символа мы используем hasNext().charAt(0).

Давайте посмотрим на фрагмент кода, чтобы прочитать некоторые числа с консоли и вывести их среднее значение.
import java.util.Scanner;
``` java
public class ScannerDemo2 {
    public static void main(String[] args)
    {
        // Declare an object and initialize with
        // predefined standard input object
        Scanner sc = new Scanner(System.in);
 
        // Initialize sum and count of input elements
        int sum = 0, count = 0;
 
        // Check if an int value is available
        while (sc.hasNextInt()) {
            // Read an int value
            int num = sc.nextInt();
            sum += num;
            count++;
        }
        if (count > 0) {
            int mean = sum / count;
            System.out.println("Mean: " + mean);
        }
        else {
            System.out.println(
                "No integers were input. Mean cannot be calculated.");
        }
    }
}
```
**Ввод**
==1 2 3 4 5 ==

**Вывод**
==Mean: 3==
### Важные моменты о классе Java Scanner

- Чтобы создать объект класса Scanner, мы обычно передаем предопределенный объект System.in, который представляет стандартный поток ввода. Мы можем передать объект класса File, если хотим прочитать входные данные из файла.
- Для чтения числовых значений определенного типа данных XYZ используется функция nextXYZ(). Например, для чтения значения типа short мы можем использовать nextShort()
- Для чтения строк мы используем nextLine().
- Для чтения одного символа мы используем next().charAt(0). функция next() возвращает следующий токен / слово во входных данных в виде строки, а функция charAt(0) возвращает первый символ в этой строке.
- Класс Scanner считывает всю строку и делит ее на токены. Токены - это небольшие элементы, которые имеют некоторое значение для компилятора Java. Например, предположим, что есть входная строка: How are you.  В этом случае объект scanner прочитает всю строку и разделит строку на токены: “How”, “are” и “you”. Затем объект выполняет итерацию по каждому токену и считывает каждый токен, используя его различные методы.