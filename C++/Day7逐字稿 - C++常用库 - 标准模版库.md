C++常用类，

string、

文件IO操作

STL（Vector、list、Set、Map）、

进程线程

Boost（网络操作、进程线程）、



===================



## 标准模板库 (STL)

​	C++的标准模板库，不但是我们在开发中的必知必会，甚至可以说是C++程序员手中最常用的那把步枪。

​	《*STL* 源码剖析》这是目前公认的STL最好的一本书，应该没有之一。作为一个C++程序员，我建议你们都读一读，不论在认知水平上，还是在面试的信心上都会上一个台阶。我不止一次听到友商的面试官对这本书的Check。

### 	大体分类

C++常用的标准模板库（STL）主要包括以下几个部分：

1. **容器（Containers）**：
   - `vector`：+动态数组，支持快速访问和末尾插入/删除操作。
   - `deque`：双端队列，与vector类似，但支持在两端进行插入和删除操作。
   - `list`：+双向链表，支持快速的插入/删除操作。
   - `queue`：队列，先进先出（FIFO）的数据结构。
   - `stack`：栈，后进先出（LIFO）的数据结构。
   - `set`：+集合，包含唯一元素的容器。
   - `multiset`：多重集合，允许存储重复元素的集合。
   - `map`：+映射，存储键值对，并根据键进行排序。
   - `multimap`：多重映射，允许存储键重复的键值对。
2. **算法（Algorithms）**：
   - 排序算法，如`sort`。
   - 查找算法，如`find`。
   - 以及其他各种通用的算法操作。
3. **迭代器（Iterators）**：
   - `random_access_iterator`：随机访问迭代器，支持像数组一样的索引访问。
   - `bidirectional_iterator`：双向迭代器，支持向前和向后遍历。
   - `forward_iterator`：前向迭代器，仅支持向前遍历。
   - `input_iterator` 和 `output_iterator`：用于输入和输出的迭代器。
4. **函数对象（Function Objects）**：也称为仿函数，它们的行为类似函数，但可以作为对象进行操作。
5. **适配器（Adaptors）**：用于改变容器、迭代器或函数对象行为的类模板。

这些STL组件为C++程序员提供了强大的工具和资源，使得他们可以编写出高质量、高效率的程序。STL几乎渗透在C++程序的角角落落里，无论是开发底层系统还是开发上层应用，STL都扮演着不可或缺的角色。同时，由于STL已经被内置到支持C++的编译器中，无需额外安装，这也使得STL被广泛使用。

### 迭代器

在STL（Standard Template Library）中，迭代器（Iterators）是一种设计模式，它使得程序员能够顺序地访问容器（如vector、list、map等）中的元素。迭代器类似于指针，它们提供了一种抽象的方式来遍历和操作容器中的元素，而不需要关心容器底层的实现细节。

#### 	迭代器类型

STL迭代器可以分为几种类型，包括：

- 输入迭代器（Input Iterators）：只能用于读取容器中的元素。
- 输出迭代器（Output Iterators）：只能用于向容器中写入元素。
- 前向迭代器（Forward Iterators）：可以读写元素，且支持递增操作，但不支持递减。
- 双向迭代器（Bidirectional Iterators）：可以读写元素，并支持递增和递减操作。
- 随机访问迭代器（Random Access Iterators）：提供完全的功能，包括读写、递增、递减以及元素间的算术运算。

#### 	迭代器的基本操作

迭代器支持一系列基本操作，包括：

- 解引用操作（Dereferencing）：通过`*it`获取迭代器`it`指向的元素的值。
- 递增操作（Incrementing）：通过`++it`将迭代器向前移动到下一个元素。
- 递减操作（Decrementing）：对于双向和随机访问迭代器，可以通过`--it`将迭代器向后移动到前一个元素。
- 比较操作（Comparison）：可以比较两个迭代器是否相等（`it1 == it2`）或不等（`it1 != it2`），也可以判断一个迭代器是否在另一个迭代器之前（`it1 < it2`）或之后（`it1 > it2`）。

#### 	迭代器使用示例

以下是一个使用迭代器的简单示例，它遍历一个`std::vector`并打印出每个元素的值：

```cpp
#include <iostream>  
#include <vector>  
using namespace std;  
  
int main() {  
    // 创建一个包含一些整数的vector  
    vector<int> numbers = {1, 2, 3, 4, 5};  
  
    // 获取指向vector开始和结束的迭代器  
    vector<int>::iterator it_begin = numbers.begin();  
    vector<int>::iterator it_end = numbers.end();  
  
    // 使用迭代器遍历vector并打印元素  
    for (vector<int>::iterator it = it_begin; it != it_end; ++it) {  
        cout << *it << " ";  
    }  
    cout << endl;  
  
    // 也可以使用基于范围的for循环，它内部也是使用迭代器  
    for (int num : numbers) {  
        cout << num << " ";  
    }  
    cout << endl;  
  
    return 0;  
}
```

在上面的代码中，我们首先创建了一个包含整数的`vector`。然后，我们使用`begin()`和`end()`成员函数获取指向`vector`开始和结束的迭代器。我们通过一个传统的for循环遍历迭代器，并使用解引用操作`*it`来获取每个元素的值。最后，我们还展示了一个基于范围的for循环，这种循环在C++11及以后的版本中非常常见，它内部也是使用迭代器来遍历容器。

需要注意的是，`end()`返回的迭代器指向容器“尾后”的位置，即最后一个元素之后的位置。因此，在循环中，我们应该检查迭代器是否等于`end()`，而不是大于它。

迭代器是STL中一个非常重要的概念，它们提供了一种统一的方式来访问和操作各种不同类型的容器。掌握迭代器的使用是理解和使用STL的关键之一。



### 	vector

`std::vector` 是C++标准模板库（STL）中提供的一个动态数组容器。它可以根据需要动态地增长或缩小，从而存储任意数量的同类型元素。`std::vector` 提供了一系列成员函数来操作其包含的元素，如添加、删除、访问和修改等。

​	可以看着是内部封装了数组的对象，内部自动改变数组的大小。画图讲解。。。

#### 		主要特性

