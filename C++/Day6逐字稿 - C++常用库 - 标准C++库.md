### 课程内容

- 常用库的总体认识
- String用法
- 标准C++库中文件流的概念与用法



## 一 C++常用库的总体认识

​	我们写的C++程序，基本上都是在使用库的过程。不管是C语言里面的Printf()，还是第一个C++程序中的cin、cout，本身就来源于标准库。今天开始，我们打开今后可能用到的库去认识一下。。。

​	C++的库大致可以分为标准库和非标准库两大类。

### 1.1 标准库

标准库是C++本身就提供的，无需进行额外的环境配置，只需在代码中包含相应的头文件即可使用。标准库包括多个部分：

1. **C库**：这是由C标准库扩展而来的，强调结构、函数和过程，不支持面向对象技术。比如malloc()、fopen()这些，你们以前都学过了。
2. **标准的C++库**：
   - **I/O流库**：用于处理输入和输出的机制，提供了方便的方式来读取和写入数据，无论是从标准输入输出（键盘和屏幕）还是从文件或其他设备。流类库具有两个平行的基类：streambuf和ios类，所有流类均以两者之一作为基类。C++为用户进行标准I/O操作定义了四个类对象：cin、cout、cerr和clog。
   - **String库**：用于字符串操作。
   - **数值库**：用于数学计算等数值操作。
3. **标准模板库 (STL)**：包含容器、算法、迭代器等核心组件，为C++程序提供高效的数据结构和算法实现。

### 1.2 非标准库

非标准库则是指那些需要进行额外环境配置才能使用的库。这些库可能并不直接包含在C++的标准发行版中，但由第三方提供，并且可能需要特定的安装和配置步骤才能在项目中使用。非标准库的种类繁多，涵盖了从图形界面开发、网络通信、数据库访问到专业领域的各种应用。例如，Qt是一个用于开发图形用户界面的非标准库，Boost库则提供了一系列高级功能和工具，而OpenGL则是一个用于3D图形渲染的库。

需要注意的是，非标准库的命名并不是官方的称呼，这里只是为了方便区分标准库和非标准库。在使用非标准库时，通常需要查阅相应的文档以了解如何正确安装、配置和使用这些库。

总的来说，C++的库生态系统非常丰富，既有标准库提供的基础功能，也有非标准库提供的专业和高级功能。开发者可以根据项目需求和个人兴趣选择合适的库进行学习和使用。

## 二 标准的C++库

### 	2.1 String

C++ 的 `std::string` 类是 C++ 标准库（String库）中用于处理字符串的主要工具。它提供了丰富的成员函数和操作符重载，使得字符串的操作变得简单而高效。

下面是一些 `std::string` 类中常用的方法：

#### 	2.1.1. 构造函数

`std::string` 类有多个构造函数，用于创建字符串对象。

```cpp
#include <iostream>  
#include <string>  
  
int main() {  
    // 使用默认构造函数  
    std::string str1;  
      
    // 使用 C 风格字符串初始化  
    std::string str2("Hello, World!");  
      
    // 使用字符数组初始化  
    char arr[] = "Hello, C++";  
    std::string str3(arr);  
      
    // 使用特定长度的字符数组初始化  
    std::string str4(arr, 5); // 仅取 arr 的前 5 个字符  
      
    // 使用指定数量的字符初始化  
    std::string str5(10, 'x'); // 创建包含 10 个 'x' 的字符串  
      
    std::cout << str1 << std::endl;  
    std::cout << str2 << std::endl;  
    std::cout << str3 << std::endl;  
    std::cout << str4 << std::endl;  
    std::cout << str5 << std::endl;  
      
    return 0;  
}
```

#### 2.1.2. 访问和修改字符串

可以使用下标操作符 `[]` 或 `at()` 函数来访问字符串中的字符，使用 `operator[]` 或 `assign()` 函数来修改字符串。

```cpp
#include <iostream>  
#include <string>  
  
int main() {  
    std::string str = "Hello";  
      
    // 访问字符串中的字符  
    char firstChar = str[0]; // 或者 str.at(0)  
    std::cout << "First character: " << firstChar << std::endl;  
      
    // 修改字符串中的字符  
    str[0] = 'h'; // 或者 str.assign(0, 'h')  
    std::cout << "Modified string: " << str << std::endl;  
      
    return 0;  
}
```

#### 2.1.3. 字符串长度和容量

`length()`, `size()`, `max_size()` 和 `capacity()` 函数用于获取字符串的长度和容量信息。

```cpp
#include <iostream>  
#include <string>  
  
int main() {  
    std::string str = "Hello, World!";  
      
    // 获取字符串长度  （接口一致性问题）
    std::cout << "Length of string: " << str.length() << std::endl;  
    std::cout << "Size of string: " << str.size() << std::endl;  
      
    // 获取字符串最大可能长度  
    std::cout << "Max size of string: " << str.max_size() << std::endl;  
      
    // 获取当前分配的存储容量  
    std::cout << "Capacity of string: " << str.capacity() << std::endl;  
      
    return 0;  
}
```

#### 2.1.4. 字符串比较

