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
