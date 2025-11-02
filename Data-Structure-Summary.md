| 语言         | 容器家族核心思想                                                     | 底层主要结构          |
| ---------- | ------------------------------------------------------------ | --------------- |
| **Python** | 少量通用容器（`list`, `dict`, `set`）+ 内建算法库（`heapq`, `collections`） | 动态数组、哈希表、二叉堆    |
| **Java**   | 多层容器体系（`List`, `Set`, `Map`, `Queue` 等接口 + 各种实现类）            | 数组、链表、哈希表、红黑树、堆 |

| 功能类别        | Python 容器                          | 底层实现                | 平均时间复杂度            | Java 容器                     | 底层实现                | 平均时间复杂度              |
| ----------- | ---------------------------------- | ------------------- | ------------------ | --------------------------- | ------------------- | -------------------- |
| **动态数组**    | `list`                             | 动态数组（连续内存块）         | 访问 O(1)，插入/删除 O(n) | `ArrayList`                 | 动态数组                | 访问 O(1)，插入/删除 O(n)   |
| **链表**      | `collections.deque`                | 双端链表块结构             | 两端插入/删除 O(1)       | `LinkedList`                | 双向链表                | 两端插入/删除 O(1)，中间 O(n) |
| **哈希表（映射）** | `dict`                             | 哈希表（Python 3.6+ 保序） | 查/增/删 O(1)         | `HashMap`                   | 哈希表（Java 8+ 链表+红黑树） | 查/增/删 O(1) 平均        |
| **哈希表（集合）** | `set`                              | 哈希表                 | 查/增/删 O(1)         | `HashSet`                   | 哈希表                 | 查/增/删 O(1) 平均        |
| **有序映射**    | `sortedcontainers.SortedDict`（第三方） | 平衡树（B-Tree）         | 查/增/删 O(log n)     | `TreeMap`                   | 红黑树                 | 查/增/删 O(log n)       |
| **有序集合**    | `sortedcontainers.SortedSet`（第三方）  | 平衡树                 | O(log n)           | `TreeSet`                   | 红黑树                 | O(log n)             |
| **优先队列**    | `heapq`                            | 二叉堆（最小堆）            | 插入/删除堆顶 O(log n)   | `PriorityQueue`             | 二叉堆（最小堆）            | 插入/删除堆顶 O(log n)     |
| **计数器**     | `collections.Counter`              | 基于 `dict` 的哈希表      | O(1) 平均            | `HashMap` + 手动计数            | 哈希表                 | O(1) 平均              |
| **队列**      | `queue.Queue`（线程安全）                | 链表                  | O(1)               | `LinkedList` / `ArrayDeque` | 链表 / 数组             | O(1)                 |

| 特性           | Python                         | Java                                             |
| ------------ | ------------------------------ | ------------------------------------------------ |
| **是否有内置平衡树** | ❌ 没有（需第三方包 `sortedcontainers`） | ✅ 有 (`TreeMap`, `TreeSet`)                       |
| **默认映射是否有序** | ✅ 从 3.7 起 `dict` 保插入顺序         | ❌ `HashMap` 无序（若要顺序用 `LinkedHashMap`）            |
| **堆**        | 仅最小堆（`heapq`）                  | 可指定比较器 → 支持任意顺序                                  |
| **并发安全容器**   | 无（需 `threading.Lock` 自行包裹）     | 提供多种线程安全容器（`ConcurrentHashMap`, `BlockingQueue`） |
| **泛型支持**     | 动态类型，无泛型                       | 强类型 + 泛型系统                                       |
| **底层性能差异**   | 动态解释型语言，开销较大                   | 编译型语言，JIT 优化更彻底，性能更高                             |

| 算法功能        | Python 推荐             | Java 推荐                      |
| ----------- | --------------------- | ---------------------------- |
| 计数统计        | `collections.Counter` | `HashMap<Integer, Integer>`  |
| 前 K 大 / 最小值 | `heapq`               | `PriorityQueue`              |
| 排序映射        | `SortedDict`（第三方）     | `TreeMap`                    |
| 不重复集合       | `set`                 | `HashSet`                    |
| 保序集合        | `SortedSet`（第三方）      | `TreeSet`                    |
| 滑动窗口        | `deque`               | `ArrayDeque`                 |
| 双端队列        | `deque`               | `LinkedList`                 |
| 字符频率表       | `dict` + Counter      | `HashMap<Character,Integer>` |

| 操作        | Python 平均复杂度  | Java 平均复杂度 |
| --------- | ------------- | ---------- |
| 查找哈希表键    | O(1)          | O(1)       |
| 插入哈希表键    | O(1)          | O(1)       |
| 删除哈希表键    | O(1)          | O(1)       |
| 查找有序映射    | O(log n)（第三方） | O(log n)   |
| 堆插入 / 删除  | O(log n)      | O(log n)   |
| 动态数组索引访问  | O(1)          | O(1)       |
| 动态数组插入/删除 | O(n)          | O(n)       |

| 操作                 | ArrayList  | LinkedList | 为什么                                        |
| ------------------ | ---------- | ---------- | ------------------------------------------ |
| **随机访问（get(i))**   | ✅ O(1)     | ❌ O(n)     | ArrayList 直接按下标访问；LinkedList 需从头/尾遍历       |
| **在末尾插入（addLast）** | ✅ 平均 O(1)* | ✅ O(1)     | ArrayList 尾插，偶尔扩容 O(n)；LinkedList 尾插直接修改指针 |
| **在中间插入 / 删除**     | ❌ O(n)     | ⚠️ O(n)    | ArrayList 需移动大量元素；LinkedList 需先遍历找到节点      |
| **在头部插入 / 删除**     | ❌ O(n)     | ✅ O(1)     | ArrayList 需整体右移；LinkedList 只需改指针           |
| **按值查找（contains）** | ❌ O(n)     | ❌ O(n)     | 都需遍历整个表                                    |