`compare()`, `operator==`, `operator!=`, `operator<`, `operator<=`, `operator>`, `operator>=` 等用于比较字符串。

```cpp
#include <iostream>  
#include <string>  
  
int main() {  
    std::string str1 = "apple";  
    std::string str2 = "banana";  
      
    // 使用 compare 函数比较字符串  
    int cmpResult = str1.compare(str2);  
    if (cmpResult < 0) {  
        std::cout << "str1 is less than str2" << std::endl;  
    } else if (cmpResult > 0) {  
        std::cout << "str1 is greater than str2" << std::endl;  
    } else {  
        std::cout << "str1 is equal to str2" << std::endl;  
    }  
      
    // 使用操作符比较字符串  
    if (str1 == str2) {  
        std::cout << "str1 is equal to str2 (using == operator)" << std::endl;  
    } else {  
        std::cout << "str1 is not equal to str2 (using == operator)" << std::endl;  
    }  
      
    return 0;  
}
```

#### 2.1.5. 字符串拼接和附加

`append()`, `operator+=`, `push back()` 等函数用于拼接或附加字符串。

```cpp
#include <iostream>  
#include <string>  
  
int main() {  
    std::string str1 = "Hello";  
    std::string str2 = "World";  
      
    // 使用 append 函数拼接字符串  
    str1.append(str2);  
    std::cout << "Concatenated string: " << str1 << std::endl;  
      
    // 使用 += 操作符拼接字符串  
    str1 += ", C++";  
    std::cout << "Modified string: " << str1 << std::endl;  
      
    // 使用 push_back 追加单个字符  
    str1.push_back('!');  
    std::cout << "String with appended character: " << str1 << std::endl;  
      
    return 0;  
}
```

#### 2.1.6. 字符串子串和查找

`substr()`, `find()`, `find_first_of()`, `find_last_of()`, `find_first_not_of()`, `find_last_not_of()` 等函数用于获取子串和查找字符串中的字符或子串。

```cpp
#include <iostream>  
#include <string>  
  
int main() {  
    std::string str = "Hello, World!";  
      
    // 获取子串  
    std::string substr = str.substr(7, 5); // 从索引 7 开始，长度为 5 的子串  
    std::cout << "Substring: " << substr << std::endl;  
      
    // 查找子串或字符  
    size_t pos = str.find("World");  
    if (pos != std::string::npos) {  
        std::cout << "Found 'World' at position: " << pos << std::endl;  
    } else {  
        std::cout << "'World' not found in the string" << std::endl;  
    }  
      
    return 0;  
}
```

#### 2.1.7. 字符串修改

`insert()`, `erase()`, `replace()`, `swap()` 等函数用于修改字符串内容。

```cpp
#include <iostream>  
#include <string>  
  
int main() {  
    std::string str = "Hello";  
      
    // 插入字符或子串  
    str.insert(1, " World"); // 在索引 1 的位置插入 " World"  
    std::cout << "Inserted string: " << str << std::endl;  
      
    // 删除字符或子串  
    str.erase(6, 5); // 从索引 6 开始，删除 5 个字符  
    std::cout << "Erased string: " << str << std::endl;  
      
    // 替换子串  
    str.replace(1, 4, "C++"); // 从索引 1 开始，替换长度为 4 的子串为 "C++"  
    std::cout << "Replaced string: " << str << std::endl;  
      
    return 0;  
}
```

这些只是 `std::string` 类中可用方法的一部分。C++ 标准库为 `std::string` 提供了丰富的功能，几乎涵盖了字符串处理的所有基本需求。对于更复杂的字符串操作，可能需要结合使用其他标准库函数或自定义函数。



#### 2.1.8 字符串分割

​	字符串分割是一个非常常用的功能，比如将字符串中"，"、"；"等分割的子串找出来，文本解析几乎必用，爬虫程序更是应该必不可少。

​	虽然string并没有提供，我觉得有必要给大家介绍。

可以使用标准库中的其他工具，如`std::istringstream`或者C++11及以后的算法如`std::sregex_token_iterator`配合正则表达式，来实现字符串的分割。

以下是三种常用的字符串分割方法：

##### 	2.1.8.1 方法一 使用`find_first_of`和`substr`成员函数

```cpp
#include <iostream>  
#include <string>  
#include <vector>  
  
std::vector<std::string> split_string(const std::string &s, char delimiter) {  
    std::vector<std::string> tokens;  
    size_t pos = 0;  
    size_t prev = 0;  
    while ((pos = s.find_first_of(delimiter, prev)) != std::string::npos) {  
        if (pos > prev) {  
            tokens.push_back(s.substr(prev, pos - prev));  
        }  
        prev = pos + 1;  
    }  
    if (prev < s.length()) {  
        tokens.push_back(s.substr(prev, std::string::npos));  
    }  
    return tokens;  
}  
  
int main() {  
    std::string str = "Hello,World,This,Is,A,Test";  
    char delimiter = ',';  
    auto tokens = split_string(str, delimiter);  
    for (const auto &token : tokens) {  
        std::cout << token << std::endl;  
    }  
    return 0;  
}
```

在这个例子中，`split_string`函数接受一个字符串`s`和一个分隔符`delimiter`作为参数，并返回一个包含分割后子字符串的`std::vector<std::string>`。

