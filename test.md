### Explain how arrays in GO works differently then C ?
In GO Array works differently than it works in C

- Arrays are values, assigning one array to another copies all the elements
- If you pass an array to a function, it will receive a copy of the array, not a pointer to it
- The size of an array is part of its type. The types [10] int and [20] int are distinct

### How to copy map in Go?
You copy a map by traversing its keys. Unfortunately, this is the simplest way to copy a map in Go:
```go
a := map[string]bool{"A": true, "B": true}
b := make(map[string]bool)
for key, value := range a {
    b[key] = value
}
```

### How do you swap two values? Provide a few examples.
Two values are swapped as easy as this:
```go
a, b = b, a
```
```go
a, b, c = b, c, a
```
The swap operation in Go is guaranteed from side effects. The values to be assigned are guaranteed to be stored in temporary variables before starting the actual assigning, so the order of assignment does not matter.


### Queue Implementation
```python
class Queue:
    def __init__(self):
        self.items = []

    def isEmpty(self):
        return self.items == []

    def enqueue(self, item):
        self.items.insert(0,item)

    def dequeue(self):
        return self.items.pop()

    def size(self):
        return len(self.items)
```

### Pivot List Implementation
```python
import functools
from typing import Optional

from list_node import ListNode
from test_framework import generic_test
from test_framework.test_failure import TestFailure
from test_framework.test_utils import enable_executor_hook


def list_pivoting(l: ListNode, x: int) -> Optional[ListNode]:
    # TODO - you fill in here.
    return None


def linked_to_list(l):
    v = list()
    while l is not None:
        v.append(l.data)
        l = l.next
    return v


@enable_executor_hook
def list_pivoting_wrapper(executor, l, x):
    original = linked_to_list(l)

    l = executor.run(functools.partial(list_pivoting, l, x))

    pivoted = linked_to_list(l)
    mode = -1
    for i in pivoted:
        if mode == -1:
            if i == x:
                mode = 0
            elif i > x:
                mode = 1
        elif mode == 0:
            if i < x:
                raise TestFailure('List is not pivoted')
            elif i > x:
                mode = 1
        else:
            if i <= x:
                raise TestFailure('List is not pivoted')

    if sorted(original) != sorted(pivoted):
        raise TestFailure('Result list contains different values')


if __name__ == '__main__':
    exit(
        generic_test.generic_test_main('pivot_list.py', 'pivot_list.tsv',
                                       list_pivoting_wrapper))
```
