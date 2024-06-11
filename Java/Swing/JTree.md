#Java #Swing #JTree

## Класс JTree

2024-06-11 09:48

Отображение иерархической информации в библиотеке [Swing](Swing) реализуется с помощью дерева **_JTree_**, основой которого является корневой узел root. Потомки корневого узла, могут иметь своих потомков, и т.д. Информация о ветвях дерева хранится в узлах nodes. Узел без потомков является листом leaf дерева. Потомки одного узла являются близнецами siblings. Путь path в дереве определяет последовательность узлов, начиная от корня, по которым следует пройти, чтобы найти нужный нам узел.

Пакет javax.swing.tree хранит основные «строительные» классы деревьев [Swing](Swing): интерфейс TreeNode, описывающий узел дерева, модель дерева с его данными, реализующую интерфейс TreeModel, модель выделения узлов дерева TreeSelectionModel, позволяющую настраивать различные режимы выделения, класс TreePath, описывающий путь в дереве.

Простые деревья можно создавать без использования моделей деревьев TreeModel и узлов TreeNode с помощью нескольких вспомогательных конструкторов класса **_JTree_**. Источником данных при создании деревьев с помощью простых конструкторов могут быть одномерные массивы, динамические массивы [Vector](Vector) или ассоциативные массивы [Hashtable](Hashtable). Эти данные конструктор «оборачивает» в стандартную модель дерева DefaultTreeModel. Но необходимо отметить, что возможности созданных этими конструкторами деревьев, весьма ограничены, поскольку иерархическая структура деревьев слишком специфична, и полностью представить ее простыми данными не так просто.

Особую роль в создании деревьев на основе разнообразных массивов играет специальный тип узла дерева DynamicUtilTreeNode. Он позволяет быстро создать список узлов-потомков для какого-либо узла на основе массива (простого или динамического), причем потомки эти добавляются к узлу только при его раскрытии пользователем, так что, если узел никогда не раскроется, потомков у него не будет.

#### Пример 1. Простой Swing пример использования JTree и TreeModel

```java
// Использование JTree, TreeModel
import java.util.*;
import javax.swing.*;
import javax.swing.tree.TreePath;
import javax.swing.tree.TreeModel;
import javax.swing.event.TreeModelListener;

public class Main extends JFrame {
    String     root  = "Корневая запись";
    String[]   nodes = new String[]  {"Напитки", "Сладости"};
    String[][] leafs = new String[][]{{"Чай", "Кофе", "Пиво", "Минералка"},
            {"Пирожное", "Мороженое", "Зефир", "Халва"}};

    // создание дерева на основе массива
    Object[] data = new Object[] { nodes[0], nodes[1],
            new String[] { leafs[0][0], leafs[0][1], leafs[0][2] }};
    public Main() {
        super("Пример использования JTree");
        setDefaultCloseOperation(EXIT_ON_CLOSE);
        // Данные для дерева на основе вектора
        Vector<String> vector = new Vector<String>();
        for (int i = 0; i < leafs[0].length; i++) {
            vector.add(leafs[0][i]);
        }
        // Данные для дерева  на основе таблицы
        Hashtable<String, String> table = new Hashtable<String, String>();
        for (int i = 0; i < nodes.length; i++) {
            table.put(nodes[i], String.valueOf(i));
        }
        // Создание деревьев
        JTree tree1 = new JTree(data);
        JTree tree2 = new JTree(vector);
        JTree tree3 = new JTree(table);
        JTree tree4 = new JTree(new SimpleModel());
        // Включение отображения корневой записи дерева
        tree3.setRootVisible(true);
        // Размещение деревьев в панели содержимого
        JPanel contents = new JPanel();
        contents.add(tree1);
        contents.add(tree2);
        contents.add(tree3);
        JScrollPane scrollPane = new JScrollPane(tree4,
                JScrollPane.VERTICAL_SCROLLBAR_AS_NEEDED,
                JScrollPane.HORIZONTAL_SCROLLBAR_ALWAYS);
        contents.add(scrollPane);
        setContentPane(contents);
        // Вывод окна на экран
        setSize(400, 300);
        setVisible(true);
    }
    // Модель данных дерева
    class SimpleModel implements TreeModel {
        // Список потомков корневой записи
        private ArrayList<String> rootList = new ArrayList<String>();
        // Дочерние узлы первого уровня
        private ArrayList<String>[] tnodes;

        public SimpleModel() {
            // Заполнение списков данными
            tnodes = (ArrayList<String>[]) new ArrayList<?>[nodes.length];
            for (int i = 0; i < nodes.length; i++) {
                rootList.add(nodes[i]);
                tnodes[i] = new ArrayList<String>();
                for (int j = 0; j < leafs[i].length; j++) {
                    tnodes[i].add(leafs[i][j]);
                }
            }
        }
        // Функция получения корневого узла дерева
        @Override
        public Object getRoot() {
            return root;
        }
        // Функция получения потомка корневого узла
        private final int getRootChild(Object node) {
            int idx = -1;
            for (int i = 0; i < rootList.size(); i++){
                if (rootList.get(i) == node) {
                    idx = i;
                    break;
                }
            }
            return idx;
        }
        // Функция получения количество потомков узла
        @Override
        public int getChildCount(Object node) {
            int idx = getRootChild(node);
            if ( node == root )
                return rootList.size();
            else if ( node == rootList.get(idx))
                return tnodes[idx].size();
            return 0;
        }
        // Функция получения потомка узла по порядковому номеру
        @Override
        public Object getChild(Object node, int index) {
            int idx = getRootChild(node);
            if ( node == root )
                return rootList.get(index);
            else if ( node == rootList.get(idx))
                return tnodes[idx].get(index);
            return null;
        }
        // Функция получения порядкового номера потомка
        @Override
        public int getIndexOfChild(Object node, Object child) {
            int idx = getRootChild(node);
            if ( node == root )
                return rootList.indexOf(child);
            else if ( node == rootList.get(idx))
                return tnodes[idx].indexOf(child);
            return 0;
        }
        // Функция определения, является ли узел листом
        @Override
        public boolean isLeaf(Object node) {
            int idx = getRootChild(node);
            if ((idx >= 0) && tnodes[idx].contains(node))
                return true;
            else
                return false;
        }
        // Функция вызывается при изменении значения некоторого узла
        @Override
        public void valueForPathChanged(TreePath path, Object value) {}
        // Метод присоединения слушателя
        @Override
        public void addTreeModelListener(TreeModelListener tml) {}
        // Методы удаления слушателя
        @Override
        public void removeTreeModelListener(TreeModelListener tml) {}
    }
    public static void main(String[] args) {
        new Main();
    }
}

```
В примере создается 4 дерева с использованием разных конструкторов **JTree**. Первое дерево создается конструктором с [массивом данных](Array). Для создания второго дерева используется динамический массив [Vector](Vector). Третье дерево создается на основе данных таблицы [Hashtable](Hashtable). Для создания четвертого дерева используется модель SimpleModel, реализующая свойства интерфейса **TreeModel**.

