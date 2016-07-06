# Kotlin

### 1. Идиомы

1. **DTO (Data Transfer Object)** - обычный объект, который используется для пересылки или хранения данных. 
  - Пример создания класса `Customer` c геттерами и сеттерами для всех полей. Модификтор `data` предоставляет методы `equals()`, `hashCode()`, `toString()`, `copy()`, а также возможность деструктурирования.
  ```Kotlin
  data class Customer(val name: String, val email: String)
  ```
  
1. **Параметры по-умолчанию** - котлин поддерживает параметры по-умолчанию.
  - Пример:
  ```Kotlin
  fun foo(a: Int = 0, b: String = "") { ... }
  ```
  
1. **Фильтрация** - у коллекций в котлине имеется метод filter, который в сочитании с лямбда-выражениями позволяет удобно отсеивать нужные значения коллекции.
  - Пример:
  ```Kotlin
  val positives = list.filter { x -> x > 0 }
  val positives = list.filter { it > 0 }
  ```
  
1. **Подстановка** - в котлине есть возможность подстановки значений переменных в строку используя имя переменной.
  - Пример:
  ```Kotlin
  val name = "NAME"
  println("Name $name")
  ```
  
1. **Проверка типа** - совмещая операторы `when` и `is` можно добиться удобной проверки на тип объекта.
  - Пример:
  ```Kotlin
  when (x) {
      is Foo -> ...
      is Bar -> ...
      else   -> ...
  }
  ```
  
1. **Диапазоны** - в котлине имееется оператор `..` для обозначения диапазонов.
  - Пример:
  ```Kotlin
  for (i in 1..100) { ... }  // closed range: includes 100
  for (i in 1 until 100) { ... } // half-open range: does not include 100
  for (x in 2..10 step 2) { ... }
  for (x in 10 downTo 1) { ... }
  if (x in 1..10) { ... }
  ```
  
1. **Read-only коллекции**
  ```Kotlin
  for (i in 1..100) { ... }  // closed range: includes 100
  for (i in 1 until 100) { ... } // half-open range: does not include 100
  for (x in 2..10 step 2) { ... }
  for (x in 10 downTo 1) { ... }
  if (x in 1..10) { ... }
  ```
  
1. **Доступ по ключу**
  ```Kotlin
  map["key"] = value
  ```

1. **Singleton**
  ```Kotlin
  object Resource {
      val name = "Name"
  }
  ```
  
1. **Выражения с возвратом значения**
  ```Kotlin
  result = when (color) {
      "Red" -> 0
      "Green" -> 1
      "Blue" -> 2
      else -> throw IllegalArgumentException("Invalid color param value")
  }
  ```
  ```Kotlin
  result = try {
      count()
  } catch (e: ArithmeticException) {
      throw IllegalStateException(e)
  }
  ```
  ```Kotlin
  result = if (param == 1) {
      "one"
  } else if (param == 2) {
      "two"
  } else {
      "three"
  }
  ```
  
***

### 1. Базовые конструкции

1. **Типы данных**
  - Синтаксис типа:
  ```Kotlin
  annotations typeDescriptor
  ```
    + `typeDescriptor` может быть функцией, пользовательским типом, nullable типом или dynamic.
    + `annotations` состоит из одной или нескольких аннотаций.
  - __`Number`__ - данный тип схож с джавовским, но не совсем. В котлине он представляет следующие типы (не наследуются): `Double`, `Float`, `Long`, `Int`, `Short`, `Byte`.
    + Десятичные числа: `123`. Long числа: `123L`
    + Шестнадцетиричные числа: `0x0F`
    + Двоичные числа: `0b00001011`
    + Числа с плавающей точкой: `123.5`, `123.5e10`. Float числа: `123.5f`
    + В котлине не поддерживается неявное преобразование малых чисел в больше (Byte в Int, например).
  - __`Char`__ - в котлине символы не могут воспринматься как числа, в отличии от джавы.
    + Экранируемые символы: `\t`, `\b`, `\n`, `\r`, `\'`, `\"`, `\\`, `\$` или символ юникода `'\uFF00'`
  - __`Boolean`__ - булев тип, принимающий `true` или `false`.
  - __`Array`__ - массивы в котлине представлены этим классом, который имеет геттер и сеттер в виде квадратных скобок.
    + В отличии от массивов в джава, массивы в котлине инварианты. Это значит, что нельзя присвоить значение типа `Array<String>` переменной типа `Array<Any>`. Для этого нужно использовать явное преобразование.
  - __`String`__ - строки как и в джава - неизменяемы, к элементам строки (символам) можно образаться с помощью геттера в виде квадратных скобок.
    + Тройные кавычки обозначают, что текст внутри них останется таким, каким он выглядит в редакторе (за исключением отступов, их можно указать с помощью знака `|`).
    + Строковые темплейты можно делать с помощью `$`: 
    ```Kotlin
    val s = "abc"
    val str = "$s.length is ${s.length}".
    ```

