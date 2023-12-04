#Java #Serializable
### Сериализация и десериализация в Java ###

2023-12-04 14:46

**Сериализация** — это процесс сохранения состояния объекта в последовательность байт. **Десериализация** — это процесс восстановления объекта из этих байт.

Любой Java-объект преобразуется в последовательность байт. Для чего это нужно? Программы не существуют сами по себе. Чаще всего они взаимодействуют друг с другом, обмениваются данными и т.д. И байтовый формат для этого удобен и эффективен. Мы можем, например, превратить наш объект класса `SavedGame` (сохраненная игра) в последовательность байт, передать эти байты по сети на другой компьютер, и на втором компьютере превратить эти байты снова в Java-объект. 

В Java за процессы сериализации отвечает интерфейс **Serializable**. Этот интерфейс крайне прост: чтобы им пользоваться, не нужно реализовывать ни одного метода! Вот так просто будет выглядеть наш класс сохранения игры:
```java
import java.io.Serializable;
import java.util.Arrays;

public class SavedGame implements Serializable {

   private static final long serialVersionUID = 1L;

   private String[] territoriesInfo;
   private String[] resourcesInfo;
   private String[] diplomacyInfo;

   public SavedGame(String[] territoriesInfo, String[] resourcesInfo, String[] diplomacyInfo){
       this.territoriesInfo = territoriesInfo;
       this.resourcesInfo = resourcesInfo;
       this.diplomacyInfo = diplomacyInfo;
   }

   public String[] getTerritoriesInfo() {
       return territoriesInfo;
   }

   public void setTerritoriesInfo(String[] territoriesInfo) {
       this.territoriesInfo = territoriesInfo;
   }

   public String[] getResourcesInfo() {
       return resourcesInfo;
   }

   public void setResourcesInfo(String[] resourcesInfo) {
       this.resourcesInfo = resourcesInfo;
   }

   public String[] getDiplomacyInfo() {
       return diplomacyInfo;
   }

   public void setDiplomacyInfo(String[] diplomacyInfo) {
       this.diplomacyInfo = diplomacyInfo;
   }

   @Override
   public String toString() {
       return "SavedGame{" +
               "territoriesInfo=" + Arrays.toString(territoriesInfo) +
               ", resourcesInfo=" + Arrays.toString(resourcesInfo) +
               ", diplomacyInfo=" + Arrays.toString(diplomacyInfo) +
               '}';
   }
}
```
Три массива данных отвечают за информацию о территориях, экономике и дипломатии, а интерфейс Serializable говорит Java-машине: «_все ок, если что, объекты этого класса можно сериализовать_». Serializable - это интерфейс-маркер.

Еще один важный момент: переменная `private static final long serialVersionUID`, которую мы определили в классе. Зачем она нужна? Это поле содержит **уникальный идентификатор версии сериализованного класса**.

Идентификатор версии есть у любого класса, который имплементирует интерфейс Serializable. Он вычисляется по содержимому класса — полям, порядку объявления, методам. И если мы поменяем в нашем классе тип поля и/или количество полей, идентификатор версии моментально изменится. serialVersionUID тоже записывается при сериализации класса. 

Когда мы пытаемся провести десериализацию, то есть восстановить объект из набора байт, значение `serialVersionUID` сравнивается со значением `serialVersionUID` класса в нашей программе. Если значения не совпадают, будет выброшено исключение java.io.InvalidClassException.

