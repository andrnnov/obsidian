#Java #Swing #JFileChooser

## Диалоговое окно JFileChooser

2024-06-13 09:38

[Swing](Swing) включает мощное средство для работы с файлами — компонент **_JFileChooser_**, представляющий контейнер, в котором расположены несколько компонентов, списков и кнопок, «управляющих» выбором файлов. **_JFileChooser_** можно добавить в любое место пользовательского интерфейса, поскольку это весьма гибкий компонент, позволяющий тонко настраивать внешний вид. При необходимости можно полностью изменить стандартное расположение входящих в **_JFileChooser_** компонентов и добавить дополнительные элементы, такие как панели предварительного просмотра файлов.

Все стандартные диалоговые окна [Swing](Swing) имеют собственные UI-представители, отвечающие за интерфейс окна в используемом приложении. Это особенно важно для внешних видов окон, имитирующих известные платформы, пользователи которых не должны ощущать значительной разницы при переходе от «родных» приложений к Java-приложения. UIManager позволяет выполнять настройку и локализацию интерфейса диалогового окна **_JFileChooser_**.

Начиная с выпуска JDK 1.3 библиотека [Swing](Swing) предлагает легко настраиваемый инструмент JFileChooser для выбора файлов и при необходимости каталогов. Особенности различных файловых систем скрыты в подклассах абстрактного класса FileSystemView, который представляет внешний вид файловой структуры согласно используемой операционной системе.

**_JFileChooser_** — это обычный компонент, унаследованный от класса JComponent, так что можно включить его в любое место интерфейса. Настроить и вывести на экран несложное диалоговое окно для открытия файла или сохранения в нем данных совсем легко.

### Конструкторы JFileChooser

```java
// Создание JFileChooser с указанием директории пользователя по умолчанию
JFileChooser() 

// Создание JFileChooser с указанием currentDirectory директории
JFileChooser(File currentDirectory) 
 
// Создание JFileChooser с указанием currentDirectory директории и
// файловой системы
JFileChooser(File currentDirectory, FileSystemView fsv) 
 
// Создание JFileChooser с определенной файловой системы
JFileChooser(FileSystemView fsv) 
 
// Создание JFileChooser с указанием currentDirectoryPath пути
JFileChooser(String currentDirectoryPath) 
 
// Создание JFileChooser с указанием currentDirectoryPath пути и
// файловой системы
JFileChooser(String currentDirectoryPath, FileSystemView fsv) 
```

### Основные метод JFileChooser

|Метод|Описание|
|---|---|
|File getCurrentDirectory()|Функция чтения текущей директории|
|String getDialogTitle()|Функция чтения заголовка окна|
|int getDialogType()|Функция чтения типа диалогового окна|
|FileFilter getFileFilter()|Функция чтения текущего фильтра|
|File getSelectedFile()|Функция чтения выделенного файла|
|File[] getSelectedFiles()|Функция получения списка выделенных файлов, если установлен флаг выделения нескольких файлов MULTI_SELECTION_ENABLED_CHANGED_PROPERTY|
|void setCurrentDirectory(File dir)|Метод определения текущей директории|
|void setDialogTitle(String dialogTitle)|Метод определения заголовка диалогового окна|
|void setDialogType(int dialogType)|Метод определения типа диалогового окна|
|void setFileFilter(FileFilter filter)|Метод установки файлового фильтра|
|void setFileSelectionMode(int mode)|Метод определения выделяемых объектов - файлы, директории или файлы с директориями|
|void setMultiSelectionEnabled(boolean b)|Метод определения возможности выделения нескольких файлов|
|void setSelectedFile(File file)|Метод выделения файла|
|void setSelectedFiles(File[] selectedFiles)|Метод выделения списка файлов, если установлен флаг выделения нескольких файлов MULTI_SELECTION_ENABLED_CHANGED_PROPERTY|
|int showDialog(Component parent, String approveButtonText)|Функция открытия окна выбора файла с настроенным наименованием кнопки|
|int showOpenDialog(Component parent)|Функция открытия диалогового окна «Открыть файл»|
|int showSaveDialog(Component parent)|Функция открытия диалогового окна «Сохранить файл»|

