
```verse
Random := module:

```
# Returns a random `float` between `Low` and `High`, inclusive.

```verse
    GetRandomFloat<native><public>(Low:float, High:float)<transacts>:float


```
    # Returns a uniformly distributed, cryptographically-secure random `int` between `Low` and `High`, inclusive. (`Low` and `High` can be out of order.)

```verse
    GetRandomInt<native><public>(Low:int, High:int)<transacts>:int


```
    # Makes an `array` with the same elements as `Input` shuffled in a random order.

```verse
    Shuffle<public>(Input:[]t where t:type)<transacts>:[]t = external {}


```
