# Colors Module

This module provides comprehensive color functionality for working with colors in the ACES 2065-1 color space in Fortnite experiences.

## Color Structure

```verse
Colors := module:
    # Represents colors as RGB triples in the ACES 2065-1 color space.
    # Component values are linear (i.e. `*gamma* = 1.0`).
    color<native><public> := struct<concrete><computes><persistable>:
```

Represents colors as RGB triples in the ACES 2065-1 color space. Component values are linear (gamma = 1.0).

### Properties

#### R (Red)
```verse
# Red component of this `color`.
R<native><public>:float = external {}
```

Red component of this color.

#### G (Green)
```verse
# Green component of this `color`.
G<native><public>:float = external {}
```

Green component of this color.

#### B (Blue)
```verse
# Blue component of this `color`.
B<native><public>:float = external {}
```

Blue component of this color.

## Arithmetic Operators

### Addition
```verse
# Makes an ACES 2065-1 `color` from the component-wise sum of `c0` and `c1`.
(/Verse.org/Colors:)operator'+'<native><public>(c0:color, c1:color)<converges>:color
```

Makes an ACES 2065-1 color from the component-wise sum of two colors.

### Subtraction
```verse
# Makes an ACES 2065-1 `color` from the component-wise difference of `c0` and `c1`.
(/Verse.org/Colors:)operator'-'<native><public>(c0:color, c1:color)<converges>:color
```

Makes an ACES 2065-1 color from the component-wise difference of two colors.

### Multiplication (Color × Color)
```verse
# Makes an ACES 2065-1 `color` from the component-wise product of `c0` and `c1`.
(/Verse.org/Colors:)operator'*'<native><public>(c0:color, c1:color)<converges>:color
```

Makes an ACES 2065-1 color from the component-wise product of two colors.

### Multiplication (Color × Scalar)
```verse
# Makes an ACES 2065-1 `color` from each component of `c` scaled by `factor`.
(/Verse.org/Colors:)operator'*'<native><public>(c:color, factor:float)<converges>:color
```

Makes an ACES 2065-1 color from each component of a color scaled by a float factor.

```verse
# Makes an ACES 2065-1 `color` from each component of `c` scaled by `factor`.
(/Verse.org/Colors:)operator'*'<native><public>(c:color, factor:int)<converges>:color
```

Makes an ACES 2065-1 color from each component of a color scaled by an integer factor.

### Multiplication (Scalar × Color)
```verse
# Makes an ACES 2065-1 `color` from each component of `c` scaled by `factor`.
(/Verse.org/Colors:)operator'*'<native><public>(factor:float, c:color)<converges>:color
```

Makes an ACES 2065-1 color from each component of a color scaled by a float factor.

```verse
# Makes an ACES 2065-1 `color` from each component of `c` scaled by `factor`.
(/Verse.org/Colors:)operator'*'<native><public>(factor:int, c:color)<converges>:color
```

Makes an ACES 2065-1 color from each component of a color scaled by an integer factor.

### Division
```verse
# Makes an ACES 2065-1 `color` from each component of `c` divided by `factor`.
(/Verse.org/Colors:)operator'/'<native><public>(c:color, factor:float)<decides><converges>:color
```

Makes an ACES 2065-1 color from each component of a color divided by a float factor.

```verse
# Makes an ACES 2065-1 `color` from each component of `c` divided by `factor`.
(/Verse.org/Colors:)operator'/'<native><public>(c:color, factor:int)<decides><converges>:color
```

Makes an ACES 2065-1 color from each component of a color divided by an integer factor.

## Color Creation Functions

### From sRGB Components
```verse
# Makes an ACES 2065-1 `color` from sRGB components `Red`, `Green`, and `Blue`.
# Normal sRGB component values are between `0.0` and `1.0`, but this can handle larger values.
MakeColorFromSRGB<native><public>((local:)Red:float, (local:)Green:float, (local:)Blue:float)<converges>:color
```

Makes an ACES 2065-1 color from sRGB components. Normal sRGB component values are between 0.0 and 1.0, but this can handle larger values.

### From sRGB Integer Values
```verse
# Makes an ACES 2065-1 `color` from the integer sRGB components `Red`, `Green`, and `Blue`.
# Valid sRGB component values are between '0' and '255', inclusive.
MakeColorFromSRGBValues<native><public>((local:)Red:int, (local:)Green:int, (local:)Blue:int)<converges>:color
```

Makes an ACES 2065-1 color from integer sRGB components. Valid sRGB component values are between 0 and 255, inclusive.

### From Hex String
```verse
# Makes an ACES 2065-1 `color` from a CSS-style sRGB `hexString`. Supported formats are:
#  * RGB
#  * RRGGBB
#  * RRGGBBAA
#  * #RGB
#  * #RRGGBB
#  * #RRGGBBAA
# An invalid hex string will return `Black`.
MakeColorFromHex<native><public>(hexString:string)<converges>:color
```

Makes an ACES 2065-1 color from a CSS-style sRGB hex string. Supported formats:
- **RGB**: 3-digit hex
- **RRGGBB**: 6-digit hex
- **RRGGBBAA**: 8-digit hex with alpha
- **#RGB**: 3-digit hex with hash
- **#RRGGBB**: 6-digit hex with hash
- **#RRGGBBAA**: 8-digit hex with hash and alpha

An invalid hex string will return Black.

### From HSV Components
```verse
# Makes an ACES 2065-1 `color` from `Hue`, `Saturation`, and `Value` components.
# Components use the HSV color model in the sRGB color space. Expected ranges:
#  * `0.0 <= Hue <= 360.0`
#  * `0.0 <= Saturation <= 1.0`
#  * `0.0 <= Value <= 1.0`
# Values out of expected ranges will undergo range reduction and conversion.
MakeColorFromHSV<native><public>(Hue:float, Saturation:float, Value:float)<converges>:color
```

Makes an ACES 2065-1 color from HSV components using the HSV color model in the sRGB color space. Expected ranges:
- **Hue**: 0.0 ≤ Hue ≤ 360.0
- **Saturation**: 0.0 ≤ Saturation ≤ 1.0
- **Value**: 0.0 ≤ Value ≤ 1.0

Values out of expected ranges will undergo range reduction and conversion.

### From Temperature
```verse
# Makes an ACES 2065-1 `color` from the chromaticity of a blackbody radiator at `Temperature` Kelvin.
# `Temperature` is clamped such that `0 <= Temperature`.
MakeColorFromTemperature<native><public>(Temperature:float)<converges>:color
```

Makes an ACES 2065-1 color from the chromaticity of a blackbody radiator at the specified temperature in Kelvin. Temperature is clamped such that 0 ≤ Temperature.

## Color Conversion Functions

### To sRGB
```verse
# Makes an sRGB `tuple` by converting `InColor` from an ACES 2065-1 `color` to sRGB.
MakeSRGBFromColor<native><public>(InColor:color)<converges>:tuple(float, float, float)
```

Makes an sRGB tuple by converting an ACES 2065-1 color to sRGB.

### To HSV
```verse
# Makes an HSV `tuple` by converting `InColor` from an ACES 2065-1 `color` to sRGB and applying the HSV color model.
MakeHSVFromColor<native><public>(InColor:color):tuple(float, float, float)
```

Makes an HSV tuple by converting an ACES 2065-1 color to sRGB and applying the HSV color model.
