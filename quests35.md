### Задачи на 35 баллов

### 1. Ханойские башни
Описание: Реализовать задачу «Ханойские башни» с выводом всех перемещений. Объяснить экспоненциальный рост шагов.

```python
def hanoi(n, source, target, auxiliary):
    if n == 1:
        print(f"Переместить диск 1 с {source} на {target}")
        return
    hanoi(n - 1, source, auxiliary, target)
    print(f"Переместить диск {n} с {source} на {target}")
    hanoi(n - 1, auxiliary, target, source)

n = 3
print(f"Дисков: {n}, шагов: {2**n - 1}")
hanoi(n, 'A', 'C', 'B')
```

Почему шаги растут экспоненциально: T(n) = 2·T(n-1) + 1 → T(n) = 2ⁿ - 1. Каждый новый диск удваивает количество операций.

### 2. Quick Sort
Описание: Реализовать быструю сортировку с выбором pivot и объяснить влияние стратегии выбора.

```
def quick_sort(arr, pivot_strategy="middle"):
    if len(arr) <= 1:
        return arr
    if pivot_strategy == "first":
        pivot = arr[0]
    elif pivot_strategy == "last":
        pivot = arr[-1]
    else:
        pivot = arr[len(arr) // 2]
    left = [x for x in arr if x < pivot]
    middle = [x for x in arr if x == pivot]
    right = [x for x in arr if x > pivot]
    return quick_sort(left, pivot_strategy) + middle + quick_sort(right, pivot_strategy)

arr = [64, 34, 25, 12, 22, 11, 90]
print(quick_sort(arr))
```

Влияние pivot: Первый/последний даёт O(n²) на отсортированном массиве. Средний/случайный даёт O(n log n).

### 3. Merge Sort с подсчётом слияний
Описание: Реализовать сортировку слиянием и вывести количество операций слияния.

```python
def merge_sort_count(arr):
    merge_count = [0]

    def merge(left, right):
        merge_count[0] += 1
        result = []
        i = j = 0
        while i < len(left) and j < len(right):
            if left[i] <= right[j]:
                result.append(left[i])
                i += 1
            else:
                result.append(right[j])
                j += 1
        result.extend(left[i:])
        result.extend(right[j:])
        return result

    def sort(arr):
        if len(arr) <= 1:
            return arr
        mid = len(arr) // 2
        return merge(sort(arr[:mid]), sort(arr[mid:]))

    return sort(arr), merge_count[0]

arr = [38, 27, 43, 3, 9, 82, 10]
sorted_arr, count = merge_sort_count(arr)
print(f"Отсортировано: {sorted_arr}")
print(f"Слияний: {count}")
```

### 4. Рекурсивный бинарный поиск
Описание: Реализовать бинарный поиск рекурсивно с обработкой отсутствия элемента.

```python
def binary_search(arr, target, left, right):
    if left > right:
        return -1
    mid = (left + right) // 2
    if arr[mid] == target:
        return mid
    elif arr[mid] > target:
        return binary_search(arr, target, left, mid - 1)
    else:
        return binary_search(arr, target, mid + 1, right)

arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
print(binary_search(arr, 7, 0, len(arr) - 1))   # 6
print(binary_search(arr, 15, 0, len(arr) - 1))  # -1
```

### 5. Односвязный список
Описание: Реализовать односвязный список с вставкой, удалением и поиском.

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None

    def insert_begin(self, data):
        node = Node(data)
        node.next = self.head
        self.head = node

    def insert_end(self, data):
        node = Node(data)
        if not self.head:
            self.head = node
            return
        curr = self.head
        while curr.next:
            curr = curr.next
        curr.next = node

    def delete(self, data):
        if not self.head:
            return
        if self.head.data == data:
            self.head = self.head.next
            return
        curr = self.head
        while curr.next and curr.next.data != data:
            curr = curr.next
        if curr.next:
            curr.next = curr.next.next

    def search(self, data):
        curr = self.head
        while curr:
            if curr.data == data:
                return True
            curr = curr.next
        return False

    def display(self):
        curr = self.head
        while curr:
            print(curr.data, end=" -> ")
            curr = curr.next
        print("None")

ll = LinkedList()
ll.insert_end(10)
ll.insert_end(20)
ll.insert_begin(5)
ll.display()
```

### 6. Очередь через два стека
Описание: Реализовать очередь на двух стеках, показав понимание FIFO и LIFO.

```python
class QueueViaStacks:
    def __init__(self):
        self.s1 = []
        self.s2 = []

    def enqueue(self, x):
        self.s1.append(x)

    def dequeue(self):
        if not self.s2:
            while self.s1:
                self.s2.append(self.s1.pop())
        if not self.s2:
            raise IndexError("Очередь пуста")
        return self.s2.pop()

q = QueueViaStacks()
q.enqueue(1)
q.enqueue(2)
q.enqueue(3)
print(q.dequeue())  # 1
print(q.dequeue())  # 2
```

### 7. Стек с минимумом за O(1)
Описание: Реализовать стек с поддержкой получения минимального элемента за константное время.

```python
class MinStack:
    def __init__(self):
        self.stack = []
        self.mins = []

    def push(self, x):
        self.stack.append(x)
        if not self.mins or x <= self.mins[-1]:
            self.mins.append(x)

    def pop(self):
        if not self.stack:
            raise IndexError("Стек пуст")
        x = self.stack.pop()
        if x == self.mins[-1]:
            self.mins.pop()
        return x

    def get_min(self):
        if not self.mins:
            raise IndexError("Стек пуст")
        return self.mins[-1]

