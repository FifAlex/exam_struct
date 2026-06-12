### Задачи на 45

### 1. Медиана двух массивов
Описание: найти медиану двух отсортированных массивов быстрее чем за O(n). Нужно придумать эффективный алгоритм.

```python
def mediana2arrs(arr1, arr2):
    mid = []
    n = len(arr1)+len(arr2)
    if n % 2 == 1:
        mid.append(n // 2)
    else:
        mid.append(n // 2)
        mid.append(n // 2 - 1)
    i = 0
    j = 0
    k = 0
    mediana = 0
    while k <= max(mid):
        if i < len(arr1) and (j >= len(arr2) or arr1[i] <= arr2[j]):
            x = arr1[i]
            i += 1
        else:
            x = arr2[j]
            j += 1
        if k in mid:
            mediana += x
        k += 1
    
    return mediana // len(mid)

a1 = [1, 2, 4, 6]
a2 = [2, 3, 7, 9, 11, 13, 27]
print(mediana2arrs(a1, a2))
```

### 2. Top-K элементы
Описание: Найти K наиболее часто встречающихся элементов массива. Решение должно быть эффективнее полной сортировки.

### 2.1 Через кучу (O(n log k))

Эффективно, когда маленькое k и большое n
```python
import heapq

def count_popular(arr, k):
    counts = {}

    for x in arr:
        counts[x] = counts.get(x, 0) + 1

    heap = []

    for num, freq in counts.items():
        if len(heap) < k:
            heapq.heappush(heap, (freq, num))
        elif freq > heap[0][0]:
            heapq.heapreplace(heap, (freq, num))

    return [num for freq, num in heap]


a = [1, 5, 3, 8, 1, 1, 8, 9, 5, 1, 6, 8, 9, 3, 3]
print(count_popular(a, 2))
```

### 2.2 Через bucketsort (O(n))

```python
def count_popular(arr, k):
    counts = {}
    max_freq = 0

    for x in arr:
        counts[x] = counts.get(x, 0) + 1
        max_freq = max(max_freq, counts[x])

    buckets = [[] for _ in range(max_freq + 1)]

    for num, freq in counts.items():
        buckets[freq].append(num)

    result = []

    for freq in range(max_freq, 0, -1):
        for num in buckets[freq]:
            result.append(num)

            if len(result) == k:
                return result

    return result
```

### 3. Heap Sort
Описание: Реализовать Heap Sort без использования встроенных структур данных.

```python
def heapify(arr, n, i):
    largest = i
    left = i*2+1
    right = i*2+2

    if left < n and arr[left] > arr[largest]:
        largest = left
    
    if right < n and arr[right] > arr[largest]:
        largest = right
    
    if largest != i:
        arr[i], arr[largest] = arr[largest], arr[i]
        heapify(arr, n, largest)
    
def heapsort(arr):
    n = len(arr)

    for i in range(n//2 - 1, -1, -1):
        heapify(arr, n, i)

    for i in range(n-1, 0, -1):
        arr[0], arr[i] = arr[i], arr[0]
        heapify(arr, i, 0)

    return arr

massiv = [7, 3, 2, 8, 9, 12, 14, 3, 78, 54, 9, 34]

print(heapsort(massiv))
```

### 4. Группировка анаграмм слов (O(n*m log m))
Описание: Сгруппировать анаграммы слов с минимальным количеством сравнений.

```python
from collections import defaultdict

def group_anagrams(words):
    groups = defaultdict(list)

    for word in words:
        key = ''.join(sorted(word))
        groups[key].append(word)

    return list(groups.values())
```
