
```verse
CreativeAnimation := module:

```
# A structure for defining Bezier interpolation parameters.
        # See https://en.wikipedia.org/wiki/B%C3%A9zier_curve for more info on Bezier curves.

```verse
        cubic_bezier_parameters<native><public> := struct<computes>:

```
            # X value of the P1 control point. `0.0 <= X0 <= 1.0` or an error will be generated when calling `animation_controller.SetAnimation`.

```verse
            X0<native><public>:float = external {}


```
            # Y value of the P1 control point.

```verse
            Y0<native><public>:float = external {}


```
            # X value of the P2 control point. `0.0 <= X1 <= 1.0 or an error will be generated when calling `animation_controller.SetAnimation`.

```verse
            X1<native><public>:float = external {}


```
            # Y value of the P2 control point.

```verse
            Y1<native><public>:float = external {}


```