Следует обратить внимание, что для первого дерева был использован вложенный массив объектов [String](String). Конструктор **JTree** для такого массива данных сформирует не только ветви первого уровня, связанные с корнем дерева, но и создаст дополнительные узлы с вложенными в них потомками 2-го уровня. К сожалению, для дополнительных узлов в качестве названий будут использованы адреса соответствующего массива в памяти. Аналогичным образом обстоит дело и при подобном использовании динамического массива.

Вектор и таблица в примере заполняются элементами в цикле динамически. В таблице определяются пары «ключ-значение», однако в интерфейсе отображаются только ключи, которые могут появиться в дереве в произвольном порядке.

Простые деревья не показывают корневой узел, и дерево больше напоминает список (первые два дерева). Чтобы корень также был отображен в интерфейсе необходимо использовать метод setRootVisible (boolean). Но название корня будет стандартным «root» (третье дерево), поскольку в простых конструкторах их невозможно определить на этапе создания. Это можно исправить с применением стандартной модели дерева, которая неявно используется классом **_JTree_**. Стандартная модель позволяет изменить названия всех узлов дерева после его создания.

Первые три дерева без панелей прокрутки не ведут себя должным образом: раскрытие или свертывание любого узла сопровождается изменением всего интерфейса. Четвертое дерево обернуто в панель прокрутки.

Интерфейс примера представлен на следующем скриншоте.
![[Ex1-JTree.png]]

### Модель дерева TreeModel

Модель дерева **TreeModel** позволяет
- описать иерархическую структуру данных с единственным корнем;
- указать количество потомков определенного узла дерева;
- получить потомка узла по его порядковому номеру;
- получить порядковый номер потомка по его значению;
- выяснить, является ли некоторый узел листом дерева.

Кроме этого, модель **TreeModel** поддерживает списки слушателей _TreeModelListener_, которые оповещаются при изменениях в модели. В _TreeModel_ в качестве узлов дерева используются самые обычные объекты [Object](Object).

В рассмотренном выше примере использована несложная модель дерева SimpleModel с обычными строками в качестве узлов. Чтобы упростить поддержку древовидной структуры, на начальном этапе рассмотрения, _JTree_ строки сохраняются в динамических списках [ArrayList](Class-ArrayList). Интерфейс **TreeModel** позволяет описать иерархическую структуру с использованием любых объектов. Дальше в качестве объектов будут рассмотрены узлы, описываемые интерфейсом TreeNode.

Интерфейс TreeModel включает несколько методов, использовать большую часть которых непросто. Поэтому в примере методы снабжены небольшими комментариями. В качестве узлов в модели используются обычные строки String. Данные узлов, имеющие потомков, хранятся в списках ArrayList, которые позволяют определять порядковые номера потомков или получать потомков по их порядковым номерам. Также с помощью списков можно без труда определить, является ли узел листом, поскольку все листы у нас также находятся в соответствующих списках.

Корнем дерева является строка root. Все принадлежащие корню дерева узлы-потомки хранятся в списке rootList. Метод _getRoot()_ возвращает корень дерева модели. Методы _getChildCount(), getChild(), getIndexOfChild()_ служат для определения количества потомков, получения самих потомков и порядковых номеров потомков узла. Метод _isLeaf()_ позволяет выяснить, является ли узел листом.

Метод valueForPathChanged() вызывается при изменении значения некоторого узла. Методы addTreeModelListener(), removeTreeModelListener() служат для подключения и отсоединения слушателей, которых нужно будет оповещать при изменениях в данных модели. В примере узлы дерева не редактируются, поэтому эти три метода такой простенькой модели не используются.

Чаще всего деревья используются для хранения иерархических массивов сложных объектов. Стандартная модель дерева **DefaultTreeModel** позволяет работать с такими узлами и использует для хранения информации об узлах специальные объекты TreeNode.

#### Конструкторы модели DefaultTreeModel

