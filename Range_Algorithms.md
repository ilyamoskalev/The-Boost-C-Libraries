#Algorithms

Вы можете думать о диапазоне как о двух итераторах, которые ссылаются на начало и конец группы элементов, которые можно перебирать. Поскольку все контейнеры поддерживают итераторы, каждый контейнер можно рассматривать как диапазон. Поскольку все алгоритмы из Boost.Range ожидают диапазона в качестве первого параметра, контейнер `Std :: vector` может быть передан непосредственно. Вам не нужно вызывать `begin()` и `end()`, а затем передать два итератора отдельно. Это защищает вас от ошибок, таких как передача итераторов begin()` и `end() в неправильном порядке или передачи итераторов, которые принадлежат двум разным контейнерам.

<a name="ex.graph_01"/>
Пример 30.1. Считаем с помощью `boost::count()`
```c++
#include <boost/range/algorithm.hpp>
#include <array>
#include <iostream>

int main()
{
  std::array<int, 6> a{{0, 1, 0, 1, 0, 1}};
  std::cout << boost::count(a, 0) << '\n';
}
```


[Пример 30.1](#ex.graph_01) использует алгоритм `boost :: count ()`, который определен в `boost / range / algorithm.hpp`. Этот заголовочный файл обеспечивает доступ ко всем алгоритмам, для которых существуют аналоги в заголовочном файле стандартной библеотеки `algorithm`.

Все алгоритмы из Boost.Range требуют , чтобы первый параметр был диапазоном. Объект типа `Std :: array` может быть передан в Boost :: Count () напрямую, так как контейнеры являются диапазоном. Поскольку `Boost :: count ()` эквивалентно `Std :: count ()`, вы должны передать в значение,с которым будут сравниваться элементы диапазона.

В [Примере 30.1](#ex.graph_01), **a** содержит три 0 , так **3** записывается в стандартный поток вывода.

[Пример 30.2](#ex.graph_02) представляет больше алгоритмов, которые, как `Boost :: count ()`, аналогичны алгоритмам из стандартной библиотеки.

<a name="ex.graph_02"/>
Пример 30.2. Range алгоритмы, связанные с алгоритмами из стандартной библиотеки
```c++
#include <boost/range/algorithm.hpp>
#include <boost/range/numeric.hpp>
#include <array>
#include <iterator>
#include <iostream>

int main()
{
  std::array<int, 6> a{{0, 1, 2, 3, 4, 5}};
  boost::random_shuffle(a);
  boost::copy(a, std::ostream_iterator<int>{std::cout, ","});
  std::cout << "\n" << *boost::max_element(a) << '\n';
  std::cout << boost::accumulate(a, 0) << '\n';
}
```

`boost :: random_shuffle ()` работает как `std :: random_shuffle ()`, изменяя порядок элементов в диапазоне случайным образом. [Пример 30.2](#ex.graph_02) использует `boost :: random_shuffle ()` генератор случайных чисел по умолчанию. Тем не менее, вы можете передать генератор случайных чисел в качестве второго параметра. Это может быть генератор случайных чисел либо из файла заголовка C ++ 11 `random` или из Boost.Random.

`boost::copy()` работает как `std::copy()`. `boost::max_element()` и `Boost::accumulate()` работатют также, как и одноименные алгоритмы из стандартной библиотеки. Как и `std::max_element()`, `boost::max_element()` возвращает итератор на элемент с наибольшим номером.

Заголовочный файл `boost/range/numeric.hpp` должен быть подключен для `boost::accumulate()`. Как и `std::accumulate()` определен в `numeric`, `boost::accumulate()` определен `boost/range/numeric.hpp` , а не в `boost/range/algorithm.hpp`.

Boost.Range также предоставляет несколько алгоритмов без аналогов в стандартной библиотеке.
<a name="ex.graph_03"/>
Пример 30.3. Range алгоритмы без аналогов в стандартной библиотеке.
```c++
#include <boost/range/algorithm_ext.hpp>
#include <array>
#include <deque>
#include <iterator>
#include <iostream>

int main()
{
  std::array<int, 6> a{{0, 1, 2, 3, 4, 5}};
  std::cout << std::boolalpha << boost::is_sorted(a) << '\n';
  std::deque<int> d;
  boost::push_back(d, a);
  boost::remove_erase(d, 2);
  boost::copy_n(d, 3, std::ostream_iterator<int>{std::cout, ","});
}
```

Алгоритмы, используемые в  [Примере 30.3](#ex.graph_03),требуют заголовочный файл`boost/range/algorithm_ext.hpp`. Этот заголовочный файл предоставляет доступ к алгоритмам,которые не имеют аналогов в стандартной библиотеке.

`boost::is_sorted()` проверяет отсортированы ли элементы в диапозоне. В  [Примере 30.3](#ex.graph_03), `boost::is_sorted()` возвращает `true` так как **a** отсортирован. Предикат может быть передан в качестве второго параметра в `boost::is_sorted()`,например, для того чтобы проверить, отсортирован ли диапозон в порядке убывания.

`boost::push_back()` принимает в качестве первого параметра контейнер и в качестве второго параметра диапозон. Контейнер должен определить функцию-член `push_back()`. Все элементы из диапозона добавляются в контейнер с помощью этой функции,в порядке определенным в диапозоне.Так как **d** создается пустым, он будет содержать те же цифры, что и
 **a**, в том же порядке, после вызова `boost::push_back()`.
 
`boost::remove_erase()` удаляет 2 из **d**. Этот алгоритм объединяет вызов функции `std::remove()` и вызов функции-члена `erase()` соответствующего контейнера. Благодаря `boost::remove_erase()`, вам не нужно искать итератор, указывающий на элемент, который нужно удалить, и передавать его в `erase()` вторым шагом.

`boost::copy_n()` аналогичен с `boost::copy()`, но копирует столько элементов, сколько передается в качестве второго параметра. [Пример 30.3](#ex.graph_03) выводит в стандартный поток вывода только первые три числа из **d**.Будет выведено 0,1,3, так как 2 было удалено из **d** в предыдущей строке.


