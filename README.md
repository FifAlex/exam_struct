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