函数内部使用一个循环来查找分隔符的位置。`find_first_of`函数从上次找到的分隔符位置`prev`开始搜索下一个分隔符的位置`pos`。如果找到了分隔符，就使用`substr`函数提取当前分隔符之前的子字符串，并将其添加到`tokens`向量中。然后更新`prev`为当前分隔符位置加1，以便在下一次循环中从下一个字符开始搜索。

最后，如果循环结束后`prev`仍然小于字符串的长度，说明最后一个分隔符之后还有剩余的子字符串，因此使用`substr`提取剩余部分并添加到`tokens`向量中。

在`main`函数中，我们调用`split_string`函数来分割字符串，并遍历返回的`tokens`向量，打印每个子字符串。

这种方法在处理简单的分隔符时非常有效，但对于复杂的分隔符模式或需要处理嵌套分隔符的情况，可能不如使用正则表达式或`std::sregex_token_iterator`那样灵活和强大。然而，对于简单的字符串分割任务，使用`find_first_of`和`substr`通常足够且性能较好。



##### 2.1.8.2 方法二：使用`std::istringstream`(字符串流)

这种方法适用于简单的分隔符，如空格、逗号等。

```cpp
#include <iostream>  
#include <sstream>  
#include <vector>  
#include <string>  
  
std::vector<std::string> split_string(const std::string &s, char delimiter) {  
    std::vector<std::string> tokens;  
    std::istringstream tokenStream(s);  
    std::string token;  
    while (std::getline(tokenStream, token, delimiter)) {  
        tokens.push_back(token);  
    }  
    return tokens;  
}  
  
int main() {  
    std::string str = "Hello,World,This,Is,A,Test";  
    char delimiter = ',';  
    auto tokens = split_string(str, delimiter);  
    for (const auto &token : tokens) {  
        std::cout << token << std::endl;  
    }  
    return 0;  
}
```

1. **创建输入字符串流**：`std::istringstream`允许你创建一个输入字符串流对象，该对象与包含数据的字符串相关联。在这个例子中，通过`std::istringstream tokenStream(s);`创建了一个`tokenStream`对象，并将要分割的字符串`s`作为输入源。
2. **从字符串中读取数据**：使用`std::getline`函数和指定的分隔符，`std::istringstream`可以从关联的字符串中读取数据。在这个例子中，`std::getline(tokenStream, token, delimiter)`从`tokenStream`中读取数据，直到遇到指定的分隔符`delimiter`为止，并将读取到的数据存储在`token`字符串中。
3. **分割字符串**：通过循环调用`std::getline`函数，并使用相同的分隔符，你可以将原始字符串分割成多个子字符串（或称为“token”）。在上面的例子中，循环继续进行，直到`std::getline`无法再读取到更多的数据为止。每次循环迭代都会读取一个新的token，并将其添加到`tokens`向量中。
4. **处理分割后的子字符串**：一旦字符串被分割成多个子字符串，你可以进一步处理它们。在这个例子中，分割后的子字符串被存储在`tokens`向量中，然后可以在循环之外对它们进行迭代和使用。
5. **另外：**每次调用`getline`时，它会从当前位置开始读取字符，直到遇到分隔符`delimiter`或者到达`tokenStream`的末尾。读取完成后，`tokenStream`内部的指针或迭代器会自动移动到读取序列之后的位置，也就是分隔符之后或者字符串末尾。这样，下一次调用`getline`时，它将继续从新的位置开始读取，从而实现了按分隔符分割字符串的效果。

##### 2.1.8.3 方法三：使用`std::sregex_token_iterator`和正则表达式

这种方法适用于复杂的分隔符模式。

```cpp
#include <iostream>  
#include <vector>  
#include <string>  
#include <regex>  
  
std::vector<std::string> split_string_regex(const std::string &s, const std::string &delimiter) {  
    std::regex re(delimiter);  
    std::sregex_token_iterator iter(s.begin(), s.end(), re, -1);  
    std::sregex_token_iterator end;  
    std::vector<std::string> tokens(iter, end);  
    return tokens;  
}  
  
int main() {  
    std::string str = "Hello:World:This:Is:A:Test";  
    std::string delimiter = ":";  
    auto tokens = split_string_regex(str, delimiter);  
    for (const auto &token : tokens) {  
        std::cout << token << std::endl;  
    }  
    return 0;  
}
```

在上面的`split_string_regex`函数中，`-1`作为`std::sregex_token_iterator`的构造函数的第四个参数意味着返回所有非分隔符的子匹配。如果你只想返回分隔符之间的内容，可以传递`0`作为这个参数，并且可能需要调整正则表达式来确保正确分割。

选择哪种方法取决于你的具体需求和你想要处理的分隔符的复杂性。对于简单的分隔符，`std::istringstream`通常足够快且易于使用。对于更复杂的分隔符模式，使用正则表达式和`std::sregex_token_iterator`可能更为合适。

#### 2.1.8.4方法四：方法一换成find

​	留给同学们自己尝试,

​	提示：如果会破坏原始字符串，可以复制一个字符串副本来做；



#### 2.1.9 关于正则表达式