Чтобы избежать таких ситуаций, мы просто вручную задаем для нашего класса этот идентификатор версии. В нашем случае он будет равен просто 1 (можешь подставить любое другое понравившееся число).
```java
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.ObjectOutputStream;

public class Main {
   public static void main(String[] args) throws IOException {
       //создаем наш объект
       String[] territoryInfo = {"У Испании 6 провинций", "У России 10 провинций", "У Франции 8 провинций"};
       String[] resourcesInfo = {"У Испании 100 золота", "У России 80 золота", "У Франции 90 золота"};
       String[] diplomacyInfo = {"Франция воюет с Россией, Испания заняла позицию нейтралитета"};

       SavedGame savedGame = new SavedGame(territoryInfo, resourcesInfo, diplomacyInfo);
       //создаем 2 потока для сериализации объекта и сохранения его в файл
       FileOutputStream outputStream = new FileOutputStream("C:\\Users\\Username\\Desktop\\save.ser");
       ObjectOutputStream objectOutputStream = new ObjectOutputStream(outputStream);
       // сохраняем игру в файл
       objectOutputStream.writeObject(savedGame);
       //закрываем поток и освобождаем ресурсы
       objectOutputStream.close();
   }
}
```
Как видишь, мы создали 2 потока — [FileOutputStream](FileOutputStream) и [ObjectOutputStream](ObjectOutputStream). Первый из них умеет записывать данные в файл, а второй — преобразует объекты в байты.

Создав такую «цепочку» из двух потоков мы выполняем обе задачи: превращаем объект `SavedGame` в набор байт и сохраняем его в файл с помощью метода `writeObject()`. 
>_Примечание: файл необязательно создавать заранее. Если файла с таким названием не существует, он будет создан автоматически_

Cодержимое файла: 
`¬н sr SavedGame [ diplomacyInfot [Ljava/lang/String;[ resourcesInfoq ~ [ territoriesInfoq ~ xpur [Ljava.lang.String;­ТVзй{G xp t pР¤СЂР°РЅС†РёСЏ РІРѕСЋРµС‚ СЃ Р РѕСЃСЃРёРµР№, РСЃРїР°РЅРёСЏ Р·Р°РЅСЏР»Р° РїРѕР·РёС†РёСЋ РЅРµР№С‚СЂР°Р»РёС‚РµС‚Р°uq ~ t "РЈ РСЃРїР°РЅРёРё 100 Р·РѕР»РѕС‚Р°t РЈ Р РѕСЃСЃРёРё 80 Р·РѕР»РѕС‚Р°t !РЈ Р¤СЂР°РЅС†РёРё 90 Р·РѕР»РѕС‚Р°uq ~ t &РЈ РСЃРїР°РЅРёРё 6 РїСЂРѕРІРёРЅС†РёР№t %РЈ Р РѕСЃСЃРёРё 10 РїСЂРѕРІРёРЅС†РёР№t &РЈ Р¤СЂР°РЅС†РёРё 8 РїСЂРѕРІРёРЅС†РёР№`

Если же мы хотим восстановить наш исходный объект, то есть, загрузиться и продолжит игру с того места, где остановились, нам нужен обратный процесс, **десериализация**. Вот как она будет выглядеть в нашем случае:
```java
import java.io.*;

public class Main {
   public static void main(String[] args) throws IOException, ClassNotFoundException {
		FileInputStream fileInputStream = new 
							FileInputStream("C:\\Users\\Username\\Desktop\\save.ser");
	    ObjectInputStream objectInputStream = new ObjectInputStream(fileInputStream);
		SavedGame savedGame = (SavedGame) objectInputStream.readObject();
		System.out.println(savedGame);
   }
}
```
Вывод:
<p style="background-color: navy; color: yellow">SavedGame{territoriesInfo=[У Испании 6 провинций, У России 10 провинций, У Франции 8 провинций], resourcesInfo=[У Испании 100 золота, У России 80 золота, У Франции 90 золота], diplomacyInfo=[Франция воюет с Россией, Испания заняла позицию нейтралитета]}</p>
А теперь давай попробуем сделать то же, но уберем из нашего класса `SavedGame` идентификатор версии. Не будем переписывать оба наших класса, код в них будет тем же, просто из класса `SavedGame` уберем `private static final long serialVersionUID`.

А при попытке его десериализовать произошло вот что: 
<p style="background-color: navy; color: red">InvalidClassException: local class incompatible: stream classdesc serialVersionUID = -196410440475012755, local class serialVersionUID = -6675950253085108747</p>
Это то самое исключение, о котором говорилось выше. 

