# Спецкурс по Java (2019)

2. [Лабораторная работа №2](#lab2)
3. [Лабораторная работа №3](#lab3)
4. [Лабораторная работа №4](#lab4)
5. [Лабораторная работа №5](#lab5)
6. [Лабораторная работа №6](#lab6)
7. [Лабораторная работа №7](#lab7)

## Лабораторная работа №2 <a name="lab2"></a>
Знакомство с основными конструкциями языка Java, принципами создания классов.

![](README/lab2.gif)

### Описание
Создан класс, реализующий работу с векторами (набор вещественных чисел, координат) и базовые операции векторной арифметики. Класс удовлетворяет следующим требованиям:
  * Экземпляр соответствовует вектору фиксированной длины (она задаётся как параметр конструктора).
  * Реализованы следующие методы:
    * доступа к элементам вектора (получения значения и изменения значения);
    * получения «длины» вектора (количества его элементов);
    * поиска минимального и максимального значений из элементов вектора;
    * сортировки вектора (по возрастанию и убыванию);
    * нахождения евклидовой нормы;
    * умножения вектора на число;
    * сложения двух векторов;
    * нахождения скалярного произведения двух векторов.

## Лабораторная работа №3 <a name="lab3"></a>
Знакомство с концепцией интерфейсов и исключительными ситуациями в Java.
### Описание
1. Описаны два класса с идентичным внешним представлением, принадлежащие одной предметной области. Оба класса содержат:
* поле — массив, поле строкового типа, поле целого типа;
* конструктор по умолчанию и конструктор с параметрами, позволяющие полностью инициализировать объект;
* методы доступа к элементам массивов и к полям;
* функциональный метод, реализующий некоторую функцию от элементов массива и полей объектов классов.
2. Описан интерфейс, задающий список сигнатур методов доступа к полям объектов и функционального метода, оба класса реализовывают интерфейс.
3. В классах переопределены методы класса Object: toString(), equals(), hashCode().
4. Организована база (массив) объектов типа интерфейс, которая заполняется объектами описанных типов вперемежку (по желанию пользователя). Возможны следующие действия:
* вывод полной информации обо всех объектах массива;
* поиск в массиве объектов, функциональный метод которых возвращают одинаковый результат, и помещение таких объектов в другой массив; 
* разбиение исходного массива на два массива, в которых хранятся однотипные элементы;
5. При описании классов описано одно объявляемое (наследное от Exception) и одно необъявляемое (наследное от RuntimeException) исключения, характеризующие ошибки, связанные с выполнением методов классов. В соответствующих методах выбрасываются/контролируются описанные исключения.
### Cемантика
Класс «Серия сочинений» (поле — массив хранит количество страниц в каждой книге серии, второе поле — название серии, третье поле — количество страниц в книге, занятых вводной информацией, функциональный метод — подсчёт общего количества страниц серии без учёта вводных страниц книг) и класс «Сборник статей» (поле — массив хранит количество страниц каждой статьи, второе поле — название сборника, третье поле — максимально допустимое количество страниц для аннотации статьи, функциональный метод — подсчёт общего количества страниц без учёта аннотаций статей).

## Лабораторная работа №4 <a name="lab4"></a>
Знакомство с механизмом ввода/вывода в Java.

![](README/lab4-1.gif)

![](README/lab4-2.gif)

![](README/lab4-3.gif)

### Описание
1. Модифицированы классы из Лабораторной работы №4 следующим образом:
* в интерфейс добавлены следующие методы:
  * записи в байтовый поток void output(OutputStream out);
  * записи в символьный поток void write(Writer out);
  * реализованы добавленные в интерфейс методы в обоих классах;
* описан класс со следующими статическими методами:
  * записи в байтовый поток void output<Интерфейс>(<Интерфейс> o, OutputStream out);
  * чтения из байтового потока <Интерфейс> input<Интерфейс>(InputStream in);
  * записи в символьный поток void write<Интерфейс> (<Интерфейс> o, Writer out);
  * чтения из символьного потока <Интерфейс> read<Интерфейс>(Reader in).

В статических методах записи делегирован вызов соответствующему методу интерфейса.
В обоих случаях записанный объект представляет собой последовательность значений своих полей.

2. Модифицированы классы в иерархии таким образом, что сериализуемы.
Добавлены в класс со статическими методами методы для вывода/ввода сериализованных объектов:
* вывод сериализованных объектов void serialize<Интерфейс> (<Интерфейс> o, OutputStream out);
* ввод десериализованного объекта <Интерфейс> deserialize<Интерфейс>(InputStream in).
3. Организован примитивный интерфейс пользователя (заполнение базы элементов с консоли, выбор типа элемента пользователем). Протестированы разработанные методы работы с потоками, а также возможности сериализации.

## Лабораторная работа №5 <a name="lab5"></a>
Знакомство с общими принципами создания многопоточных приложений.

![](README/lab5.gif)

### Задание 1
Созданы два класса нитей, наследующие от класса Thread, взаимодействующие друг с другом с помощью промежуточного объекта типа интерфейс из ЛР3.

Первая нить последовательно заполняет поле-массив промежуточного объекта произвольными различными величинами. Каждый раз, когда она помещает значение в массив, она выводит на экран сообщение вида “WRITE ### TO POSITION ###”. По достижении конца массива нить заканчивает своё выполнение.

Вторая нить последовательно считывает значения из массива и выводит их на экран сообщениями вида “READ ### FROM POSITION ###”. По достижении конца массива нить заканчивает своё выполнение.

В методе main() созданы 3 участвующих в процессе объекта (две нити и объект интерфейса для записи/чтения в него).
### Задание 2
Созданы два новых класса нитей (реализуют интерфейс Runnable), обеспечивающие последовательность операций чтения-записи (т.е. на экран сообщения выводятся в порядке write-read-write-read-…) независимо от приоритетов потоков. Для этого описан некий вспомогательный класс <Интерфейс>Synchronizer, объект которого используется при взаимодействии нитей.
### Задание 3
Добавлена в класс со статическими методами обработки объектов (созданный в ЛР4) реализация метода <Интерфейс> synchronized<Интерфейс> (<Интерфейс> i), возвращающий ссылку на оболочку указанного интерфейса, безопасная с точки зрения многопоточности. Для этого описан новый класс, реализующий интерфейс <Интерфейс> и представляющий собой оболочку, синхронизирующую все методы интерфейса (состоящая из синхронизированных методов интерфейса).
## Лабораторная работа №6 <a name="lab6"></a>
Знакомство с механизмом образцов проектирования «Итератор», «Декоратор» и упрощённой версией «Фабричного метода».
### Задание 1
Модифицирован интерфейс таким образом, чтобы он реализовывал интерфейс java.util.Iterable.

Реализован метод java.util.Iterator iterator(), унаследованный из интерфейса, в двух классах. Для этого описан дополнительный класс итератора с соответствующими методами итератора (из стандартного интерфейса java.util.Iterator). Объект итератора возвращается из метода iterator() классов. Итератор позволяет обойти все элементы поля-массива.
### Задание 2
Проверена работа итератора (с использованием улучшенного цикла for).
### Задание 3
Добавлено в класс со статическими методами описание ещё одного статического метода <Интерфейс> unmodifiable<Интерфейс>(<Интерфейс> о), возвращающего ссылку на экземпляр неизменяемой оболочки указанного объекта. Для этого описан новый класс-декоратор для типа <Интерфейс>, который содержит объект типа <Интерфейс>, сам реализует <Интерфейс>, а все методы интерфейса делегирует внутреннему объекту, кроме методов изменения объекта. Декоратор выбрасывает исключение UnsupportedOperationException в случае попытки изменения состояния внутреннего объекта.
### Задание 4
Описан новый интерфейс <Интерфейс>Factory, содержащий единственный метод createInstance() для создания экземпляра по умолчанию.
### Задание 5
В классе со статическими методами создано приватное статическое поле factory типа <Интерфейс>Factory и соответствующий ему публичный метод set<Интерфейс>Factory, позволяющие, соответственно, хранить ссылку и устанавливать ссылку на текущую фабрику объектов. Для каждого типа объекта из иерархии нужно описан класс соответствующей фабрики (реализующей метод createInstance()). По умолчанию поле ссылается на объект одного из двух класса Factory, порождающего экземпляры одного из классов.
### Задание 6
В классе со статическими методами описан метод public static createInstance(), с помощью текущей фабрики создающий новый экземпляр объекта. В остальных методах прямое создание экземпляров заменено на вызов этого метода.

## Лабораторная работа №7 <a name="lab7"></a>
Знакомство с технологией Swing, обработкой событий и PLaF.

![](README/lab7.gif)

### Задание 1
Написано оконное Swing-приложение для игры в «больше-меньше». Игра заключается в следующем: пользователь загадывает число из указанного диапазона, приложение пытается его угадать. На каждое предположение приложения о загаданном числе пользователь указывает, является ли загаданное число больше, меньше, или приложение угадало. 

Приложение реализовано со следующей функциональностью:
* ввод минимального и максимального значений диапазона, из которого пользователь может загадать число;
* предположение приложения о загаданном пользователем числе;
* указание пользователя, является ли предположенное число больше или меньше загаданного;
* вывод завершающего сообщения о победе и предложение сыграть ещё раз;
* вывод завершающего сообщения о жульничестве и предложение сыграть ещё раз.
### Задание 2
Добавлена на форму радиокнопка на несколько позиций, соответствующих различным доступным PLaF. При выборе пользователем одного из предлагаемых значений изменяется внешний вид программы.