正则表达式是对字符串操作的一种逻辑公式，它使用事先定义好的一些特定字符以及这些特定字符的组合来构成一个“规则字符串”，这个“规则字符串”用来表达对字符串的一种过滤逻辑。

正则表达式的特点包括：

1. 灵活性、逻辑性和功能性非常强，可以迅速地用极简单的方式达到字符串的复杂控制。
2. 对于刚接触的人来说，可能比较晦涩难懂。

正则表达式的应用非常广泛，尤其在文本处理方面。它可以用于匹配文本中符合特定模式的字符串，例如匹配邮箱地址、手机号码等；也可以在文本中搜索符合特定模式的字符串，并将其替换为其他内容；还可以从文本中提取出符合特定模式的信息，例如提取网页中的链接、抓取日志中的特定数据等；此外，正则表达式还可以用于校验用户输入的合法性，例如验证密码是否符合要求、验证表单中的数据是否符合规定等。

总之，正则表达式是一种强大的文本处理工具，在编程、文本编辑、数据提取等多个领域都有广泛的应用。

​	正则表达式本身是可以成为一堂课的，这里只是做一个印子，如果以后用到或者有兴趣，大家可以知道怎么去了解他，目前只是有这个概念。





### 	2.2 数值库

标准C++库的数值库（numeric library）提供了丰富的数学计算、随机数生成以及数值比较等功能。以下是一些主要的接口及其简要介绍：

1. **数学函数**：

   - `std::abs()`：返回数的绝对值。
   - `std::sqrt()`：计算平方根。
   - `std::pow()`：计算幂。
   - `std::sin()`, `std::cos()`, `std::tan()` 等：三角函数。
   - `std::log()`, `std::exp()` 等：对数和指数函数。

   示例：

   ```cpp
   double x = 4.0;  
   double y = std::sqrt(x);  // y 将为 2.0
   ```

2. **随机数生成**：

   - `std::rand()`：生成一个伪随机数。
   - `std::srand()`：设置随机数生成器的种子。
   - C++11 引入了 `<random>` 头文件，提供了更强大和灵活的随机数生成功能，如 `std::mt19937`（Mersenne Twister算法）等。了解就好！

   示例（使用 `<random>`）：

   ```cpp
   #include <random>  
   std::random_device rd;  // 随机设备，用于生成种子  
   std::mt19937 gen(rd()); // Mersenne Twister随机数生成器  
   std::uniform_int_distribution<> dis(1, 6); // 均匀分布，范围1到6  
   int dice_roll = dis(gen); // 生成一个1到6的随机数，模拟掷骰子
   ```

3. **数值比较**：

   - `std::min()`, `std::max()`：返回两个数中的最小值和最大值。
   - `std::clamp()`：将值限制在给定的范围内。

   示例：

   ```cpp
   int a = 5, b = 10, c = 3;  
   int min_val = std::min(a, b);  // min_val 将为 5  
   int clamped_val = std::clamp(c, 1, 5); // clamped_val 将为 3，因为c已经在范围内
   ```

4. **数学函数**

   `sin()`, `cos()`, 以及其他类似的三角函数和数学函数属于数值库（numeric library）。这些函数通常定义在 `<cmath>` 头文件中（在C语言标准库中则是 `<math.h>`）。

   在C++中，为了使用这些数学函数，你需要包含 `<cmath>` 头文件。例如：

   ```cpp
   #include <cmath>  
   #include <iostream>  
     
   int main() {  
       double radians = 1.0; // 角度对应的弧度值  
       double sine = std::sin(radians);  
       double cosine = std::cos(radians);  
     
       std::cout << "Sine: " << sine << std::endl;  
       std::cout << "Cosine: " << cosine << std::endl;  
     
       return 0;  
   }
   /*
   注意：这些数学函数期望其参数是以弧度为单位的。如果你有一个以度为单位的角度，你需要先将其转换为弧度。转换的公式是：`弧度 = 角度 * (π / 180)`。
   */
   ```

   

   C++标准库中的数值库不仅提供了基本的数学运算和三角函数，还包括了其他复杂的数学函数，如双曲函数、指数和对数函数、幂函数、取整函数、浮点数分解函数等。这些函数在科学和工程计算、图形处理、物理模拟等许多领域都非常有用。

   在C++中，`<cmath>` 是C++标准库的一部分，它提供了与C语言 `<math.h>` 头文件中相似的函数，但是以C++的方式进行了封装，通常是通过命名空间 `std` 来访问这些函数。这样做的好处是提高了代码的可读性和安全性，避免了命名冲突。

数值库的功能远不止上述列举的，标准库为各种数值计算和数学运算提供了丰富的工具。在实际应用中，根据具体需求选择合适的函数和算法是非常重要的。同时，随着C++标准的不断更新，数值库的功能也在不断扩展和优化。

### 	2.3 文件IO操作

在C++标准库中，文件I/O则是基础的I/O操作之一。

C++标准库提供了几个类用于文件I/O操作，其中最主要的是`std::ifstream`（用于从文件读取数据）、`std::ofstream`（用于向文件写入数据）和`std::fstream`（同时支持读写操作）。这些类都是基于流（stream）的概念设计的，使得文件操作与标准输入/输出流（如`std::cin`和`std::cout`）的操作方式非常相似。

