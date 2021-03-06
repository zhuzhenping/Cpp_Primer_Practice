# 第九章 顺序容器

**顺序容器**：
- 标准库定义了三种顺序容器：vector，list和deque。
- 顺序容器适配器（adapter）：stack，queue，priority_queue。
- 直接复制：将一个容器复制给另一个容器时，类型必须匹配：容器类型和元素类型都必须相同。
- 使用迭代器复制：不要求容器类型相同，容器内的元素类型也可以不同。
- 接受容器大小做形参的构造函数只适用于顺序容器，而关联容器不支持这种初始化。

**容器内元素的类型约束**：
- 元素类型必须支持赋值运算；
- 元素类型的对象必须可以复制。
- 除了输入输出标准库类型外，其他所有标准库类型都是有效的容器元素类型。

**begin和end**：
- `c.begin()`：返回一个迭代器，它指向容器 c 的第一个元素。
- `c.end()`：返回一个迭代器，它指向容器 c 的最后一个元素的下一位置。
- `c.rbegin()`：返回一个逆序迭代器，它指向容器 c 的最后一个元素。
- `c.rend()`：返回一个逆序迭代器，它指向容器 c 的第一个元素前面的位置。

**顺序容器中添加元素的操作**：
- `c.push_back(t)`：在容器尾部添加t，返回void。
- `c.push_front(t)`：在容器前端添加t，返回void，只适用于list和deque。
- `c.insert(p, t)`：在迭代器p所指向的元素**前**插入t，返回指向新元素的迭代器。
- `c,insert(p, n, t)`：在迭代器p所指向的元素**前**插入n个t的新元素，返回void。
- `c.insert(p, b, e)`：在迭代器p偶只想的元素**前**插入由迭代器b和e标记的范围内的元素，返回void。

**顺序容器的大小操作**：
- `c.size()`：返回容器中c的元素个数，类型：`c::size_type`。
- `c.max_size()`：返回容器c可容纳的最多元素个数。
- `c.empty()`：返回容器大小是否为0。
- `c.resize(n)`：调整c的长度大小为n，多删少增。
- `c.resize(n,t)`：调整长度为n，新增的元素值是t。

**顺序容器访问元素**：
- `c.back()`：返回最后一个元素的引用，前提是c非空。
- `c.front()`：返回第一个元素的引用，前提是c非空。
- `c[n]`：返回下标是n的引用，只适用于vector和deque。
- `c.at(n)`：返回下标是n的引用，只适用于vector和deque。

**顺序容器删除元素**：
- `c.erase(p)`：删除迭代器p所指的元素。
- `c.erase(b, e)`：删除迭代器b到e内的所有元素。
- `c.clear()`：删除c内所有元素。
- `c.pop_back()`：删除c的最后一个元素，返回void。
- `c.pop_front()`：删除c的第一个元素，返回void，只适用于list和deque。

**顺序容器的赋值操作**：
- `c1=c2`：删除c1所有元素，将c2的元素复制给c1。
- `c1.swap(c2)`：交换内容。
- `c.assign(b, e)`：先删除c所有元素，将迭代器b到e标记范围内所有元素复制到c中。
- `c.assign(n, t)`：先删除c所有元素，将c中心设置为存储n个值为t的元素。

**vector vs. list**：
- vector容器的元素是连续存放的；
- list容器的元素是非连续存放（链表）；
- vector和deque支持快速随机访问；
- list类型可以支持

**string**：
- `s.insert(p, t)`：在迭代器p指向的元素之前插入t，**返回指向t的迭代器**。
- `s.insert(p, n, t)`：在迭代器p指向的元素之前插入n个值为t的新元素，返回void。
- `s.insert(p, b, e)`：在迭代器p指向的元素之前插入迭代器b到e范围内所有元素，返回void。
- `s.assign(b, e)`：用b到e的元素替换s，返回s。
- `s.assign(n, t)`：用值为t的n个副本替换s，返回s。
- `s.erase(p)`：删除迭代器p指向的元素，返回下一个元素的迭代器。
- `s.erase(b, e)`：删除从b到e的所有元素，返回下一个元素的迭代器。
- 还可以用`pos` 和 `len`表示下标和长度，代替上面的b，e。
- `s.substr(pos, len)`：返回当前对象的子串。
- `s.append(args)`：将args串接在s后面，返回s引用。
- `s.replace(pos, len, args)`：删除s中从下标pos开始的len个字符，并用args替换。
- `s.find(args)`：args在s中的第一次出现。
- `s.rfind(args)`：最后一次出现。
- string采用字典顺序比较。

**适配器**：
- 适配器是使一事物的行为类似于另一事物的行为的一种机制，例如stack可以使任何一种顺序容器以栈的方式工作。
- 初始化 `deque<int> deq; stack<int> stk(deq);`
- 默认的`stack`和`queue`都是基于`deque`实现，`priority_queue`是基于`vector`实现。
- 创建适配器时，指定一个顺序容器，可以覆盖默认的基础容器： `stack<string, vector<string> > str_stk;`。

**stack**：
- `s.pop()`：删除栈顶元素，不返回。
- `s.top()`：返回栈顶元素，不删除。
- `s.push(item)`：雅俗新元素。

**queue和priority_queue**：
- `q.pop()`：删除队首元素，但不返回。
- `q.front()`：返回队首元素的值，不删除。
- `q.top()`：返回具有最高优先级的元素值，不删除。
- `q.push(item)`：在队尾压入一个新元素。