1. **动态大小**：`std::vector` 可以根据需要动态地分配和释放内存，以适应存储的元素数量的变化。

2. **连续存储**：`std::vector` 保证其内部元素在内存中连续存储，这使得它可以像数组一样通过索引直接访问元素，并且元素的访问速度非常快。

3. **随机访问迭代器**：由于元素连续存储，`std::vector` 提供了随机访问迭代器，允许在常数时间内访问任意位置的元素。

   

#### 		主要成员函数

1. `push_back(const T& value)`：在向量末尾添加一个元素。
2. `pop_back()`：删除向量末尾的元素。
3. `size()`：返回向量中元素的个数。
4. `empty()`：检查向量是否为空。
5. `at(size_t pos)`：返回指定位置的元素（带边界检查）。
6. `operator[](size_t pos)`：返回指定位置的元素（不带边界检查）。
7. `begin()` 和 `end()`：返回指向向量开头和末尾的迭代器。
8. `clear()`：删除向量中的所有元素。
9. `insert(iterator pos, const T& value)`：在指定位置插入一个元素。
10. `erase(iterator pos)`：删除指定位置的元素。



#### 		示例

下面是一个简单的例子，展示了如何使用 `std::vector`：

```cpp
#include <iostream>  
#include <vector>  
  
int main() {  
    // 创建一个空的vector<int>  
    std::vector<int> vec;  
  
    // 使用push_back添加元素  
    vec.push_back(1);  
    vec.push_back(2);  
    vec.push_back(3);  
  
    // 输出vector的大小  
    std::cout << "Size of vector: " << vec.size() << std::endl;  
  
    // 使用at访问并输出元素  
    for (size_t i = 0; i < vec.size(); ++i) {  
        std::cout << "Element at position " << i << ": " << vec.at(i) << std::endl;  
    }  
  
    // 使用[]访问并修改元素  
    for (size_t i = 0; i < vec.size(); ++i) {  
        vec[i] *= 2; // 将每个元素乘以2  
    }  
  
    // 输出修改后的vector  
    std::cout << "Modified vector:" << std::endl;  
    for (const auto& elem : vec) {  
        std::cout << elem << " ";  
    }  
    std::cout << std::endl;  
  
    // 在特定位置插入元素  
    vec.insert(vec.begin() + 1, 4); // 在第二个位置插入4  
  
    // 删除特定位置的元素  
    vec.erase(vec.begin() + 2); // 删除第三个位置的元素  
  
    // 再次输出vector，使用begin()和end()  
    std::cout << "Vector after insert and erase:" << std::endl;  
    for (std::vector<int>::iterator it = vec.begin(); it != vec.end(); ++it) {  
        std::cout << *it << " ";  
    }  
    std::cout << std::endl;  
    
    return 0;  
}
```

在这个例子中，我们首先创建了一个空的 `std::vector<int>`，然后使用 `push_back` 方法向其中添加了几个整数。接着，我们遍历并输出了向量的每个元素，然后使用 `[]` 运算符修改了这些元素的值。之后，我们在向量的特定位置插入了一个新元素，并删除了另一个元素。最后，我们再次输出了修改后的向量。

这个简单的例子展示了 `std::vector` 的基本用法和其主要成员函数的一些用途。在实际应用中，`std::vector` 的用途非常广泛，几乎在任何需要动态数组的地方都可以使用它。

### List

`std::list` 是C++标准模板库（STL）中的一种双向链表容器。与数组和`std::vector`不同，`std::list`的元素在内存中不是连续存储的，而是通过指针或迭代器链接在一起。这种结构使得`std::list`在插入和删除元素时具有较高的效率，因为不需要移动其他元素来保持连续性。

#### 	主要特性

1. **双向链表**：`std::list`中的每个元素都保存着指向其前一个元素和后一个元素的指针（或迭代器）。这使得从任意位置向前或向后遍历都很容易。
2. **动态大小**：`std::list`的大小可以动态地增长或缩小，以适应存储的元素数量的变化。
3. **高效插入和删除**：在`std::list`中插入或删除元素通常只需要更新相邻元素的指针，而不需要移动其他元素。因此，在列表中间插入或删除元素通常比在`std::vector`中更快。



#### 	主要成员函数

1. `push_back(const T& value)`：在列表末尾添加一个元素。
2. `push_front(const T& value)`：在列表开头添加一个元素。
3. `pop_back()`：删除列表末尾的元素。
4. `pop_front()`：删除列表开头的元素。
5. `insert(iterator pos, const T& value)`：在指定位置插入一个元素。
6. `erase(iterator pos)`：删除指定位置的元素。
7. `remove(const T& value)`：删除所有等于给定值的元素。
8. `sort()`：对列表中的元素进行排序。
9. `size()`：返回列表中元素的个数。
10. `empty()`：检查列表是否为空。
11. `begin()` 和 `end()`：返回指向列表开头和末尾的迭代器。
12. `rbegin()` 和 `rend()`：返回指向列表末尾和开头的反向迭代器，用于反向遍历列表。



#### 	示例1 添加删除与遍历

下面是一个简单的例子，展示了如何使用 `std::list`：

```cpp
#include <iostream>  
#include <list>  
  
int main() {  
    // 创建一个空的std::list<int>  
    std::list<int> myList;  
  
    // 使用push_back在列表末尾添加元素  
    myList.push_back(1);  
    myList.push_back(2);  
    myList.push_back(3);  
  
    // 输出列表的大小  
    std::cout << "Size of list: " << myList.size() << std::endl;  
  
    // 使用迭代器遍历并输出列表中的元素  
    for (std::list<int>::iterator it = myList.begin(); it != myList.end(); ++it) {  
        std::cout << *it << " ";  
    }  
    std::cout << std::endl;  
  
    // 使用push_front在列表开头添加元素  
    myList.push_front(0);  
  
    // 使用insert在指定位置插入元素  
    std::list<int>::iterator it = myList.begin();  
    std::advance(it, 2); // 将迭代器移动到第三个位置（从0开始计数）  
    myList.insert(it, 4); // 在第三个位置插入4  
  
    // 输出修改后的列表  
    std::cout << "Modified list:" << std::endl;  
    for (const auto& elem : myList) { // 使用基于范围的for循环遍历  
        std::cout << elem << " ";  
    }  
    std::cout << std::endl;  
  
    // 删除指定位置的元素  
    it = myList.begin();  
    std::advance(it, 3); // 将迭代器移动到第四个位置  
    myList.erase(it); // 删除该位置的元素  
  
    // 再次输出列表  
    std::cout << "List after erase:" << std::endl;  
    for (const auto& elem : myList) {  
        std::cout << elem << " ";  
    }  
    std::cout << std::endl;  
  
    return 0;  
}
```