### Режимы работы JFileChooser

Перед открытием диалогового окна для выбора файлов или директории необходимо определить режим работы **_JFileChooser_**. Компонент **_JFileChooser_** может работать в одном из трех режимов, который сохраняется в свойстве _fileSelectionMode_ :
- FILES_ONLY - доступны только файлы, независимо от того, сохраняется файл или открывается. По умолчанию **_JFileChooser_** работает именно в этом режиме.
- FILES_AND_DIRECTORIES - доступны каталоги и файлы. Этот режим следует использовать только в том случае, когда необходимо поменять общие свойства файловой системы (файлы не отличаются от каталогов).
- DIRECTORIES_ONLY - доступны только каталоги.

Для определения режима используется метод _setFileSelectionMode(mode)_.

### Возвращаемые компонентом JFileChooser значения

- APPROVE_OPTION - выбор файла в диалоговом окне прошел успешно; выбранный файл можно получить методом getFile();
- CANCEL_OPTION - выбор файла отменен нажатием на кнопке _Cancel_;
- ERROR_OPTION - при выборе файла произошла ошибка, или было закрыто диалоговое окно выбора файла.

#### Пример 1. Использование JFileChooser

В примере _FileChooserTest.java_ используется диалоговое окно выбора файла и директории с использованием компонента **_JFileChooser_**. Интерфейс окна включает 3 кнопки, по нажатию на которые открывается соответствующее диалоговое окно. Интерфейс главного окна представлен на следующем скриншоте.
![[Ex1_1-FileChooser.png]]

