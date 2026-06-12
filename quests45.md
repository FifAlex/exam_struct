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