在这个例子中，我们首先创建了一个空的`std::list<int>`，然后使用`push_back`和`push_front`在列表的末尾和开头添加元素。接着，我们使用迭代器遍历并输出了列表中的元素。之后，我们使用`insert`在指定位置插入了新元素，并使用基于范围的for循环输出了修改后的列表。最后，我们使用`erase`删除了指定位置的元素，并再次输出了列表。

#### 	示例2 排序

再来看个例子

```cpp
#include <iostream>  
#include <list>  
#include <algorithm> // 需要包含这个头文件来使用 sort()  
  
int main() {  
    // 创建一个std::list<int>并初始化一些元素  
    std::list<int> myList = {5, 3, 1, 4, 2};  
  
    // 输出未排序的列表  
    std::cout << "Unsorted list: ";  
    for (const auto& elem : myList) {  
        std::cout << elem << " ";  
    }  
    std::cout << std::endl;  
  
    // 使用sort()对列表进行排序  
    myList.sort();  
  
    // 输出排序后的列表  
    std::cout << "Sorted list: ";  
    for (const auto& elem : myList) {  
        std::cout << elem << " ";  
    }  
    std::cout << std::endl;  
  
    // 使用rbegin()和rend()进行反向遍历  
    std::cout << "Reverse traversal of sorted list: ";  
    for (auto it = myList.rbegin(); it != myList.rend(); ++it) {  
        std::cout << *it << " ";  
    }  
    std::cout << std::endl;  
  
    return 0;  
}

/* 输出结果
Unsorted list: 5 3 1 4 2   
Sorted list: 1 2 3 4 5   
Reverse traversal of sorted list: 5 4 3 2 1
*/
```

在这个例子中，我们首先创建了一个 `std::list<int>` 并初始化了几个整数。然后我们使用 `sort()` 函数对列表进行排序。排序后，我们首先使用正向迭代器遍历并输出排序后的列表。接着，我们使用 `rbegin()` 和 `rend()` 来获取反向迭代器，并使用它们从列表的末尾开始反向遍历列表，输出每个元素。



#### 	示例3 splice、unique、merge

除了上面提到的基本成员函数，`std::list` 还支持一些其他的操作，比如 `splice`（将一个列表的元素移动到另一个列表），`unique`（删除连续重复的元素），`merge`（合并两个已排序的列表）等。这些函数提供了更多的灵活性，使得 `std::list` 在处理复杂的数据结构时非常有用。

```cpp
#include <iostream>  
#include <list>  
  
/////////////////////////////////// `splice`的使用
int main() {  
    // 创建两个列表 list1 和 list2  
    std::list<int> list1 = {1, 2, 3, 4, 5};  
    std::list<int> list2 = {6, 7, 8, 9, 10};  
  
    // 输出原始列表  
    std::cout << "Original list1: ";  
    for (int num : list1) {  
        std::cout << num << " ";  
    }  
    std::cout << std::endl;  
    std::cout << "Original list2: ";  
    for (int num : list2) {  
        std::cout << num << " ";  
    }  
    std::cout << std::endl;  
  
    // 将 list2 的前两个元素移动到 list1 的末尾  
    auto it = list2.begin();  
    std::advance(it, 2); // 移动到第三个位置的前一个迭代器  
    list1.splice(list1.end(), list2, list2.begin(), it);  
    // splice的本意可以理解成合并，这里增加的参数是合并的大小
    // list1.splice(list1.end(), list2);  
  
    // 输出移动后的列表  
    std::cout << "List1 after splice: ";  
    for (int num : list1) {  
        std::cout << num << " ";  
    }  
    std::cout << std::endl;  
    std::cout << "List2 after splice: ";  
    for (int num : list2) {  
        std::cout << num << " ";  
    }  
    std::cout << std::endl;  
  
    return 0;  
}
// 在 `splice` 示例中，我们将 `list2` 的前两个元素移动到 `list1` 的末尾。`splice` 函数接受一个目标迭代器（指定移动元素应该放置的位置）和两个源迭代器（定义要移动的元素的范围）。

/////////////////////////////////// `unique`的使用
int main() {  
    // 创建一个包含重复元素的列表  
    std::list<int> myList = {1, 2, 2, 3, 3, 3, 4, 4, 4, 4};  
  
    // 输出原始列表  
    std::cout << "Original list with duplicates: ";  
    for (int num : myList) {  
        std::cout << num << " ";  
    }  
    std::cout << std::endl;  
  
    // 删除连续重复的元素  
    myList.unique();  
  
    // 输出删除重复元素后的列表  
    std::cout << "List after unique(): ";  
    for (int num : myList) {  
        std::cout << num << " ";  
    }  
    std::cout << std::endl;  
  
    return 0;  
}
// 在 `unique` 示例中，我们删除了`unique` 示例中的连续重复元素。`unique` 函数会删除列表中连续的重复元素，它依赖于元素的顺序。


/////////////////////////////////// `merge`的使用
int main() {  
    // 创建两个已排序的列表  
    std::list<int> list1 = {1, 3, 5};  
    std::list<int> list2 = {2, 4, 6};  
  
    // 输出原始列表  
    std::cout << "Original list1: ";  
    for (int num : list1) {  
        std::cout << num << " ";  
    }  
    std::cout << std::endl;  
    std::cout << "Original list2: ";  
    for (int num : list2) {  
        std::cout << num << " ";  
    }  
    std::cout << std::endl;  
  
    // 合并两个列表  
    list1.merge(list2);  
  
    // 输出合并后的列表  
    std::cout << "Merged list: ";  
    for (int num : list1) {  
        std::cout << num << " ";  
    }  
    std::cout << std::endl;  
  
    // list2 现在为空，因为所有元素都已移动到 list1  
    std::cout << "list2 after merge: ";  
    for (int num : list2) {  
        std::cout << num << " ";  
    }  
    std::cout << std::endl;  
  
    return 0;  
}
// 对于 `merge` 示例，它合并两个已排序的列表。这里不需要额外的修改，因为 `merge` 函数会自动处理合并操作，并将 `list2` 的所有元素移动到 `list1` 中，同时保持排序顺序。在合并后，`list2` 会变为空，因为所有元素都已经被移动到 `list1` 中。
```