#### 		2.3.1 什么是流（stream）

流（stream）是C++中用于处理输入/输出操作的一个抽象概念。在C++标准库中，流被实现为一系列的类，这些类封装了底层设备（如文件、控制台等）的输入/输出操作。通过流，程序员可以以一种统一、高效的方式处理各种输入/输出任务。

流基类主要包括`std::istream`（输入流基类）和`std::ostream`（输出流基类）。这两个基类定义了流的基本操作，而具体的输入/输出设备（如文件、控制台等）则由它们的派生类来实现。

`std::istream` 和 `std::ostream`

- `std::istream`：这是所有输入流类的基类。它定义了从流中读取数据的基本操作，如`operator>>`、`getline()`等。
- `std::ostream`：这是所有输出流类的基类。它定义了向流中写入数据的基本操作，如`operator<<`、`put()`等。

简单理解：**流水管道**、**传送带**、**通讯线路**；数据从一端到另一端的一种方式，我们关心的是接口的统一性，至于流中装的是什么数据，并不是关心的重点。

#### 		2.3.2 如何读取文件的感性认识

下面是一个简单的例子，展示了如何使用`std::ifstream`从文件中读取数据：

```cpp
#include <iostream>  
#include <fstream>  
#include <string>  
  
int main() {  
    std::ifstream inputFile("example.txt"); // 打开文件example.txt进行读取  
  
    if (!inputFile) { // 检查文件是否成功打开  
        std::cerr << "无法打开文件example.txt" << std::endl;  
        return 1;  
    }  
  
    std::string line;  
    while (std::getline(inputFile, line)) { // 从文件中逐行读取数据  
        std::cout << line << std::endl; // 输出读取到的行  
    }  
  
    inputFile.close(); // 关闭文件  
    return 0;  
}
```

在上面的例子中，我们首先创建了一个`std::ifstream`对象`inputFile`，并尝试打开名为"example.txt"的文件进行读取。如果文件打开失败，我们输出一个错误消息并返回1。然后，我们使用`std::getline`函数从文件中逐行读取数据，并将每一行存储在一个`std::string`对象`line`中。最后，我们输出每一行的内容，并在完成读取后关闭文件。

#### 2.3.3 如何读写文件与调用参数

我们先罗列一些 `std::fstream` 中常用的接口：

1. 构造函数：

   - `fstream()`：默认构造函数，创建一个未关联任何文件的文件流对象。
   - `fstream(const char* filename, ios_base::openmode mode = ios_base::in | ios_base::out)`：使用给定的文件名和模式打开一个文件。

2. 打开文件：

   - `void open(const char* filename, ios_base::openmode mode = ios_base::in | ios_base::out)`：使用指定的文件名和模式打开文件。如果文件已经打开，则先关闭它。
   - `bool is_open()`：检查文件是否已成功打开。

3. 关闭文件：

   - `void close()`：关闭当前打开的文件。

4. 读取数据：

   - `istream& read(char* s, streamsize n)`：从文件中读取指定数量的字符，并存储在提供的字符数组中。
   - `istream& getline(char* s, streamsize n)`：从文件中读取一行，直到遇到换行符或达到指定的字符数，并存储在字符数组中。
   - `istream& operator>>(type& value)`：从文件中读取数据，并将其存储在提供的变量中。

5. 写入数据：

   - `ostream& write(const char* s, streamsize n)`：将指定数量的字符写入文件。
   - `ostream& put(char c)`：将一个字符写入文件。
   - `ostream& operator<<(const type& value)`：将变量的值写入文件。

6. 文件定位：

   - `istream& seekg(streampos pos)`：设置文件的读取位置。
   - `ostream& seekp(streampos pos)`：设置文件的写入位置。
   - `streampos tellg()`：返回当前读取位置。
   - `streampos tellp()`：返回当前写入位置。

7. 错误处理：

   - `void clear()`：清除文件流的错误状态标志。
   - `streamsize bad()`：返回与流关联的“bad bit”的值。
   - `streamsize eof()`：返回与流关联的“end-of-file bit”的值。
   - `streamsize fail()`：返回与流关联的“fail bit”的值。

   

下面我们来看看同时对文件进行读写的例子。

`std::fstream` 是C++标准库中的一个类，它用于文件的读写操作。这个类结合了 `std::ifstream`（用于输入文件流）和 `std::ofstream`（用于输出文件流）的功能，使得在同一个文件流对象上既可以读取数据也可以写入数据。使用 `std::fstream` 可以方便地处理那些需要同时读写文件的场景。

`std::fstream` 提供了与 `std::ifstream` 和 `std::ofstream` 类似的成员函数和操作符，如 `open`、`close`、`read`、`write`、`getline`、`>>` 和 `<<` 等，用于打开文件、关闭文件、读取数据、写入数据和格式化输入/输出。

下面是一个使用 `std::fstream` 的例子，展示了如何打开一个文件，写入一些数据，然后再读取这些数据：

