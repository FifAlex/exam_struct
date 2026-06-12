# Алгоритмы и структуры данных — сборник решений

## Задачи на 25 баллов

### 1. Сортировка пузырьком с выводом после каждого прохода

**Описание:** Реализовать сортировку пузырьком для массива чисел. Выводить массив после каждого прохода, чтобы видеть, как элементы «всплывают».

```python
def bubble_sort_verbose(arr):
    n = len(arr)
    for i in range(n):
        swapped = False
        for j in range(n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                swapped = True
        print(f"После прохода {i + 1}: {arr}")
        if not swapped:
            break
    return arr

arr = [64, 34, 25, 12, 22, 11, 90]
print("Исходный:", arr)
bubble_sort_verbose(arr)
```

### 2. Проверка сортированности

Описание: Проверить, отсортирован ли массив, без встроенных функций сортировки.

```python
def is_sorted(arr):
    for i in range(len(arr) - 1):
        if arr[i] > arr[i + 1]:
            return False
    return True

print(is_sorted([1, 2, 3, 4, 5]))  # True
print(is_sorted([1, 3, 2, 4, 5]))  # False
```

### 3. Второй по величине элемент за один проход

Описание: Найти второй максимум без сортировки, за O(n).

```python
def second_largest(arr):
    if len(arr) < 2:
        return None
    first = second = float('-inf')
    for x in arr:
        if x > first:
            second = first
            first = x
        elif x > second and x != first:
            second = x
    return second if second != float('-inf') else None

print(second_largest([10, 5, 8, 20, 15]))  # 15
print(second_largest([5, 5, 5, 5]))        # None
```

### 4. Линейный поиск элемента
Описание: Найти элемент в массиве и вернуть его индекс или сообщить об отсутствии.

```python
def linear_search(arr, target):
    for i, x in enumerate(arr):
        if x == target:
            return i
    return -1

arr = [10, 20, 30, 40, 50]
idx = linear_search(arr, 30)
print(f"Найден на индексе {idx}" if idx != -1 else "Не найден")
```

### 5. Стек на массиве
Описание: Реализовать стек с операциями push, pop и top.

```python
class Stack:
    def __init__(self):
        self.items = []

    def push(self, x):
        self.items.append(x)

    def pop(self):
        if self.items:
            return self.items.pop()
        else:
            print("Стек пуст")

    def top(self):
        if self.items:
            return self.items[-1]
        else:
            print("Стек пуст")

s = Stack()
s.push(10)
s.push(20)
print(s.top())  # 20
print(s.pop())  # 20
print(s.top())  # 10
```

### 6. Очередь на массиве
Описание: Реализовать очередь с операциями enqueue и dequeue.

```python
class Queue:
    def __init__(self):
        self.items = []

    def enqueue(self, x):
        self.items.append(x)

    def dequeue(self):
        if self.items:
            return self.items.pop(0)
        else:
            print("Очередь пуста")


q = Queue()
q.enqueue(10)
q.enqueue(20)
print(q.dequeue())  # 10
print(q.dequeue())  # 20
```

### 7. Проверка скобок через стек
Описание: Проверить корректность круглых и квадратных скобок в выражении.

```python
def is_valid_brackets(s):
    stack = []
    pairs = {')': '(', ']': '['}
    for ch in s:
        if ch in '([':
            stack.append(ch)
        elif ch in ')]':
            if not stack or stack.pop() != pairs[ch]:
                return False
    return len(stack) == 0

print(is_valid_brackets("([])[]"))   # True
print(is_valid_brackets("([)]"))     # False
print(is_valid_brackets("(([]"))     # False
```

### 8. Размен монет (жадный алгоритм)
Описание: Разменять сумму минимальным количеством монет номиналами 1, 2, 5, 10.

```python
def min_coins(amount):
    coins = [10, 5, 2, 1]
    result = {}
    for coin in coins:
        count = amount // coin
        if count > 0:
            result[coin] = count
            amount -= count * coin
    return result

print(min_coins(27))  # {10: 2, 5: 1, 2: 1}
```

### 9. Максимальное количество встреч
Описание: Выбрать максимальное число непересекающихся встреч. Каждая встреча задана временем начала и конца

```python
def max_meetings(meetings):
    meetings.sort(key=lambda x: x[1])
    selected = []
    last_end = float('-inf')
    for start, end in meetings:
        if start >= last_end:
            selected.append((start, end))
            last_end = end
    return selected

meetings = [(1, 3), (2, 5), (3, 8), (4, 6), (6, 9), (8, 10)]
print(max_meetings(meetings))  # [(1, 3), (3, 8), (8, 10)]
```