```java
@ConstructorProperties(value="root")
public DefaultTreeModel(TreeNode root);
public DefaultTreeModel(TreeNode root, boolean asksAllowsChildren);
```

Флаг _asksAllowsChildren_ определяет как метод модели _isLeaf_ будет выяснять, является ли узел листом, или нет.  
- asksAllowsChildren = false; узел будет листом, если он не имеет потомков;  
- asksAllowsChildren = true; узел будет листом, если он не может иметь потомков.

### Узел дерева TreeNode

Интерфейс **TreeNode** содержит характеристики узла дерева, включающие перечисление (Enumeration) потомков и получение одного из них по порядковому номеру (объект типа TreeNode), а также информацию о предке узла и о том, является ли данный узел листом.

Унаследованный от _TreeNode_ потомок MutableTreeNode определяет несколько дополнительных методов, позволяющих динамически добавлять к узлу новых потомков, удалять их (по номеру или по значению), менять предков узла или удалять данный узел из списка потомков предка. Кроме этого, интерфейс _MutableTreeNode_ включает метод setUserObject(), который позволяет быстро обновить данные, хранящиеся в узле. Данные могут иметь любой тип.

Библиотека [Swing](Swing) предоставляет стандартную реализацию интерфейса _MutableTreeNode_ в виде класса **DefaultMutableTreeNode**, который позволяет работать с узлом **TreeNode**. Данный класс включает различные методы, которые помогают определить принадлежность некоторого узла дереву, является ли узел потомком или предком для другого узла, выяснить общего предка нескольких узлов, получить путь до корня дерева, работать с листьями, принадлежащими узлу и т.п. _DefaultMutableTreeNode_ позволяет получать различные перечисления узлов и их потомков.

Для создания древовидной структуры с помощью класса _DefaultMutableTreeNode_ необходимо для каждого узла создать отдельный объект этого класса, передавая конструктору данные, которые он будет хранить. Именно эти данные используются деревом для вывода узла на экран. Далее с помощью методов добавления узла add() в конец списка или вставки узла в произвольную позицию insert() организуются иерархические отношения узлов.

Cтандартная модель _DefaultTreeModel_ работает с узлами TreeNode. Эта модель может использовать в качестве узлов любые объекты, реализующие интерфейс **TreeNode**, но чаще всего ей передаются экземпляры класса _DefaultMutableTreeNode_.

#### Конструктор узла дерева DefaultMutableTreeNode

```java
public DefaultMutableTreeNode(Object userObject, boolean allowsChildren)
```
Конструктор создания узла без родителя с определением объекта userObject. Если значение флага allowsChildren будет _false_, то узел не будет иметь потомков и в интерфейсе будет представлен листом. В противном случае будет ветью и сможет иметь потомков.

#### Пример 2. Использование DefaultTreeModel и DefaultMutableTreeNode

В следующем примере первоначально создается древовидная структура из стандартных узлов _DefaultMutableTreeNode_. Сначала определяется корень дерева root, к которому подключаются потомки 1-го уровня. Корень является узлом нулевого уровня. Далее в цикле к потомкам 1-го уровня присоединяются листья. Уровень любого узла можно узнать с использованием метода getLevel().

Для создания модели дерева **DefaultTreeModel** необходимо в её конструктор передать корневой узел дерева **TreeNode**. Всё остальное модель реализует сама и представит дерево в интерфейсе окна.

```java
// Swing пример использования стандартной модели дерева DefaultTreeModel
// и узлов DefaultMutableTreeNode
import javax.swing.*;
import javax.swing.tree.*;
import java.awt.GridLayout;

public class Main extends JFrame {
    final   String     ROOT  = "Корневая запись";
    // Массив листьев деревьев
    final   String[]   nodes = new String[]  {"Напитки", "Сладости"};
    final   String[][] leafs = new String[][]{{"Чай", "Кофе", "Коктейль",
            "Сок", "Морс", "Минералка"},
            {"Пирожное", "Мороженое", "Зефир", "Халва"}};
    public Main() {
        super("Пример использования DefaultTreeModel");
        setDefaultCloseOperation(EXIT_ON_CLOSE);
        // Создание древовидной структуры
        DefaultMutableTreeNode root = new DefaultMutableTreeNode(ROOT);
        // Ветви первого уровня
        DefaultMutableTreeNode drink = new DefaultMutableTreeNode(nodes[0]);
        DefaultMutableTreeNode sweet = new DefaultMutableTreeNode(nodes[1]);
        // Добавление ветвей к корневой записи
        root.add(drink);
        root.add(sweet);
        // Добавление к корневой записи новой ветви
        root.add(new DefaultMutableTreeNode("Фрукты", true));
        // Добавление листьев
        for ( int i = 0; i < leafs[0].length; i++)
            drink.add(new DefaultMutableTreeNode(leafs[0][i], false));
        for ( int i = 0; i < leafs[1].length; i++)
            sweet.add(new DefaultMutableTreeNode(leafs[1][i], false));

        // Создание стандартной модели и дерево
        DefaultTreeModel treeModel1 = new DefaultTreeModel(root, true);
        JTree tree1 = new JTree(treeModel1);

        // Создание модели дерева, начиная с drink
        DefaultTreeModel treeModel2 = new DefaultTreeModel(drink);
        JTree tree2 = new JTree(treeModel2);
        // Размещение деревьев в интерфейсе
        JPanel contents = new JPanel(new GridLayout(1, 2));
        contents.add(new JScrollPane(tree1));
        contents.add(new JScrollPane(tree2));
        setContentPane(contents);
        setSize(400, 300);
        // Открываем окно
        setVisible(true);
    }
    public static void main(String[] args) {
        new Main();
    }
}
```
Следует обратить внимание на узел «Фрукты», который подключается к корневому узлу. В качестве параметра _allowsChildren_ конструктору передается значение true. Этот флаг управляет методом getAllowsChildren() интерфейса TreeNode. Если флаг true, то узел может иметь потомки, даже если их в данный момент нет. Для флага false узел является листом.