```cpp
#include <iostream>  
#include <fstream>  
#include <string>  
  
int main() {  
    std::fstream file("example.txt"); // 创建一个fstream对象，尝试打开example.txt文件  
  
    if (!file) { // 检查文件是否成功打开  
        std::cerr << "无法打开文件example.txt" << std::endl;  
        return 1;  
    }  
  
    // 写入数据到文件  
    file << "Hello, World!" << std::endl;  
    file << "这是一个测试文件。" << std::endl;  
  
    // 将文件指针移动到文件开头，以便读取数据  
    file.clear(); // 清除可能的错误标志 比如读取到文件末尾或错误的写入等 
    file.seekg(0, std::ios::beg); // 将get指针移动到文件开头  
  
    // 从文件读取数据  
    std::string line;  
    while (std::getline(file, line)) {  
        std::cout << line << std::endl;  
    }  
  
    file.close(); // 关闭文件  
    return 0;  
}
```

在上面的代码中，我们首先创建了一个 `std::fstream` 对象 `file` 并尝试打开名为 "example.txt" 的文件。如果文件打开成功，我们使用插入操作符 `<<` 将两行文本写入文件。然后，我们使用 `clear` 方法清除可能由写入操作产生的任何错误标志，并使用 `seekg` 方法将文件的读取指针（get pointer）移动到文件的开头。这样我们就可以从头开始读取文件内容了。接下来，我们使用 `std::getline` 函数从文件中逐行读取数据，并将每一行输出到控制台。最后，我们调用 `close` 方法关闭文件。

请注意，如果文件不存在并且没有指定打开模式为创建文件（如 `std::ios::out | std::ios::app` 或 `std::ios::out | std::ios::trunc`），那么 `std::fstream` 将无法打开文件，并且 `file` 对象将转换为 `false`。在实际应用中，你可能需要更详细地处理文件打开失败的情况，并可能需要指定打开模式来确保文件被正确创建或打开。

需要注意的是，文件I/O操作可能会受到操作系统、文件权限、文件路径等因素的影响，因此在实际应用中需要仔细处理这些潜在的问题。

2.3.4 读写参数 `std::ios`

`std::ios` 是 C++ 标准库中的一个类，它定义了一系列与文件读写相关的类型（或称为标志、模式），这些类型可以通过位或（bitwise OR）操作组合起来，以指定文件流的打开方式和行为。以下是一些常用的 `std::ios` 相关的文件读写类型：

1. `std::ios::in`：
   - 含义：以输入模式打开文件，用于从文件中读取数据。
   - 作用：允许程序从文件中读取数据。
2. `std::ios::out`：
   - 含义：以输出模式打开文件，用于向文件中写入数据。
   - 作用：允许程序向文件中写入数据。如果文件已存在，写入会覆盖现有内容。
3. `std::ios::app`：
   - 含义：以追加模式打开文件。
   - 作用：在追加模式下，文件内容将被保留，并且写入的数据将追加到文件的末尾，而不是覆盖现有内容。
4. `std::ios::ate`：
   - 含义：打开文件并将文件指针移到文件的末尾。
   - 作用：文件打开后，文件指针会立即移到文件的末尾，允许直接追加数据。
5. `std::ios::trunc`：
   - 含义：截断文件。
   - 作用：如果文件已经存在且以写入模式打开，将截断（清空）文件的内容。如果文件不存在，则忽略此标志。
6. `std::ios::binary`：
   - 含义：以二进制模式打开文件。
   - 作用：在二进制模式下，文件中的数据将按照其原始的二进制形式进行读写，而不是经过任何文本转换。这对于处理非文本文件（如图像、音频等）非常重要。
7. `std::ios::nocreate`：
   - 含义：不创建新文件。
   - 作用：如果指定的文件不存在，则不会创建新文件，并且打开操作将失败。
8. `std::ios::noreplace`：
   - 含义：不替换已存在的文件。
   - 作用：如果文件已存在，则不会替换它，并且打开操作可能会失败（取决于其他使用的标志）。

这些标志可以通过位或操作组合起来，以同时指定多个文件打开选项。例如，如果你想以二进制追加模式打开一个文件，你可以使用 `std::ios::binary | std::ios::app`。

C++ 标准库提供了三个主要的文件流类：`std::ifstream`（用于输入）、`std::ofstream`（用于输出）和 `std::fstream`（同时支持输入和输出）。这些类都继承自 `std::ios_base`，因此它们都可以使用 `std::ios` 中定义的文件打开类型和标志。

*尝试：文件打开方式，指定与不指定*



### 2.4 线程模块

C++标准库中的线程模块为开发者提供了创建和管理线程的能力。线程是并发执行的最小单元，允许多个任务同时运行，从而提高了程序的执行效率。C++11标准引入了`<thread>`头文件，其中包含了创建和管理线程的相关类和函数。

### 主要组件

1. **std::thread 类**：这是C++标准库中用于表示和管理线程的主要类。通过实例化这个类并传入一个可调用的对象（如函数、函数对象、Lambda表达式等），你可以创建一个新的线程来执行该对象。
2. **std::this_thread 类**：这个类提供了一组静态成员函数，用于获取当前线程的标识符、睡眠（让出CPU时间片）以及请求中断等。
3. **std::mutex 类**：在多线程环境中，通常需要使用互斥锁（mutex）来保护共享资源，以避免数据竞争和不一致。`std::mutex`提供了基本的锁机制。
4. **其他同步原语**：如`std::condition_variable`、`std::future`和`std::promise`等，用于更复杂的线程同步和通信。