```java
// Пример использования диалоговых окон работы с файлами и директориями
import javax.swing.*;
// import javax.swing.filechooser.FileNameExtensionFilter;
import java.awt.event.*;

public class Main extends JFrame {
    private static final long serialVersionUID = 1L;
    private  JButton      btnSaveFile   = null;
    private  JButton      btnOpenDir    = null;
    private  JButton      btnFileFilter = null;
    private  JFileChooser fileChooser   = null;
    private final String[][] FILTERS = {{"docx", "Файлы Word (*.docx)"},
            {"pdf" , "Adobe Reader(*.pdf)"}};

    public Main() {
        super("Пример FileChooser");
        setDefaultCloseOperation(EXIT_ON_CLOSE);
        // Кнопка создания диалогового окна для выбора директории
        btnOpenDir = new JButton("Открыть директорию");
        // Кнопка создания диалогового окна для сохранения файла
        btnSaveFile = new JButton("Сохранить файл");
        // Кнопка создания диалогового окна для сохранения файла
        btnFileFilter = new JButton("Фильтрация файлов");

        // Создание экземпляра JFileChooser
        fileChooser = new JFileChooser();
        // Подключение слушателей к кнопкам
        addFileChooserListeners();
        // Размещение кнопок в интерфейсе
        JPanel contents = new JPanel();
        contents.add(btnOpenDir   );
        contents.add(btnSaveFile  );
        contents.add(btnFileFilter);
        setContentPane(contents);
        // Вывод окна на экран
        setSize(360, 110);
        setVisible(true);
    }
    private void addFileChooserListeners() {
        btnOpenDir.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                fileChooser.setDialogTitle("Выбор директории");
                // Определение режима - только каталог
                fileChooser.setFileSelectionMode(JFileChooser.DIRECTORIES_ONLY);
                int result = fileChooser.showOpenDialog(Main.this);
                // Если директория выбрана, покажем ее в сообщении
                if (result == JFileChooser.APPROVE_OPTION )
                    JOptionPane.showMessageDialog(Main.this,
                            fileChooser.getSelectedFile());
            }
        });
        btnSaveFile.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                fileChooser.setDialogTitle("Сохранение файла");
                // Определение режима - только файл
                fileChooser.setFileSelectionMode(JFileChooser.FILES_ONLY);
                int result = fileChooser.showSaveDialog(Main.this);
                // Если файл выбран, то представим его в сообщении
                if (result == JFileChooser.APPROVE_OPTION )
                    JOptionPane.showMessageDialog(Main.this,
                            "Файл '" + fileChooser.getSelectedFile() +
                                    " ) сохранен");
            }
        });
        btnFileFilter.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                fileChooser.setDialogTitle("Выберите файл");
                // Определяем фильтры типов файлов
                for (int i = 0; i < FILTERS[0].length; i++) {
                    FileFilterExt eff = new FileFilterExt(FILTERS[i][0],
                            FILTERS[i][1]);
                    fileChooser.addChoosableFileFilter(eff);
                }
//                FileNameExtensionFilter filter = new FileNameExtensionFilter(
//                        "Word & Excel", "docx", "xlsx");
//                fileChooser.setFileFilter(filter);

                // Определение режима - только файл
                fileChooser.setFileSelectionMode(JFileChooser.FILES_ONLY);
                int result = fileChooser.showOpenDialog(Main.this);
                // Если файл выбран, покажем его в сообщении
                if (result == JFileChooser.APPROVE_OPTION )
                    JOptionPane.showMessageDialog(Main.this,
                            "Выбран файл ( " +
                                    fileChooser.getSelectedFile() + " )");
            }
        });
    }
    // Фильтр выбора файлов определенного типа
    class FileFilterExt extends javax.swing.filechooser.FileFilter {
        String extension  ;  // расширение файла
        String description;  // описание типа файлов

        FileFilterExt(String extension, String descr) {
            this.extension = extension;
            this.description = descr;
        }
        @Override
        public boolean accept(java.io.File file) {
            if(file != null) {
                if (file.isDirectory())
                    return true;
                if( extension == null )
                    return (extension.length() == 0);
                return file.getName().endsWith(extension);
            }
            return false;
        }
        // Функция описания типов файлов
        @Override
        public String getDescription() {
            return description;
        }
    }

    public static void main(String[] args)
    {
        // Локализация компонентов окна JFileChooser
        UIManager.put("FileChooser.saveButtonText", "Сохранить");
        UIManager.put("FileChooser.openButtonText", "Открыть");
        UIManager.put("FileChooser.cancelButtonText", "Отмена");
        UIManager.put("FileChooser.fileNameLabelText", "Наименование файла");
        UIManager.put("FileChooser.filesOfTypeLabelText", "Типы файлов");
        UIManager.put("FileChooser.lookInLabelText", "Директория");
        UIManager.put("FileChooser.saveInLabelText", "Сохранить в директории");
        UIManager.put("FileChooser.folderNameLabelText", "Путь директории");

        new Main();
    }
}
```
В примере определены кнопки, компонент выбора файла _fileChooser_ и параметры файлового фильтра FILTERS. В конструкторе определяется интерфейс окна и вызывается метод _addFileChooserListeners()_ для подключения к кнопкам слушателей.

Следует отметить, что компоненты диалогового окна локализованы с использованием метода _put_ менеджера пользовательского интерфейса **UIManager** библиотеки [Swing](Swing).

### Листинг метода addFileChooserListeners

В методе _addFileChooserListeners()_ к каждой кнопке подключается свой слушатель, который формирует собственное диалоговое окно с определенными настройками.

#### Выбор директории

```java
btnOpenDir.addActionListener(new ActionListener() {
    public void actionPerformed(ActionEvent e) {
        fileChooser.setDialogTitle("Выбор директории");
        // Определение режима - только каталог
        fileChooser.setFileSelectionMode(JFileChooser.DIRECTORIES_ONLY);
        int result = fileChooser.showOpenDialog(FileChooserTest.this);
        // Если директория выбрана, покажем ее в сообщении
        if (result == JFileChooser.APPROVE_OPTION )
                  JOptionPane.showMessageDialog(FileChooserTest.this, 
                                                fileChooser.getSelectedFile());
    }
});
```
В коде определяется заголовок окна и режим открытия (JFileChooser.DIRECTORIES_ONLY). Интерфейс окна **JFileChooser** в режиме выбора директории представлен на следующем скриншоте.
![[Ex1_2-FileChooser.png]]
![[Ex1_3-FileChooser.png]]

