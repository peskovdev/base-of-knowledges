## For statements

- If you modify collection while iterating - use `list.copy()` or create a new one

## Range() function

- `range(x, y, s)`: `x`-start, `y`-end, `s`-step (or increment)
- `range(x)` = `range(0, x)`
- To iterate over the indices of a sequence, you can combine range() and len() as follows:
`for i in range(len(list)):` (or use `enumerate` as substitute)

## Break and continue Statements, and else Clauses on Loops

- `else` clauses is executed when the loop terminates through exhaustion of the
iterable (with `for`) or when the condition becomes false (with `while`)
**# but NOT break statement**

## Match statements:
- Syntax:
  ```
  match variable:                                               
      case value1:                if variable == value1:        
          action()                    action()                  
      case val2 | val1:           elif variable in (val2, val1):
          action()        VS          action()                  
      case value3:                elif variable == value3:      
          action()                    action()                  
      case value4:                elif variable == value4:      
          action()                    action()                  
      case _:                     else:                         
          action()                    action()                  
  ```
- Only the first pattern that matches gets executed

## Function
- The default value is evaluated only once! `def f(L=[]):` - `L` the same list for all cals
- Special parameters: `/` and `*`:
  ```
  def example(pos_only, /, pos_or_kwd, *, kwd_only):
  ```
- Arbitary argument lists (`*args`)
    - Any formal parameters which occur after the *args parameter are ‘keyword-only’ arguments
## Lambda expressions
- Syntax: `lambda a, c: a + c`
