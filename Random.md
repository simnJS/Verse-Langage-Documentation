# Random Module

This module provides random number generation and array shuffling functionality for Fortnite experiences.

## Random Number Generation

### GetRandomFloat
```verse
Random := module:
    # Returns a random `float` between `Low` and `High`, inclusive.
    GetRandomFloat<native><public>(Low:float, High:float)<transacts>:float
```

Returns a random float between Low and High, inclusive.

### GetRandomInt
```verse
# Returns a uniformly distributed, cryptographically-secure random `int` between `Low` and `High`, inclusive. (`Low` and `High` can be out of order.)
GetRandomInt<native><public>(Low:int, High:int)<transacts>:int
```

Returns a uniformly distributed, cryptographically-secure random integer between Low and High, inclusive. Low and High can be specified in any order.

## Array Operations

### Shuffle
```verse
# Makes an `array` with the same elements as `Input` shuffled in a random order.
Shuffle<public>(Input:[]t where t:type)<transacts>:[]t = external {}
```

Creates an array with the same elements as the input array but shuffled in a random order. Works with arrays of any type.