Понятно, что строки и примитивы сериализуются легко: наверняка в Java есть какие-то встроенные механизмы для этого. Но что, если в нашем `serializable`-классе есть поля, выраженные не примитивами, а ссылками на другие объекты? Давай, например, создадим отдельные классы `TerritoriesInfo`, `ResourcesInfo` и `DiplomacyInfo` для работы с нашим классом `SavedGame`.
```java
public class TerritoriesInfo {

   private String info;

   public TerritoriesInfo(String info) {
       this.info = info;
   }

   public String getInfo() {
       return info;
   }

   public void setInfo(String info) {
       this.info = info;
   }

   @Override
   public String toString() {
       return "TerritoriesInfo{" + "info='" + info + '\'' + '}';
   }
}

public class ResourcesInfo {

   private String info;

   public ResourcesInfo(String info) {
       this.info = info;
   }

   public String getInfo() {
       return info;
   }

   public void setInfo(String info) {
       this.info = info;
   }

   @Override
   public String toString() {
       return "ResourcesInfo{" + "info='" + info + '\'' + '}';
	}
}

public class DiplomacyInfo {

   private String info;

   public DiplomacyInfo(String info) {
       this.info = info;
   }

   public String getInfo() {
       return info;
   }

   public void setInfo(String info) {
       this.info = info;
   }

   @Override
   public String toString() {
       return "DiplomacyInfo{" + "info='" + info + '\'' + '}';
   }
}
```
А вот теперь перед нами возник вопрос: а должны ли все эти классы быть Serializable, если мы хотим сериализовать изменившийся класс `SavedGame`?
```java
import java.io.Serializable;
import java.util.Arrays;

public class SavedGame implements Serializable {

   private TerritoriesInfo territoriesInfo;
   private ResourcesInfo resourcesInfo;
   private DiplomacyInfo diplomacyInfo;

   public SavedGame(TerritoriesInfo territoriesInfo, ResourcesInfo resourcesInfo, DiplomacyInfo diplomacyInfo) {
       this.territoriesInfo = territoriesInfo;
       this.resourcesInfo = resourcesInfo;
       this.diplomacyInfo = diplomacyInfo;
   }

   public TerritoriesInfo getTerritoriesInfo() {
       return territoriesInfo;
   }

   public void setTerritoriesInfo(TerritoriesInfo territoriesInfo) {
       this.territoriesInfo = territoriesInfo;
   }

   public ResourcesInfo getResourcesInfo() {
       return resourcesInfo;
   }

   public void setResourcesInfo(ResourcesInfo resourcesInfo) {
       this.resourcesInfo = resourcesInfo;
   }

   public DiplomacyInfo getDiplomacyInfo() {
       return diplomacyInfo;
   }

   public void setDiplomacyInfo(DiplomacyInfo diplomacyInfo) {
       this.diplomacyInfo = diplomacyInfo;
   }

   @Override
   public String toString() {
       return "SavedGame{" +
               "territoriesInfo=" + territoriesInfo +
               ", resourcesInfo=" + resourcesInfo +
               ", diplomacyInfo=" + diplomacyInfo +
               '}';
   }
}
```
Что ж, давай проверим это на практике! Оставим пока все как есть и попробуем сериализовать объект `SavedGame`:
```java
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.ObjectOutputStream;

public class Main {

   public static void main(String[] args) throws IOException {

       //создаем наш объект
       TerritoriesInfo territoriesInfo = new TerritoriesInfo("У Испании 6 провинций, у России 10 провинций, у Франции 8 провинций");
       ResourcesInfo resourcesInfo = new ResourcesInfo("У Испании 100 золота, у России 80 золота, у Франции 90 золота");
       DiplomacyInfo diplomacyInfo =  new DiplomacyInfo("Франция воюет с Россией, Испания заняла позицию нейтралитета");


       SavedGame savedGame = new SavedGame(territoriesInfo, resourcesInfo, diplomacyInfo);

       FileOutputStream fileOutputStream = new FileOutputStream("C:\\Users\\Username\\Desktop\\save.ser");
       ObjectOutputStream objectOutputStream = new ObjectOutputStream(fileOutputStream);

       objectOutputStream.writeObject(savedGame);

       objectOutputStream.close();
   }
}
```
Результат: 
<p style="background-color: navy; color: red">Exception in thread "main" java.io.NotSerializableException: DiplomacyInfo</p>
Не вышло! Собственно, вот и ответ на наш вопрос. **При сериализации объекта сериализуются все объекты, на которые он ссылается в своих переменных экземпляра.** И если те объекты тоже ссылаются на третьи объекты, они тоже сериализуются. И так до бесконечности. Все классы в этой цепочке должны быть Serializable, иначе их невозможно будет сериализовать и будет выброшено исключение.

