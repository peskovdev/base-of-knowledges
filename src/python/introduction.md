## Numbers

- Division
    - Division always returns a floating point number
    - `num1 // num2`: floor division (return int & round down)
- Multiply
    - `**` operator to calculate powers
    - Since `**` has higher precedence than `-`, `-3**2` will be interpreted as `-(3**2)`
    and thus result in `-9`. To avoid this and get `9`, you can use `(-3)**2`.
- Operators with mixed type operands convert the integer operand to floating point
    - 4 * 3.75 = 15.0
    - 2 + 2.0 = 4.0
- In interactive mode, the last printed expression is assigned to the variable `_`


## Strings

- `\` - escape characters
- `r'string'` - raw strings (escapes - `\` )
- strings can be concatenated (glued together) with the `+` operator, and repeated with `*`
- concatenated variable and string literal: `f'{str_var}' "new string"` (or use `+`)
- string is indexed (can iterate)
- `word[0:2]`  - characters from position 0 (included) to 2 (excluded)
- Slice indices have useful defaults; an omitted first index defaults to zero,
an omitted second index defaults to the size of the string being sliced.
- Attempting to use an index that is too large will result in an error,
However, out of range slice indexes are handled gracefully when used for slicing
- String CAN NOT be changed!!! They are immutable.
- The built-in function len() returns the length of a string: `len('str')`


## Lists

- also can be endexed and sliced
- all slice operations return a new list containing the requested elements
- `my_list` and `my_list[:]` are 2 different list. `my_list[:]` returns a NEW list.
- lists support concatenation
- lists are mutable type
- Assignment to slices is also possible, and this can even change the size of
the list or clear it entirely (`my_list[3:5] = []`)


## While
- anything with non-zero length is true, empty sequences are false


## print
- `print('msg', end=', ')`: `end=` can use custom ending instead of `\n`
