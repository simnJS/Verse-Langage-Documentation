
```verse
Colors := module:

```
# Represents colors as RGB triples in the ACES 2065-1 color space.
    # Component values are linear (i.e. `*gamma* = 1.0`).

```verse
    color<native><public> := struct<concrete><computes><persistable>:
        @editable

```
        # Red component of this `color`.

```verse
        R<native><public>:float = external {}

        @editable

```
        # Green component of this `color`.

```verse
        G<native><public>:float = external {}

        @editable

```
        # Blue component of this `color`.

```verse
        B<native><public>:float = external {}


```
    # Makes an ACES 2065-1 `color` from the component-wise sum of `c0` and `c1`.

```verse
    (/Verse.org/Colors:)operator'+'<native><public>(c0:color, c1:color)<converges>:color


```
    # Makes an ACES 2065-1 `color` from the component-wise difference of `c0` and `c1`.

```verse
    (/Verse.org/Colors:)operator'-'<native><public>(c0:color, c1:color)<converges>:color


```
    # Makes an ACES 2065-1 `color` from the component-wise product of `c0` and `c1`.

```verse
    (/Verse.org/Colors:)operator'*'<native><public>(c0:color, c1:color)<converges>:color


```
    # Makes an ACES 2065-1 `color` from each component of `c` scaled by `factor`.

```verse
    (/Verse.org/Colors:)operator'*'<native><public>(c:color, factor:float)<converges>:color


```
    # Makes an ACES 2065-1 `color` from each component of `c` scaled by `factor`.

```verse
    (/Verse.org/Colors:)operator'*'<native><public>(c:color, factor:int)<converges>:color


```
    # Makes an ACES 2065-1 `color` from each component of `c` scaled by `factor`.

```verse
    (/Verse.org/Colors:)operator'*'<native><public>(factor:float, c:color)<converges>:color


```
    # Makes an ACES 2065-1 `color` from each component of `c` scaled by `factor`.

```verse
    (/Verse.org/Colors:)operator'*'<native><public>(factor:int, c:color)<converges>:color


```
    # Makes an ACES 2065-1 `color` from each component of `c` divided by `factor`.

```verse
    (/Verse.org/Colors:)operator'/'<native><public>(c:color, factor:float)<decides><converges>:color


```
    # Makes an ACES 2065-1 `color` from each component of `c` divided by `factor`.

```verse
    (/Verse.org/Colors:)operator'/'<native><public>(c:color, factor:int)<decides><converges>:color


```
    # Makes an ACES 2065-1 `color` from sRGB components `Red`, `Green`, and `Blue`.
    # Normal sRGB component values are between `0.0` and `1.0`, but this can handle larger values.

```verse
    MakeColorFromSRGB<native><public>((local:)Red:float, (local:)Green:float, (local:)Blue:float)<converges>:color


```
    # Makes an sRGB `tuple` by converting `InColor` from an ACES 2065-1 `color` to sRGB.

```verse
    MakeSRGBFromColor<native><public>(InColor:color)<converges>:tuple(float, float, float)


```
    # Makes an ACES 2065-1 `color` from the integer sRGB components `Red`, `Green`, and `Blue`.
    # Valid sRGB component values are between '0' and '255', inclusive.

```verse
    MakeColorFromSRGBValues<native><public>((local:)Red:int, (local:)Green:int, (local:)Blue:int)<converges>:color


```
    # Makes an ACES 2065-1 `color` from a CSS-style sRGB `hexString`. Supported formats are:
    #  * RGB
    #  * RRGGBB
    #  * RRGGBBAA
    #  * #RGB
    #  * #RRGGBB
    #  * #RRGGBBAA
    # An invalid hex string will return `Black`.

```verse
    MakeColorFromHex<native><public>(hexString:string)<converges>:color


```
    # Makes an ACES 2065-1 `color` from `Hue`, `Saturation`, and `Value` components.
    # Components use the HSV color model in the sRGB color space. Expected ranges:
    #  * `0.0 <= Hue <= 360.0`
    #  * `0.0 <= Saturation <= 1.0`
    #  * `0.0 <= Value <= 1.0`
    # Values out of expected ranges will undergo range reduction and conversion.

```verse
    MakeColorFromHSV<native><public>(Hue:float, Saturation:float, Value:float)<converges>:color


```
    # Makes an HSV `tuple` by converting `InColor` from an ACES 2065-1 `color` to sRGB and applying the HSV color model.

```verse
    MakeHSVFromColor<native><public>(InColor:color):tuple(float, float, float)


```
    # Makes an ACES 2065-1 `color` from the chromaticity of a blackbody radiator at `Temperature` Kelvin.
    # `Temperature` is clamped such that `0 <= Temperature`.

```verse
    MakeColorFromTemperature<native><public>(Temperature:float)<converges>:color


```
