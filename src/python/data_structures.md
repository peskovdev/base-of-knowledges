## List
- Methods:
    - `append(x)` - Add an item to the end of the list. Equivalent to `a[len(a):] = [x]`
    - `extend(iterable)` - Multiply append. Equivalent to `a[len(a):] = iterable`
    - `insert(i, x)` - Append before position
    - `remove(x)` - Remove the first item from the list whose value is equal to `x`
    **(# Raises ValueError)**
    - `pop([i])` - Remove and return by position **(# Raises ValueError)**
    - `clear()` remove all items from the list. Equivalent to `del a[:]`
    - `index(x[, start[, end]])` - Return zero-based index. Start and and optional for slices **(# Raises ValueError)**
    - `count(x)` - Return the number of times x appears in the list
    - ! `sort(*, key=None, reverse=False)` - skiped (but by default sort by alphabet)
    - `reverse()` - Reverse the elements of the list
    - `copy()` - Return a shallow copy of the list. Equivalent to `a[:]`
