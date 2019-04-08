## Table of Contents
1. [List](#list)
2. [String](#string)
3. [Set](#set)
4. [Dictionary](#dictionary)
5. [Deque](#deque)
6. [Heap](#heap)
7. [Synchronized Queue](#synchronized-queue)
8. [General Collections](#general-collections)

## List

Let's define `a = []` as a list.

1. Appends an element to a list, `a.append(4)`.
2. Extends `a` with another list, `a.extend([1,2,3])`.
3. Removes and returns the last element of the list, `last_element = a.pop()`
4. Removes all items from a list, `a.clear()`
5. Reverses all the items in a list in place, `a.reverse()` or `b = a[::-1]` depending on the use case.
6. Returns a shallow copy of a list, `shallow_copy_of_a = a.copy()`
7. Returns the first k element in a list, `a[:k]`
8. Returns the last k element in a list, `a[-k:]`. Please note that `a[k:]` doesn't return last k element
but it returns all the elements starting from the k-th, assuming zero index.
9. Returns all the odd-indexed elements, `a[::2]`. This is just an example to show the usage of the stride number.
10. Sort the list. `b = sorted(a)` returns a new sorted list; `a.sort()` sorts the list in-place. Both
`sorted` and `.sort()` have attributes `reverse=` and `key=`. For example, we can sort a list in-place with
the first element in ascending order, `a.sort(key=lambda x: x[0], reverse=True)`.
11. Is a list is empty: `not a`.
12. Iterate all elements paired with their indices, use `enumerate(a)`.
13. Zip k lists: `zip(a, b, c...)`, where a, b, c are lists.

## String

```Python
# string is iterable.
a = "Test String"
```
1. formatting. `'To format {} string {}'.format(3, 'correctly')`.
2. Is prefixed or suffixed with? `a.startswith('Test')`/`a.endswith('ing')`.
3. What type is this string? `a.islower()`/`a.isupper()`/`a.isdecimal()`/`a.isalnum()`/`a.isnumeric()`/...
4. Convert between upper and lower cases. `a.upper()`/`a.lower()`.
5. Split and Join. `a.split()` (by space), `a.split('t')` (by a character), `','.join(['a', 'b', 'c'])`
6. Concatenate. `a + a`
7. Find/Replace. `a.find('est')`/`a.replace('est', 'new_est')`.
8. String slices (substrings), same with list. `a[5:]` (this will evaluate to `'String'`).

## Set

Let's define `a = set()` as a Set.

1. Initialization: `a = {1, 2, 3}`. Empty set should be created with `set()` but not `{}` since `{}` creates ane mpty dictionary.
2. Tell whether an element in a Set by `3 in a`.
3. Is a Set is empty? `not a`
4. Append an elment to a Set, `b = a | {1}`, please note that `a | {1}` will not change `a`.
5. Operations between two sets:
  + elements in a but not in b (diff): `a - b`
  + elements in both a and b (AND): `a ^ b`
  + elements in a or b or both (UNION): `a | b`

## Dictionary

Let's define `a = {}` as a Dictionary.

1. Is a Dictionary empty? Same as all above.
2. Is a key in dict? `key in a`.
3. Add/Mutate a value of a key. `a[key] = val`.
4. Remove a key in a dict. `del a[key]`
5. (Python3) Returns an iterator of all kv pairs: `a.items()`. This is useful for looping, i.e., `for k, v in a.items(): pass`.
6. Get all keys/values of a dict, `a.keys()`/`a.values()`.

## Deque

```Python
from collections import deque

a = deque([1, 2, 3])
```

1. Append to the right side (Enqueuing), `a.append(2)`.
2. Append to the left side, `a.appendleft(2)`.
3. Extend to the right/left side, `a.extend([1, 2, 3])`/`a.extendleft([1, 2, 3])`.
4. Pop from right side, `right_most_element = a.pop()`.
5. Pop from left side, `left_most_element = a.popleft()`.
6. `a.copy()`, `a.clear()`, `a.reverse()` have all same semantics as `list` objects.

## Heap

```Python
import heapq

a = []
```

1. Heapify a list (transform a list into a heap **in place**, linear time), `heaqp.heapify(a)`. This function returns None.
2. Push a value onto heap, `heapq.heappush(a, 1)`.
3. Pop and return the smallest item from heap, `smallest = heapq.heappop(a)`
4. Peek the smallest item from heap, `smallest = a[0]`.
5. If the items are tuples, the heapq uses the first element in a tuple as key.
6. Max heap: enqueue negative values as key.

## Synchronized Queue

Please note that the queue has an embedded lock mechanism to provide thread-safe read/write.

```Python
from queue import Queue, LifoQueue, PriorityQueue

q = Queue(maxsize=0)
lifo_q = LifoQueue(maxsize=0)  # Stack
p_q = PriorityQueue(maxsize=0)

q.empty()  # Is the queue empty?
q.full()   # Is the queue full?
p_q.put((10, item))          # Thread-safe enqueue. For priority queue, 10 is the priority num.
p_q.put_nowait((10, item))   # Thread-unsafe enqueue.
front_most = q.get()         # Thread-safe dequeue
front_most = q.get_nowait()  # Thread-unsafe dequeue.

a = []
```

## General Collections

1. Counter (like a wrapper of a dictionary)

        ```Python
        >>> c = Counter('count the occurrence of all letters.')
        >>> c.most_common(3)
        [('r', 3), ... ]
        >>> c = Counter({'red': 4, 'blue': 2})
        >>> sum(c.values())   # total of all counts
        >>> for k, cnt_k in c.items():
        ...     pass
        ```

2. defaultdict (Wrapper of a regular Python dictionary)

    Take a constructor of the value type in its constructor, for example,

        ```Python
        >>> d = defaultdict(list)
        >>> for k, v in s:
        ...     d[k].append(v)
        ```

3. OrderedDict

    Ordered dictionary.

        ```Python
        >>> d = OrderedDict.fromkeys('abcde')
        >>> d.move_to_end('b')
        >>> ''.join(d.keys())
        'acdeb'
        >>> d.move_to_end('b', last=False)
        >>> ''.join(d.keys())
        'bacde'
        >>> last_key, value = d.popitem()  # pop the last item
        ```
