### Basic syntax

```
package main

// imports
import "fmt"

func main() {
  // instructions
}
```

### vars & pointers
- define:
  ```
  var var_name type = value
  var i float64 = 3.1125
  var str string = "blablabla"
  var isValid bool = true
  
  // or
  new_str := "value"
  ```
- pointers
  ```
  func main() {
    var x = 0
    pointer(&x)
    fmt.Println(x)
  }

  func pointer (x *int) {
    *x = 2
  }
  ```

### I/O
```
import "fmt"

Println("blablabla")
Printf("%f", 3.123)
```

### if/else & case

```
var age = 10

if age < 5 {
  fmt.Println("Too small")
} else if age == 5 {
  fmt.Println("Not bad")
} else if (age > 5) && (age <= 18) {
  var grade = age - 5
  fmt.Println("You're studying in", grade, "course")
} else {
  fmt.Println("Go to university!")
}

switch age {
  case 5: fmt.Println ("You are 5")
  case 15: fmt.Println ("You are 15")
  case 10: fmt.Println ("You are 10")
  default: fmt.Println ("unknown")
}
```

### Cycles
```
var i = 1
for i < 10 {
  fmt.Println(i)
  i++
}

// or

for i := 0; i <= 10; i++ {
 fmt.Println(i)
}

for i, value := range array {
  fmt.Println(value, i)
}
```

### Arrays
- List
  ```
  var arr[3] int
  arr[0] = 35
  arr[1] = 12
  arr[2] = 92

  nums := [3] float64 {4.25, 1.12, 92.11}

  for i, value := range nums {
    fmt.Println(value, i)
  }
  ```
- Slice
  ```
  // When declaring a slice, you omit its size in the brackets,
  // like this:
  myslice := []string
  // This tells Go that the size of the array underlying the slice can be dynamically changed.
  ```
- Maps (dict)
  ```
  // make(map[key-type]value-type)
  web_sites := make(map[string]float64)

  web_sites["yandex"] = 0.98
  web_sites["youtube"] = 0.99

  fmt.Println(web_sites["ItProger"])
  ```

### func
- Default
  ```
  func main() {
    summed_result, message := sum(2, 3)
    fmt.Println(message, summed_result)
  }

  func sum (num1 int, num2 int) (int, string) {
    result := num1 + num2
    return result, "Your sum is:"
  }
  ```
- замыкания?
  ```
  var num = 3
  multiple := func() int {
    num *= 2
    return num
  }
  fmt.Println(multiple())
  ```

### defer
```
package main

import "fmt"

func main() {
  defer two()
  one()
  // 1 2
}

func one () {
  fmt.Println("1")
}

func two () {
  fmt.Println("2")
}
```

### Package manager
- Write neccessary imports in your modules
- Install by command: `go mod tidy`
- Install by command: `go get github.com/devpeskov/go_greetings`

### Replace remote module on local
```
go mod edit -replace github.com/devpeskov/go_greetings=../greetings
go mod tidy
```