1. **Операции** - операции в котлине разделяются на следующие группы:
  - Арифметические операции: `+`, `-`, `/`, `*`, `%`, `++`, `--`.
  - Сравнительные операции: `==`, `!=`, `>`, `>=`, `<=`, `<`.
  - Побитовые операции: `&`, `|`, `^`, `~`, `<<`, `>>`, `>>>`.
  - Логические операции: `&&`, `||`, `!`.
  - Операции присваивания: `=`, `+=`, `-=`, `*=`, `/=`, `%=`, `<<=`, `>>=`, `&=`, `^=`, `|=`.
  - Прочие операции: `() ? () : ()`, `instanceof`

### 1. Элементы

Обозначение нотаций, которые будут использоваться для определения синтаксиса элементов:
+ Имена конечных элементов начинаются с большой буквы. (SimpleName)
+ Имена неконечных элементов начинаются с маленькой буквы. (kotlinFile)
+ Оператор `|` обозначает "или".
+ Оператор `*` обозначает "может содержать несколько".
+ Оператор `+` обозначает "сожержит несколько".
+ Оператор `?` обозначает "может содержать один".
+ Оператор `X{Y}` обозначает непустую последовательность из X-ов, разделенных символом Y.
+ Оператор `++` обозначает, что между операндами недопустимы пробелы или комментарии.  
+ Операнд `SEMI` обозначает новую строку или точку с запятой.  
  

1. **kotlinFile** - файл состоит из начального поля и может содержать несколько объектов высокого уровня.
  - Синтаксис:
  ```Kotlin
  preamble toplevelObject*
  ```

1. **script** - скрипт состоит из начального поля и может содержать несколько выражений.
  - Синтаксис:
  ```Kotlin
  preamble expression*
  ```

1. **preamble** - начальное поле может содержать файловые аннотации, заголовок пакета и несколько импортов. 
  - Синтаксис:
  ```Kotlin
  fileAnnotations? packageHeader? import*
  ```

1. **fileAnnotations** - файловые аннотации могут содержать несколько файловых аннотаций.
  - Синтаксис:
  ```Kotlin
  fileAnnotation*
  ```

1. **fileAnnotation** - файловая аннотация содержит одну или более аннотацию.
  - Синтаксис:
  ```Kotlin
  "@" "file" ":" ("[" annotationEntry+ "]" | annotationEntry)
  ```

1. **packageHeader** - заголовок пакета содержит модификаторы и последовательность имен.
  - Синтаксис:
  ```Kotlin
  modifiers "package" SimpleName{"."} SEMI?
  ```

1. **import** - импорт состоит из последовательности имен и может содержать в конце '*' или еще одно имя.
  - Синтаксис:
  ```Kotlin
  "import" SimpleName{"."} ("." "*" | "as" SimpleName)? SEMI?
  ```

1. **toplevelObject** - высокоуровневый объект - это пакет, класс, объект, функция или проперти.
  - Синтаксис:
  ```Kotlin
  package | class | object | function | property
  ```

1. **package** - пакет состоит из последовательности имен, может содержать импорты и высокоуровневые объекты.
  - Синтаксис:
  ```Kotlin
  "package" SimpleName{"."} "{"
     import*
     toplevelObject*
  "}"
  ```

1. **class** - класс состоит из модификаторов, имени, ограничений, тела класса или перечисления, а также может содержать параметры типов, основной контруктор, аннотации с последовательностью делегатов и пустое тело класса.
  - Синтаксис:
  ```Kotlin
  modifiers ("class" | "interface") SimpleName
      typeParameters?
      primaryConstructor?
      (":" annotations delegationSpecifier{","})?
      typeConstraints
      (classBody? | enumClassBody)
  ```

