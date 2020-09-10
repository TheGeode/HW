This algotithm pushes numbers from input file into a heap and then gets the maximum element of the heap until there are no elements left in it.

Main file (heapSort.py)

```python
import heap

name = "input.txt"
rf = open(name, "r")

myheap = heap.Heap(0,[])

n = int(rf.readline().strip())

mylist = list(map(int, rf.readline().strip().split(' ')))

for i in range(n) :
    myheap.add(mylist[i], 0)

for i in range(n) :
    val, spec = myheap.cut()
    print(val, end=" ")
    
print()
```

heap library (heap.py)

```python
class Element(object) :
    def __init__(self, val1, arr) :
        self.val = val1
        self.specs = arr

    def getval(self) :
        return(self.val)

    def setval(self, val1):
        self.val = val1

    def getspec(self, num) :
        return(self.specs[num])

    def getspecs(self) :
        return(self.specs)

class Heap(object) :
    def __init__(self, N1, heap1) :
        self.N = N1
        self.heap = heap1

    def heapify(self, num) :
        left = self.heap[num].val + 1
        right = self.heap[num].val + 1

        if num * 2 + 1 < self.N :
            left = self.heap[num * 2 +1].val
        if num * 2 + 2 < self.N :
            right = self.heap[num * 2 +2].val
        minv = min(self.heap[num].val,min(left, right))
        if minv == left :
            self.heap[2 * num + 1], self.heap[num] = self.heap[num], self.heap[2 * num + 1]
            self.heapify(2 * num + 1)
            return
        if minv == right :
            self.heap[2 * num + 2], self.heap[num] = self.heap[num], self.heap[2 * num + 2]
            self.heapify(2 * num + 2)
            return
        return
    
    def heapifyUp(self, num) :
        if num == 0 :
            return

        parent = (num - 1) // 2
        if self.heap[parent].val > self.heap[num].val :
            self.heap[parent], self.heap[num] = self.heap[num], self.heap[parent]
            self.heapifyUp(parent)
            return
        return

    def look(self) :
        return(self.heap[0].val, self.heap[0].specs)

    def cut(self) :
        ans = self.heap[0]
        self.heap[self.N - 1], self.heap[0] = self.heap[0], self.heap[self.N - 1]
        self.N -= 1
        self.heapify(0)
        return(ans.val, ans.specs)

    def add(self, newe, specs) :
        if self.N < len(self.heap):
            self.heap[self.N] = Element(newe, specs)
            self.N += 1
        else :
            self.heap.append(Element(newe, specs))
            self.N += 1
        self.heapifyUp(self.N - 1)
	
    def getSize(self) :
        return(self.N)
```