这些示例展示了 `std::list` 的一些高级用法，特别是处理列表元素时的灵活性和效率。在实际应用中，根据具体需求选择合适的成员函数可以大大提高代码的可读性和效率。

#### 示例4 特殊结构排序

当需要对自定义数据结构的对象进行排序时，确实需要为这些对象定义比较规则。在C++中，你可以通过为自定义数据结构重载 `<` 运算符或者提供一个自定义的比较函数（或函数对象）来实现这一点。这里我将为你提供一个例子，说明如何为自定义数据结构进行排序。

假设你有一个简单的自定义数据结构 `Person`，包含姓名（`name`）和年龄（`age`），你想要根据年龄对 `Person` 对象进行排序：

```cpp
#include <iostream>  
#include <list>  
#include <algorithm>  
#include <string>  
  
// 自定义数据结构 Person  
struct Person {  
    std::string name;  
    int age;  
  
    // 构造函数  
    Person(std::string n, int a) : name(n), age(a) {}  
  
    // 重载 '<' 运算符以定义比较规则  
    bool operator<(const Person& other) const {  
        return age < other.age;  
    }  
};  
  
int main() {  
    // 创建一个包含 Person 对象的 list  
    std::list<Person> people = {  
        {"Alice", 30},  
        {"Bob", 20},  
        {"Charlie", 25},  
        {"Dave", 20}  
    };  
  
    // 输出原始列表  
    std::cout << "Original list of people:" << std::endl;  
    for (const auto& person : people) {  
        std::cout << person.name << ": " << person.age << std::endl;  
    }  
  
    // 使用 sort 对 list 进行排序  
    people.sort(); // 这里会自动调用我们重载的 '<' 运算符  
  
    // 输出排序后的列表  
    std::cout << "Sorted list of people by age:" << std::endl;  
    for (const auto& person : people) {  
        std::cout << person.name << ": " << person.age << std::endl;  
    }  
  
    return 0;  
}
```

在这个例子中，我们为 `Person` 结构体重载了 `<` 运算符，以便 `std::list::sort` 可以使用它来比较 `Person` 对象。重载 `<` 运算符使得 `sort` 函数能够知道如何根据 `Person` 对象的 `age` 成员变量来比较它们。

当你调用 `people.sort()` 时，`std::list` 会使用 `<` 运算符来比较 `people` 列表中的 `Person` 对象，并根据比较结果对它们进行排序。

如果你不想或不能重载 `<` 运算符（例如，如果你的类已经有一个 `<` 运算符的重载，并且它的语义与排序不同），你可以提供一个自定义的比较函数或函数对象给 `sort` 函数。下面是如何使用自定义比较函数的例子：

```cpp
// 自定义比较函数  
bool compareByAge(const Person& a, const Person& b) {  
    return a.age < b.age;  
}  
  
// ... 在 main 函数中 ...  
  
// 使用自定义比较函数对 list 进行排序  
people.sort(compareByAge);

// 或者写成Lambda 表达式
people.sort([](Person& a,Person& b){
    return a.age < b.age;
});  
```

在这个例子中，我们定义了一个名为 `compareByAge` 的函数，它接受两个 `Person` 引用并返回一个布尔值，表示第一个对象是否应该在排序后位于第二个对象之前。然后我们将这个函数作为参数传递给 `sort` 方法。

使用重载 `<` 运算符：代码简洁、直观；更重要的是对象自带排序逻辑；

使用比较函数：灵活、多变，可适应不同的排序逻辑；

#### 	总结

值得注意的是，虽然 `std::list` 在插入和删除操作上有优势，但在遍历和访问元素上可能不如 `std::vector` 或 `std::array` 高效，因为后者提供了连续的内存空间，可以通过下标直接访问元素。因此，在选择使用哪种容器时，需要根据具体的应用场景和需求来权衡。

总的来说，`std::list` 是一个功能强大且灵活的容器，适用于需要频繁进行插入和删除操作，同时不太关心访问速度的场景。通过合理地使用它的成员函数和迭代器，可以有效地处理链表结构的数据。

往往用于样本数据量比较大，对顺序要求比较高的地方。对其遍历的操作可能是在启动、关闭、或者适时数据保存时。并不会频繁的遍历，单也是可承受的。

### Set

STL（Standard Template Library，标准模板库）中的`set`是一个关联容器，它包含唯一元素的集合。`set`中的元素自动按升序排列，并且不允许重复元素。`set`的内部实现通常使用红黑树来保证其有序性和快速查找的特性。

#### 	基本特性

1. **有序性**：`set`中的元素默认按升序排列，你也可以通过提供自定义的比较函数来改变元素的排序方式。
2. **唯一性**：`set`中的元素必须是唯一的，不允许重复。
3. **动态性**：你可以随时向`set`中添加或删除元素，而不需要考虑元素的位置或大小。

#### 主要操作

1. **插入元素**：使用`insert`函数插入一个元素。如果元素已存在，则插入操作无效。
2. **删除元素**：使用`erase`函数删除一个元素。
3. **查找元素**：使用`find`函数查找一个元素，如果找到则返回指向该元素的迭代器，否则返回`end()`迭代器。
4. **遍历元素**：可以使用迭代器遍历`set`中的所有元素。

#### 举例说明

下面是一个简单的例子，展示了如何使用`set`：