### 示例程序

下面是一个简单的示例程序，展示了如何使用`std::thread`类来创建和管理线程：

在这个示例中，我们定义了一个`thread_function`函数，它接受一个整数参数并输出一些信息。然后，在`main`函数中，我们创建了两个线程`t1`和`t2`，并将`thread_function`函数作为它们的执行函数。每个线程都传入了一个不同的参数（1和2）。最后，我们使用`join`函数等待两个线程执行完毕。当所有线程都执行完毕后，主线程继续执行并输出一条信息。

```cpp
#include <iostream>  
#include <thread> // 包含线程库的头文件  
#include <chrono> // 用于休眠的函数  
  
// 定义一个简单的函数，用于在线程中执行  
void thread_function(int id) {  
    std::cout << "线程 " << id << " 开始执行" << std::endl;  
    std::this_thread::sleep_for(std::chrono::seconds(1)); // 线程休眠1秒  
    std::cout << "线程 " << id << " 结束执行" << std::endl;  
}  
  
int main() {  
    // 创建两个线程，分别执行 thread_function 函数，并传入不同的参数  
    std::thread t1(thread_function, 1);  
    std::thread t2(thread_function, 2);  
  
    // 等待两个线程执行完毕  
    t1.join();  
    t2.join();  
  
    std::cout << "主线程继续执行" << std::endl;  
    return 0;  
}
```



2.4.3 线程锁

C++标准库为多线程同步提供了多种锁类型，每种锁都有其特定的使用场景和优势。以下是C++标准库中几种常见的线程锁类型及其简要介绍和示例：

### 1. `std::mutex`

`std::mutex` 是最基本的互斥锁类型，用于保护共享资源，防止多个线程同时访问。

**示例**：

```cpp
#include <iostream>  
#include <thread>  
#include <mutex>  
  
std::mutex mtx; // 全局互斥锁  
int shared_data = 0;  
  
void increment() {  
    std::lock_guard<std::mutex> lock(mtx); // 使用锁保护区域  
    for (int i = 0; i < 1000; ++i) {  
        ++shared_data;  
    }  
}  
  
int main() {  
    std::thread t1(increment);  
    std::thread t2(increment);  
  
    t1.join();  
    t2.join();  
  
    std::cout << "Shared data: " << shared_data << std::endl;  
    return 0;  
}
```

### 2. `std::timed_mutex` 和 `std::recursive_timed_mutex`

这些锁类型与 `std::mutex` 和 `std::recursive_mutex` 类似，但提供了尝试锁定和定时锁定的功能。如果无法立即获取锁，线程可以等待指定的时间段。

**示例**（使用 `std::timed_mutex`）：

```cpp
#include <iostream>  
#include <thread>  
#include <chrono>  
#include <mutex>  
  
std::timed_mutex mtx;  
  
void try_lock() {  
    if (mtx.try_lock_for(std::chrono::seconds(1))) { // 尝试锁定1秒  
        std::cout << "Thread acquired the lock." << std::endl;  
        mtx.unlock();  
    } else {  
        std::cout << "Thread failed to acquire the lock." << std::endl;  
    }  
}  
  
int main() {  
    std::thread t1(try_lock);  
    std::thread t2(try_lock);  
  
    t1.join();  
    t2.join();  
    return 0;  
}
```

### 3. `std::recursive_mutex`

`std::recursive_mutex` 允许同一线程多次获取同一把锁，而不会造成死锁。这在某些递归算法中可能很有用。

**示例**：

```cpp
#include <iostream>  
#include <thread>  
#include <mutex>  
  
std::recursive_mutex mtx;  
  
void recursive_function() {  
    std::lock_guard<std::recursive_mutex> lock(mtx);  
    std::cout << "Thread is inside the recursive function." << std::endl;  
    // ... 可能还有其他需要锁定mtx的代码 ...  
}  
  
void work() {  
    std::lock_guard<std::recursive_mutex> lock(mtx);  
    std::cout << "Thread is doing work." << std::endl;  
    recursive_function(); // 可以在已锁定mtx的情况下再次锁定mtx  
}  
  
int main() {  
    std::thread t1(work);  
    std::thread t2(work);  
  
    t1.join();  
    t2.join();  
    return 0;  
}
```

### 4. `std::unique_lock`

`std::unique_lock` 是一个灵活的锁包装器，它提供了比 `std::lock_guard` 更多的控制，例如延迟锁定、尝试锁定、手动解锁等。

**示例**：

