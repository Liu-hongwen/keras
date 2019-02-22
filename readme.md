https://nbviewer.jupyter.org/

def qs(a, left, right):        
    if left >= right:
        return a
    
    low = left
    high = right
    k = a[low]
    
    while left < right:
        while left < right and a[right] > k:
            right -= 1
        a[left] = a[right]

        while left < right and a[left] <= k:
            left += 1
        a[right] = a[left]
        
    a[right] = k
    
    qs(a, low, left - 1)
    qs(a, right + 1, high)

predictions = [32,6,4,2,63,77,84,11,23]
qs(predictions, 0, len(predictions)-1)
print(predictions) 


import random
def sift(data, low, high):
    i = low      # 父节点
    j = 2 * i + 1   # 左子节点
    tmp = data[i]   # 父节点值
    while j <= high:    # 子节点在节点中
        if j < high and data[j] > data[j + 1]:  # 有右子节点且右节点比父节点值大
            j += 1
        if tmp > data[j]:
            data[i] = data[j]   # 将父节点替换成新的子节点的值
            i = j   # 变成新的父节点
            j = 2 * i + 1   # 新的子节点
        else:
            break
    data[i] = tmp   # 将替换的父节点值赋给最终的父节点

def heap_sort(data):
    n = len(data)
    # 创建堆
    for i in range(n//2 - 1, -1, -1):
        sift(data, i, n-1)

    # 挨个出数
    for i in range(n - 1, -1, -1):    # 从大到小
        data[0], data[i] = data[i], data[0]     # 将最后一个值与父节点交互位置
        sift(data, 0, i-1)


li = list(range(10))
random.shuffle(li)
print(li)
heap_sort(li)
print(li)