Интерфейс примера представлен на следующем скриншоте.
![[Ex2-JTree.png]]
В стандартной модели **DefaultTreeModel** поддерживаются два способа определения листьев дерева. Согласно первому способу узел является листом, если у него в данный момент нет потомков. Согласно второму способу узел не является листом, если его метод getAllowsChildren() возвращает true, т.е. потомки могут появиться. Для использования второго способа необходимо в конструктор DefaultTreeModel передать asksAllowsChildren со значением true или вызвать метод setAsksAllowsChildren(true). Вторая модель дерева treeModel2 создается с помощью узла drink; в модели отсутствуют пустые «папки», поэтому второй параметр конструктора не используется и листами считаются все узлы без потомков.

Чтобы дерево отображало данные достаточно передать модель данных в соответствующий конструктор **JTree** или вызвать метод дерева setModel(), если используется другой конструктор.

Стандартная модель включает целый набор методов для динамического изменения узлов и потомков, начиная от полной смены корня методом setRoot() и вставки методом insertNodeInto() узла типа MutableTreeNode в узел такого же типа в произвольную позицию с оповещением слушателей и заканчивая простым изменением узлов DefaultMutableTreeNode. Если необходимо изменить узлы, не касаясь модели, то необходимо ей об этом сообщить вызовом метода reload() модели. Данный метод сообщает слушателям об изменении всей модели. Имеется перегруженная версия этого метода reload(), сообщающего об изменениях в определенном узле дерева. Можно также обратиться к методам вида nodesXXX(), например, метод nodesChanged(), позволяющих сообщать об изменениях в потомках некоторого узла.

При создании деревьев чаще всего используются стандартная модель _DefaultTreeModel_ и узлы _DefaultMutableTreeNode_, которые позволяют манипулировать данными. Основные преимущества применения модели связаны с тем, что данные отделяются от интерфейса и модель может быть разделена между несколькими видами.

### Модель выделения TreeSelectionModel

Информация о выделенных узлах дерева хранится в специальной модели, реализующая интерфейс _TreeSelectionModel_. Данная модель позволяет выделить один узел, несколько смежных узлов или несколько несмежных узлов. В дереве с его иерархической структурой нельзя использовать индексы для управления выделенными узлами.

Для определения местоположения узла в дереве _TreeSelectionModel_ использует два способа. В первую очередь, это путь TreePath, включающий наборы узлов, перемещаясь по которым от корня можно достигнуть требуемого узла. Во-вторых, это номер строки в дереве. Второй способ для одного и того же выделения возвращает разные значения в зависимости от раскрытия или свертывания предков.

Основные две группы методов модели выделения **TreeSelectionModel** включают методы вида addSelectionPath(s), которые добавляют к уже имеющемуся выделению новый узел с заданным путем TreePath, и методы вида setSelectionPath(s), которые заменяют текущее выделение новым, также с заданным путем TreePath. Именно эти методы выполняют основную работу. К примеру, если TreeSelectionModel работает в режиме выделения только одного узла, то при вызове метода addSelectionPath() модель снимает имеющееся выделение и добавляет новый выделенный узел. Если бы поддерживался режим произвольного выделения, то данный метод просто добавлял новые узлы к имеющимся. Это же относится и к методам setSelectionPath(s), который последний выделенный в дереве узел отмечает моделью выделения особым образом. Этот узел можно получить методом getLeadSelectionPath().

**TreeSelectionModel** поддерживает слушателей _TreeSelectionListener_, которые оповещаются при изменении выделенных узлов дерева. Как правило, в дереве по умолчанию используется стандартная модель выделения DefaultTreeSelectionModel.

#### Пример 3. Использование модели выделения TreeSelectionModel

В следующем примере TreeSelectionModelTest создаются три дерева со стандартными моделями выделения DefaultTreeModel, но с разными режимами работы этих моделей. Для деревьев в методе createTreeModel() создается простая модель данных с корнем и двумя потомками с листьями. Для определения режима выделения используется метод setSelectionMode() с параметром. Для этого нужно получить используемую деревом модель выделения методом getSelectionModel(). Но можно предварительно определить модель выделения и подключить ее к дереву.