```cpp
#include <iostream>  
#include <thread>  
#include <mutex>  
#include <chrono>  
  
std::mutex mtx;  
  
void print_block(int n, char c) {  
    std::unique_lock<std::mutex> lck(mtx, std::defer_lock); // 延迟锁定  
    std::cout << "Thread " << std::this_thread::get_id() << " is trying to lock" << std::endl;  
    if (lck.try_lock_for(std::chrono::seconds(1))) { // 尝试锁定1秒  
        std::cout << "Thread " << std::this_thread::get_id() << " locked mutex!" << std::endl;  
        for (int i = 0; i < n; ++i) { std::cout << c; }  
        std::cout<< std::endl;
} else {
    std::cout << "Thread " << std::this_thread::get_id() << " failed to lock mutex!" << std::endl;
    }
}

int main() {
    std::thread th1(print_block, 50, '*');
    std::thread th2(print_block, 50, '$');

    th1.join();  
    th2.join();  

    return 0;
}
```

### 5. `std::lock`  

`std::lock` 是一个用于同时锁定多个互斥体的实用函数，它确保了死锁不会发生（通过避免嵌套锁定）。  

**示例**：  

```cpp  
#include <iostream>  
#include <thread>  
#include <mutex>  
  
std::mutex mtx1, mtx2;  
  
void print_ids(int id1, int id2) {  
    std::lock(mtx1, mtx2); // 同时锁定 mtx1 和 mtx2  
    std::cout << "Thread " << std::this_thread::get_id()  
              << " with ids " << id1 << " & " << id2 << std::endl;  
    mtx1.unlock(); // 手动解锁 mtx1  
    mtx2.unlock(); // 手动解锁 mtx2  
}  
  
int main() {  
    std::thread th1(print_ids, 1, 2);  
    std::thread th2(print_ids, 3, 4);  
  
    th1.join();  
    th2.join();  
  
    return 0;  
}
```

请注意，上述示例中的锁类型和函数仅用于演示目的。在实际应用中，应该根据具体需求选择适当的锁类型，并确保正确使用锁来避免死锁、竞态条件和其他同步问题。同时，使用锁时应尽量减小锁定区域的范围，以减少线程之间的争用，从而提高程序的性能。



C++标准库提供的线程锁主要是互斥锁（mutex）类型的实现，如`std::mutex`、`std::timed_mutex`、`std::recursive_mutex`等。这些锁都属于悲观锁（pessimistic locking）的范畴，即它们假设最坏的情况，即总是认为会发生并发冲突，因此在访问共享资源之前会先锁定它。

乐观锁（optimistic locking）并不是C++标准库直接提供的一种锁类型。乐观锁是一种思想，它假设多线程并发访问共享资源时，冲突的情况不会频繁发生，因此它不会在访问共享资源之前立即锁定它，而是在更新数据时检查数据是否在此期间被其他线程修改过。如果数据未被修改，则提交事务；否则，回滚事务并重试。乐观锁通常用于数据库系统或某些特定的并发控制场景中。

在C++中，要实现乐观锁的效果，通常需要结合原子操作（`std::atomic`）和条件变量（`std::condition_variable`）等机制来手动实现。例如，你可以使用`std::atomic`来存储共享资源的版本号或时间戳，并在每次更新前检查这个值是否改变，从而决定是否需要回滚操作。

总结来说，C++标准库主要提供的是悲观锁类型的实现，而乐观锁并不是标准库直接提供的一种锁类型，但你可以结合标准库提供的工具（如原子操作和条件变量）来实现乐观锁的效果。





### 	2.5 其他标准C++库

​		标准的C++库是一个庞大的集合，包含了各种用于支持C++编程的类和函数。如果不包含标准模板库（STL），标准的C++库仍然包含了许多重要的组件和功能。除了上面介绍的字符串处理和数值库以外，还有很多：

1. **基本输入输出流**：这包括用于标准输入/输出操作的流对象，如`std::cin`、`std::cout`、`std::cerr`和`std::clog`。这些对象使得从控制台读取和写入数据变得简单。
2. **本地化**：C++库提供了支持本地化的功能，允许程序根据用户的语言和地区设置来显示信息。
3. **时间处理**：库中包含了对时间的处理功能，如获取当前时间、时间格式化等。
4. **内存管理**：虽然内存管理通常通过new和delete操作符以及智能指针等语言特性进行，但标准库也提供了一些辅助工具，如内存分配函数。
5. **异常处理**：C++的异常处理机制（包括`try`、`catch`和`throw`关键字）也是标准库的一部分，用于处理程序运行时的错误情况。

此外，标准C++库还包括了一些其他的功能和组件，如C语言库的重新实现（如`std::cstdlib`、`std::cctype`等），这些库在C++中得到了保留并进行了适当的修改以适应C++的命名空间和其他特性。

总的来说，即使不包括STL，标准的C++库仍然为程序员提供了大量的工具和功能，用于构建各种复杂和高效的程序。然而，需要注意的是，STL作为C++标准库的一部分，提供了许多非常有用的容器、算法和迭代器，对于现代C++编程来说是非常重要的。



## 作业题：

我们今天学习了string的用法以及文件读写；这两个接口在一起我们可以做文件格式转换的模块，比如将C++写的协议或者ProtoBuff文件转换成前端可以直接使用的Ts/Js。这在很多公司非常常见。今天可以简单的做个小工具，通过读取一个CPP文件，1）统计有多少行，2）将里面的std::去掉或添加。功能2需要判断是否存在using namespace std，并添加此行，如果是添加std::可以事先指定哪些关键字需要添加std::。