1. **primaryConstructor** - основной конструктор содержит последовательность параметров функции и может содержать модификаторы.
  - Синтаксис:
  ```Kotlin
  (modifiers "constructor")? ("(" functionParameter{","} ")")
  ```

1. **classBody** - тело класса содержит члены класса.
  - Синтаксис:
  ```Kotlin
  ("{" members "}")?
  ```

1. **members** - члены класса могут содержать члены определения.
  - Синтаксис:
  ```Kotlin
  memberDeclaration*
  ```

1. **delegationSpecifier** - делегат состоит из вызова конструктора, пользовательского типа или явного делегирования.
  - Синтаксис:
  ```Kotlin
  constructorInvocation | userType | explicitDelegation
  ```

1. **explicitDelegation** - 
  - Синтаксис:
  ```Kotlin
  preamble toplevelObject*
  ```

1. **typeParameters** - 
  - Синтаксис:
  ```Kotlin
  preamble toplevelObject*
  ```

1. **typeParameter** - 
  - Синтаксис:
  ```Kotlin
  preamble toplevelObject*
  ```

1. **typeConstraints** - 
  - Синтаксис:
  ```Kotlin
  preamble toplevelObject*
  ```

1. **typeConstraint** - 
  - Синтаксис:
  ```Kotlin
  preamble toplevelObject*
  ```

1. **kotlinFile** - 
  - Синтаксис:
  ```Kotlin
  preamble toplevelObject*
  ```

***

### 3. ООП

1. **ООП (Объектно Ориентированное Программирование)** - методология программирования, основанная на представлении программы в виде совокупности объектов, каждый из которых является экземпляром определенного класса, а классы в свою очередь образуют иерархию наследования.

2. **Инкапсуляция** - сокрытие реализации.
    - Реализуется с помощью модификаторов видимости: `default`, `public`, `protected,` `private`.

3. **Полиморфизм** - парадигма ООП. Существует несколько его разновидностей:
    - **Ad-hoc (ситуативный) полиморфизм** — функция по-разному работает с данными разных типов из заранее фиксированного набора. Реализуется с помощью перегрузки методов.
    - **Параметрический полиморфизм** — функция работает одинаково с данными произвольных типов. Реализуется с помощью дженериков и параметризованных классов. 
    - **Полиморфизм подтипов** — функция работает одинако-во с данными типов, являющихся подтипами одного общего супер-типа, редоставляющего общий интерфейс. Реализуется с помощью наследования и иерархии классов.
    - **Динамический полиморфизм** — то, какой метод (из суперкласса или из подкласса) будет вызван, зависит от настоящего типа объекта, т.е. от того, объект какого класса на самом деле содержится в переменной. Реализуется с помощью позднего связыванания.

4. **Наследование** - возможность создавать потомков и переопределять часть функциональности класса.
    - Реализуется с помощью ключевого слова extends.
    - Java не поддерживает множественное наследование классов.

5. **Абстракция** - это выделение общих характеристик объекта, отличая от всех других объектов.
    - Реализуется с помощью абстрактных классов и интерфейсов.

6. **Класс** — это описание структуры и поведения объектов.

7. **Объекты** — это участки памяти виртуальной машины, содержащие своё состояние в виде полей.

***

### 4. Базовые конструкции

1. **Типы данных** - в Java существует два типа данных: примитивные и ссылочные:
    - Примитивные типы: `byte`, `short`, `int`, `float`, `double`, `long`, `boolean`, `char`.
    - Ссылочные типы: обертки примитивных типов, объекты классов, массивы.

2. **Операции** - операции в Java разделяются на следующие группы:
    - Арифметические операции: `+`, `-`, `/`, `*`, `%`, `++`, `--`.
    - Сравнительные операции: `==`, `!=`, `>`, `>=`, `<=`, `<`.
    - Побитовые операции: `&`, `|`, `^`, `~`, `<<`, `>>`, `>>>`.
    - Логические операции: `&&`, `||`, `!`.
    - Операции присваивания: `=`, `+=`, `-=`, `*=`, `/=`, `%=`, `<<=`, `>>=`, `&=`, `^=`, `|=`.
    - Прочие операции: `() ? () : ()`, `instanceof`