#### Сохранение файла

```java
btnSaveFile.addActionListener(new ActionListener() {
    public void actionPerformed(ActionEvent e) {
        fileChooser.setDialogTitle("Сохранение файла");
        // Определение режима - только файл
        fileChooser.setFileSelectionMode(JFileChooser.FILES_ONLY);
        int result = fileChooser.showSaveDialog(FileChooserTest.this);
        // Если файл выбран, то представим его в сообщении
        if (result == JFileChooser.APPROVE_OPTION )
            JOptionPane.showMessageDialog(FileChooserTest.this, 
                              "Файл '" + fileChooser.getSelectedFile() + 
                              " ) сохранен");
    }
});
```
В коде определяется заголовок окна и режим открытия (JFileChooser.FILES_ONLY). Интерфейс окна **JFileChooser** в режиме сохранения файла представлен на следующем скриншоте.
![[Ex1_4-FileChooser.png]]
![[Ex1_5-FileChooser.png]]

#### Использование фильтра

Покажем два способа подключения файлового фильтра. Первый способ - файловый фильтр можно создать и подключить к объекту _JFileChooser_ с использованием класса _FileNameExtensionFilter_, пример использования которого представлен в следующем коде.
```java
import javax.swing.filechooser.FileNameExtensionFilter;
...
FileNameExtensionFilter filter = new FileNameExtensionFilter(
                                         "Word & Excel", "docx", "xlsx");
fileChooser.setFileFilter(filter);
```

Второй способ - используем вспомогательный [внутренний класс](https://java-online.ru/java-inner-class.xhtml) FileFilterExt, наследующий свойства класса **FileFilter**, в котором определяем два поля (расширение файлов extension, описание description) и переопределяем методы _accept_ и _getDescription_.

```java
// Фильтр выбора файлов определенного типа
class FileFilterExt extends javax.swing.filechooser.FileFilter 
{
    String extension  ;  // расширение файла
    String description;  // описание типа файлов

    FileFilterExt(String extension, String descr)
    {
        this.extension = extension;
        this.description = descr;
    }
    @Override
    public boolean accept(java.io.File file)
    {
        if(file != null) {
            if (file.isDirectory())
                return true;
            if( extension == null )
                return (extension.length() == 0);
            return file.getName().endsWith(extension);
        }
        return false;
    }
    // Функция описания типов файлов
    @Override
    public String getDescription() {
        return description;
    }
}
```
В следующем коде слушателя выбора файла для кнопки _btnFileFilter_ определяется заголовок окна, в цикле создаются экземпляры фильтров _FileFilterExt_, которые подключаются к _fileChooser_, и определяется режим открытия (JFileChooser.FILES_ONLY).
```java
btnFileFilter.addActionListener(new ActionListener()
{
    public void actionPerformed(ActionEvent e)
    {
        fileChooser.setDialogTitle("Выберите файл");
        // Определяем фильтры типов файлов
        for (int i = 0; i < FILTERS[0].length; i++) {
            FileFilterExt eff = new FileFilterExt(FILTERS[i][0], 
                                                  FILTERS[i][1]);
            fileChooser.addChoosableFileFilter(eff);
        }
        // Определение режима - только файл
        fileChooser.setFileSelectionMode(JFileChooser.FILES_ONLY);
        int result = fileChooser.showSaveDialog(FileChooserTest.this);
        // Если файл выбран, покажем его в сообщении
        if (result == JFileChooser.APPROVE_OPTION )
            JOptionPane.showMessageDialog(FileChooserTest.this,
                                  "Выбран файл ( " + 
                                   fileChooser.getSelectedFile() + " )");
        }
});
```
Интерфейс окна **JFileChooser** в режиме выбора файла с использованием файлового фильтра представлен на следующем скриншоте.
![[Ex1_6-FileChooser.png]]