Три возможных режима выделения узлов дерева описаны константами интерфейса TreeSelectionModel. Для первого дерева установлен режим SINGLE_TREE_SELECTION, позволяющий выделить только один узел. Для второго дерева установлен режим CONTIGUOUS_TREE_SELECTION, допускающий выделение смежных узлов. Для третьего дерева создается стандартная модель выделения с режимом DISCONTIGUOUS_TREE_SELECTION и передается затем в метод setSelectionModel() класса JTree. Данный режим выделения в стандартной модели используется по умолчанию. К третьему дереву дополнительно подключен слушатель событий от модели выделения TreeSelectionListener, который позволит отслеживать выделения в дереве пользователем и выводить соответствующее сообщение в консоль.
```java
// Использование модели выделения дерева TreeSelectionModel
import javax.swing.*;
import javax.swing.tree.*;
import javax.swing.event.*;
import java.awt.GridLayout;

public class TreeSelectionModelTest extends JFrame {
    // Текстовое поле для представления пути
    private JTextArea  taSelection = new JTextArea(5, 20);
    final   String     ROOT  = "Корневая запись";
    // Массив листьев деревьев
    final   String[]   nodes = new String[]  {"Напитки", "Сладости"};
    final   String[][] leafs = new String[][]{{"Чай", "Кофе", "Коктейль", 
                                               "Сок", "Морс", "Минералка"},
                                   {"Пирожное", "Мороженое", "Зефир", "Халва"}};
    public TreeSelectionModelTest() {
        super("TreeSelectionModes");
        setDefaultCloseOperation(EXIT_ON_CLOSE);
        // Создание модели дерева
        TreeModel model = createTreeModel();
        // Дерево с одиночным режимом выделения
        JTree tree1 = new JTree(model);
        // Дерево с выделением непрерывными интервалами
        JTree tree2 = new JTree(model);
        // Дерево с выделением прерывных интервалов
        JTree tree3 = new JTree(model);

        // Определение отдельной модели выделения
        TreeSelectionModel selModel = new DefaultTreeSelectionModel();
        selModel.setSelectionMode(TreeSelectionModel.DISCONTIGUOUS_TREE_SELECTION);

        // Подключение моделей выделения
        tree1.getSelectionModel().
                setSelectionMode(TreeSelectionModel.SINGLE_TREE_SELECTION);
        tree2.getSelectionModel().
                setSelectionMode(TreeSelectionModel.CONTIGUOUS_TREE_SELECTION);
        tree3.setSelectionModel(selModel);
        // Подключаем слушателя выделения
        tree3.addTreeSelectionListener(new SelectionListener());
        // Панель деревьев
        JPanel contents = new JPanel(new GridLayout(1, 3));
        // Размещение деревьев в интерфейсе
        contents.add(new JScrollPane(tree1));
        contents.add(new JScrollPane(tree2));
        contents.add(new JScrollPane(tree3));
        getContentPane().add(contents);
        // Размещение текстового поля в нижней части интерфейса
        getContentPane().add(new JScrollPane(taSelection), BorderLayout.SOUTH);
        setSize(500, 300);
        // Вывод окна на экран
        setVisible(true);
    }
    // Иерархическая модель данных TreeModel для деревьев
    private TreeModel createTreeModel() {
        // Корневой узел дерева
        DefaultMutableTreeNode root = new DefaultMutableTreeNode(ROOT);
        // Добавление ветвей - потомков 1-го уровня
        DefaultMutableTreeNode drink = new DefaultMutableTreeNode(nodes[0]);
        DefaultMutableTreeNode sweet = new DefaultMutableTreeNode(nodes[1]);
        // Добавление ветвей к корневой записи
        root.add(drink);
        root.add(sweet);
        // Добавление листьев - потомков 2-го уровня
        for ( int i = 0; i < leafs[0].length; i++)
            drink.add(new DefaultMutableTreeNode(leafs[0][i], false));
        for ( int i = 0; i < leafs[1].length; i++)
            sweet.add(new DefaultMutableTreeNode(leafs[1][i], false));
        // Создание стандартной модели
        return new DefaultTreeModel(root);
    }
    // Слушатель выделения узла в дереве
    class SelectionListener implements TreeSelectionListener {
        public void valueChanged(TreeSelectionEvent e) {
            if (taSelection.getText().length() > 0)
                taSelection.append("-----------------------------------\n");
            // Источник события - дерево
            JTree tree = (JTree)e.getSource();
            // Объекты-пути ко всем выделенным узлам дерева
            TreePath[] paths = e.getPaths();
            taSelection.append(String.format("Изменений в выделении узлов : %d\n", 
                                               paths.length));
            // Список выделенных элементов в пути
            TreePath[] selected = tree.getSelectionPaths();
            int[] rows = tree.getSelectionRows();
            // Выделенные узлы
            for (int i = 0; i < selected.length; i++) {
                taSelection.append(String.format("Выделен узел : %s (строка %d)\n",
                                    selected[i].getLastPathComponent(), rows[i]));
            }
            // Отображение полных путей в дереве для выделенных узлов
            for (int j = 0; j < selected.length; j++) {
                TreePath path = selected[j];
                Object[] nodes = path.getPath();
                String text = "ThreePath : ";
                for (int i = 0; i < nodes.length; i++) {
                    // Путь к выделенному узлу
                    DefaultMutableTreeNode node = (DefaultMutableTreeNode)nodes[i];
                    if (i > 0)
                        text += " >> ";
                    text += String.format("(%d) ", i) + node.getUserObject();
                }
                text += "\n";
                taSelection.append(text);
            }
        }
    }
    public static void main(String[] args) {
        new TreeSelectionModelTest();
    }
}
```
Для размещения в интерфейсе трех деревьев используется панель с табличным расположением [GridLayout](GridLayout), разделенная на три ячейки, в которых размещаются панели прокрутки с деревьями. В нижней части окна размещается многострочное текстовое поле JTextArea с названием taSelection, в котором отображается сообщение о событиях, поступающих слушателю событий от модели выделения.

Присоединить слушателя _TreeSelectionListener_ можно как к модели выделения, так и к самому дереву JTree. Различие связано с тем, что будет возвращать метод getSource(). В первом случае он вернет ссылку на модель выделения, в которой произошло изменение, а во втором — ссылку на само дерево. В классе **JTree** дублируются все методы модели выделения. Они просто делегируют ей свои вызовы. Кроме этого, в классе JTree есть несколько весьма полезных методов, способных упростить работу с выделенными узлами. Поэтому лучше присоединять слушателя непосредственно к дереву.