3. **Строка** - последовательность символов, в Java строки являются объектами.
    - Строки реализованы с помощью класса `String`.
    - Строки в Java неизменяемы (immutable) в целях безопасности, поэтому строки могут кэшировать свой хэшкод, что делает ее очень быстрой как ключ для `HashMap`. При том, строки могут свободно использоваться различными потоками, не боясь, что кто-то их изменит, таким образом отпадает необходимость в синхронизации.
    - Если строку нужно изменять, то следует использовать `StringBuilder` или `StringBuffer`.
    - `StringTokenizer` - позволяет разбивать текст на лексемы, отделяемые разделителями. Парсит данные. Быстрый. Не поддерживает регулярные выражения. Устаревший.
    - `String.split` - позволяет разбивать текст на лексемы, отделяемые разделителями. Поддерживает регулярные выражения. Возвращаемым значением является массив строк. Работает медленее, чем `StringTokenizer`.
    - `Formatter` - обеспечивает преобразование формата, позволяющее выводить числа, строки, время и даты в любом необходимом разработчику виде.
    - `Pattern` - применяется для определения регулярных выражений (шаблонов), для которых ищется соответствие в строке, файле или другом объекте, представляющем последовательность символов.
    - `Matcher` - если необходимо найти соответствия внутри строки, необходимо использовать этот класс.

4. **Массив** - фиксированная структура данных.
    - Массивы в Java объявляются следующим образом: 
    ```Java
    dataType[] arrayRefVar = new dataType[arraySize];
    dataType[] arrayRefVar = {value0, value1, ..., valueK};
    ```
    - Также существует Arrays класс, который предоставляет статические методы для манипуляций с массивами, такие как: 
    ```Java
    public static int binarySearch(Object[] a, Object key)
    public static boolean equals(long[] a, long[] a2)
    public static void fill(int[] a, int val)
    public static void sort(Object[] a)
    ```

***
    
### 5. Модификаторы

1. **`private`** (переменные / конструкторы / методы / внутренние классы) - члены класса доступны только внутри класса.
 
2. **`package-private`** или **`default`** (переменные / конструкторы / методы / классы) - члены класса видны внутри пакета.

3. **`protected`** (переменные / методы / конструкторы / внутренние классы) - члены класса доступны внутри пакета и в классах-наследника.

4. **`public`** (все) - члены класса доступны всем.

5. **`static`** (логические блоки / переменные / методы / классы) - статические блоки выполняются во время загрузки класса. К статическим методам и переменным можно обращаться через имя класса. 

6. **`abstract`** (методы / классы) - абстрактные классы должны наследоваться, а абстрактные методы - реализовываться.

7. **`final`** (переменные / методы / классы) - переменные, которым было присвоино значение, не могут быть переприсвоены. Методы не могут быть перегруженны. Классы не могут быть наследованы.

8. **`synchronized`** (методы / части метода) - метод может одновременно использоваться только одним потоком.
 
9. **`transient`** (переменные) - переменная не сериализуется. Локальные переменные не могут быть объявлены как transient. 

10. **`volatile`** (переменные) - значение переменной, объявленной как volatile, измененное одним потоком, асинхронно меняется и для других потоков. 

11. **`native`** (методы) - обозначает, что метод написан на другом языке программирования.
 
12. **`strictfp`** (методы / классы) - обеспечивает выполнение операций над числами типа float и double (с плавающей запятой) по стандарту IEEE 754.

***

### 6. Дженерики

1. **Дженерики** — реализация обобщенного программирования, включающая в себя поддержку обобщенных классов и обобщенных методов. 

2. **Обобщенные классы** - обобщенные (параметризованные) классы могут использоваться для следующих целей:
    - Коллекции и контейнеры: `List<Integer>`, `Set<Long>`, `Map<String, Runnable>`, `Future<HttpResponse>`, `Optional<Model>`.
    - Компараторы
    ```Java
    public interface Comparator<T> {
        int compare(T left, T right);
    }
    ```
    - Объекты-команды
    ```Java
    public interface Function<F, T> {
        T apply(F arg);
    }
    public interface Callable<T> {
        T call() throws Exception;
    }
    ```
    - Провайдеры
    ```Java
    public interface Provider<T> {
        T get();
    }
    public interface ThrowingProvider<T, E extends Throwable> {
        T get() throws E;
    }
    ```
    - Обобщенные DAO
    ```Java
    public abstract class GenericDAO<T, ID> {
        protected GenericDAO(Class<T> clazz) { ... }
        public T findById(ID id) { ... }
    }
    ```
    - Конверторы
    ```Java
    public interface StringConverter<T> {
        T fromString(String s);
        String toString(T obj);
    }
    ```
    - Кортежи
    ```Java
    public class TwoTuple<A,B> { 
        public final A first; 
        public final B second; 
        public TwoTuple(A a, B b) { 
            first = a; second = b; 
        }
    }
    ```

