# ASCII码表

ord()   chr()

0:48  A:65  a:97

# 字典

```python
from collections import defaultdict

# 以 list 为默认工厂函数
d = defaultdict(list)

# 向不存在的键添加值时，默认创建一个空列表
d['a'].append(1)
d['a'].append(2)
d['b'].append(3)

print(d)
```

```python
from collections import defaultdict

# 以 int 为默认工厂函数，返回值初始化为 0
d = defaultdict(int)

# 对不存在的键进行加法操作时，默认值会从 0 开始
d['a'] += 1
d['b'] += 1
d['b'] += 2

print(d)
```

# 浮点数保留

```python
a=3.1415926
print(f'{a:.2f}')
```

# 区间问题

## 1 区间合并



### 1.1 题意描述



区间合并问题大概**题意**就是：

给出一堆区间，要求**合并**所有**有交集的区间** （端点处相交也算有交集）。最后问合并之后的**区间**。

如下图所示：

[![img](https://camo.githubusercontent.com/0e350b8ff5ecaf8c148e015b6e421864e84d9a12386a9d63a71e29d3d16e1dbc/68747470733a2f2f706963342e7a68696d672e636f6d2f38302f76322d36653362623539656436633134656163666131333331633634356434616664665f31343430772e6a7067)](https://camo.githubusercontent.com/0e350b8ff5ecaf8c148e015b6e421864e84d9a12386a9d63a71e29d3d16e1dbc/68747470733a2f2f706963342e7a68696d672e636f6d2f38302f76322d36653362623539656436633134656163666131333331633634356434616664665f31343430772e6a7067)

区间合并问题示例：合并结果包含3个区间

### 1.2 解题步骤



【**步骤一**】：按照区间**左端点**从小到大排序。

【**步骤二**】：维护前面区间中最右边的端点为ed。从前往后枚举每一个区间，判断是否应该将当前区间视为新区间。

假设当前遍历到的区间为第i个区间 [li,ri]，有以下两种情况：

- li≤ed：说明当前区间与前面区间**有交集**。因此**不需要**增加区间个数，但需要设置 ed=max(ed,ri)。
- li>ed: 说明当前区间与前面**没有交集**。因此**需要**增加区间个数，并设置 ed=max(ed,ri)。

## 2 选择不相交区间



### 2.1 题意描述



**选择不相交区间问题**大概题意就是：

给出一堆区间，要求选择**尽量多**的区间，使得这些区间**互不相交**，求可选取的区间的**最大数量**。这里端点相同也算有重复。

如下图所示：

[![img](https://camo.githubusercontent.com/2dc533ce376bd15b39587b6618320d00e570ced6203accc4873315df133f4564/68747470733a2f2f706963312e7a68696d672e636f6d2f38302f76322d36393066376535336664333463333938303266343566343862353964356335615f31343430772e77656270)](https://camo.githubusercontent.com/2dc533ce376bd15b39587b6618320d00e570ced6203accc4873315df133f4564/68747470733a2f2f706963312e7a68696d672e636f6d2f38302f76322d36393066376535336664333463333938303266343566343862353964356335615f31343430772e77656270)

选择不相交区间问题示例：结果包含3个区间

### 2.2 解题步骤



【**步骤一**】：按照区间**右端点**从小到大排序。

【**步骤二**】：从前往后依次枚举每个区间。

假设当前遍历到的区间为第i个区间 [li,ri]，有以下两种情况：

- li≤ed：说明当前区间与前面区间有交集。因此直接跳过。
- li>ed: 说明当前区间与前面没有交集。因此选中当前区间，并设置 ed=ri。

## 3 区间选点问题



### 3.1 题意描述



**区间选点问题**大概题意就是：

给出一堆区间，取**尽量少**的点，使得每个区间内**至少有一个点**（不同区间内含的点可以是同一个，位于区间端点上的点也算作区间内）。

如下图所示：

[![img](https://camo.githubusercontent.com/66ab2da6ceb1201d6fe916fab8a0e81392c7d174caee8a288c148484aacb1c04/68747470733a2f2f706963612e7a68696d672e636f6d2f38302f76322d61376566303231653131393165633533663230363039626138373062343462615f31343430772e77656270)](https://camo.githubusercontent.com/66ab2da6ceb1201d6fe916fab8a0e81392c7d174caee8a288c148484aacb1c04/68747470733a2f2f706963612e7a68696d672e636f6d2f38302f76322d61376566303231653131393165633533663230363039626138373062343462615f31343430772e77656270)

区间选点问题示例，最终至少选择3个点

这个题可以转化为上一题的**求最大不相交区间**的数量。

对于这些**最大的不相交区间**，肯定是每个区间都需要选出一个点。而其他的区间都是和这些选出的区间有重复的，我们只需要把点的位置选在**重合**的部分即可。

也可以换一种思路：

我们将区间按照**右端点**从小到大排序，这时我们应该尽量选择**当前区间最右边的点**。

因为最右边的点可能和下面的其他区间重复，所以至少不比选择区间靠前位置的点差。

所以，最后的解法与选择不相交区间问题解法完全一样。

### 3.2 解题步骤



【**步骤一**】：按照区间右端点从小到大排序。

【**步骤二**】：从前往后依次枚举每个区间。

假设当前遍历到的区间为第i个区间 [li,ri]，有以下两种情况：

- li≤ed：说明当前区间与前面区间有交集，前面已经选点了。因此直接跳过。
- li>ed: 说明当前区间与前面没有交集。因此选中当前区间，并设置 ed=ri。

## 4 区间覆盖问题

### 4.1 题意描述



**区间覆盖问题**大概题意就是：

给出一堆区间和一个目标区间，问最少选择多少区间可以**覆盖**掉题中给出的这段目标区间。

如下图所示：

[![img](https://camo.githubusercontent.com/04a9b706eb35a148dd3582449d774249276673c3f28d7d61d3a52f008849482d/68747470733a2f2f706963332e7a68696d672e636f6d2f38302f76322d36363034316439393431363637343832666335316164656234613631366636345f31343430772e77656270)](https://camo.githubusercontent.com/04a9b706eb35a148dd3582449d774249276673c3f28d7d61d3a52f008849482d/68747470733a2f2f706963332e7a68696d672e636f6d2f38302f76322d36363034316439393431363637343832666335316164656234613631366636345f31343430772e77656270)

区间覆盖问题示例，最终至少选择2个区间才能覆盖目标区间

### 4.2. 解题步骤



【**步骤一**】：按照区间左端点从小到大排序。

**步骤二**】：**从前往后**依次枚举每个区间，在所有能覆盖当前目标区间起始位置start的区间之中，选择**右端点**最大的区间。

假设右端点最大的区间是第$i$个区间，右端点为 ri。

最后将目标区间的start更新成$r_i$

## 5 区间分组问题



### 5.1 题意描述



**区间分组**问题大概题意就是：给出一堆区间，问最少可以将这些区间分成多少组使得每个组内的区间互不相交。

如下图所示：

[![img](https://camo.githubusercontent.com/e9c9db829c87cffcfd601b481ece465482fb8f6a9a22a87cb2d0676ea85d70d5/68747470733a2f2f706963322e7a68696d672e636f6d2f38302f76322d36633661303435643438316464633434633636623034366566336537643463645f31343430772e77656270)](https://camo.githubusercontent.com/e9c9db829c87cffcfd601b481ece465482fb8f6a9a22a87cb2d0676ea85d70d5/68747470733a2f2f706963322e7a68696d672e636f6d2f38302f76322d36633661303435643438316464633434633636623034366566336537643463645f31343430772e77656270)

区间分组问题示例，最少分成3个组

### 5.2. 解题步骤



【**步骤一**】：按照区间左端点从小到大排序。

【**步骤二**】：从**前往后**依次枚举每个区间，判断当前区间能否被放到某个现有组里面。

（即判断是否存在某个组的右端点在当前区间之中。如果可以，则不能放到这一组）

假设现在已经分了 m 组了，第 k 组最右边的一个点是 rk，当前区间的范围是 [Li,Ri] 。则：

如果$L_i \le r_k$ 则表示第 i 个区间无法放到第 k 组里面。反之，如果 Li>rk， 则表示可以放到第 k 组。

- 如果所有 m 个组里面没有组可以接收当前区间，则当前区间新开一个组，并把自己放进去。
- 如果存在可以接收当前区间的组 k，则将当前区间放进去，并更新当前组的 rk=Ri。

**注意：**

为了能快速的找到能够接收当前区间的组，我们可以使用**优先队列 （小顶堆）**。

优先队列里面记录每个组的右端点值，每次可以在 O(1) 的时间拿到右端点中的的最小值。

# 冒泡排序

```python
def BubbleSort(arr):
    for i in range(len(arr) - 1):
        for j in range(len(arr) - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
    return arr

if __name__ == "__main__":
    arr_in = [6, 5, 18, 2, 16, 15, 19, 13, 10, 12, 7, 9, 4, 4, 8, 1, 11, 14, 3, 20, 17, 10]
    print(arr_in)
    arr_out = BubbleSort(arr_in)
    print(arr_out)
```

改进：

```python
def bubble_sort(arr):
    n = len(arr)
    for i in range(n):
        # 标记是否发生了交换
        swapped = False
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                # 交换元素
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                swapped = True
        # 如果没有发生交换，说明数组已经排序完成
        if not swapped:
            break
    return arr
```

# 不知道多少组输入

```python
while True:
    try:
        ...
    except EOFError:
        break
```

# 递归优化

递归程序在处理大规模问题时经常会遇到两个主要问题：**递归深度限制** 和 **重复计算子问题**。这两个问题可以通过以下两种方法来解决：

**增加递归深度限制**：使用 `sys.setrecursionlimit` 来增加 Python 的递归深度限制。

**缓存中间结果**：使用 `functools.lru_cache` 或其他形式的 memoization（记忆化）来避免重复计算。

Python 默认的递归深度限制是 1000，对于某些问题来说可能不够。你可以通过 `sys.setrecursionlimit` 来增加这个限制。

```
import sys
sys.setrecursionlimit(1 << 30)  # 将递归深度限制设置为 2^30
```



使用 `functools.lru_cache` 可以缓存函数的返回值，从而避免重复计算相同的子问题。这对于递归算法尤其有用，可以显著提高性能。

```python
from functools import lru_cache

@lru_cache(maxsize=None)
def recursive_function(n):
    if n == 0:
        return 1
    elif n == 1:
        return 1
    else:
        return recursive_function(n - 1) + recursive_function(n - 2)
```

# heapq

### 1. **基本函数**

#### **1.1 `heapq.heappush(heap, item)`**

将元素 `item` 推入堆中，并保持堆的性质。

```python
import heapq

heap = []
heapq.heappush(heap, 3)
heapq.heappush(heap, 1)
heapq.heappush(heap, 4)
heapq.heappush(heap, 2)
print(heap)  # [1, 2, 4, 3]（最小值始终在索引 0）
```

#### **1.2 `heapq.heappop(heap)`**

弹出堆中的最小元素，同时保持堆的性质。

```python
print(heapq.heappop(heap))  # 1
print(heap)  # [2, 3, 4]
```

#### **1.3 `heapq.heappushpop(heap, item)`**

先将 `item` 推入堆，然后弹出并返回堆中的最小元素。这比单独调用 `heappush` 和 `heappop` 更高效。

```python
heap = [1, 3, 5]
heapq.heapify(heap)
print(heapq.heappushpop(heap, 2))  # 1
print(heap)  # [2, 3, 5]
```

#### **1.4 `heapq.heapreplace(heap, item)`**

弹出堆中的最小元素，同时将 `item` 推入堆。与 `heappushpop` 类似，但顺序不同。

```python
heap = [1, 3, 5]
heapq.heapify(heap)
print(heapq.heapreplace(heap, 2))  # 1
print(heap)  # [2, 3, 5]
```

### 2. **将列表转为堆**

#### **2.1 `heapq.heapify(iterable)`**

将一个列表原地转换为堆结构。

```python
nums = [3, 1, 4, 1, 5, 9]
heapq.heapify(nums)
print(nums)  # [1, 1, 4, 3, 5, 9]
```

------

### 3. **获取堆中最大或最小的 N 个元素**

使用 `heapq.nlargest(n, iterable)` 和 `heapq.nsmallest(n, iterable)`。

```python
nums = [3, 1, 4, 1, 5, 9]
print(heapq.nlargest(2, nums))  # [9, 5]
print(heapq.nsmallest(2, nums))  # [1, 1]
```

------

### 4. **最大堆实现**

`heapq` 默认实现的是最小堆。如果需要最大堆，可以将元素取反来实现：

```python
nums = [3, 1, 4, 1, 5, 9]
max_heap = []
for num in nums:
    heapq.heappush(max_heap, -num)  # 取反存入

print(-heapq.heappop(max_heap))  # 9
print([-x for x in max_heap])  # [5, 4, 1, 1, 3]
```

------

### 5. **优先级队列**

结合元组使用，可以实现带优先级的队列。

```python
tasks = [(2, "Task A"), (1, "Task B"), (3, "Task C")]
heapq.heapify(tasks)
while tasks:
    priority, task = heapq.heappop(tasks)
    print(f"Processing {task} with priority {priority}")
# 输出:
# Processing Task B with priority 1
# Processing Task A with priority 2
# Processing Task C with priority 3
```

# deque

在 Python 中，`deque` 是双端队列（double-ended queue）的缩写，是 `collections` 模块中提供的一种数据结构。`deque` 支持在两端（队首和队尾）快速地添加和删除元素，适合实现队列、栈等常用数据结构。

### 导入方式

```python
from collections import deque
```

------

### 特性

1. **双端操作**：
   - 允许在两端添加或移除元素。
   - 比 Python 的内置列表在两端操作时效率更高，时间复杂度为 O(1)O(1)O(1)，而列表在队首操作的时间复杂度为 O(n)O(n)O(n)。
2. **线程安全**：
   - `deque` 是线程安全的，适合多线程环境中操作队列。
3. **可调整长度**：
   - 可以设置最大长度（`maxlen`），达到最大长度时，添加新元素会自动删除最老的元素。

------

### 常用方法

#### 创建 `deque`

```python
from collections import deque

# 创建一个空的 deque
dq = deque()

# 创建一个包含初始元素的 deque
dq = deque([1, 2, 3])
```

#### 添加和删除元素

```python
dq = deque([1, 2, 3])

# 在右端添加元素
dq.append(4)  # [1, 2, 3, 4]

# 在左端添加元素
dq.appendleft(0)  # [0, 1, 2, 3, 4]

# 删除右端的元素
dq.pop()  # [0, 1, 2, 3]

# 删除左端的元素
dq.popleft()  # [1, 2, 3]
```

#### 限制长度

```python
dq = deque(maxlen=3)  # 设置最大长度为 3
dq.extend([1, 2, 3])  # [1, 2, 3]
dq.append(4)          # [2, 3, 4]，超出长度限制时会自动移除最左边的元素
```

#### 扩展和旋转

```python
dq = deque([1, 2, 3])

# 在右端扩展多个元素
dq.extend([4, 5])  # [1, 2, 3, 4, 5]

# 在左端扩展多个元素
dq.extendleft([0, -1])  # [-1, 0, 1, 2, 3, 4, 5]

# 旋转元素
dq.rotate(2)  # [4, 5, -1, 0, 1, 2, 3]，正数表示向右旋转
dq.rotate(-1) # [5, -1, 0, 1, 2, 3, 4]，负数表示向左旋转
```

#### 检查和清空

```python
# 检查元素
print(3 in dq)  # True

# 清空队列
dq.clear()
print(dq)  # deque([])
```

# strip

`strip()` 是 Python 中的一个字符串方法，用于移除字符串两端的空白字符（包括空格、换行符、制表符等）。它还可以接受一个可选参数，用于指定要移除的字符。

### 示例：

```python
# 移除两端的空白字符
text = "   Hello, World!   "
cleaned_text = text.strip()
print(cleaned_text)  # 输出: "Hello, World!"

# 移除指定字符
text = "***Hello, World!***"
cleaned_text = text.strip('*')
print(cleaned_text)  # 输出: "Hello, World!"
```

# 切片

`[::-1]` 是 Python 中用于字符串、列表等可迭代对象的一种切片语法，用于反转该对象。

- `:` 表示切片的开始和结束，`[start:stop:step]` 是切片的标准格式。
- `start` 和 `stop` 如果省略，表示从头到尾。
- `step` 设置为 `-1` 表示反向切片。

例如，对于字符串和列表：

```python
# 反转字符串
s = "hello"
reversed_s = s[::-1]  # 输出 "olleh"

# 反转列表
lst = [1, 2, 3, 4, 5]
reversed_lst = lst[::-1]  # 输出 [5, 4, 3, 2, 1]
```

# 素数

```python
朴素法（时间复杂度是O(N^2)）
primesNumber = []
def is_prime(n):
	for i in range(2, n-1):
		if n % i == 0:
		return False
	return True
def primes(number):
	for i in range(2, number):
		if is_prime(i):
			primesNumber.append(i)
primes(10000)
print(primesNumber)

埃氏筛
def sieve_of_eratosthenes(n):
	# 创建一个布尔列表，初始化为 True，表示所有数字都假设为素数
	primes = [True] * (n + 1)
	primes[0] = primes[1] = False # 0 和 1 不是素数
	# 从 2 开始，处理每个数字
	for i in range(2, int(n**0.5) + 1):
		if primes[i]: # 如果 i 是素数
			# 将 i 的所有倍数标记为非素数
			for j in range(i * i, n + 1, i):
				primes[j] = False
	# 返回所有素数
	return [x for x in range(2, n + 1) if primes[x]]

欧拉筛
# 返回小于r的素数列表
def oula(r):
	# 全部初始化为0
	prime = [0 for i in range(r+1)]
	# 存放素数
	common = []
	for i in range(2, r+1):
		if prime[i] == 0:
			common.append(i)
		for j in common:
			if i*j > r:
				break
			prime[i*j] = 1
			#将重复筛选剔除
			if i % j == 0:
				break
	return common
prime = oula(20000)
print(prime)
```

# permutations

`itertools.permutations` 是 Python 中用于生成所有排列的函数。如果你指的是 `itertools.permutations`，那么它的基本用法是：

### 用法

```python
import itertools

# 示例列表
data = [1, 2, 3]

# 生成所有排列
result = itertools.permutations(data)

# 打印结果
for perm in result:
    print(perm)
```

### 解释：

- ```
  itertools.permutations(iterable, r)
  ```

  ：

  - `iterable` 是你想要排列的可迭代对象（比如列表、元组等）。
  - `r` 是排列的长度。如果你没有指定 `r`，默认值是 `len(iterable)`，即生成全排列。
  - 返回值是一个迭代器，包含所有可能的排列，每个排列是一个元组。

### 示例输出：

对于 `data = [1, 2, 3]`，默认情况下，生成的是所有 3 个元素的排列：

```python
(1, 2, 3)
(1, 3, 2)
(2, 1, 3)
(2, 3, 1)
(3, 1, 2)
(3, 2, 1)
```

### 限制排列长度

如果你只想生成特定长度 `r` 的排列，可以这样做：

```python
result = itertools.permutations(data, 2)
for perm in result:
    print(perm)
```

这会输出长度为 2 的排列：

```python
(1, 2)
(1, 3)
(2, 1)
(2, 3)
(3, 1)
(3, 2)
```

# enumerate

`enumerate()` 是 Python 中一个非常实用的内置函数，它用来同时遍历一个可迭代对象（如列表、元组、字符串等）及其索引（位置）。返回的是一个 `enumerate` 对象，实际上是一个包含索引和值的元组。

### 语法：

```python
enumerate(iterable, start=0)
```

- `iterable`：可以是任何可迭代对象（如列表、元组、字符串等）。
- `start`：索引的起始值，默认是 `0`，可以设置为其他值。

### 示例：

1. **基本用法：**

   ```python
   my_list = ['apple', 'banana', 'cherry']
   
   for index, value in enumerate(my_list):
       print(f"Index: {index}, Value: {value}")
   ```

   输出：

   ```python
   Index: 0, Value: apple
   Index: 1, Value: banana
   Index: 2, Value: cherry
   ```

2. **指定起始索引：**

   ```python
   my_list = ['apple', 'banana', 'cherry']
   
   for index, value in enumerate(my_list, start=1):
       print(f"Index: {index}, Value: {value}")
   ```

   输出：

   ```python
   Index: 1, Value: apple
   Index: 2, Value: banana
   Index: 3, Value: cherry
   ```

3. **用在列表推导式中：**

   ```python
   my_list = ['apple', 'banana', 'cherry']
   indexed_list = [f"{index}: {value}" for index, value in enumerate(my_list)]
   print(indexed_list)
   ```

   输出：

   ```python
   ['0: apple', '1: banana', '2: cherry']
   ```