```cpp
#include <iostream>  
#include <set>  


int main() {  
    // 创建一个空的 set 容器  
    std::set<int> mySet;  
  
    // 插入元素  
    mySet.insert(3);  
    mySet.insert(1);  
    mySet.insert(4);  
    mySet.insert(1);  // 重复插入，实际上不会添加新元素  
  
    // 遍历并打印 set 中的元素  
    for (int num : mySet) {  
        std::cout << num << " ";  
    }  
    std::cout << std::endl;  
  
    // 查找元素  
    auto it = mySet.find(2);  
    if (it != mySet.end()) {  
        std::cout << "找到元素 2" << std::endl;  
    } else {  
        std::cout << "未找到元素 2" << std::endl;  
    }  
  
    // 删除元素  
    mySet.erase(1);  
    mySet.erase(mySet.find(4));  // 通过迭代器删除元素  
  
    // 再次遍历并打印 set 中的元素  
    for (int num : mySet) {  
        std::cout << num << " ";  
    }  
    std::cout << std::endl;  
  
    return 0;  
}
```

输出：

```
1 3 4   
未找到元素 2  
3
```

在上面的例子中，我们首先创建了一个空的`set`容器，并插入了一些元素。注意，当我们尝试插入重复的元素（在这个例子中是数字1）时，`set`会自动忽略这个操作，因为`set`不允许重复元素。然后，我们使用范围for循环遍历并打印`set`中的所有元素，它们是按升序排列的。接下来，我们尝试查找一个不存在的元素（在这个例子中是数字2），并输出相应的信息。最后，我们删除了一些元素，并再次遍历并打印`set`中的剩余元素。

​	在很多操作中，需要记录某种行为、状态或者具体对象是否出现过，就可以使用Set。







----



### Map

STL（Standard Template Library，标准模板库）中的`map`是一个关联容器，它存储的元素都是键值对（key-value pair），并且根据键（key）的值自动进行排序。`map`不允许有重复的键，每个键在`map`中只能出现一次。`map`通常使用红黑树作为其底层数据结构，因此插入、删除和查找操作的平均时间复杂度都是对数级别的。

#### 	基本特性

1. **有序性**：`map`中的元素按照键的值自动排序。默认情况下，键按升序排列，但你也可以通过提供自定义的比较函数来改变排序方式。
2. **唯一性**：`map`中的键必须是唯一的，不允许重复。如果尝试插入具有相同键的新元素，将不会添加新元素，并且原始元素的值不会被更改。
3. **动态性**：你可以随时向`map`中添加或删除元素，而不需要考虑元素的位置或大小。



#### 	主要操作

1. **插入元素**：使用`insert`函数插入一个键值对。如果键已存在，则不会添加新元素，但你可以使用`operator[]`或`at`函数来修改已存在键的值。
2. **删除元素**：使用`erase`函数删除一个元素。
3. **查找元素**：使用`find`函数查找一个键对应的元素，如果找到则返回指向该元素的迭代器，否则返回`end()`迭代器。你也可以使用`count`函数来检查一个键是否存在。
4. **遍历元素**：可以使用迭代器遍历`map`中的所有元素。



#### 	示例说明1

下面是一个简单的例子，展示了如何使用`map`：

```cpp
#include <iostream>  
#include <map>  
#include <string>  
  
using namespace std;  
  
int main() {  
    // 创建一个空的 map 容器  
    map<string, int> myMap;  
  
    // 插入元素  
    myMap["张三"] = 25;  
    myMap["李四"] = 30;  
    myMap["王五"] = 35;  
  
    // 尝试插入一个已存在的键（李四），不会添加新元素  
    myMap["李四"] = 40;  // 李四的值仍然是 30，不会被更改为 40  
  
    // 遍历并打印 map 中的元素  
    for (const auto& kv : myMap) {  
        cout << kv.first << ": " << kv.second << endl;  
    }  
  
    // 查找元素  
    auto it = myMap.find("赵六");  
    if (it != myMap.end()) {  
        cout << "找到元素 " << it->first << ": " << it->second << endl;  
    } else {  
        cout << "未找到元素 赵六" << endl;  
    }  
  
    // 使用 at 函数访问元素（如果键不存在，会抛出异常）  
    try {  
        int value = myMap.at("张三");  
        cout << "张三 的值是 " << value << endl;  
    } catch (const out_of_range& e) {  
        cout << "键 张三 不存在: " << e.what() << endl;  
    }  
  
    // 删除元素  
    myMap.erase("王五");  
  
    // 再次遍历并打印 map 中的元素  
    for (const auto& kv : myMap) {  
        cout << kv.first << ": " << kv.second << endl;  
    }  
  
    return 0;  
}
```

输出：

```
李四: 40
王五: 35
张三: 25
未找到元素 赵六
张三 的值是 25
李四: 40
张三: 25
```

在上面的例子中，我们首先创建了一个空的`map`容器，并插入了一些键值对。注意，当我们尝试插入一个已存在的键（"Bob"）时，原始的值（30）不会被新值（40）覆盖。然后，我们使用范围for循环遍历并打印`map`中的所有元素。接下来，我们尝试查找一个不存在的键（"David"），并输出相应的信息。我们还展示了如何使用`at`函数来访问元素的值，如果键不存在，`at`函数会抛出一个异常。最后，我们删除了一个元素，并再次遍历并打印`map`中的剩余元素。

#### 示例说明2

假设我们有一个学生信息管理系统，需要记录每个学生的姓名和对应的成绩。我们可以使用`map`来存储这些信息，以便根据姓名查找成绩或进行其他操作。

