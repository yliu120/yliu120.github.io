## Table of Contents
1. [List](#list)
2. [String](#string)
3. [Set](#set)
4. [Dictionary](#dictionary)
5. [Deque](#deque)
6. [Heap](#heap)
7. [Synchronized Queue](#synchronized-queue)
8. [General Collections](#general-collections)
9. [Itertools](#itertools)
10. [Functools](#functools)
11. [Tricks](#tricks)

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
14. `nums[:]` returns a copy of nums 
15. `list1+list2` gives a new list that is the concatenation of list1 and list2.

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
5. `covered.update({a, b, c, d})` Add a, b, c,d into set.
6. Operations between two sets:
  + elements in a but not in b (diff): `a - b`
  + elements in both a and b (AND): `a ^ b`
  + elements in a or b or both (UNION): `a | b`

## Dictionary

Let's define `a = {}` as a Dictionary.

1. Is a Dictionary empty? Same as all above.
2. Is a key in dict? `key in a`.
3. Add/Mutate a value of a key. `a[key] = val`.
4. Remove a key in a dict. `del a[key]` or `a.pop(key)`
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
Heaps are binary trees for which every parent node has a value less than or equal to any of its children. This implementation uses arrays for which heap[k] <= heap[2*k+1] and heap[k] <= heap[2*k+2] for all k, counting elements from zero. Its smallest element is always the root, heap[0] (Min heap).

1. Heapify a list (transform a list into a heap **in place**, linear time), `heaqp.heapify(a)`. This function returns None. O(n)
2. Push a value onto heap, `heapq.heappush(a, 1)`.
3. Pop and return the smallest item from heap, `smallest = heapq.heappop(a)`
4. Peek the smallest item from heap, `smallest = a[0]`.
5. `heapq.nlargest(n, iterable[, key])` Return a list with the n largest elements from the dataset defined by iterable.
    Example: 
    ```Python
    counts = collections.Counter(nums)
    return heapq.nlargest(k, counts.keys(), key=counts.get)
    
    heapq.nsmallest(K, points, lambda (x, y): x * x + y * y)
    ```
6. If the items are tuples, the heapq uses the first element in a tuple as key.
7. Max heap: enqueue negative values as key.

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
   >>> c.most_common(1)[0][0]
   'r'
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
        
## itertools

+ `itertools.chain(iter1, iter2, iter3)`
  ```Python
  a = range(5)
  b = range(3)
  # Will print 0, 1, 2, 3, 4, 0, 1, 2
  for i in itertools.chain(a, b):
    print(i)
  ```

+ `itertools.combinations('ABCD', 2) # --> AB AC AD BC BD CD`
+ `itertools.permutations('ABCD', 2)` almost same as above but returns all permutations.
+ `itertools.product('ABCD', 'xy') # --> Ax Ay Bx By Cx Cy Dx Dy`

## functools

+ `reduce`
  ```Python
  functools.reduce(lambda x, y: x+y, [1, 2, 3, 4, 5]) calculates ((((1+2)+3)+4)+5)
  ```
  Please note that map() is a builtin function. For example, `map(lambda x: x**2, [1, 2, 3]) # --> [1, 4, 9]`.


## Tricks
1. lambda function:
    +   `dist = lambda i: points[i][0]**2 + points[i][1]**2`   `dist(i)` represent dist of point[i] to (0, 0)
2. random
    +   `random.randint(1, n)` 
    +   `random.randrange(stop)` `random.randrange(start, stop[, step])` Return a randomly selected element from range(start, stop, step). 
    +   `random.random()` Return the next random floating point number in the range [0.0, 1.0).
    +   `random.choice(seq)` Return a random element from the non-empty sequence seq. If seq is empty, raises IndexError.
    
3. `bisect.bisect(a, x, lo=0, hi=len(a))` returns an insertion point which comes after (to the right of)
     any existing entries of x in a.  `bisect.bisect_left(a, x, lo=0, hi=len(a)`the insertion point will be
     before (to the left of) any existing entries.
    
   `bisect.insort(a, x, lo=0, hi=len(a)` inserting x in a after any existing entries of x.
   `bisect.insort_left(a, x, lo=0, hi=len(a)` inserting x in a before any existing entries of x
4. others
    +   `s = cmp(x, 0)`
    +   `words = re.findall("\w+", paragraph.lower())`  find all the words in list with lowercase
    
      `bisect.insort(a, x, lo=0, hi=len(a)` inserting x in a after any existing entries of x. `bisect.insort_left(a, x, lo=0, hi=len(a)` inserting x in a before any existing entries of x

    +    `Trie = lambda: collections.defaultdict(Trie)`
    +    `int(k, 16)` 
    +    ` def __hash__(self): return hash(self.content)`