3. **Обобщенные методы** - обобщенные (параметризованные) методы могут использоваться для следующих целей:
    - Обобщенные фабричные методы:
    ```Java
    public static <T extends Enum<T>> EnumSet<T> allOf(Class<T> clazz);
    public static <T> ImmutableList<T> of(T pɴ, T pɵ, T... other);
    public <T> T getInstance(Key<T> key);
    ```
    - Методы-преобразователи
    ```Java
    public static <T> Iterable<T> skip(Iterable<T> iterable, int n);
    public static <F, T> Iterable<T> transform(Iterable<F> iterable, Function<F, T> function);
    ```
    - Обобщенные утилитные методы
    ```Java
    public static <T extends Comparable<T>> T max(Iterable<T> xs);
    ```
    
4. **Wildcards** - wildcards существуют трех типов:
    - Wildcards with upper bound:
    ```Java
    public static double sumOfList(List<? extends Number> list);
    ```
    - Unbounded wildcard
    ```Java
    void printCollection(Collection<?> c);
    ```
    - Wildcards with lower bound
    ```Java
    public static void addNumbers(List<? super Integer> list);
    ```
    
***

### 7. Многопоточность

1. **Многопоточность** - это когда множество процессов делят общие вычислительные ресурсы, такие как CPU, между собой.
    - Многопотчная программа содержит 2 или более частей, который могут работать одновременно, и каждая часть может выполнять свое действие, тем самым создавая оптимальные условия для использования доступных ресурсов.
    - Многопоточность расширяет идею многозадачности в приложениях, где можно разделить определенные операции в индивидуальные потоки.
    - Операционная система разделяет вычислительное время не только между различными программами, но и между потоками этих приложений.

2. **Поток** в Java представлен классом `java.lang.Thread`, объекты которого являются потоками, работающими внутри текущей JVM. 
    - Каждый поток может работать параллельно.
    - Начиная с версии 1.5 в состав стандартной библиотеки Java входит пакет `java.util.concurrent`, в котором содержится большое количество различных классов, помогающих при разработке многопоточных программ.

3. **Создание потока**. Для того, чтобы выполнить какую-либо задачу в отдельном потоке, можно создать новый поток с помощью конструктора класса `Thread`, передать ему `Runnable` и запустить его.
    - Пример создания потока:
    ```Java
    new Thread(new Runnable() {
        @Override public void run() { /* ... */ }
    }).start();
    new Thread(() -> { /* ... */ }).start();
    ```
    
4. **Создание сервисного потока**. Выполнение Java-машины завершается, когда завершатся все потоки, не являющиеся сервисными, т.е. те, у которых не установлен флаг daemon.
    - Пример создания сервисного потока:
    ```Java
    Thread t = new Thread(() -> { ... });
    t.setDaemon(true);
    t.start();
    ```
    
5. **Критические секции**. При работе потоков с общей изменяемой памятью неизбежно возникает проблема синхронизации действий этих потоков. 
    - Самым простым способом упорядочить работу потоков с общими данными являются `synchronized-блоки`.

6. **synchronized-блоками**  обозначаются критические секции — участки кода, которые в каждый момент времени могут выполняться только одним потоком. 
    - Синхронизация потоков всегда происходит с использованием какого-либо объекта. 
    - Поток, входящий в synchronized-блок, захватывает монитор, связанный с объектом этого блока.
    - Пример создания synchronized-блока:
    ```Java
    private static final Object lock = new Object();
    private static void transfer(int amount) {
        synchronized (lock) {
            account1 = account1 - amount;
            account2 = account2 + amount;
        }
    }
    ```
    
7. **Замки** - являются более мощной версией synchronized-блока. Основные интерфейсы замков — `java.util.concurrent.locks.Lock` и `ReadWriteLock`, а наиболее полезные классы — `ReentrantLock` и `ReentrantReadWriteLock`.
    - Пример создания замка:
    ```Java
    private static final Lock lock = new ReentrantLock();
    lock.lock();
    try {
        // критическая секция
    } 
    finally { 
        lock.unlock(); 
    }
    ```
    
