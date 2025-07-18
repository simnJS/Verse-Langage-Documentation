# Animation Module

This module provides animation functionality with Bezier curve interpolation support.

## Cubic Bezier Parameters Structure

```verse
Animation := module:
    # A structure for defining Bezier interpolation parameters.
    # See https://en.wikipedia.org/wiki/B%C3%A9zier_curve for more info on Bezier curves.
    cubic_bezier_parameters<native><public> := struct<computes>:
```

A structure for defining Bezier interpolation parameters. See [Bezier curves](https://en.wikipedia.org/wiki/B%C3%A9zier_curve) for more information.

### Control Point P1

#### X0
```verse
# X value of the P1 control point. `0.0 <= X0 <= 1.0` or an error will be generated when calling `animation_controller.SetAnimation`.
X0<native><public>:float = external {}
```

X coordinate of the P1 control point. Must be between 0.0 and 1.0, otherwise an error will be generated when calling `animation_controller.SetAnimation`.

#### Y0
```verse
# Y value of the P1 control point.
Y0<native><public>:float = external {}
```

Y coordinate of the P1 control point.

### Control Point P2

#### X1
```verse
# X value of the P2 control point. `0.0 <= X1 <= 1.0 or an error will be generated when calling `animation_controller.SetAnimation`.
X1<native><public>:float = external {}
```

X coordinate of the P2 control point. Must be between 0.0 and 1.0, otherwise an error will be generated when calling `animation_controller.SetAnimation`.

#### Y1
```verse
# Y value of the P2 control point.
Y1<native><public>:float = external {}
```

Y coordinate of the P2 control point.