```cpp
#include <iostream>  
#include <map>  
#include <string>  
  
using namespace std;  
  
int main() {  
    // 创建一个 map 容器用于存储学生姓名和成绩  
    map<string, int> studentScores;  
  
    // 插入学生成绩信息  
    studentScores["张三"] = 90;  
    studentScores["李四"] = 85;  
    studentScores["王五"] = 92;  
    studentScores["赵六"] = 88;  
  
    // 遍历并打印所有学生的姓名和成绩  
    cout << "所有学生的姓名和成绩：" << endl;  
    for (const auto& kv : studentScores) {  
        cout << kv.first << "：" << kv.second << endl;  
    }  
  
    // 根据姓名查找学生成绩  
    string nameToSearch;  
    cout << "请输入要查找的学生姓名：";  
    cin >> nameToSearch;  
    auto it = studentScores.find(nameToSearch);  
    if (it != studentScores.end()) {  
        cout << nameToSearch << "的成绩是：" << it->second << endl;  
    } else {  
        cout << "未找到学生：" << nameToSearch << endl;  
    }  
  
    // 修改学生成绩  
    string nameToUpdate;  
    int newScore;  
    cout << "请输入要修改成绩的学生姓名：";  
    cin >> nameToUpdate;  
    cout << "请输入新的成绩：";  
    cin >> newScore;  
    if (studentScores.find(nameToUpdate) != studentScores.end()) {  
        studentScores[nameToUpdate] = newScore;  
        cout << nameToUpdate << "的成绩已更新为：" << newScore << endl;  
    } else {  
        cout << "未找到学生：" << nameToUpdate << "，无法更新成绩" << endl;  
    }  
  
    // 删除学生成绩信息  
    string nameToDelete;  
    cout << "请输入要删除的学生姓名：";  
    cin >> nameToDelete;  
    if (studentScores.erase(nameToDelete)) {  
        cout << nameToDelete << "的成绩信息已删除" << endl;  
    } else {  
        cout << "未找到学生：" << nameToDelete << "，无法删除成绩信息" << endl;  
    }  
  
    // 再次遍历并打印剩余学生的姓名和成绩  
    cout << "剩余学生的姓名和成绩：" << endl;  
    for (const auto& kv : studentScores) {  
        cout << kv.first << "：" << kv.second << endl;  
    }  
  
    return 0;  
}
```

在这个例子中，我们首先创建了一个`map`容器`studentScores`，用于存储学生的姓名（作为键）和成绩（作为值）。然后，我们插入了几个学生的成绩信息，并遍历打印了所有学生的姓名和成绩。

接下来，我们实现了根据姓名查找学生成绩的功能。用户输入要查找的姓名，程序使用`find`函数在`map`中查找对应的成绩，并输出结果。

然后，我们实现了修改学生成绩的功能。用户输入要修改的学生姓名和新的成绩，程序检查该学生是否存在，如果存在则更新成绩。

最后，我们实现了删除学生成绩信息的功能。用户输入要删除的学生姓名，程序尝试从`map`中删除对应的成绩信息，并输出相应的结果。

通过这个例子，你可以看到`map`在实际应用中的灵活性和便利性。它不仅可以存储键值对，而且可以根据键高效地查找、修改和删除元素。

```
如果有时间，重写学生管理系统，使用map！！！如果没有时间作为作业题
```



### Queue

提供了队列的基本操作，如入队（在尾部插入元素）、出队（从头部删除元素）以及查看队首元素等。`queue`是一种先进先出（FIFO）的数据结构，通常用于在程序中按照特定顺序处理一系列的元素。

在C++中，你可以通过包含头文件`<queue>`来使用STL的`queue`。下面是一个使用`queue`的简单例子：

```cpp
#include <iostream>  
#include <queue>  
using namespace std;  
  
int main() {  
    // 创建一个int类型的queue  
    queue<int> q;  
  
    // 入队操作  
    q.push(1);  
    q.push(2);  
    q.push(3);  
  
    // 输出队列的大小  
    cout << "队列的大小: " << q.size() << endl;  
  
    // 查看队首元素，但不删除  
    cout << "队首元素: " << q.front() << endl;  
  
    // 查看队尾元素  
    cout << "队尾元素: " << q.back() << endl;  
  
    // 出队操作  
    int front_element = q.front();  
    q.pop();  
    cout << "出队元素: " << front_element << endl;  
  
    // 再次查看队首元素  
    cout << "新的队首元素: " << q.front() << endl;  
  
    return 0;  
}
```

这个程序的输出将是：

```makefile
队列的大小: 3  
队首元素: 1  
队尾元素: 3  
出队元素: 1  
新的队首元素: 2
```

在这个例子中，我们首先创建了一个`int`类型的`queue`对象`q`。然后，我们使用`push`方法将三个整数入队。接着，我们使用`size`方法获取队列的大小，使用`front`方法查看队首元素，使用`back`方法查看队尾元素。然后，我们再次使用`front`方法获取队首元素，并使用`pop`方法将其出队。最后，我们再次查看队首元素，以验证出队操作是否成功。

需要注意的是，虽然在这个例子中我们使用了`using namespace std;`来避免在每次使用STL组件时都写`std::`前缀，但在实际的大型项目中，为了避免命名冲突，通常建议显式地使用`std::`前缀。

### stack

`stack`是一个后进先出（LIFO，Last In First Out）的数据结构，也被称为栈。它只允许在栈顶进行插入和删除操作。栈是一种非常有用的数据结构，经常用于实现函数调用、撤销操作等场景。

STL中的`stack`模板类定义在`<stack>`头文件中，其基本语法如下：

```cpp
#include <stack>  
  
std::stack<T> stk;
```

其中，`T`是栈中元素的类型。

`stack`类提供了几个基本的成员函数，用于操作栈：

- `push(x)`：将元素`x`压入栈顶。
- `pop()`：删除栈顶的元素。
- `top()`：返回栈顶元素的引用。
- `empty()`：如果栈为空，则返回`true`，否则返回`false`。
- `size()`：返回栈中元素的个数。

下面是一个使用`stack`的简单示例：

```cpp
#include <iostream>  
#include <stack>  
  
#include <iostream>  
#include <stack>  
using namespace std;  
  
int main() {  
    stack<int> stk;  
  
    // 压入元素  
    stk.push(1);  
    stk.push(2);  
    stk.push(3);  
  
    // 输出栈的大小  
    cout << "栈的大小: " << stk.size() << endl;  
  
    // 检查栈是否为空  
    if (!stk.empty()) {  
        // 输出栈顶元素并准备移除  
        int topElement = stk.top();  
        cout << "即将被移除的栈顶元素: " << topElement << endl;  
          
        // 弹出栈顶元素  
        stk.pop();  
    } else {  
        cout << "栈为空，无法移除元素" << endl;  
    }  
  
    // 再次输出栈的大小和新的栈顶元素（如果栈不为空）  
    cout << "移除元素后的栈大小: " << stk.size() << endl;  
    if (!stk.empty()) {  
        cout << "新的栈顶元素: " << stk.top() << endl;  
    } else {  
        cout << "栈为空，无栈顶元素" << endl;  
    }  
  
    return 0;  
}
```