7. **Пулы потоков** - это набор потоков, которым можно передавать какие-либо задачи (например, Runnable) на выполнение. 
    - Создание потока — дорогая операция, и часто большинство задач выполняются недолго. Поэтому имеет смысл переиспользовать уже созданные потоки для  различных задач. 
    - Пример создания пула потоков:
    ```Java
    Executor executor = Executors.newFixedThreadPool(4);
    executor.execute(() -> /* ... */ );
    executor.execute(new Runnable() {
        @Override public void run() { /* ... */ } 
    });
    ```
    
8. **Жизненный цикл потока**. Поток проходит через несколько стадий своего жизненного цикла:
    - New - новый поток начинает свой жизненный цикл с изначального состояния. Он остается в нем до тех пор, пока программа не запустит его.
    - Runnable - после того, как поток создался, его надо запустить, в связи с чем, он перейдет в данное состояние. Поток в таком состоянии уже выполняет свои функции.
    - Waiting - иногда переходы между потоками занимают некоторое время, во время которого поток находится в таком состоянии, до тех пор, пока другой поток не переведет его в состояние runnable.
    - Timed waiting - runnable поток может установить время ожидания для какого-то события, после чего перейдет в данное состояние. Он перейдет обратно в runnable только после того, как истечет указанное время, или если событие, которого он ждет, произойдет.
    - Terminated - runnable поток завершается после выполнения своих функций (или его завершают) и переходит в данное состояние.
    - Диаграмма жизненого цикла потока:
    ![Диаграмма жизненого цикла потока](http://www.tutorialspoint.com/java/images/Thread_Life_Cycle.jpg)

9. **Приоритет** - каждый поток имеет приоритет, который помогает операционной системе распознавать порядок в котором потоки будут работать: `MIN_PRIORITY`, `NORM_PRIORITY`, `MAX_PRIORITY`.

***

### 8. Коллекции

1. **Массив**. Массивы встроены в язык и довольно производительны; они часто служат основой других коллекций.

2. **Интерфейс `Collection<T>`** является базовым интерфейсом для линейных коллекций. Он предоставляет основные операции, общие для всех коллекций.
    - Данный интерфейс предоставляет следующие методы: `add()`, `addAll()`, `clear()`, `contains()`, `containsAll()`, `equals()`, `hashCode()`, `isEmpty()`, `iterator()`, `remove()`, `removeAll()`, `size()`, `toArray()`.
    - Абстрактный класс `AbstractCollection` реализует большинство методов этого интерфейса.

3. **Интерфейс `List<T>`** является одним из наиболее часто используемых интерфейсов коллекций, который обозначает упорядоченную коллекцию. Каждый элемент списка имеет целочисленный индекс; возможно добавление и удаление элементов по индексу. Дополнительно этот интерфейс предоставляет специальный итератор `ListIterator<T>`, который позволяет перемещаться по списку в обе стороны и вставлять новые элементы.
    - Данный интерфейс предоставляет следующие методы: `get()`, `indexOf()`, `lastIndexOf()`, `listIterator()`, `set()`, `subList()`.
    - Абстрактный класс `AbstractList` наследуется от `AbstractCollection` и реализует большинство методов `List` интерфейса.
    - Абстрактный класс `AbstractSequentialList ` наследуется от `AbstractList` и реализует большинство методов `List` интерфейса с упором на последовательный, чем на случайный доступ к элементам.

4. **Реализация `ArrayList<T>`** используется чаще всего в интерфейсе `List`. По сути является реализацией списка на основе массива. Кроме того, `ArrayList` очень эффективно использует память, и операции, основанные на доступе по индексу (сортировка, перемешивание, бинарный поиск и т.д.), выполняются быстро.
    - Данная реализация предоставляет следующие методы: `ensureCapacity()`, `removeRange()`, `trimToSize()`, `clone()`.

5. **Реализация `LinkedList<T>`** используется гораздо реже. Является реализацией списка на основе двусвязного списка. `LinkedList` эффективнее при вставке/удалении элементов в начале или конце и при вставке/удалении в середине после итерации до нужного места. Также `LinkedList` потребляет значительно больше памяти, чем `ArrayList`.
    - Данная реализация предоставляет следующие методы: `addFirst()`, `addLast()`, `clone()`, `getFirst()`, `getLast()`, ` removeFirst()`, `removeLast()`.

6. **Интерфейс `Set<T>`** предоставляет абстракцию математического множества, т.е. неупорядоченную коллекцию, не содержащую одинаковых элементов. Из-за неупорядоченности элементы множества нельзя получить по их индексу, поэтому для множеств не имеет смысла сортировка и перемешивание элементов. Однако при этом операции проверки на наличие элемента во множестве эффективнее, чем в списке.
    - Данный интерфейс предоставляет следующие методы: `isEmpty()`.
    - Абстрактный класс `AbstractSet` наследуется от `AbstractCollection` и реализует большинство методов `Set` интерфейса.

7. **Интерфейс `SortedSet<T>`** является расширением `Set<T>`. Он предполагает наличие отношения порядка на своих элементах. Из-за этого `SortedSet` предоставляет дополнительные операции.
    - Данный интерфейс предоставляет следующие методы: `clone()`, `comparator()`, `first()`, `headSet()`, `last()`, `subSet()`, `tailSet()`.

8. **Реализация `HashSet<T>`** — это наиболее часто используемая реализация множества, потому что основные задачи множества она выполняет наиболее эффективно. HashSet основан на `HashMap`. Поэтому, в частности, для использования `HashSet` необходима правильная реализация методов `equals()` и `hashCode()`.
    - Данная реализация наследуется от `AbstractSet`.
    - Данная реализация предоставляет следующие методы: `clone()`.

9. **Реализация `LinkedHashSet<T>`** объединяет множество на основе хеш-таблицы и связный список. Эффективность всех операций на нём та же, что и у `HashSet`, но порядок итерации по нему не псевдослучаен, а соответствует порядку добавления элементов в это множество. `LinkedHashSet` основан на `LinkedHashMap` и наследует `HashSet`, поэтому для него также справедливы условия на методы `equals()` и `hashCode()` у элементов.
    - Данная реализация наследуется от `HashSet`.

10. **Реализация `TreeSet<T>`** — это множество, основанное на `TreeMap`. Оно реализует интерфейс `SortedSet<T>`, и в нём могут храниться только элементы, на которых задано отношение порядка. Класс `TreeSet` основан на `TreeMap`, и поэтому все операции над элементами имеют логарифмическую сложность. Это хуже, чем у `HashSet`, поэтому TreeSet используется только тогда, когда необходимо так или иначе сортировать элементы множества.
    - Данная реализация наследуется от `AbstractSet`.
    - Данная реализация предоставляет следующие методы: `clone()`, `comparator()`, `first()`, `last()`, `headSet()`, `subSet()`, `tailSet()`.

11. **Интерфейс `Queue<T>`** представляет собой контейнер, в который можно добавлять элементы и доставать их оттуда. Релизации `Queue<T>` могут ограничивать максимальное количество элементов в коллекции. Поэтому `Queue<T>` предоставляет два набора методов для указанных операций. Первый набор в граничных ситуациях выбрасывает исключение, а второй — возвращает специальное значение (null или boolean).
    - Абстрактный класс `AbstractQueue` наследуется от `AbstractCollection` и реализует большинство методов `Queue` интерфейса.
    - Данный интерфейс предоставляет следующие методы: `offer()`, `peek()`, `poll()`.

12. **Интерфейс `Deque<T>`** обозначает дек, структуру данных, являющуюся одновременно стеком и очередью. В дек можно добавлять и удалять элементы с двух сторон.
    - Данный интерфейс предоставляет следующие методы: `offer()`, `peek()`, `poll()`, `addFirst()`, `addLast()`, `descendingIterator()`, `element()`, `getFirst()`, `getLast()`, `offerFirst()`, `offerLast()`, `peekFirst()`, `peekLast()`, `pollFirst()`, `pollLast()`, `pop()`, `push()`, `removeFirst()`, `removeFirstOccurrence()`, `removeLast()`, `removeLastOccurrence()`, `size()`.

13. **Реализация `ArrayDeque<T>`** с помощью массива - наиболее удобная и эффективная.
    - Данная реализация наследуется от `AbstractCollection` и реализует интерфейс `Deque`.
    - Данный интерфейс предоставляет следующие методы: `isEmpty()`, `clone()`, `toArray()`.

14. **`java.util.Arrays`** предоставляет статические методы для манипуляций с массивами, такие как: `binarySearch()`, `equals()`, `fill()`, `sort()`.

15. **`java.util.Collections`** предоставляет статические методы для манипуляций с массивами, такие как: `binarySearch()`, `fill()`, `sort()`, `copy()`, `enumeration()`, `indexOfSubList()`, `lastIndexOfSubList()`, `list()`, `max()`, `min()`, `nCopies()`, `replaceAll()`, `reverse()`, `reverseOrder()`, `rotate()`, `shuffle()`, `singleton()`, `singletonList()`, `singletonMap()`, `swap()`, `synchronizedCollection()`, `synchronizedList()`, `synchronizedMap()`, `synchronizedSet()`, `synchronizedSortedMap()`, ` synchronizedSortedSet()`, `unmodifiableCollection()`, `unmodifiableList()`, `unmodifiableMap()`, `unmodifiableSet()`, `unmodifiableSortedMap()`, `unmodifiableSortedSet()`.

16. Иерархия коллекций  
    ![Иерархия коллекций](https://i.gyazo.com/c728629e97972ba7d715d23c2f3e7b51.png)

***

### 9. Мапы

1. **Интерфейс `Map<K, V>`** представляет абстракцию ассоциативного массива (словаря, отображения). Он хранит пары (ключ, значчение) и поддерживает три основные операции: `put`, `get`, `remove`. При этом предполагается, что ключи уникальны. Если операция `put` вызывается с ключом, который уже есть в ассоциативном массиве, соответствующее значение будет заменено.
    - Абстрактный класс `AbstractMap` реализует большинство методов `Map` интерфейса.
    - Данный интерфейс предоставляет следующие методы: `clear()`, `containsKey()`, `containsValue()`, `entrySet()`, `equals()`, `get()`, `hashCode()`, `isEmpty()`, `keySet()`, `put()`, `putAll()`, `remove()`, `size()`, `values()`.

2. **Интерфейс `SortedMap<K, V>`** обозначает словарь, в котором на ключах задано отношение порядка. Аналогично `SortedSet<T>`, `SortedMap<K, V>` предоставляет дополнительные операции. Предполагается, что эти операции словарь способен выполнять эффективно.
    - Данный интерфейс наследуется от `Map` интерфейса.
    - Данный интерфейс предоставляет следующие методы: `comparator()`, `firstKey()`, `headMap()`, `lastKey()`, `subMap()`, `tailMap()`.

3. **Реализация `HashMap<K, V>`** - словарь на основе хеш-таблицы. Из-за этого все операции над `HashMap` очень эффективны. HashMap реализован как хеш-таблица на основе цепочек. Внутри он содержит массив «корзин», каждая из которых является односвязным списком. Поэтому элементы словаря должны корректно реализовывать методы `equals()` и `hashCode()`. Для идеальной хеш-функции эффективность операций константная.
    - Данная реализация наследуется от `AbstractMap` и реализует `Map` интерфейс.
    - Данная реализация предоставляет следующие методы: `clone()`.

4. **Реализация `LinkedHashMap<K, V>`** объединяет хеш-таблицу и связный список. Используется, когда необходимо сохранять порядок добавления элементов в словарь. Помимо структуры хеш-таблицы, `LinkedHashMap` добавляет новые записи в связный список. С помощью этого можно восстановить порядок добавления элементов. Эффективность операций у `LinkedHashMap` та же, что и у обычного `HashMap`, но из-за дополнительной структуры на элементах потребление памяти выше.
    - Данная реализация наследуется от `HashMap` и реализует `Map` интерфейс.
    - Данная реализация предоставляет следующие методы: `removeEldestEntry()`.

5. **Реализация `TreeMap<K, V>`** — это реализация словаря на основе красно-чёрного бинарного дерева поиска (дерево образуют ключи). Эта структура требует отношения порядка на элементах, поэтому `TreeMap` реализует интерфейс `SortedMap`. Поскольку внутри `TreeMap` используется бинарное дерево, то все операции имеют логарифмическую эффективность.
    - Данная реализация наследуется от `AbstractMap` и реализует `SortedMap` интерфейс.
    - Данная реализация предоставляет следующие методы: `clone()`.

6. Иерархия мапов  
    ![Иерархия мапов](https://i.gyazo.com/edfb3a3797946a21747880fcac1507ba.png)

***


[pojo]: https://ru.wikipedia.org/wiki/POJO
[javabeans]: https://ru.wikipedia.org/wiki/JavaBeans