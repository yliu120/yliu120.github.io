# Useful But Easy to Forget Python APIs

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

## Deque

## Heap
