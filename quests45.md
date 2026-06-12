### Звдачи на 45

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
```
a1 = [1, 2, 4, 6]
a2 = [2, 3, 7, 9, 11, 13, 27]
print(mediana2arrs(a1, a2))