这个程序的输出将是：

```bash
栈的大小: 3
即将被移除的栈顶元素: 3
移除元素后的栈大小: 2
新的栈顶元素: 2
```

在这个示例中，我们首先创建了一个`int`类型的`stack`对象`stk`。然后，我们使用`push`函数将三个整数压入栈中。接着，我们使用`size`函数输出栈的大小，使用`top`函数输出栈顶元素。最后，我们使用`pop`函数弹出栈顶元素，并再次使用`top`函数输出新的栈顶元素。



### 如何选择STL中哪一个类？

​	首先了解业务逻辑，找出核心关键点，也就是最重要的逻辑和最常用的逻辑，再看这个逻辑是查找、遍历、插入等里面的哪一种？如果样本数据量本身很小，尽量使用数组，否则就在其他类里面找。

​	一般对于大样本数据，遍历的可能性不大，倾向于选择map；

​	非常需要遍历的，能使用数组（含Vector）尽量使用，不行则使用list；

​	其他的根据实际需要进行选择，一般用于算法中的中间数缓存。

​	*如果有时间以学生管理系统为例，进一步分析拆解怎么使用，使用哪些STL类*。。。



### STL算法概述

STL算法的特点在于它们不依赖于特定的容器类型，只要容器支持迭代器（Iterator），就可以使用这些算法。这使得STL算法非常灵活和通用。

#### std::sort() 使用

`std::sort()` 是STL中的一个排序算法，它可以对指定范围内的元素进行排序。其基本语法如下：

```cpp
#include <algorithm> // 包含sort算法的头文件  
#include <vector>    // 包含vector容器的头文件  
  
std::sort(iterator start, iterator end);
```

其中，`start` 和 `end` 是指向要排序的序列的起始和结束位置的迭代器。结束位置的迭代器指向序列中“最后一个元素之后”的位置。

下面是一个使用 `std::sort()` 对 `std::vector` 中的整数进行排序的示例：

```cpp
#include <iostream>  
#include <vector>  
#include <algorithm>  
using namespace std;  
  
int main() {  
    vector<int> numbers = {5, 2, 8, 1, 9};  
  
    // 使用 std::sort() 对 vector 中的整数进行排序
    sort(numbers.begin(), numbers.end());  
  
    for (int num : numbers) {  
        cout << num << " ";  
    }  
    cout << endl;  
  
    return 0;  
}
```

输出将会是排序后的序列：

```
复制代码1 2 5 8 9
```

#### std::find() 使用

`std::find()` 是STL中的一个查找算法，用于在序列中查找指定的元素。其基本语法如下：

```cpp
#include <algorithm> // 包含find算法的头文件  
  
iterator std::find(iterator start, iterator end, const value_type& val);
```

其中，`start` 和 `end` 是指向要搜索的序列的起始和结束位置的迭代器，`val` 是要查找的值。如果找到该值，`std::find()` 返回一个指向该值的迭代器；如果未找到，则返回 `end` 迭代器。

下面是一个使用 `std::find()` 在 `std::vector` 中查找特定整数的示例：

```cpp
#include <iostream>  
#include <vector>  
#include <algorithm>  
using namespace std;  
  
int main() {  
    vector<int> numbers = {5, 2, 8, 1, 9};  
    int toFind = 8;  
  
    // 使用 std::find() 在 vector 中查找特定整数，返回的是迭代器
    auto it = find(numbers.begin(), numbers.end(), toFind);  
  
    if (it != numbers.end()) {  
        // 注意：这里使用distance来获取返回两个迭代器之间元素的数量（距离）
        cout << "Found " << toFind << " at position: " << distance(numbers.begin(), it) << endl;  
    } else {  
        cout << toFind << " not found in the vector." << endl;  
    }  
  
    return 0;  
}
```

如果找到值为8的元素，程序将输出其位置；否则，将输出未找到的消息。

对于 `std::sort()` 和其他许多STL算法，你还可以提供自定义的比较函数，以控制排序或查找的顺序。例如，你可以通过提供一个比较函数来按降序排序整数，或者根据自定义的结构体或类的某个成员进行排序。



### STL函数对象（Function Objects）

STL（Standard Template Library，标准模板库）中的函数对象（Function Objects）也被称为仿函数（Functors），是一种特殊的对象，它们通过重载函数调用操作符`operator()`，使得这些对象可以像普通函数那样被调用。

*仿函数（function objects，也称为函数对象）其实是C++语言特性的一部分，而不是STL特有的。但是，在STL中，仿函数被广泛用作算法（如`sort`、`find_if`等）的自定义条件或操作。因此，虽然仿函数不是STL独有的，但它们与STL紧密相关，并且在STL的实现和使用中扮演着重要角色。因此很多大纲都把他当做了STL讲解的一部分，我们这里只是通过示例代码了解结构。*

函数对象在STL中广泛应用，尤其是在算法中。STL算法通常需要函数对象或普通函数作为参数，以提供自定义的操作或比较逻辑。使用函数对象而不是普通函数的优势在于，函数对象可以拥有自己的状态，这使得它们能够保存并传递额外的信息，实现更复杂的逻辑。

函数对象通常通过定义一个类，并在其中重载`operator()`来实现。重载后的操作符可以接收任意数量和类型的参数，并返回任意类型的值。

#### 	示例1：自定义比较函数对象

