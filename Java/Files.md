#Java #Files 
## Класс Files ###

2023-11-24 15:00

Для работы с файлами, есть утилитный класс — **`java.nio.file.Files`**.  Все методы этого класса статические и работают с объектами типа [[Files, Path#Path|Path]].

|Метод|Описание|
|---|---|
|`Path createFile(Path path)`|Создает новый файл с путем `path`|
|`Path createDirectory(Path path)`|Создает новую директорию|
|`Path createDirectories(Path path)`|Создает несколько директорий|
|`Path createTempFile(prefix, suffix)`|Создает временный файл|
|`Path createTempDirectory(prefix)`|Создает временную директорию|
|`void delete(Path path)`|Удаляет файл или директорию, если она пуста|
|`Path copy(Path src, Path dest)`|Копирует файл|
|`Path move(Path src, Path dest)`|Перемещает файл|
|`boolean isDirectory(Path path)`|Проверяет, что путь — это директория, а не файл|
|`boolean isRegularFile(Path path)`|Проверяет, что путь — это файл, а не директория|
|`boolean exists(Path path)`|Проверяет, что объект по заданному пути существует|
|`long size(Path path)`|Возвращает размер файла|
|`byte[] readAllBytes(Path path)`|Возвращает все содержимое файла в виде массива байт|
|`String readString(Path path)`|Возвращает все содержимое файла в виде строки|
|`List<String> readAllLines(Path path)`|Возвращает все содержимое файла в виде списка строк|
|`Path write(Path path, byte[])`|Записывает в файл массив байт|
|`Path writeString(Path path, String str)`|Записывает в файл строку|
|`DirectoryStream<Path> newDirectoryStream(Path dir)`|Возвращает коллекцию файлов (и поддиректорий) из заданной директории|
#### Создание файлов и директорий ####
|Код|Примечание|
|---|---|
|`Files.createFile(Path.of("c:\\readme.txt"));`|Создает файл|
|`Files.createDirectory(Path.of("c:\\test"));`|Создает директорию|
|`Files.createDirectories(Path.of("c:\\test\\1\\2\\3"));`|Создает директорию и все нужные поддиректории, если их не существует.|
#### Копирование, перемещение и удаление ####
|Код|Примечание|
|---|---|
|Path path1 = Path.of("c:\\readme.txt");||
|Path path2 = Path.of("c:\\readme-copy.txt");||
|Files.copy(path1, path2);|Копирует файл|
|||
|Path path1 = Path.of("c:\\readme.txt");||
|Path path2 = Path.of("d:\\readme-new.txt");|Перемещает и|
|Files.move(path1, path2);|переименовывает файл|
|||
|Path path = Path.of("d:\\readme-new.txt");||
|Files.delete(path);|Удаляет файл|
#### Проверка типа файла и факта существования ####
|Код|Примечание|
|---|---|
|Files.isRegularFile(Path.of("c:\\readme.txt"));|true|
|Files.isDirectory(Path.of("c:\\test"));|true|
|Files.exists(Path.of("c:\\test\\1\\2\\3"));|false|
|Files.size(Path.of("c:\\readme.txt"));|10112|
#### Работа с содержимым файла ####
|Код|Описание|
|---|---|
|Path path = Path.of("c:\\readme.txt");|Читаем содержимое файла|
|List`<String>` list = Files.readAllLines(path);| в виде списка строк.|
|||
|for (String str : list)  System.out.println(str);| Выводим строки на экран|
#### Получение содержимого директории ####

Остался еще самый интересный метод — получение файлов и поддиректорий в заданной директории.

Для этого есть специальный метод — `newDirectoryStream()`, который возвращает специальный объект типа `DirectoryStream<Path>`. У него есть итератор(!), и с помощью этого итератора можно получить все файлы и поддиректории заданной директории.

Выглядит проще, чем кажется:
```java
Path path = Path.of("c:\\windows");

try (DirectoryStream<Path> files = Files.newDirectoryStream(path)) {
	for (Path path : files)
	    System.out.println(path);
}
```
Объект `DirectoryStream<Path>` обладает двумя свойствами. Во-первых, у него есть итератор, который возвращает пути к файлам, и мы можем этот объект использовать внутри цикла `for-each`.

А во-вторых, этот объект является потоком данных, и его нужно закрывать с помощью метода `close()`, ну или использовать внутри `try`-with-resources.

