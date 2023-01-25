### Output

```js
alert();
console.log();
document.write();  // like append
```

### Math
- `+`, `-`, `=`, `+=`, `%`, `++`;
- Math.{floor, ceil, round, abs, PI, etc...}();


### Arrays
```js
// init
var my_array = ["Red", "Blue", "Green"];
var my_array = new Array("Red", "Blue", "Green");

// some info
my_array.length

// add
my_array[n] = "value";
my_array.push("value");

// delete
```

### Cycles
```js
var i = 0;
while (i < 10) {
  console.log('in while-cycle', i);
  i++;
}

var i = 20;
do {
  console.log('in do-while-cycle', i);

} while (i < 10);

for (var i = 0; i < 10; i++) {
  console.log('in for-cycle', i);
}
```

### If && Switch
```js
if (condition && condition) {
  instruction;
} else if (condition || condition) {
  instruction;
} else {
  instruction;
}
```
```js
var res = 3;
switch (res) {
  case 1:
      alert("Res is 1");
    break;
  case 2:
      alert("Res is 2");
    break;
  case 3:
      alert("Res is 3");
    break
  default:
      alert("Res is unknown");
}
```
### Functions
```js
function func_name (word) {
  document.write (word + "<br>");
}

func_name("Hello")
```
### A strange objects
```js
// 1
// just as dict
var person = {
  firstName: 'Brad',
  age: 45,
  children: ['Kate', 'pery'],
  adress: {
    street: 'erm',
    city: 'kar',
    postcode: '123123'
  },
  Name: function () {
    return this.firstName + ", ваше имя" + this.age
  }
}
console.log(person.Name());


// 2
// strange way
var apple = new Object();
apple.color = 'green';
apple.shape = 'round';
console.log(apple.shape);

apple.describe = function () {
  return 'An aple is ' + this.color;
}
console.log(apple.describe());


// 3 with function
function Fruit (color, shape) {
  this.color = color;
  this.shape = shape;
}

var melon = new Fruit ('yellow', 'round');
var apple = new Fruit ('yellow', 'round');
```
### Events
```html
<p id="text">Just text</p>

<button onmouseover="change_color('blue');">Синий</button>
<button onmouseover="change_color('red');">Красный</button>
<br>

<form name="my_form" action="" action="" onsubmit="return validateForm();" method="post">
  Name: <input type="text" name="fname">
  <input type="submit" value="submit">
</form>

<script>
  function change_color(color) {
    var element = document.getElementById("text");
    element.style.color = color;
  }


  function validateForm() {
    var element = document.forms["my_form"]["fname"].value;
    if (element == "") {
      alert("Name must be set");
      return false
    }
  }
</script>
```