```cpp
#include <iostream>  
#include <vector>  
#include <algorithm>  
  
using namespace std;  
  
// 定义一个比较整数大小的函数对象  
struct CompareInts {  
    bool operator()(int a, int b) const {  
        return a < b;  
    }  
};  
  
int main() {  
    vector<int> vec = {5, 2, 9, 1, 5, 6};  
  
    // 使用自定义比较函数对象对vector进行排序  
    sort(vec.begin(), vec.end(), CompareInts());  
  
    // 输出排序后的vector  
    for (int num : vec) {  
        cout << num << ' ';  
    }  
    cout << endl;  
  
    return 0;  
}
```

在这个例子中，`CompareInts`是一个函数对象，它重载了`operator()`来比较两个整数的大小。然后，我们创建了一个`CompareInts`的实例并将其传递给`std::sort`函数，作为排序的比较逻辑。

#### 	示例2：使用Lambda表达式作为函数对象

C++11及以后的版本支持Lambda表达式，它们提供了一种更简洁的方式来定义函数对象。

```cpp
#include <iostream>  
#include <vector>  
#include <algorithm>  
  
int main() {  
    std::vector<int> vec = {5, 2, 9, 1, 5, 6};  
  
    // 使用Lambda表达式对vector进行排序  
    std::sort(vec.begin(), vec.end(), [](int a, int b) { return a < b; });  
  
    // 输出排序后的vector  
    for (int num : vec) {  
        std::cout << num << ' ';  
    }  
    std::cout << std::endl;  
  
    return 0;  
}
```

在这个例子中，Lambda表达式`[](int a, int b) { return a < b; }`直接作为比较逻辑传递给了`std::sort`函数。Lambda表达式在语法上更加简洁，并且可以在需要时捕获局部变量。

#### 	示例3：自定义累加函数对象

```cpp
#include <iostream>  
#include <vector>  
#include <numeric>  
  
using namespace std;  
  
// 定义一个累加数值的函数对象  
struct Accumulator {  
    int sum;  
  
    // 构造函数初始化累加和  
    Accumulator() : sum(0) {}  
  
    // 重载函数调用操作符，实现累加  
    void operator()(int value) {  
        sum += value;  
    }  
  
    // 获取累加结果  
    int getSum() const {  
        return sum;  
    }  
};  
  
int main() {  
    vector<int> numbers = {1, 2, 3, 4, 5};  
    Accumulator acc;  
  
    // 使用for_each和函数对象进行累加  
    for_each(numbers.begin(), numbers.end(), acc);  
  
    // 输出累加结果  
    cout << "The sum of numbers is: " << acc.getSum() << endl;  
  
    return 0;  
}
```

在这个例子中，`Accumulator`是一个函数对象，它有一个`sum`成员变量来保存累加结果。重载的`operator()`用于累加每个元素，而`getSum`函数用于获取最终的累加和。

函数对象在STL中提供了一种灵活的方式来定义和传递自定义行为，使得算法能够更通用和可重用。无论是使用传统的类定义的函数对象，还是使用Lambda表达式，它们都能够扩展STL算法的功能，并适应不同的需求。

### STL适配器（Adaptors）

在C++的STL（标准模板库）中，适配器（Adaptors）是一种设计模式，它允许将一个类的接口转换为客户端所期望的另一种接口，从而使原本不兼容的接口能够协同工作。STL中的适配器主要有三种类型：容器适配器、迭代器适配器和函数对象适配器。

**下面以容器适配器为例简单介绍一下**

容器适配器为STL容器提供了不同的接口或行为。最常见的容器适配器是`std::stack`、`std::queue`和`std::priority_queue`，它们分别基于`std::deque`、`std::list`或`std::vector`等底层容器来实现。这些适配器提供了栈、队列和优先队列的接口，使得我们可以像操作这些数据结构一样操作底层容器。

​	示例：使用`std::stack`适配器

```cpp
#include <iostream>  
#include <stack>  // 这些头文件包含了容器适配器的定义。
#include <vector>  
  
using namespace std;  
  
int main() {  
    stack<int, vector<int>> st; // 使用vector作为底层容器的stack，不定义则默认是deque
  
    st.push(1);  // 这里st.push(1);会调用vector<int>的push_back方法，因为st的底层容器是一个vector<int>
    st.push(2);  
    st.push(3);  
  
    while (!st.empty()) {  
        cout << st.top() << ' ';  
        st.pop();  
    }  
    cout << endl;  
  
    return 0;  
}
```

容器适配器的使用是通过包含相应的头文件并创建对应类型的对象来体现的。这些对象的行为类似于我们期望的数据结构（如栈、队列和优先级队列），但实际上它们是基于其他容器（如`vector`、`deque`或`list`）实现的。

以`stack`为例，当我们包含`<stack>`头文件并创建一个`std::stack<int>`对象时，我们实际上是在使用一个容器适配器。这个适配器内部使用了一个默认的底层容器（通常是`deque`）来存储元素，并提供了栈的接口（如`push`、`pop`和`top`）。我们不需要关心底层容器的实现细节，只需要通过适配器提供的接口来使用栈的功能。

同样地，对于`queue`和`priority_queue`，我们也是通过包含相应的头文件并创建对象来使用容器适配器的。这些适配器提供了队列和优先级队列的接口，使得我们可以方便地使用这些数据结构，而无需手动实现它们。

**关于适配器**

只是使用STL（Standard Template Library）中的容器适配器如`stack`，并且没有特殊需求去定制或了解底层实现细节，那么你通常只需要关心`stack`提供了哪些接口和功能，而不需要过多关注适配器是如何实现的。

STL的设计目标之一就是提供一个抽象层，使得用户可以方便地使用各种数据结构，而不需要了解这些数据结构背后的具体实现。容器适配器就是这种抽象的一个例子。它们隐藏了底层容器的复杂性，提供了一个统一、简洁的接口来使用不同的数据结构。

因此，在大多数情况下，你只需要知道如何使用`stack`的接口，比如`push`、`pop`、`top`等，而不需要关心它是如何基于某个底层容器（如`vector`、`deque`等）来实现的。这种抽象和封装使得代码更加清晰、易于理解和维护。

当然，如果你对底层实现感兴趣，或者需要定制适配器的行为，那么你可以深入研究适配器的实现原理和STL的源代码。但这通常不是使用STL的基本要求，也不是大多数应用程序开发人员的日常工作







### 作业题