s = MinStack()
s.push(5)
s.push(3)
s.push(7)
print(s.get_min())  # 3
s.pop()
print(s.get_min())  # 3
s.pop()
print(s.get_min())  # 5
```

### 8. Алгоритм Дейкстры с выводом пути
Описание: Найти кратчайший путь во взвешенном графе, вывести расстояние и сам путь.

```python
import heapq


def dijkstra(graph, start, end):
    # Кратчайшие расстояния от start
    dist = {vertex: float("inf") for vertex in graph}
    dist[start] = 0

    # Предыдущая вершина на кратчайшем пути
    prev = {vertex: None for vertex in graph}

    # Приоритетная очередь (расстояние, вершина)
    pq = [(0, start)]

    while pq:
        current_dist, current_vertex = heapq.heappop(pq)

        # Пропускаем устаревшую запись
        if current_dist > dist[current_vertex]:
            continue

        # Перебираем соседей
        for neighbor, weight in graph[current_vertex]:
            new_dist = current_dist + weight

            if new_dist < dist[neighbor]:
                dist[neighbor] = new_dist
                prev[neighbor] = current_vertex
                heapq.heappush(pq, (new_dist, neighbor))

    # Если путь не существует
    if dist[end] == float("inf"):
        return float("inf"), []

    # Восстановление пути
    path = []
    current = end

    while current is not None:
        path.append(current)
        current = prev[current]

    path.reverse()

    return dist[end], path


# Пример графа
graph = {
    "A": [("B", 1), ("C", 4)],
    "B": [("A", 1), ("C", 2), ("D", 5)],
    "C": [("A", 4), ("B", 2), ("D", 1)],
    "D": [("B", 5), ("C", 1)]
}

distance, path = dijkstra(graph, "A", "D")

print("Кратчайшее расстояние:", distance)
print("Кратчайший путь:", " -> ".join(path))
```

### 9. Алгоритм Прима
Описание: Построить минимальное остовное дерево алгоритмом Прима.

```python
import heapq

def prim(graph, start):
    visited = set()
    mst = []
    total = 0
    pq = [(0, None, start)]

    while pq and len(visited) < len(graph):
        w, u, v = heapq.heappop(pq)
        if v in visited:
            continue
        visited.add(v)
        if u:
            mst.append((u, v, w))
            total += w
        for nxt, weight in graph[v]:
            if nxt not in visited:
                heapq.heappush(pq, (weight, v, nxt))

    return mst, total

graph = {
    'A': [('B', 2), ('C', 3), ('D', 6)],
    'B': [('A', 2), ('D', 1)],
    'C': [('A', 3), ('D', 4)],
    'D': [('A', 6), ('B', 1), ('C', 4)],
}

mst, w = prim(graph, 'A')
print(f"MST: {mst}, Вес: {w}")
```

### 10. Алгоритм Крускала
Описание: Построить минимальное остовное дерево алгоритмом Крускала с Union-Find.

```python
class UnionFind:
    def __init__(self, vertices):
        self.parent = {v: v for v in vertices}
        self.rank = {v: 0 for v in vertices}

    def find(self, x):
        if self.parent[x] != x:
            self.parent[x] = self.find(self.parent[x])
        return self.parent[x]

    def union(self, x, y):
        rx, ry = self.find(x), self.find(y)
        if rx == ry:
            return False
        if self.rank[rx] < self.rank[ry]:
            self.parent[rx] = ry
        elif self.rank[rx] > self.rank[ry]:
            self.parent[ry] = rx
        else:
            self.parent[ry] = rx
            self.rank[rx] += 1
        return True

def kruskal(graph):
    vertices = list(graph.keys())
    edges = set()
    for u in graph:
        for v, w in graph[u]:
            edges.add((tuple(sorted([u, v])), w))
    edges = sorted(edges, key=lambda x: x[1])

    uf = UnionFind(vertices)
    mst = []
    total = 0
    for (u, v), w in edges:
        if uf.union(u, v):
            mst.append((u, v, w))
            total += w
    return mst, total

graph = {
    'A': [('B', 2), ('C', 3), ('D', 6)],
    'B': [('A', 2), ('D', 1)],
    'C': [('A', 3), ('D', 4)],
    'D': [('A', 6), ('B', 1), ('C', 4)],
}

mst, w = kruskal(graph)
print(f"MST: {mst}, Вес: {w}")
```

### 11. HashMap с цепочками
Описание: Реализовать собственную хеш-таблицу с цепочками для разрешения коллизий.

```python
class HashMap:
    def __init__(self, capacity=16):
        self.capacity = capacity
        self.size = 0
        self.buckets = [[] for _ in range(capacity)]

    def _hash(self, key):
        return hash(key) % self.capacity

    def put(self, key, value):
        idx = self._hash(key)
        for i, (k, v) in enumerate(self.buckets[idx]):
            if k == key:
                self.buckets[idx][i] = (key, value)
                return
        self.buckets[idx].append((key, value))
        self.size += 1

    def get(self, key):
        idx = self._hash(key)
        for k, v in self.buckets[idx]:
            if k == key:
                return v
        return None

    def remove(self, key):
        idx = self._hash(key)
        for i, (k, v) in enumerate(self.buckets[idx]):
            if k == key:
                del self.buckets[idx][i]
                self.size -= 1
                return True
        return False

hm = HashMap()
hm.put("apple", 5)
hm.put("banana", 7)
print(hm.get("apple"))   # 5
hm.remove("apple")
print(hm.get("apple"))   # None
```

