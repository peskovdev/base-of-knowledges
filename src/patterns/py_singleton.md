#### Quasi-Singleton

```py
class Foo:
    __some_value = None

    @staticmethod
    def get_value():
        if Foo.__some_value is None:
            Foo.__some_value = []
        return Foo.__some_value


__some_value = Foo.get_value()
__some_value2 = Foo.get_value()
__some_value.append(1)
__some_value2.append(2)
print(Foo.get_value())
```