В примере слушатель SelectionListener описан во [внутреннем классе](https://java-online.ru/java-inner-class.xhtml). Каждый раз при изменении в выделенных узлах дерева вызывается метод слушателя _valueChanged()_ с параметром TreeSelectionEvent, позволяющий получить источник события в виде дерева JTree, список путей узлов, связанных со сменой выделения методом getPaths(). Обратите внимание, что этот метод не позволяет получить выделенные в данный момент узлы дерева, он только содержит список изменившихся узлов. То есть, если в дереве выделено несколько узлов и пользователь решает выделить еще один, то данный метод вернет только один путь для нового выделенного узла, так как остальные при этом не изменяются.

О выделенных узлах можно узнать с помощью метода getSelectionPaths(), который имеется и в модели выделения, и в дереве. Метод дерева просто обращается к модели выделения. Данный метод возвращает массив объектов-путей TreePath ко всем выделенным узлам дерева. При использовании стандартной модели путь состоит из списка объектов-узлов TreeNode. Как правило, весь путь к выделенному узлу не требуется. Чаще используется информация о самом выделенном узле. Для получения этой информации служит метод getLastPathComponent(), возвращающий последний узел в пути.

При использовании TreeSelectionModel можно работать не только с путями, но и со строками. Поскольку дерево на экране отображается последовательно, то можно подсчитать, на какой строке находится тот или иной узел. Получить номера строк выделенных узлов позволяет метод getSelectionRows(). Но необходимо отметить, что у строк есть недостаток: при свертывании или развертывании узлов дерева их номера меняются.

Запустив пример и выделяя различные узлы деревьев можно увидеть разницу в режимах выделения. Дополнительные режимы выделения доступны при нажатых управляющих клавишах Ctrl и Shift. Интерфейс примера использования модели выделения **TreeSelectionModel** представлен на следующем скриншоте.
![[Ex3-JTree.png]]
В примере расписываются пути **TreePath** выделенных элементов. Для этого используется метод getPath(), возвращающий массив узлов ведущих к выделенным элементам начиная с корня. Так как используется стандартная модель и данные узлов хранятся в объектах типа DefaultMutableTreeNode, то можно преобразовывать узлы, из которых состоит путь, к данному типу. Данные узлов, составляющих путь, получаем методом _getUserObject()_ и отображаем в текстовом поле taSelection. В скобках указан уровень узла, после которого следует его наименование.

#### Методы работы с выделениями

| Метод                                        | Описание                                                                                                 |
| -------------------------------------------- | -------------------------------------------------------------------------------------------------------- |
| addSelectionPath(s),  <br>addSelectionRow(s) | Методы принадлежат модели TreeSelectionModel и позволяют программно прибавлять к выделенным узлам новые. |
| setSelectionPath(s),  <br>setSelectionRow(s) | Методы принадлежат модели TreeSelectionModel и позволяют программно устанавливать выделения узлов.       |
| clearSelection()                             | Очистка всех выделенных узлов дерева.                                                                    |
| getMinSelectionRow()                         | Метод получения номера первого выделенного узла (строки).                                                |
| getMaxSelectionRow()                         | Метод получения номера последнего выделенного узла (строки).                                             |
| isPathSelected(),  <br>isRowSelected()       | Методы получения выделенных узлов дерева.                                                                |

### Внешний вид узлов

Для настройки отображения узлов дерева _JТrее_ следует использовать специальный отображающий объект (Renderer), реализующий интерфейс **TreeCellRenderer**. Для специфичного отображения элементов дерева можно использовать раскраску, иконки, HTML стили. Общие унаследованные от базового класса JComponent свойства типа font и foreground позволяют установить цвета и шрифты для всех узлов дерева.

Интерфейс отображающего объекта **TreeCellRenderer** включает всего один метод _getTreeCellRendererComponent()_, возвращающий графический компонент, который отображает узел дерева. Используется данный компонент точно также, как и в случае с [[JTable#Отображение значения, DefaultTableCellRenderer|ячейкой таблицы]] - он не добавляется на экран, а остается незамеченным для графической системы. Дерево использует его как особую «кисть», вызывая метод paint() компонента в том месте, где располагается отображаемый в данный момент узел. Следующий код можно использовать как шаблон для разработки собственного отображающего объекта.
```java
// Класс отображения объекта
class TextCellRenderer extends DefaultTreeCellRenderer 
{
    // Метод получения компонента для прорисовки
    @Override
    public Component getTreeCellRendererComponent(JTree tree, Object value, boolean selected, 
                                    boolean expanded, boolean leaf, int row, boolean hasFocus)
    {
        // Надпись из базового класса
        JLabel label = (JLabel)super.getTreeCellRendererComponent(
                        tree, value, selected, expanded, leaf, row, hasFocus);
        // . . .
        return tree;
    }
}
```

По умолчанию в дереве _JТrее_ используется стандартный отображающий объект **DefaultTreeCellRenderer**, унаследованный от надписи [JLabel](JLabel) и возвращающий для каждого узла соответствующим образом настроенный экземпляр самого себя, то есть надписи. При этом _DefaultTreeCellRenderer_ отключает все стандартные механизмы надписи JLabel типа оповещения об изменении надписи и значка, автоматическую валидацию надписи.

В узле дерева могут храниться сложные объекты. Для преобразования такого объекта в строку с последующим отображением в узле _DefaultTreeCellRenderer_ не вызывает метод toString() напрямую, а применяет метод _convertValueToText()_ класса JTree. По умолчанию данный метод просто вызывает для узла метод toString(), который следует переопределить.

Объект DefaultTreeCellRenderer способен не только на отображение текста узла со стандартными значками. Его можно довольно тонко настроить, чтобы ваше дерево приняло именно тот внешний вид, который необходим приложению. При этом не стоит забывать, что стандартный отображающий объект унаследован от надписи [JLabel](JLabel), а значит, можно использовать в тексте узла язык HTML, начиная его с комбинации символов `<html>`.

#### Свойства стандартного отображающего объекта DefaultTreeCellRenderer

|Свойства|Описание|
|---|---|
|font|Определение используемого отображающим объектом шрифта. Этого же эффекта можно добиться установкой свойства font для дерева JTree.|
|closedIcon|Отображение иконки свернутого узла.|
|openIcon|Отображение иконки раскрытого узла.|
|leafIcon|Отображение иконки узла, являющегося листом.|
|backgroundNonSelectionColor,  <br>backgroundSelectionColor|Определение цвета фона отображаемых узлов. Первое свойство для не выделенного узла, второе свойства для выделенного узла.|
|textNonSelectionColor,  <br>textSelectionColor|Определение цвета текста отображаемых узлов. Первое свойство для не выделенного узла, второе свойства для выделенного узла.|

#### Пример 4. Листинг примера использования DefaultTreeCellRenderer

```java
// Пример использования стандартного отображащего объекта DefaultTreeCellRenderer
import javax.swing.*;
import javax.swing.tree.*;

public class Main extends JFrame
{
    final   String     ROOT  = "<html><font color=blue>Корневая запись";
    // Массив листьев деревьев
    final   String[]   nodes = new String[]  {"<html><pre>Напитки", "Сладости", "Фрукты"};
    final   String[][] leafs = new String[][]{{"Чай", "Кофе", "Коктейль", "Сок", "Морс", "Минералка"},
            {"<html><i>Пирожное", "<html><i>Мороженое",
                    "<html><b>Зефир", "<html><b>Халва"},
            {"Груша"}};
    public Main() {
        super("Пример TreeCellRenderer");
        setDefaultCloseOperation(EXIT_ON_CLOSE);
        // Создание модели дерева
        JTree tree = new JTree(createTreeModel());
        // Создание и настройка отображающего объекта
        DefaultTreeCellRenderer renderer = new DefaultTreeCellRenderer();
        renderer.setLeafIcon  (new ImageIcon("c://users//minipc//onedrive//документы//obsidian vault//java//swing//icon//man.png"));
        renderer.setOpenIcon  (new ImageIcon("c://users//minipc//onedrive//документы//obsidian vault//java//swing//icon//woman.png"));
        renderer.setClosedIcon(new ImageIcon("c://users//minipc//onedrive//документы//obsidian vault//java//swing//icon//star.png"));
        // Определение в дереве отображающего объекта
        tree.setCellRenderer(renderer);
        // Размещение дерева в интерфейсе
        getContentPane().add(new JScrollPane(tree));
        setSize(300, 300);
        // Вывод окна на экран
        setVisible(true);
    }
    // Иерархическая модель данных TreeModel для деревьев
    private TreeModel createTreeModel() {
        // Корневой узел дерева
        DefaultMutableTreeNode root = new DefaultMutableTreeNode(ROOT);
        // Добавление ветвей - потомков 1-го уровня
        DefaultMutableTreeNode drink = new DefaultMutableTreeNode(nodes[0]);
        DefaultMutableTreeNode sweet = new DefaultMutableTreeNode(nodes[1]);
        DefaultMutableTreeNode fruit = new DefaultMutableTreeNode(nodes[2], true);
        // Добавление ветвей к корневой записи
        root.add(drink);
        root.add(sweet);
        root.add(fruit);
        // Добавление листьев - потомков 2-го уровня
        for ( int i = 0; i < leafs[0].length; i++)
            drink.add(new DefaultMutableTreeNode(leafs[0][i], false));
        for ( int i = 0; i < leafs[1].length; i++)
            sweet.add(new DefaultMutableTreeNode(leafs[1][i], false));
        for ( int i = 0; i < leafs[2].length; i++)
            fruit.add(new DefaultMutableTreeNode(leafs[2][i], false));
        // Создание стандартной модели
        return new DefaultTreeModel(root);
    }

    public static void main(String[] args) {
        new Main();
    }
}
```
В примере создается дерево на основе стандартной модели, как и предыдущем примере c выделением узлов. Единственное отличие от предыдущего примера связано с тем, что для некоторых узлов используется HTML-разметка с использованием тега `<html>`.

Для подключения к узлам иконок были использованы методы setLeafIcon(), setOpenIcon(), setClosedIcon() отображающего объекта DefaultTreeCellRenderer.

Интерфейс примера использования DefaultTreeCellRenderer представлен на следующем скриншоте.
![[Ex4-JTree.png]]

#### Пример 5. Дерево с использованием флажков JCheckBox

Стандартный отображающий объект DefaultTreeCellRenderer имеет ограниченные возможности, связанные с определением иконок и стиля текста для всех узлов дерева. В отдельных случаях возникает необходимость использовать собственный отображающий объект. Для этого следует наследовать свой отображающий объект от TreeCellRenderer и переопределить метод getTreeCellRendererComponent().

Исходный код пример дерева с использованием флажков в листовых узлах CheckBoxTreeTest.

Листинг CheckBoxTreeTest.java
```java
import javax.swing.*;
import javax.swing.tree.*;

public class CheckBoxTreeTest extends JFrame 
{
	private static final long serialVersionUID = 1L;
	final   String     ROOT  = "Корневая запись";
	// Массив листьев деревьев
	final   String[]   nodes = new String[]  {"Напитки", "Сладости"};
	final   String[][] leafs = new String[][]{{"Чай", "Кофе", "Коктейль", "Сок", "Морс", "Минералка"},
			                                  {"Пирожное", "Мороженое", "Зефир", "Халва"}};
	public CheckBoxTreeTest()
	{
		super("Пример JTree с флажками");
		setDefaultCloseOperation(EXIT_ON_CLOSE);
		// Создание модели дерева
		TreeModel model = createTreeModel();
		// Создание дерева
		CheckBoxTree tree = new CheckBoxTree(model);
		// Размещение дерева в интерфейсе
		getContentPane().add(new JScrollPane(tree));
		// Вывод окна на экран
		setSize(400, 300);
		setVisible(true);
	}
	// Иерархическая модель данных TreeModel для деревьев
	private TreeModel createTreeModel()
	{
		// Корневой узел дерева
		DefaultMutableTreeNode root = new DefaultMutableTreeNode(ROOT);
		// Добавление ветвей - потомков 1-го уровня
		DefaultMutableTreeNode drink = new DefaultMutableTreeNode(nodes[0]);
		DefaultMutableTreeNode sweet = new DefaultMutableTreeNode(nodes[1]);
		// Добавление ветвей к корневой записи
		root.add(drink);
		root.add(sweet);
		// Добавление листьев - потомков 2-го уровня
		for ( int i = 0; i < leafs[0].length; i++)
			drink.add(new DefaultMutableTreeNode(new CheckBoxElement(false, leafs[0][i])));
		for ( int i = 0; i < leafs[1].length; i++)
			sweet.add(new DefaultMutableTreeNode(new CheckBoxElement(false, leafs[1][i])));
		// Создание стандартной модели
		return new DefaultTreeModel(root);
	}
	public static void main(String[] args) {
		new CheckBoxTreeTest();
	}
}
```

Листинг CheckBoxTree.java
```java
// Дерево с отображаением флажков в листьях import java.awt.*;  
import java.awt.event.*;  
import javax.swing.*;  
import javax.swing.tree.*;  
  
public class CheckBoxTree extends JTree  
{  
   private static final long serialVersionUID = 1L;  
   // Стандартный объект для отображения узлов  
   private DefaultTreeCellRenderer renderer = new DefaultTreeCellRenderer();  
   // Конструктор  
   public CheckBoxTree(TreeModel model)   
   {  
      super(model);  
      // Слушатель мыши  
      addMouseListener(new MouseListener());  
      // Определение собственного отображающего объекта  
      setCellRenderer(new CheckBoxRenderer());  
   }  
   // Объект отображения узлов дерева с использованием флажков  
   class CheckBoxRenderer extends JCheckBox implements TreeCellRenderer  
   {  
      private static final long serialVersionUID = 1L;  
      public CheckBoxRenderer() {  
         // Флажок будет прозрачным  
         setOpaque(false);  
      }  
      // Метод получения компонента узла  
      public Component getTreeCellRendererComponent(JTree tree, Object value, boolean selected,  
                                   boolean expanded, boolean leaf, int row, boolean hasFocus)  
      {  
         // Проверка принадлежности узла к стандартной модели  
         if (!(value instanceof DefaultMutableTreeNode)) {  
            // Если нет, то используется стандартный объект  
            return renderer.getTreeCellRendererComponent(tree, value, selected, expanded, leaf, row, hasFocus);  
         }  
         Object data = ((DefaultMutableTreeNode)value).getUserObject();  
         // Проверка, являются ли данные CheckBoxElement  
         if (data instanceof CheckBoxElement ) {  
            CheckBoxElement element = (CheckBoxElement)data;  
            // Настройка флажка и текста  
            setSelected(element.selected);  
            setText(element.text);  
            return this;         }  
         // В противном случае метод возвращает стандартный объект  
         return renderer.getTreeCellRendererComponent(tree, value, selected, expanded, leaf, row, hasFocus);  
      }  
   }  
   // Слушатель событий мыши  
   class MouseListener extends MouseAdapter  
   {  
      public void mousePressed(MouseEvent e)  
      {  
         // Путь к узлу  
         TreePath path = getClosestPathForLocation(e.getX(), e.getY());  
         if (path == null)   
            return;  
         DefaultMutableTreeNode node = (DefaultMutableTreeNode)path.getLastPathComponent();  
         // Проверка принадлежности узла к стандартной модели  
         if (node.getUserObject() instanceof CheckBoxElement) {  
            // Изменение состояния флажка  
            CheckBoxElement element = (CheckBoxElement)node.getUserObject();  
            element.selected = ! element.selected;  
            repaint();  
         }  
      }  
   }  
}
```

Листинг CheckBoxElement.java
```java
/**
 * Класс определения параметров элемента узла дерева 
 */
public class CheckBoxElement
{
	// Данные узла
	public boolean selected;
	public String  text;
	// Конструктор
	public CheckBoxElement(boolean selected, String text)
	{
		this.selected = selected;
		this.text = text;
	}
}
```
**Вывод:**
![[Ex5-JTree.png]]