Что делать, например, если часть класса при сериализации нам не нужна? Или, к примеру, класс `TerritoryInfo` в нашей программе достался нам «по наследству» в составе какой-то библиотеки. При этом он не является Serializable, и мы, соответственно, не можем его менять.

Проблемы такого рода решаются в Java при помощи ключевого слова `transient`. Если добавить к полю класса это ключевое слово — значение этого поля не будет сериализовано. Давай попробуем сделать одно из полей нашего класса `SavedGame transient`, после чего сериализуем и восстановим один объект.
```java
import java.io.Serializable;

public class SavedGame implements Serializable {

   private transient TerritoriesInfo territoriesInfo;
   private ResourcesInfo resourcesInfo;
   private DiplomacyInfo diplomacyInfo;

   public SavedGame(TerritoriesInfo territoriesInfo, ResourcesInfo resourcesInfo, DiplomacyInfo diplomacyInfo) {
       this.territoriesInfo = territoriesInfo;
       this.resourcesInfo = resourcesInfo;
       this.diplomacyInfo = diplomacyInfo;
   }

   //...геттеры, сеттеры, toString()...
}



import java.io.FileOutputStream;
import java.io.IOException;
import java.io.ObjectOutputStream;

public class Main {

   public static void main(String[] args) throws IOException {

       //создаем наш объект
       TerritoriesInfo territoriesInfo = new TerritoriesInfo("У Испании 6 провинций, у России 10 провинций, у Франции 8 провинций");
       ResourcesInfo resourcesInfo = new ResourcesInfo("У Испании 100 золота, у России 80 золота, у Франции 90 золота");
       DiplomacyInfo diplomacyInfo =  new DiplomacyInfo("Франция воюет с Россией, Испания заняла позицию нейтралитета");


       SavedGame savedGame = new SavedGame(territoriesInfo, resourcesInfo, diplomacyInfo);

       FileOutputStream fileOutputStream = new FileOutputStream("C:\\Users\\Username\\Desktop\\save.ser");
       ObjectOutputStream objectOutputStream = new ObjectOutputStream(fileOutputStream);
       objectOutputStream.writeObject(savedGame);
       objectOutputStream.close();
   }
}


import java.io.*;

public class Main {
   public static void main(String[] args) throws IOException, ClassNotFoundException {
       FileInputStream fileInputStream = new FileInputStream("C:\\Users\\Username\\Desktop\\save.ser");
       ObjectInputStream objectInputStream = new ObjectInputStream(fileInputStream);
       SavedGame savedGame = (SavedGame) objectInputStream.readObject();
       System.out.println(savedGame);
       objectInputStream.close();
   }
}
```
А вот и результат: 
<p style="background-color: navy; color: yellow">SavedGame{territoriesInfo=null, resourcesInfo=ResourcesInfo{info='У Испании 100 золота, у России 80 золота, у Франции 90 золота'}, diplomacyInfo=DiplomacyInfo{info='Франция воюет с Россией, Испания заняла позицию нейтралитета'}}</p>

Заодно мы получили ответ на вопрос, какое же значение будет присвоено `transient`-полю. Ему присваивается значение по умолчанию. В случае с объектами это `null`.