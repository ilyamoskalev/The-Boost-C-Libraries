#Algorithms

Вы можете думать о диапазоне как о двух итераторах, которые ссылаются на начало и конец группы элементов, которые можно перебирать. Поскольку все контейнеры поддерживают итераторы, каждый контейнер можно рассматривать как диапазон. Поскольку все алгоритмы из Boost.Range ожидают диапазона в качестве первого параметра, контейнер `Std :: vector` может быть передан непосредственно. Вам не нужно вызывать `begin()` и `end()`, а затем передать два итератора отдельно. Это защищает вас от ошибок, таких как передача итераторов begin()` и `end() в неправильном порядке или передачи итераторов, которые принадлежат двум разным контейнерам.

<a name="ex.graph_01"/>
Ghbvth 30.1. Считаем с помощью `boost::count()`
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